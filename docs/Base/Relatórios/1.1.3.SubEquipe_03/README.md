# 1.1.3. SubEquipe_03 — GoFs Comportamentais + IA Generativa

**Estado:** em elaboração. A subequipe aplica padrões comportamentais aos módulos que assumiu desde a Entrega 02 — autenticação, moderação e telemetria. **Chain of Responsibility** na autenticação (Hugo Freitas Silva) está modelado, implementado, testado e demonstrado em vídeo: [1.1.3.3. Modelagem](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md), [1.1.3.4. Sequência](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) e [ADR-004](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md). **Observer** com Strategy de despacho no `StreamChannel` (Eduardo Lôbo Moreira) está na branch [`docs/subequipe-03-modelagem-observer`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/tree/docs/subequipe-03-modelagem-observer), ainda não integrada à `main`. O padrão de Philipe Amâncio Reis Caetano está a definir.

## Integrantes

| Matrícula | Integrante | GitHub |
| --- | --- | --- |
| 24/1041302 | Hugo Freitas Silva | [@HugoFreitass](https://github.com/HugoFreitass) |
| 24/1040350 | Philipe Amâncio Reis Caetano | [@Phill-Chill](https://github.com/Phill-Chill) |
| 24/1011027 | Eduardo Lôbo Moreira | [@EduLoboM](https://github.com/EduLoboM) |

Composição mantida conforme a [introdução da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Introducao).

## Foco do relatório

**GoFs Comportamentais + IA Generativa.** A entrega mínima deste foco inclui um padrão comportamental, modelo UML, código e vídeo demonstrando sua execução, além dos pontos de vista individuais.

## Estrutura da subequipe e focos entregues

```text
SubEquipe_03 — GoFs Comportamentais + IA Generativa
├── 📘 Documentação · docs/Base/Relatórios/1.1.3.SubEquipe_03/
│   ├── README.md                                   relatório geral (contexto, escolha, execução, versões)
│   ├── 1.1.3.3.ModelagemChainOfResponsibility.md   UML de classes + evidências COR-E01–COR-E06
│   ├── 1.1.3.4.SequenciaChainOfResponsibility.md   UML de sequência (login com segundo fator)
│   ├── ADR/ADR-004-chain-of-responsibility-autenticacao.md
│   └── assets/chain-of-responsibility/             .puml, .svg, .png, evidências e vídeo
└── 💻 Código · g6-streaming-entrega03-subgrupo03-codigo (branch feat/autenticacao-chainOfResponsibilityBehavioralGoF)
    ├── src/autenticacao/cadeia/                          Handler, ConcreteHandlers, contexto e montagem das cadeias
    ├── src/autenticacao/dominio/                          recortes do diagrama de autenticação da Entrega 02
    ├── src/autenticacao/login-service.ts                     Client
    ├── src/autenticacao/demo.ts                             demonstração no terminal
    └── tests/                                      56 testes (node:test)
```

O Observer de Eduardo, na branch citada acima, acrescenta as páginas 1.1.3.1, 1.1.3.2, 1.1.3.5, 1.1.3.6, o ADR-003 e a pasta `codigo/`; os nomes usados aqui não colidem com os dela.

| Foco da entrega | Chain of Responsibility (autenticação) | Onde |
| --- | --- | --- |
| Contexto e justificativa | ✅ Hugo | [Contexto](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=contexto-problema) · [ADR-004](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md) |
| Modelagem UML — classes | ✅ Hugo | [1.1.3.3](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md) |
| Modelagem UML — sequência | ✅ Hugo | [1.1.3.4](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) |
| Implementação e testes | ✅ Hugo · 56 testes | <a href="https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/feat/autenticacao-chainOfResponsibilityBehavioralGoF/" target="_blank" rel="noopener"><code>g6-streaming-entrega03-subgrupo03-codigo</code></a> |
| Execução documentada | ✅ `npm run demo` | [Execução](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=execução-e-vídeo-do-padrão-em-funcionamento) |
| Vídeo | ✅ Hugo (2 min 20 s) | [Vídeo](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=vídeo-do-chain-of-responsibility) |
| IA Generativa | 🟡 Hugo preenchido; Philipe e Eduardo a preencher nesta página | [Relatos](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=participantes-no-foco--lições-aprendidas-e-ia-generativa) |

Legenda: ✅ entregue · 🟡 em andamento · ⬜ não iniciado. A tabela descreve o que está nesta branch; o Observer será acrescentado quando a branch de Eduardo for integrada.

## Participantes no foco — lições aprendidas e IA Generativa

| Integrante | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| --- | --- | --- |
| Hugo Freitas Silva | [Ver relato](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=hugo-freitas-silva) | [Ver relato](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=hugo-freitas-silva) |
| Philipe Amâncio Reis Caetano | A preencher pelo integrante | A preencher pelo integrante |
| Eduardo Lôbo Moreira | A preencher pelo integrante | A preencher pelo integrante |

Cada integrante deverá explicar o que aprendeu, como colaborou e, caso tenha usado IA, qual ferramenta utilizou, o apoio recebido, como validou os resultados e quais limitações encontrou. Informar também quando não houver uso de IA.

### Hugo Freitas Silva

| Campo | Conteúdo |
| -- | -- |
| Lições aprendidas | - Chain of Responsibility não é só "uma lista de `if` em classes": o ganho apareceu quando a mesma família de elos montou **duas** cadeias (login e step-up) sem duplicar regra. Com uma cadeia só, o padrão quase não se pagaria.<br>- A consequência do GoF de que o pedido pode chegar ao fim da cadeia sem tratamento é aceitável em muitos domínios, mas não em autenticação. Tratar o fim da cadeia como recusa (falha fechada) foi a decisão mais importante do desenho.<br>- A ordem dos elos é um requisito de segurança, não um detalhe: verificar o estado da conta antes da senha revelaria contas suspensas a quem não sabe a senha. Por isso a ordem ficou protegida por teste.<br>- O modelo da Entrega 02 tinha as classes de autenticação, mas não a coordenação entre elas; um padrão comportamental preenche exatamente esse tipo de lacuna. |
| Uso da IA Generativa (senso crítico) | **Ferramenta:** Claude Code (Anthropic), usado no terminal sobre os repositórios das três entregas.<br>**Onde entrou:** Levantamento do que as Entregas 01 e 02 já diziam sobre autenticação (NFR O05–O07 e C03, escopo da SubEquipe_03, diagrama de classes de autenticação) e do que os colegas já haviam feito (Builder e Factory Method da SubEquipe_01, Observer de Eduardo); comparação das alternativas; escrita do código TypeScript, dos testes, dos diagramas PlantUML, do ADR-004 e destas páginas; captura das evidências e geração do vídeo a partir da saída real dos comandos.<br>**Narração do vídeo de código:** a voz do vídeo não é a minha gravada; o texto da narração foi sintetizado com a voz neural *Brian Multilingual* do Microsoft Edge TTS (biblioteca `edge-tts`), escolhida entre duas amostras por soar mais natural. Conferi a pronúncia dos termos técnicos e a sincronia de cada fala com a tela correspondente.<br>**Como validei:**<br>- O TOTP foi conferido contra os vetores de teste do Apêndice B da RFC 6238 [1]; o filtro de Bloom, contra as fórmulas de dimensionamento [2] e uma medição de falso positivo.<br>- 56 testes e a verificação de tipos estrita (`tsc --noEmit`) passam; um teste confere a ordem dos elos e outro, o ponto de parada e a trilha de cada recusa.<br>- A saída da demonstração foi lida caso a caso. Ela revelou um erro do primeiro roteiro: uma falha de senha de um cenário anterior contava para o limite de tentativas do cenário seguinte, e o bloqueio aparecia na quinta tentativa em vez da sexta. O roteiro foi corrigido para usar outra conta.<br>- Os links das referências foram abertos e os trechos citados (OWASP [3, 4], Spring Security [5], RFC 6238 §5.2 [1]) conferidos na fonte. Onde não havia o texto exato da edição em português do GoF, a citação virou paráfrase. |
| Exemplo concreto (acerto) | A IA localizou nas Entregas 01 e 02 os requisitos que a cadeia precisava atender (NFR O05–O07, conflito C03 e o diagrama de classes de autenticação) e propôs reaproveitar a mesma família de elos em duas cadeias, login e step-up — a decisão que justifica o padrão. |
| Exemplo concreto (erro/alucinação) e correção aplicada | - As páginas do livro GoF não foram conferidas no exemplar; a referência é feita ao padrão, não a páginas.<br>- A IA propôs inicialmente executar o TypeScript direto pelo Node 22; a versão instalada pelo sistema operacional não tem esse suporte, e o projeto passou a usar `tsx`.<br>- O modelo previa Argon2id, indisponível no `crypto` do Node 22; a troca por scrypt é uma revisão declarada (D9 do ADR-004), não uma equivalência.<br>- Todo o código e o texto foram produzidos com apoio da IA; a responsabilidade pelas decisões e pela conferência contra as entregas anteriores é minha.<br>Correções: troca para `tsx`; scrypt registrado como revisão declarada (D9 do ADR-004); roteiro da demonstração corrigido para não somar falhas entre cenários. |
| Comprobatório (commit/PR) | [Código no repositório dedicado](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/feat/autenticacao-chainOfResponsibilityBehavioralGoF) · [Versionamentos & Participações](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=versionamentos--participações) |

## Metodologia

Como contexto de planejamento inicial, a [ata da Reunião Geral 1](/Projeto/Atas/ata-G01-2026-10-05.md) registra a sugestão de Observer para notificações e mensagens de chat. A ata não registra uma escolha final; esta seção deve descrever as decisões e o trabalho efetivamente adotados pela subequipe.

**Chain of Responsibility (Hugo Freitas Silva).** O trabalho seguiu cinco passos:

1. **Estudo do padrão.** Aula de GoFs comportamentais da disciplina, slides 9 e 61 [6], capítulo do padrão no GoF [7] e materiais de referência sobre o padrão [8, 9].
2. **Releitura das entregas anteriores.** Escopo do produto e NFR Framework da SubEquipe_03 na Entrega 01, diagrama de classes de autenticação e modelagem dinâmica da Entrega 02. Cada afirmação usada virou evidência arquivada (COR-E03 a COR-E06).
3. **Decisão antes do código.** Regras A1–A8 e decisões D1–D9 registradas no [ADR-004](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md), com sete alternativas comparadas.
4. **Código, testes e modelos em conjunto.** Um elo por classe, com testes isolados por sucessor dublê; diagramas PlantUML desenhados a partir do código e conferidos contra ele; demonstração com relógio fixo para a saída ser reproduzível.
5. **Revisão por pares.** Eduardo Lôbo Moreira e Philipe Amâncio Reis Caetano revisaram todo o material do padrão — código e testes, ADR-004, diagramas, relatório, vídeo e referências —, conforme registrado em [Versionamentos & Participações](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=versionamentos--participações).

Ferramentas: TypeScript, `node:test`, `tsx`, PlantUML, Docsify, Git e GitHub. A metodologia da subequipe como um todo (reuniões, divisão e revisões entre os três integrantes) está **a preencher pela subequipe**, relacionando atas aos [registros de reuniões](/Projeto/Atas/README.md).

## GoF Comportamental

### Contexto (problema)

A autenticação é responsabilidade da SubEquipe_03 desde a Entrega 01, em que "Login/Cadastro & Autenticação (incl. 2FA/OAuth)" foi o fluxo mínimo da subequipe (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e03-e01-escopo-fluxo-login-subequipe03.png" target="_blank" rel="noopener">COR-E03</a>). O NFR Framework da mesma entrega pediu rate limiting no login (O07), MFA para quem transmite (O05) e credenciais com função de derivação resistente (O06), e resolveu o conflito C03 exigindo MFA **só** de criadores e transações financeiras (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e04-e01-nfr-o05-o06-o07.png" target="_blank" rel="noopener">COR-E04</a>, <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e05-e01-nfr-conflito-c03.png" target="_blank" rel="noopener">COR-E05</a>). Na Entrega 02, o diagrama de classes de autenticação modelou as peças — atestação do cliente com prova de trabalho, conta e estado, credencial, filtro de senhas vazadas, TOTP, sessão, desafio de step-up e auditoria (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e06-e02-classes-autenticacao.png" target="_blank" rel="noopener">COR-E06</a>).

O que faltava era a coordenação: a modelagem dinâmica da Entrega 02 registra que o detalhamento do login, do desafio de borda, do MFA e da emissão de tokens não foi concluído. Escritas num único método, essas verificações viram uma sequência de condicionais em que cada regra conhece as outras, e o step-up (rotação de stream key, saque) repetiria metade do login. Detalhes em [ADR-004 §1](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_1-contexto).

### Escolha e justificativa

**Chain of Responsibility** (padrão comportamental GoF) para o login e o step-up: cada verificação é um elo — limite de tentativas, atestação do cliente, senha, estado da conta, senha vazada, segundo fator — que **recusa**, **responde** (com um desafio de segundo fator) ou **repassa** ao próximo; o último elo cria a sessão ou conclui o step-up. O `LoginService` entrega o pedido só ao primeiro elo e não sabe qual vai respondê-lo, que é a intenção do padrão no GoF [7] e na aula da disciplina [6]: evitar a dependência entre quem solicita e quem trata, com a base mantendo o ponteiro para o "próximo" (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e01-slide09-visao-geral-comportamentais.png" target="_blank" rel="noopener">COR-E01</a>, <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e02-slide61-modelagem-chain.png" target="_blank" rel="noopener">COR-E02</a>). O Spring Security organiza a autenticação da mesma forma, com uma cadeia de filtros [10] e um `ProviderManager` que delega a uma lista de provedores [5].

Alternativas descartadas, com o argumento de cada uma — método único, Strategy (que já é usado por Eduardo no despacho do Observer), State, Template Method, Decorator e pipeline de funções — estão em [ADR-004 §3](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_3-alternativas-consideradas), junto das regras A1–A8 e das decisões D1–D9.

**Limites declarados:** o fim da cadeia recusa (falha fechada), diferente do GoF, em que o pedido pode ficar sem tratamento [7] (D2); o `RateLimitHandler` age também na volta do pedido, variação de cadeia de filtros que o GoF puro não prevê (D5); e a credencial usa scrypt [11] em vez do Argon2id [12] da Entrega 01, porque o módulo `crypto` do Node 22 não oferece Argon2 [13]; o OWASP indica scrypt nesse caso [4] (D9).

**Relação com os outros padrões do grupo.** O Builder e o Factory Method da SubEquipe_01 criam a configuração e o conteúdo da transmissão; o Observer de Eduardo reage a eventos do canal. O Chain of Responsibility fica antes de todos eles: decide se a pessoa entra e, no step-up, se pode executar ações sensíveis sobre o canal, como rotacionar a stream key que o fluxo de transmissão usa.

### Modelagem (notação UML)

**Chain of Responsibility — classes.** Diagrama "antes" (recorte do diagrama de autenticação da Entrega 02) e "depois" (padrão aplicado), correspondência entre participantes GoF e classes, regras A1–A8 e evidências: [1.1.3.3. Modelagem — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md). Fonte editável em PlantUML e exportações PNG/SVG em <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/chain-of-responsibility-classes-v1.puml" target="_blank" rel="noopener"><code>assets/chain-of-responsibility/</code></a>. Autoria: Hugo Freitas Silva.

**Chain of Responsibility — sequência.** Login de uma criadora com segundo fator, com o ponto de parada de cada recusa, o desafio TOTP e a volta pelo `RateLimitHandler`: [1.1.3.4. Sequência — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md). Fonte editável em <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/chain-of-responsibility-sequencia-v1.puml" target="_blank" rel="noopener"><code>chain-of-responsibility-sequencia-v1.puml</code></a>. Autoria: Hugo Freitas Silva.

![Diagrama de classes do Chain of Responsibility](assets/chain-of-responsibility/chain-of-responsibility-classes-v1.png)

*Figura 1 — Diagrama de classes do Chain of Responsibility aplicado à autenticação, v1. Autoria: Hugo Freitas Silva, 2026.*

### Implementação (código)

Código em <a href="https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/feat/autenticacao-chainOfResponsibilityBehavioralGoF/" target="_blank" rel="noopener"><code>g6-streaming-entrega03-subgrupo03-codigo</code></a> — repositório de código dedicado da subequipe, branch `feat/autenticacao-chainOfResponsibilityBehavioralGoF`, como o Observer de Eduardo (`feat/moderacao-observerBehavioralGoF`) e o chat de Philipe (`feat/chat-observerBehavioralGoF`). TypeScript sem dependência de execução: a criptografia (scrypt, HMAC, SHA-256) vem do módulo `node:crypto`; `tsx`, `typescript` e `@types/node` são só de desenvolvimento. Um arquivo por participante:

| Participante | Arquivo | Trecho que realiza o padrão |
| --- | --- | --- |
| Handler | `src/autenticacao/cadeia/authentication-handler.ts` | interface `AuthenticationHandler` (`setNext`, `handle`); `AbstractAuthenticationHandler.handle` registra o elo na trilha e chama `next.handle`; sem sucessor, recusa com `UNHANDLED` |
| ConcreteHandler | `rate-limit-handler.ts`, `client-integrity-handler.ts`, `password-handler.ts`, `account-status-handler.ts`, `leaked-password-handler.ts`, `two-factor-handler.ts` | cada `handle` verifica uma regra e devolve a recusa ou chama `super.handle(context)` |
| ConcreteHandler terminal | `session-issuer-handler.ts`, `step-up-grant-handler.ts` | tratam o pedido (sessão + token, ou desafio concluído) e não repassam |
| Client | `src/autenticacao/login-service.ts` | `login` e `confirmStepUp` entregam o contexto ao primeiro elo e registram a auditoria |
| Request | `src/autenticacao/cadeia/authentication-context.ts` | `AuthenticationRequest` e `AuthenticationContext` (conta, marcas e trilha) |
| Montagem | `src/autenticacao/cadeia/authentication-chains.ts` | `buildLoginChain` e `buildStepUpChain`, com `setNext` encadeado |

O [README do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/README.md) resume participantes e limites. O segundo fator é TOTP [1], construído sobre o HOTP [14]; a sessão recebe um JWT assinado com HMAC-SHA-256 [15]; a lista de senhas vazadas é um filtro de Bloom [2] com índices por hash duplo [16], e exigir a troca dessas senhas segue a recomendação de comparar senhas com listas de comprometidas [17]. São 56 testes: os elos isolados com um sucessor dublê, as duas cadeias montadas, o `LoginService`, o domínio e os vetores da RFC 6238.

### Execução e vídeo do padrão em funcionamento

**Pré-requisitos:** Node 20 ou superior e npm. Nenhuma outra dependência global; o TypeScript roda pelo `tsx`, sem etapa de build.

```bash
git clone https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo.git
cd g6-streaming-entrega03-subgrupo03-codigo
git checkout feat/autenticacao-chainOfResponsibilityBehavioralGoF
npm ci          # instala as dependências de desenvolvimento travadas no package-lock
npm run check   # tipos (tsc --noEmit) e os 56 testes (node:test)
npm run demo    # demonstração no terminal
```

**Cenário demonstrado (`npm run demo`).** Cinco contas fictícias, relógio fixo e ids sequenciais, para a saída ser igual a cada execução:

1. **Cadeias montadas** — ordem dos elos no login e no step-up.
2. **Espectador sem segundo fator** — o pedido percorre os sete elos e recebe sessão e token.
3. **Criadora com segundo fator (C03)** — sem código, o `TwoFactorHandler` responde com desafio; com código, a sessão é criada; o mesmo código de novo é recusado (RFC 6238 §5.2 [1]).
4. **Senha vazada** — autentica com a marca `PASSWORD_CHANGE_REQUIRED`.
5. **Recusas** — cada uma vem de um elo diferente: cliente automatizado, e-mail inexistente e senha errada (mesma resposta), conta suspensa (só após a senha), criador sem segundo fator.
6. **Limite de tentativas** — após cinco falhas, nem a senha correta passa.
7. **Step-up** — rotação da stream key com a cadeia de step-up.
8. **Cadeia sem elo terminal** — o pedido é recusado com `UNHANDLED` (falha fechada).
9. **Auditoria** — eventos registrados pelo `LoginService`.

**Resultado esperado** (parte 3, saída real):

```text
=== 3. Criadora com segundo fator (C03 da Entrega 01) ===

ana@exemplo.com, senha correta, sem código:
  resultado:  CHALLENGE
  desafio:    TOTP_REQUIRED (emitido por TwoFactorHandler)
  passou por: RateLimitHandler → ClientIntegrityHandler → PasswordHandler → AccountStatusHandler → LeakedPasswordHandler

ana@exemplo.com, senha correta, código 477625:
  resultado:  AUTHENTICATED
  sessão:     sessao-02 (conta conta-ana)
  token:      eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9…
  marcas:     (nenhuma)
  passou por: RateLimitHandler → ClientIntegrityHandler → PasswordHandler → AccountStatusHandler → LeakedPasswordHandler → TwoFactorHandler → SessionIssuerHandler

ana@exemplo.com, o mesmo código 477625 de novo (reuso, RFC 6238 §5.2):
  resultado:  REJECTED
  motivo:     INVALID_TOTP — código do autenticador inválido ou já utilizado
  recusado:   TwoFactorHandler
  passou por: RateLimitHandler → ClientIntegrityHandler → PasswordHandler → AccountStatusHandler → LeakedPasswordHandler
```

A linha `passou por` é a trilha registrada pela base do Handler: mostra até onde o pedido foi e confere, em execução, a ordem desenhada no diagrama de sequência. A demonstração reduz o custo do scrypt (N = 2^14) para rodar em cerca de 3 s; o padrão do código é o do OWASP (N = 2^17) [4].

#### Vídeo do Chain of Responsibility

| Campo | Conteúdo |
| --- | --- |
| Link do vídeo | <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/video/chain-of-responsibility-demo.mp4" target="_blank" rel="noopener"><code>chain-of-responsibility-demo.mp4</code></a> |
| Duração | 2 min 31 s, com narração em português (voz sintetizada), 1920×1080 |
| Participantes (nome e papel no vídeo) | Hugo Freitas Silva — roteiro, código exibido e apresentação (identificado na abertura e no cabeçalho de todas as telas) |
| Data de gravação | 19/10/2026 |

<video controls preload="metadata" width="100%" src="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/video/chain-of-responsibility-demo.mp4"></video>

**Roteiro.**

| Tempo | Etapa | Comando ou arquivo | O que a tela mostra |
| --- | --- | --- | --- |
| 00:00–00:18 | Abertura | — | Padrão, autor, subequipe e repositório de código |
| 00:18–00:38 | Estrutura | `git checkout feat/autenticacao-chainOfResponsibilityBehavioralGoF` | Pastas `cadeia/` e `dominio/`, `LoginService`, demonstração e testes |
| 00:38–01:02 | Handler | `authentication-handler.ts` | Sucessor, repasse padrão e recusa no fim da cadeia (falha fechada) |
| 01:02–01:27 | Montagem | `npm run demo`, parte 1, e `authentication-chains.ts` | Cadeias de login e de step-up montadas com as mesmas classes |
| 01:27–01:50 | Login | `npm run demo`, partes 2 e 3 | Entrada sem segundo fator, desafio TOTP, entrada com código e recusa do reuso |
| 01:50–02:12 | Recusas | `npm run demo`, parte 5 | Cada recusa parte de um elo diferente; mesma resposta para e-mail inexistente e senha errada |
| 02:12–02:30 | Verificação | `npm run check` | Tipos sem erro e 56 testes passando |

**Como foi produzido.** Um script executou os comandos no código do repositório dedicado e renderizou cada tela com a saída real (1920×1080, H.264); os trechos de código são os arquivos versionados. O texto da narração foi redigido com apoio de IA, revisado por mim e sintetizado por voz neural (ver [relato de IA](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=hugo-freitas-silva)).

## Rastreabilidade & Elos com Outros Artefatos

A [modelagem da SubEquipe_03 na Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.SubEquipe_03) e o [NFR Framework da SubEquipe_03 na Entrega 01](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_01/#/Base/Relatorios/1.1.3.SubEquipe_03/2.NFRFramework) são as origens das regras abaixo. Os links de código apontam para a `main`, onde a pasta estará após a integração do pull request.

| Problema ou requisito | Artefato de origem (link) | Elemento do modelo | Trecho de código (link) | Evidência de execução (link) |
| --- | --- | --- | --- | --- |
| Login e autenticação como fluxo da SubEquipe_03 | [Escopo do Produto, Entrega 01](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_01/#/Projeto/EscopoProduto) (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e03-e01-escopo-fluxo-login-subequipe03.png" target="_blank" rel="noopener">COR-E03</a>) | Client `LoginService` e cadeia de login | [`login-service.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/login-service.ts) · [`authentication-chains.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/authentication-chains.ts) | Demo, partes 1 e 2 · teste `é montada na ordem decidida no ADR-004` |
| Ordem e coordenação do login não modeladas | [Modelagem Dinâmica, Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica) (delimitação) | Handler e [sequência](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) | [`authentication-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/authentication-handler.ts) | Linhas `passou por` da demo |
| A1 — rate limiting no login (O07) | NFR, Entrega 01 (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e04-e01-nfr-o05-o06-o07.png" target="_blank" rel="noopener">COR-E04</a>) | `RateLimitHandler`, `LoginRateLimiter` | [`rate-limit-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/rate-limit-handler.ts) | Demo, parte 6 · teste `cinco falhas bloqueiam a sexta tentativa…` |
| A2 — atestação antes do hash (DE01) | Classes de autenticação, Entrega 02 (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e06-e02-classes-autenticacao.png" target="_blank" rel="noopener">COR-E06</a>) | `ClientIntegrityHandler`, `ClientIntegrityAttestation` | [`client-integrity-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/client-integrity-handler.ts) | Demo, parte 5 (webdriver) · testes `recusa atestação …` |
| A3 — mesma resposta para e-mail inexistente e senha errada | OWASP *Authentication Cheat Sheet* [3]; `Credential` da Entrega 02 (COR-E06) | `PasswordHandler` | [`password-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/password-handler.ts) | Demo, parte 5 · teste `e-mail inexistente e senha errada têm a mesma recusa` |
| A4 — estado da conta só após a senha | `AccountStatus`, Entrega 02 (COR-E06) | `AccountStatusHandler` | [`account-status-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/account-status-handler.ts) | Demo, parte 5 (conta suspensa) · teste `conta suspensa só é revelada a quem prova a senha` |
| A5 — senha vazada marca troca (DE02) | `LeakedPasswordBloomFilter`, Entrega 02 (COR-E06) | `LeakedPasswordHandler` | [`leaked-password-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/leaked-password-handler.ts) | Demo, parte 4 |
| A6 — MFA de criadores (O05, C03) | NFR, Entrega 01 (COR-E04, <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e05-e01-nfr-conflito-c03.png" target="_blank" rel="noopener">COR-E05</a>) | `TwoFactorHandler`, `Account.requiresMfa` | [`two-factor-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/two-factor-handler.ts) | Demo, partes 3 e 5 · testes de `TwoFactorHandler` |
| A7 — TOTP ±1 passo, sem reuso | RFC 6238 §5.2 [1]; `TwoFactorAuth`, Entrega 02 | `TwoFactorAuth.verifyToken` | [`two-factor-auth.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/dominio/two-factor-auth.ts) | Demo, parte 3 (reuso) · vetores da RFC 6238 |
| A8 — fim da cadeia recusa | [ADR-004, D2](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_4-decisão) | `AbstractAuthenticationHandler` | [`authentication-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/authentication-handler.ts) | Demo, parte 8 · teste `sem sucessor, recusa com UNHANDLED` |
| Step-up antes de ação sensível | `StepUpAuthChallenge`, `StepUpTrigger`, Entrega 02 (COR-E06) | `buildStepUpChain`, `StepUpGrantHandler` | [`authentication-chains.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/cadeia/authentication-chains.ts) | Demo, parte 7 · teste `conclui o desafio com senha e código` |
| Auditoria de eventos de segurança | `IAuditLogger`, `SecurityEventType`, Entrega 02 (COR-E06) | Client `LoginService` | [`login-service.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/autenticacao-chainOfResponsibilityBehavioralGoF/src/autenticacao/login-service.ts) | Demo, parte 9 · testes de `LoginService` |

As evidências COR-E01–COR-E06 são capturas arquivadas em [Modelagem — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md?id=evidências), cada uma com fonte e data no rodapé.

## Senso Crítico

**Benefícios que as evidências sustentam.**

- Cada regra mora em uma classe e é testada isoladamente com um sucessor dublê; a suíte tem um grupo de testes por elo.
- As mesmas classes montam duas cadeias (login e step-up); o step-up não duplicou nenhuma regra (demo, parte 7).
- O Client não depende de quem responde: o `LoginService` trata da mesma forma uma recusa do primeiro elo, um desafio do sexto e uma sessão do sétimo.

**Custos e limites.**

- **A ordem vira contrato implícito.** O diagrama de classes não mostra a ordem; trocar dois elos de lugar quebraria A4. Mitigação: teste da ordem montada e elos que recusam quando falta a conta no contexto (D4).
- **Mais classes.** Oito elos para o que seria um método; o padrão só se paga porque há duas cadeias e porque as regras mudam independentemente.
- **Variações em relação ao GoF puro**, declaradas no ADR: falha fechada no fim da cadeia (D2) e elo que age na volta (D5). Ambas existem na indústria (cadeias de filtros), mas precisam ser ditas.
- **Recorte.** Repositórios em memória e cadeia síncrona; emissão do desafio de prova de trabalho, OAuth e passkeys fora do escopo; scrypt em vez de Argon2id (D9).

**Decisões revistas ao longo do trabalho.**

- **A ordem senha × estado da conta foi invertida** em relação à primeira ideia (estado primeiro, por ser mais barato): verificar o estado antes revelaria contas suspensas a quem não sabe a senha (A4).
- **O limite de tentativas passou a agir na volta.** Contar toda tentativa na ida puniria quem acertou a senha; só o fim da cadeia sabe se a falha foi de credencial (D5).
- **Argon2id virou scrypt** ao descobrir que o Node 22 não tem Argon2 no módulo `crypto`; foi registrado como revisão (D9), não como equivalência.

**Coerência entre UML e implementação.** Os diagramas foram desenhados a partir do código: classes, métodos e visibilidades coincidem com `src/autenticacao/` do repositório de código, e a ordem das mensagens do diagrama de sequência é a da montagem `buildLoginChain`, verificada por teste. Divergências conhecidas: o diagrama de sequência desenha cada recusa voltando só ao elo anterior (fragmento `break`), enquanto no código ela volta elo a elo até o Client — simplificação declarada na [página da sequência](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md?id=senso-crítico).

## Referências

1. M'RAIHI, David; MACHANI, Salah; PEI, Mingliang; RYDELL, Johan. **TOTP: Time-Based One-Time Password Algorithm**. RFC 6238, Internet Engineering Task Force (IETF), 2011. Disponível em: <https://datatracker.ietf.org/doc/html/rfc6238>. Acesso em: 18 out. 2026.
2. BLOOM, Burton H. Space/Time Trade-offs in Hash Coding with Allowable Errors. **Communications of the ACM**, v. 13, n. 7, p. 422-426, 1970.
3. OPEN WEB APPLICATION SECURITY PROJECT (OWASP). **Authentication Cheat Sheet**. OWASP Foundation. Disponível em: <https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html>. Acesso em: 18 out. 2026.
4. OPEN WEB APPLICATION SECURITY PROJECT (OWASP). **Password Storage Cheat Sheet**. OWASP Foundation. Disponível em: <https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html>. Acesso em: 18 out. 2026.
5. SPRING. **Spring Security Reference: Servlet Authentication Architecture**. Disponível em: <https://docs.spring.io/spring-security/reference/servlet/authentication/architecture.html>. Acesso em: 18 out. 2026.
6. SERRANO, Milene. **Arquitetura e Desenho de Software — Aula: GoFs Comportamentais**. Material didático da disciplina Arquitetura e Desenho de Software, Universidade de Brasília (UnB-FGA), [2019?].
7. GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; VLISSIDES, John. **Padrões de Projeto: Soluções Reutilizáveis de Software Orientado a Objetos**. Porto Alegre: Bookman, 2000.
8. REFACTORING.GURU. **Chain of Responsibility**. Disponível em: <https://refactoring.guru/pt-br/design-patterns/chain-of-responsibility>. Acesso em: 18 out. 2026.
9. SOURCEMAKING. **Chain of Responsibility Design Pattern**. Disponível em: <https://sourcemaking.com/design_patterns/chain_of_responsibility>. Acesso em: 18 out. 2026.
10. SPRING. **Spring Security Reference: Architecture**. Disponível em: <https://docs.spring.io/spring-security/reference/servlet/architecture.html>. Acesso em: 18 out. 2026.
11. PERCIVAL, Colin; JOSEFSSON, Simon. **The scrypt Password-Based Key Derivation Function**. RFC 7914, Internet Engineering Task Force (IETF), 2016. Disponível em: <https://datatracker.ietf.org/doc/html/rfc7914>. Acesso em: 18 out. 2026.
12. BIRYUKOV, Alex; DINU, Daniel; KHOVRATOVICH, Dmitry; JOSEFSSON, Simon. **Argon2 Memory-Hard Function for Password Hashing and Proof-of-Work Applications**. RFC 9106, Internet Research Task Force (IRTF), 2021. Disponível em: <https://datatracker.ietf.org/doc/html/rfc9106>. Acesso em: 18 out. 2026.
13. NODE.JS. **Crypto — Node.js v22 Documentation**. OpenJS Foundation. Disponível em: <https://nodejs.org/docs/latest-v22.x/api/crypto.html>. Acesso em: 18 out. 2026.
14. M'RAIHI, David; BELLARE, Mihir; HOORNAERT, Frank; NACCACHE, David; RANEN, Ohad. **HOTP: An HMAC-Based One-Time Password Algorithm**. RFC 4226, Internet Engineering Task Force (IETF), 2005. Disponível em: <https://datatracker.ietf.org/doc/html/rfc4226>. Acesso em: 18 out. 2026.
15. JONES, Michael; BRADLEY, John; SAKIMURA, Nat. **JSON Web Token (JWT)**. RFC 7519, Internet Engineering Task Force (IETF), 2015. Disponível em: <https://datatracker.ietf.org/doc/html/rfc7519>. Acesso em: 18 out. 2026.
16. KIRSCH, Adam; MITZENMACHER, Michael. Less Hashing, Same Performance: Building a Better Bloom Filter. **Random Structures & Algorithms**, v. 33, n. 2, p. 187-218, 2008.
17. GRASSI, Paul A. et al. **Digital Identity Guidelines: Authentication and Lifecycle Management**. NIST Special Publication 800-63B. Gaithersburg: National Institute of Standards and Technology, 2017. Disponível em: <https://doi.org/10.6028/NIST.SP.800-63b>. Acesso em: 18 out. 2026.

## Versionamentos & Participações

Registrar apenas alterações efetivamente realizadas, incluindo autoria, revisão e links para commits ou pull requests.

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| --- | --- | --- | --- | --- | --- |
| 1.0 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Código do Chain of Responsibility: domínio derivado da Entrega 02, Handler, oito ConcreteHandlers, montagem das cadeias de login e step-up, `LoginService`, 56 testes, demonstração e manual do código | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): execução de `npm run check` e `npm run demo`; conferência de cada elo contra as regras A1–A8 e dos testes de ordem e de ponto de parada da cadeia | [`6b7cdba`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/6b7cdba) · [`21ee94d`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/21ee94d) · [`076bd49`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/076bd49) · [`38bf862`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/38bf862) |
| 1.1 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | ADR-004: contexto, regras A1–A8, sete alternativas, decisão e decisões D1–D9 | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência das regras A1–A8 contra a Entrega 01 (O05–O07, C03) e a Entrega 02, das alternativas descartadas e das decisões D1–D9 | [`7363f87`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/7363f87) |
| 1.2 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Diagrama de classes (PlantUML, SVG, PNG), correspondência com a Entrega 02 e evidências COR-E01 a COR-E06 | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência dos participantes e relações do diagrama contra o código, da correspondência com as classes de autenticação da Entrega 02 e das evidências COR-E01 a COR-E06 | [`b671baf`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/b671baf) |
| 1.3 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Diagrama de sequência do login com segundo fator | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência da ordem das mensagens contra `buildLoginChain` e dos caminhos de recusa, desafio e sucesso | [`ff624e6`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/ff624e6) |
| 1.4 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Este relatório: estado, estrutura, relato de IA de Hugo, metodologia do padrão, contexto, escolha, modelagem, implementação, execução, vídeo do padrão em funcionamento (2 min 20 s), rastreabilidade, senso crítico e referências em ABNT | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): leitura do relatório, conferência dos links de rastreabilidade, dos comandos de execução e do vídeo | [`6b738dd`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/6b738dd) · [`4e802a1`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/4e802a1) |
| 1.5 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Navegação, visão geral do módulo, checklist e quadro de participações atualizados com o Chain of Responsibility | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência da navegação e do estado da SubEquipe_03 na visão geral, no checklist e no quadro de participações | [`49c371c`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/49c371c) |
| 1.6 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Referências refeitas no formato da SubEquipe_03 na Entrega 01: lista numerada pela ordem de citação, citações numéricas no texto, sem a coluna de fundamentação e sem os artefatos do próprio grupo; o mesmo no ADR-004 e na legenda da modelagem | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência do formato das referências com o da Entrega 01, das citações numéricas e dos links | [`555c4a9`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/555c4a9) |
| 1.7 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Revisão de Eduardo Lôbo Moreira e Philipe Amâncio Reis Caetano registrada nas versões 1.0 a 1.6, no ADR-004 (status aceito) e nas páginas de modelagem e sequência; revisão por pares acrescentada à metodologia | Não se aplica (registro da revisão) | [`2c57706`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/2c57706) |
| 1.8 | 19/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Código migrado para o repositório dedicado da subequipe (branch `feat/autenticacao-chainOfResponsibilityBehavioralGoF`), no padrão dos repositórios de Philipe e da SubEquipe_01; links, estrutura e passo a passo atualizados; novo vídeo com narração sintetizada, roteiro atualizado e zoom nas figuras do padrão; relato de IA no modelo da Entrega 01, com o uso de voz sintética na narração | A revisar | [PR do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/feat/autenticacao-chainOfResponsibilityBehavioralGoF) |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
