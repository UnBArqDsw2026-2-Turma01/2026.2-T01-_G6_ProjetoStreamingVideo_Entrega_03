# ADR-004 — Chain of Responsibility para a autenticação

| Campo | Valor |
| --- | --- |
| Status | Proposta (aguarda revisão de um integrante da SubEquipe_03 no pull request) |
| Data | 18/10/2026 |
| Autor | Hugo Freitas Silva |
| Revisor | A preencher |
| Escopo | Escolha do padrão, regras de autenticação e decisões de projeto. Modelagem em [1.1.3.3](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md) e [1.1.3.4](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md); código em <a href="https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/tree/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/codigo-autenticacao" target="_blank" rel="noopener"><code>codigo-autenticacao/</code></a>. |

> O número 004 segue o [ADR-003](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/tree/docs/subequipe-03-modelagem-observer) do Observer, de Eduardo Lôbo Moreira, ainda em branch própria. Cada afirmação sobre as entregas anteriores aponta para uma evidência `COR-E01`–`COR-E06` arquivada em <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e03-e01-escopo-fluxo-login-subequipe03.png" target="_blank" rel="noopener"><code>assets/chain-of-responsibility/evidencias/</code></a>. O que não tem evidência está marcado como *decisão de projeto*.

## 1. Contexto

A autenticação é responsabilidade da SubEquipe_03 desde a Entrega 01: o fluxo mínimo da subequipe foi "Login/Cadastro & Autenticação (incl. 2FA/OAuth)", justificado por ser "a porta de entrada de todo o sistema" (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e03-e01-escopo-fluxo-login-subequipe03.png" target="_blank" rel="noopener">COR-E03</a>). As entregas anteriores deixaram um conjunto de verificações que uma tentativa de login precisa atravessar:

| Origem | O que exige do login | Evidência |
| --- | --- | --- |
| Entrega 01 — NFR, O07 | Rate limiting nos endpoints de login contra *credential stuffing* | <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e04-e01-nfr-o05-o06-o07.png" target="_blank" rel="noopener">COR-E04</a> |
| Entrega 01 — NFR, O05 e O06 | MFA para quem transmite; credencial com função de derivação resistente (Argon2id) | COR-E04 |
| Entrega 01 — NFR, C03 | MFA obrigatório **apenas** para criadores e transações financeiras; acesso simplificado para espectadores | <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e05-e01-nfr-conflito-c03.png" target="_blank" rel="noopener">COR-E05</a> |
| Entrega 02 — classes de autenticação | `ClientIntegrityAttestation` (prova de trabalho, sinal de webdriver), `Account` + `AccountStatus`, `Credential`, `LeakedPasswordBloomFilter`, `TwoFactorAuth`, `Session`, `StepUpAuthChallenge`, `IAuditLogger` | <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e06-e02-classes-autenticacao.png" target="_blank" rel="noopener">COR-E06</a> |

**O que o modelo da Entrega 02 não diz.** O diagrama de classes tem as peças, mas não diz em que ordem elas são consultadas, quem decide parar o fluxo nem quem responde ao usuário. A própria modelagem dinâmica da SubEquipe_03 na Entrega 02 registra que "o detalhamento dinâmico de login, desafio de borda, MFA e emissão de tokens [...] não é apresentado como concluído" ([Foco 02 da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica)). Este ADR preenche essa lacuna.

**O problema de desenho.** Escritas em um único método, as verificações viram uma sequência de `if` em que cada regra conhece as outras: o limite de tentativas precisa saber quais recusas contam como falha de credencial; o segundo fator precisa saber se a senha já foi conferida; o step-up (rotação de stream key, saque) repete metade do login com outra terminação. Acrescentar uma verificação — por exemplo, OAuth ou passkeys, previstos no modelo — exigiria editar o método inteiro.

## 2. Regras de autenticação envolvidas

O prefixo `A` evita confusão com `R1`–`R5` do Builder e `F1`–`F6` do Factory Method.

| Id | Regra | Origem | Elo que verifica |
| --- | --- | --- | --- |
| A1 | Cinco falhas de credencial por e-mail ou por IP em 15 minutos bloqueiam novas tentativas até a janela expirar | O07 (COR-E04); limites numéricos são *decisão de projeto* (valores de referência) | `RateLimitHandler` |
| A2 | Cliente sem atestação válida (prova de trabalho, idade, sinal de webdriver) é barrado **antes** do hash da senha | `ClientIntegrityAttestation`, decisão DE01 da Entrega 02 (COR-E06) | `ClientIntegrityHandler` |
| A3 | E-mail inexistente e senha errada recebem a mesma resposta e o mesmo custo de hash | OWASP *Authentication Cheat Sheet* (mensagem genérica e tempo de resposta equivalente) [1] | `PasswordHandler` |
| A4 | O estado da conta (`SUSPENDED`, `DEACTIVATED`, `PENDING_VERIFICATION`) só é revelado a quem provou a senha | `AccountStatus` da Entrega 02; a ordem é *decisão de projeto* | `AccountStatusHandler` |
| A5 | Senha presente em lista de vazamentos não bloqueia o login, mas marca troca obrigatória | `LeakedPasswordBloomFilter`, DE02 da Entrega 02; NIST SP 800-63B pede a comparação ao cadastrar ou trocar a senha [2]; aplicá-la no login é *decisão de projeto* | `LeakedPasswordHandler` |
| A6 | Segundo fator exigido de criadores (que, sem fator cadastrado, são recusados) e de qualquer conta com 2FA ativo | O05 e C03 (COR-E04, COR-E05); gateway "2FA ativa" do BPMN da Entrega 01 | `TwoFactorHandler` |
| A7 | Código TOTP vale no passo atual ±1 e não pode ser reutilizado | RFC 6238, §5.2 [3] | `TwoFactorAuth.verifyToken` |
| A8 | Requisição que chega ao fim da cadeia sem ser tratada é **recusada** | *Decisão de projeto* (ver D2) | `AbstractAuthenticationHandler` |

## 3. Alternativas consideradas

| # | Alternativa | A favor | Contra |
| --- | --- | --- | --- |
| A | Método único `login()` com as verificações em sequência | Nenhuma classe nova; fácil de ler enquanto é pequeno | Toda regra nova edita o mesmo método; o step-up duplicaria o trecho comum; testar uma regra isolada exige montar o login inteiro |
| B | **Strategy** (uma estratégia de autenticação por tipo de conta) | Separa o "como autenticar" de quem pede | Não é o caso: as verificações **somam-se**, não se substituem. Um criador passa pelas mesmas etapas que um espectador, mais uma. O Eduardo já usa Strategy no despacho do Observer, onde a troca do algoritmo inteiro faz sentido |
| C | **State** (máquina de estados da tentativa de login) | Explicita estados como "aguardando segundo fator" | O único estado intermediário real é o desafio TOTP; os demais passos não têm comportamento próprio a alternar. A tentativa é uma passagem, não um objeto de vida longa |
| D | **Template Method** (classe base com passos fixos e ganchos) | Ordem dos passos garantida pela base | A ordem fica fixa na herança: o step-up, que pula atestação e lista de vazamentos e termina em outro passo, viraria outra subclasse com ganchos vazios |
| E | **Decorator** (cada verificação envolve um autenticador) | Composição em tempo de execução, como no Chain | A intenção é acrescentar responsabilidade a um objeto, e não decidir quem trata o pedido; um decorador que recusa sem chamar o componente distorce o padrão. Estruturalmente parecido com E, mas com a intenção errada |
| **F** | **Chain of Responsibility**: um elo por verificação, cada um decide recusar, responder ou repassar | **Cada regra em uma classe testável isoladamente; a ordem é dada pela montagem e pode variar (login × step-up); o Client não sabe qual elo responde; uma verificação nova entra como um elo** | **A ordem passa a ser uma dependência implícita entre elos; uma cadeia mal montada pode deixar o pedido sem tratamento (resolvido por A8); depurar exige seguir a trilha** |
| G | Lista de funções de middleware (pipeline funcional) | Menos classes; comum em frameworks web | É o mesmo mecanismo sem a estrutura do padrão: perde a classe nomeada por elo, com suas dependências, e o vocabulário GoF que a disciplina pede para modelar em UML |

A literatura e a indústria apontam na mesma direção. Na seção de aplicabilidade do padrão, o GoF o indica quando mais de um objeto pode tratar uma solicitação sem que se saiba de antemão qual, e quando o conjunto de tratadores precisa ser definido dinamicamente [4] — os dois casos aparecem aqui (login × step-up). O Spring Security, referência de mercado, organiza a autenticação como uma cadeia de filtros (`SecurityFilterChain`) [5], e seu `ProviderManager` "delega a uma lista de instâncias de `AuthenticationProvider`" [6] (tradução nossa), que é a mesma ideia.

## 4. Decisão

Adotar **F**: Chain of Responsibility.

| Participante GoF | Classe | Arquivo |
| --- | --- | --- |
| Handler | `AuthenticationHandler` (interface) e `AbstractAuthenticationHandler` (sucessor e repasse padrão) | `cadeia/authentication-handler.ts` |
| ConcreteHandler | `RateLimitHandler`, `ClientIntegrityHandler`, `PasswordHandler`, `AccountStatusHandler`, `LeakedPasswordHandler`, `TwoFactorHandler`, `SessionIssuerHandler`, `StepUpGrantHandler` | `cadeia/*-handler.ts` |
| Client | `LoginService` (`login`, `confirmStepUp`) | `login-service.ts` |
| Request | `AuthenticationRequest`, transportado por `AuthenticationContext` | `cadeia/authentication-context.ts` |

### Decisões de projeto derivadas

| # | Decisão | Motivo | Impacto nas entregas anteriores |
| --- | --- | --- | --- |
| D1 | O Handler abstrato implementa o repasse; cada ConcreteHandler verifica e chama `super.handle()` | É a implementação padrão do GoF e a estrutura do slide 61 da aula [7] (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e02-slide61-modelagem-chain.png" target="_blank" rel="noopener">COR-E02</a>): "*if (I can handle request) handle it, else super.handle()*" | — |
| D2 | Fim da cadeia **recusa** com `UNHANDLED` (falha fechada) | O GoF lista entre as consequências do padrão que o tratamento da solicitação não é garantido [4]. Em autenticação, um pedido sem resposta não pode ser lido como aprovado | Regra A8 |
| D3 | Ordem do login: limite → atestação → senha → estado → vazamento → segundo fator → sessão | Primeiro o que é barato e barra automação (o hash é o passo caro); estado só depois da senha (A4); segundo fator depois de tudo que pode recusar sem interação | Ordem não estava no modelo da Entrega 02 |
| D4 | Um contexto compartilhado (`AuthenticationContext`) leva a conta, as marcas e a trilha de elos | Elos posteriores dependem do que anteriores descobriram (a conta localizada pela senha). Elos que precisam da conta recusam com `UNHANDLED` se ela não estiver lá, em vez de falhar silenciosamente | — |
| D5 | Um elo pode agir **na volta**: `RateLimitHandler` lê o resultado devolvido pelo restante da cadeia para contar falhas | Só o fim da cadeia sabe se a falha foi de credencial; contar antes puniria quem acertou. É a variação "cadeia de filtros"; no GoF puro o elo trata **ou** repassa | — |
| D6 | O desafio TOTP é um **tratamento** (`CHALLENGE`), não um erro | Pedir o segundo fator é resposta legítima: o `TwoFactorHandler` é o elo que trata esse pedido, e a cadeia para ali | Torna explícito o gateway "2FA ativa" do BPMN da Entrega 01 |
| D7 | Duas cadeias montadas por funções (`buildLoginChain`, `buildStepUpChain`) com as mesmas classes | O step-up do modelo da Entrega 02 (`StepUpAuthChallenge`) reaproveita senha, estado e segundo fator, sem atestação nem lista de vazamentos, e termina em `StepUpGrantHandler` | Dá comportamento a `StepUpAuthChallenge` |
| D8 | A auditoria fica no Client, e não em um elo | O registro precisa do resultado final, qualquer que seja o elo que respondeu | Usa os valores de `SecurityEventType` da Entrega 02 |
| D9 | Hash com scrypt (RFC 7914) nos parâmetros mínimos do OWASP, e não Argon2id | O Node 22 não oferece Argon2 [8] no módulo `crypto` [9]; o OWASP indica scrypt [10] quando Argon2id não está disponível [11] | Revisão declarada de O06 (Entrega 01) e de `Credential.algorithm` |

## 5. Consequências

**Fica mais fácil:** testar cada regra isoladamente, com um sucessor dublê (cada elo tem sua suíte em `test/handlers.test.ts`); montar fluxos diferentes com os mesmos elos (login e step-up); acrescentar uma verificação — OAuth, passkeys, verificação de dispositivo — como uma classe nova e uma linha na montagem, sem editar os elos existentes.

**Fica mais difícil / custo:**

- **A ordem vira contrato.** Trocar `PasswordHandler` e `AccountStatusHandler` de lugar revelaria contas suspensas a quem não sabe a senha (A4). A ordem é protegida por um teste que confere a sequência montada e por D4.
- **Oito classes** para o que seria um método. Com uma regra só, o padrão não se pagaria.
- **Rastreamento.** Quem lê o código não vê o fluxo em um lugar só; a trilha (`trail`) registrada no contexto e o diagrama de sequência compensam isso.
- **D5 afasta-se do GoF puro.** É uma variação conhecida (filtros de servlet, Spring Security), mas precisa ser dita na apresentação.

**Riscos e limites declarados**

- Repositórios, sessões e auditoria são em memória e a cadeia é síncrona; num serviço real os elos seriam assíncronos (consulta a banco e cache distribuído).
- A emissão do desafio de prova de trabalho e seu uso único não estão implementados. O mecanismo real de atestação da plataforma de referência é proprietário; o BPMN da Entrega 01 já o tratava como inferência.
- O limite de tentativas usa janela fixa; um atacante distribuído em muitos IPs só é contido pela chave por e-mail.
- OAuth, passkeys e cadastro de conta ficam fora deste recorte.

## 6. Referências

1. OPEN WEB APPLICATION SECURITY PROJECT (OWASP). **Authentication Cheat Sheet**. OWASP Foundation. Disponível em: <https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html>. Acesso em: 18 out. 2026.
2. GRASSI, Paul A. et al. **Digital Identity Guidelines: Authentication and Lifecycle Management**. NIST Special Publication 800-63B. Gaithersburg: National Institute of Standards and Technology, 2017. Disponível em: <https://doi.org/10.6028/NIST.SP.800-63b>. Acesso em: 18 out. 2026.
3. M'RAIHI, David; MACHANI, Salah; PEI, Mingliang; RYDELL, Johan. **TOTP: Time-Based One-Time Password Algorithm**. RFC 6238, Internet Engineering Task Force (IETF), 2011. Disponível em: <https://datatracker.ietf.org/doc/html/rfc6238>. Acesso em: 18 out. 2026.
4. GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; VLISSIDES, John. **Padrões de Projeto: Soluções Reutilizáveis de Software Orientado a Objetos**. Porto Alegre: Bookman, 2000.
5. SPRING. **Spring Security Reference: Architecture**. Disponível em: <https://docs.spring.io/spring-security/reference/servlet/architecture.html>. Acesso em: 18 out. 2026.
6. SPRING. **Spring Security Reference: Servlet Authentication Architecture**. Disponível em: <https://docs.spring.io/spring-security/reference/servlet/authentication/architecture.html>. Acesso em: 18 out. 2026.
7. SERRANO, Milene. **Arquitetura e Desenho de Software — Aula: GoFs Comportamentais**. Material didático da disciplina Arquitetura e Desenho de Software, Universidade de Brasília (UnB-FGA), [2019?].
8. BIRYUKOV, Alex; DINU, Daniel; KHOVRATOVICH, Dmitry; JOSEFSSON, Simon. **Argon2 Memory-Hard Function for Password Hashing and Proof-of-Work Applications**. RFC 9106, Internet Research Task Force (IRTF), 2021. Disponível em: <https://datatracker.ietf.org/doc/html/rfc9106>. Acesso em: 18 out. 2026.
9. NODE.JS. **Crypto — Node.js v22 Documentation**. OpenJS Foundation. Disponível em: <https://nodejs.org/docs/latest-v22.x/api/crypto.html>. Acesso em: 18 out. 2026.
10. PERCIVAL, Colin; JOSEFSSON, Simon. **The scrypt Password-Based Key Derivation Function**. RFC 7914, Internet Engineering Task Force (IETF), 2016. Disponível em: <https://datatracker.ietf.org/doc/html/rfc7914>. Acesso em: 18 out. 2026.
11. OPEN WEB APPLICATION SECURITY PROJECT (OWASP). **Password Storage Cheat Sheet**. OWASP Foundation. Disponível em: <https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html>. Acesso em: 18 out. 2026.

## Histórico de versões

| Versão | Data | Autor | Descrição | Revisor |
| --- | --- | --- | --- | --- |
| 1.0 | 18/10/2026 | [@HugoFreitass](https://github.com/HugoFreitass) | Contexto, regras A1–A8, alternativas, decisão e decisões derivadas D1–D9 | A preencher |
| 1.1 | 18/10/2026 | [@HugoFreitass](https://github.com/HugoFreitass) | Referências numeradas no formato da SubEquipe_03 na Entrega 01, com citações numéricas no texto | A preencher |
