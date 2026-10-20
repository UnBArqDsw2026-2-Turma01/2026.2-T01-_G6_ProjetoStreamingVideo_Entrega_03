# 1.1.3. SubEquipe_03 — GoFs Comportamentais + IA Generativa

**Estado:** em elaboração. A SubEquipe 03 aborda os **Padrões de Projeto GoF Comportamentais** divididos em três focos funcionais complementares da plataforma de streaming:

1. **Moderação Reativa e Segurança de Transmissão:** modelagem e implementação do padrão **GoF Observer** aplicado ao ciclo de vida de lives e ao pipeline reativo de moderação no `StreamChannel` (elaborado por **Eduardo Lôbo Moreira**), registrado em [1.1.3.1. Modelagem — Observer (Moderação)](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md), [1.1.3.2. Sequência — Observer (Moderação)](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) e em [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md).
2. **Autenticação:** padrão **GoF Chain of Responsibility** aplicado ao login e à reautenticação (*step-up*), elaborado por **Hugo Freitas Silva**, registrado em [1.1.3.3. Modelagem](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md), [1.1.3.4. Sequência](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) e [ADR-004](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md).
3. **Chat em Tempo Real:** padrão **GoF Observer** aplicado à sala de chat (`ChatRoom`), integrado à moderação, elaborado por **Philipe Amâncio Reis Caetano**; o código está integrado ao [repositório de código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main/src/chat) e a documentação do foco está em elaboração.

Este relatório reúne a Entrega 03 da subequipe. Os focos de **Moderação** e **Autenticação** estão modelados, implementados, testados e documentados; o foco de **Chat** tem código e testes integrados, e a modelagem, o vídeo e o relato individual de Philipe serão acrescentados pelo integrante responsável. O código dos três focos está na `main` do [repositório de código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo).

---

## Integrantes e Divisão de Focos

| Matrícula | Integrante | GitHub | Foco Comportamental na Entrega 03 |
| :---: | :--- | :---: | :--- |
| 24/1011027 | Eduardo Lôbo Moreira | [@EduLoboM](https://github.com/EduLoboM) | **Moderação Reativa e Segurança de Transmissão** (Padrão: **GoF Observer**) |
| 24/1041302 | Hugo Freitas Silva | [@HugoFreitass](https://github.com/HugoFreitass) | **Autenticação e Sessão** (Padrão: **GoF Chain of Responsibility**) |
| 24/1040350 | Philipe Amâncio Reis Caetano | [@Phill-Chill](https://github.com/Phill-Chill) | **Chat em Tempo Real** (Padrão: **GoF Observer**) |

Composição mantida conforme a [introdução da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Introducao).

---

## Foco do relatório

**GoFs Comportamentais + IA Generativa.** A entrega mínima deste foco inclui ao menos um padrão comportamental por foco da plataforma, modelo UML, código e vídeo demonstrando sua execução, além dos pontos de vista individuais.

## Estrutura da subequipe e focos entregues

```text
SubEquipe_03 — GoFs Comportamentais + IA Generativa
├── 📘 Documentação · este repositório · docs/Base/Relatórios/1.1.3.SubEquipe_03/
│   ├── README.md                     relatório geral (contexto, escolha, execução, versões)
│   ├── 1.1.3.1.ModelagemObserver.md  UML de classes GoF, componentes e casos de uso (Foco: Moderação)
│   ├── 1.1.3.2.SequenciaObserver.md  UML de sequência de moderação, estados e atividades (Foco: Moderação)
│   ├── 1.1.3.3.ModelagemChainOfResponsibility.md  UML de classes + evidências COR-E01–COR-E06 (Foco: Autenticação)
│   ├── 1.1.3.4.SequenciaChainOfResponsibility.md  UML de sequência do login com segundo fator (Foco: Autenticação)
│   ├── 1.1.3.5.Video.md              vídeos dos padrões (Autenticação publicado; roteiro da Moderação)
│   ├── 1.1.3.6.IAGenerativa.md       pontos de vista individuais (Eduardo e Hugo preenchidos; Philipe a preencher)
│   ├── ADR/ADR-003-observer-concorrente-notificacoes-twitch.md
│   ├── ADR/ADR-004-chain-of-responsibility-autenticacao.md
│   └── assets/                       exportações SVG/PNG de diagramas e prints de fontes
└── 💻 Código-fonte e Executáveis · repositório separado · g6-streaming-entrega03-subgrupo03-codigo
    ├── src/patterns/observer/        StreamChannel, interfaces e observadores de moderação
    ├── src/patterns/strategy/        estratégias de despacho síncrono e assíncrono
    ├── src/engine/algorithms/        algoritmos de Entropia, Visão Computacional, DMCA e dHash
    ├── src/__tests__/                13 testes unitários automatizados (Node Test Runner)
    ├── src/interactive.ts            console interativo REPL com comandos em tempo real (Iniciativa Extra)
    ├── src/webServer.ts              dashboard web de moderação em tempo real (Iniciativa Extra)
    ├── src/demo.ts                   demonstração automatizada nos canais YouTube, Twitch e Kick
    ├── src/benchmark.ts              teste de carga comparativo com 2.000 espectadores (Iniciativa Extra)
    ├── src/autenticacao/             Chain of Responsibility: elos (cadeia/), domínio da Entrega 02, LoginService e demo
    ├── src/chat/ · src/moderation/   Observer da sala de chat e contratos de moderação
    └── tests/                        56 testes da autenticação e 5 do chat (Node Test Runner)
```

| Foco da entrega | Moderação: Observer (`StreamChannel`) | Autenticação: GoF Comportamental | Chat: GoF Comportamental | Onde |
| :--- | :---: | :---: | :---: | :--- |
| **Contexto e justificativa** | ✅ Eduardo | ✅ Hugo | 🟡 pendente (Philipe) | [Contexto](#contexto-problema) · [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md) · [ADR-004](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md) |
| **Modelagem UML — Classes** | ✅ Eduardo | ✅ Hugo | 🟡 pendente | [1.1.3.1](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md) · [1.1.3.3](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md) |
| **Modelagem UML — Sequência** | ✅ Eduardo | ✅ Hugo | 🟡 pendente | [1.1.3.2](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) · [1.1.3.4](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) |
| **Implementação e Testes** | ✅ integrado em 17/10/2026 | ✅ 56 testes ([PR #2 do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/2)) | ✅ 5 testes ([PR #1 do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/1)) | [Repositório de código (`main`)](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main) · `npm test` |
| **Execução documentada** | ✅ `demo` · `benchmark` · `interactive` · `web` | ✅ `demo:autenticacao` · `check:autenticacao` | 🟡 pendente | [Execução](#execução-e-vídeo-do-padrão-em-funcionamento) |
| **Vídeo** | ⬜ roteiro pronto | ✅ 2 min 05 s | ⬜ a preencher | [1.1.3.5](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md) |
| **IA Generativa** | 🟡 Eduardo preenchido | ✅ Hugo preenchido | 🟡 a preencher | [1.1.3.6](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md) |

Legenda: ✅ entregue · 🟡 em andamento · ⬜ não iniciado.

---

## IA Generativa e vídeo

Os pontos de vista individuais ficam em [1.1.3.6. IA Generativa](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md) e os vídeos dos padrões em [1.1.3.5. Vídeo](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md).

| Integrante | Foco | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| :--- | :--- | :--- | :--- |
| **Eduardo Lôbo Moreira** | Moderação Reativa (Observer) | Desacoplamento no GoF canônico e modelagem temporal | [Preenchido](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md?id=eduardo-lôbo-moreira-foco-moderação-reativa-gof-observer) |
| **Hugo Freitas Silva** | Autenticação (Chain of Responsibility) | Mesma família de elos em duas cadeias; falha fechada; ordem dos elos como requisito de segurança | [Preenchido](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md?id=hugo-freitas-silva-foco-autenticação-chain-of-responsibility) |
| **Philipe Amâncio Reis Caetano** | Chat em Tempo Real | A preencher pelo integrante | A preencher pelo integrante |

---

## Metodologia

Como contexto de planejamento inicial, a [ata da Reunião Geral 1](/Projeto/Atas/ata-G01-2026-10-05.md) registra a sugestão de Observer para notificações e mensagens de chat. A ata não registra uma escolha final; esta seção deve descrever as decisões e o trabalho efetivamente adotados pela subequipe.

**Chain of Responsibility (Hugo Freitas Silva).** O trabalho seguiu cinco passos:

1. **Estudo do padrão.** Aula de GoFs comportamentais da disciplina, slides 9 e 61 [6], capítulo do padrão no GoF [7] e materiais de referência sobre o padrão [8, 9].
2. **Releitura das entregas anteriores.** Escopo do produto e NFR Framework da SubEquipe_03 na Entrega 01, diagrama de classes de autenticação e modelagem dinâmica da Entrega 02. Cada afirmação usada virou evidência arquivada (COR-E03 a COR-E06).
3. **Decisão antes do código.** Regras A1–A8 e decisões D1–D9 registradas no [ADR-004](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md), com sete alternativas comparadas.
4. **Código, testes e modelos em conjunto.** Um elo por classe, com testes isolados por sucessor dublê; diagramas PlantUML desenhados a partir do código e conferidos contra ele; demonstração com relógio fixo para a saída ser reproduzível.
5. **Revisão e integração.** O código entrou na `main` do repositório de código pelo [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/2), revisado e integrado por Philipe Amâncio Reis Caetano; a documentação, pelo [PR #12](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/12).

Ferramentas: TypeScript, `node:test`, `tsx`, PlantUML, Docsify, Git e GitHub.

**Organização da subequipe.** Cada integrante assumiu um foco do produto — moderação (Eduardo), autenticação (Hugo) e chat (Philipe) — e desenvolveu o código numa branch própria do [repositório de código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo), integrada à `main` por pull request: [#3](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/3) (Observer da moderação), [#1](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/1) (chat, revisado e integrado por Hugo) e [#2](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/2) (autenticação, revisado e integrado por Philipe). A documentação seguiu o mesmo fluxo neste repositório. A subequipe não registrou atas próprias nesta entrega; o planejamento comum está na [Reunião Geral 1](/Projeto/Atas/ata-G01-2026-10-05.md) e nos [registros de reuniões](/Projeto/Atas/README.md).

## GoF Comportamental

### Contexto (problema)

#### Foco 1: Moderação Reativa e Segurança de Transmissão (Eduardo Lôbo Moreira)

Em plataformas de streaming UGC (*User-Generated Content*) como **Twitch**, **YouTube Live** e **Kick.com**, a gestão de uma transmissão ao vivo impõe dois desafios centrais:

1. **Notificação de Alta Escala:** Quando um criador entra ao vivo (*go live*), milhares de seguidores, servidores de Discord e sistemas móveis devem ser sinalizados imediatamente. Um laço síncrono linear tradicional congela a thread principal do canal por mais de 10 segundos para 2.000 inscritos, degradando a interface do criador.
2. **Fiscalização de Conformidade e Segurança em Tempo Real:** Streams abertas estão sujeitas a invasões de bots (chat raids), transmissões de conteúdo impróprio (violência extrema / gore, nudez explícita) e uso não autorizado de faixas musicais protegidas por direitos autorais (DMCA). O sistema de transmissão precisa reagir instantaneamente a esses incidentes aplicando salvaguardas (ativação de Content Warning 18+, silenciamento de áudio ou encerramento compulsório) sem acoplar o canal às regras de cada inteligência artificial ou algoritmo de moderação.

#### Foco 2: Autenticação — Chain of Responsibility (Hugo Freitas Silva)

A autenticação é responsabilidade da SubEquipe_03 desde a Entrega 01, em que "Login/Cadastro & Autenticação (incl. 2FA/OAuth)" foi o fluxo mínimo da subequipe (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e03-e01-escopo-fluxo-login-subequipe03.png" target="_blank" rel="noopener">COR-E03</a>). O NFR Framework da mesma entrega pediu rate limiting no login (O07), MFA para quem transmite (O05) e credenciais com função de derivação resistente (O06), e resolveu o conflito C03 exigindo MFA **só** de criadores e transações financeiras (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e04-e01-nfr-o05-o06-o07.png" target="_blank" rel="noopener">COR-E04</a>, <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e05-e01-nfr-conflito-c03.png" target="_blank" rel="noopener">COR-E05</a>). Na Entrega 02, o diagrama de classes de autenticação modelou as peças — atestação do cliente com prova de trabalho, conta e estado, credencial, filtro de senhas vazadas, TOTP, sessão, desafio de step-up e auditoria (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e06-e02-classes-autenticacao.png" target="_blank" rel="noopener">COR-E06</a>).

O que faltava era a coordenação: a modelagem dinâmica da Entrega 02 registra que o detalhamento do login, do desafio de borda, do MFA e da emissão de tokens não foi concluído. Escritas num único método, essas verificações viram uma sequência de condicionais em que cada regra conhece as outras, e o step-up (rotação de stream key, saque) repetiria metade do login. Detalhes em [ADR-004 §1](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_1-contexto).

#### Foco 3: Chat em Tempo Real (Philipe Amâncio Reis Caetano)

**Pendente:** Contexto e requisitos de mensageria em salas de chat, moderação distribuída e entrega em tempo real a preencher pelo integrante Philipe Amâncio Reis Caetano.

---

### Escolha e justificativa

#### Foco 1: Moderação Reativa — GoF Observer (Eduardo Lôbo Moreira)

**Padrão GoF Observer** (Slides 08 e 53) para `StreamChannel` e pipeline de moderação:
- Define uma dependência um-para-muitos entre objetos, de forma que quando o `StreamChannel` (Sujeito) muda de estado ou identifica um evento, todos os observadores inscritos são notificados e atualizados automaticamente.
- Atende integralmente ao Princípio Aberto/Fechado (OCP), permitindo plugar novos sistemas de moderação ou canais de notificação sem alterar o código do canal.
- A entrega das notificações aos observadores é delegada via **GoF Strategy** (`INotificationDispatchStrategy`), permitindo alternar dinamicamente entre um laço síncrono linear e um despacho assíncrono concorrente com Worker Pool (**Iniciativa Extra**).

Alternativas consideradas e descartadas (*Polling* periódico pelos clientes e *GoF Mediator*), juntamente com os limites declarados, estão detalhadas no [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md).

#### Foco 2: Autenticação — Chain of Responsibility (Hugo Freitas Silva)

**Chain of Responsibility** (padrão comportamental GoF) para o login e o step-up: cada verificação é um elo — limite de tentativas, atestação do cliente, senha, estado da conta, senha vazada, segundo fator — que **recusa**, **responde** (com um desafio de segundo fator) ou **repassa** ao próximo; o último elo cria a sessão ou conclui o step-up. O `LoginService` entrega o pedido só ao primeiro elo e não sabe qual vai respondê-lo, que é a intenção do padrão no GoF [7] e na aula da disciplina [6]: evitar a dependência entre quem solicita e quem trata, com a base mantendo o ponteiro para o "próximo" (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e01-slide09-visao-geral-comportamentais.png" target="_blank" rel="noopener">COR-E01</a>, <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e02-slide61-modelagem-chain.png" target="_blank" rel="noopener">COR-E02</a>). O Spring Security organiza a autenticação da mesma forma, com uma cadeia de filtros [10] e um `ProviderManager` que delega a uma lista de provedores [5].

Alternativas descartadas, com o argumento de cada uma — método único, Strategy (que já é usado por Eduardo no despacho do Observer), State, Template Method, Decorator e pipeline de funções — estão em [ADR-004 §3](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_3-alternativas-consideradas), junto das regras A1–A8 e das decisões D1–D9.

**Limites declarados:** o fim da cadeia recusa (falha fechada), diferente do GoF, em que o pedido pode ficar sem tratamento [7] (D2); o `RateLimitHandler` age também na volta do pedido, variação de cadeia de filtros que o GoF puro não prevê (D5); e a credencial usa scrypt [11] em vez do Argon2id [12] da Entrega 01, porque o módulo `crypto` do Node 22 não oferece Argon2 [13]; o OWASP indica scrypt nesse caso [4] (D9).

**Relação com os outros padrões do grupo.** O Builder e o Factory Method da SubEquipe_01 criam a configuração e o conteúdo da transmissão; o Observer de Eduardo reage a eventos do canal. O Chain of Responsibility fica antes de todos eles: decide se a pessoa entra e, no step-up, se pode executar ações sensíveis sobre o canal, como rotacionar a stream key que o fluxo de transmissão usa.

#### Foco 3: Chat em Tempo Real (Philipe Amâncio Reis Caetano)

**Pendente:** Escolha e justificativa do padrão GoF comportamental aplicado ao chat a preencher por Philipe Amâncio Reis Caetano.

---

### Modelagem (notação UML)

#### Foco 1: Moderação Reativa — GoF Observer (Eduardo Lôbo Moreira)

- **Diagrama de Classes UML (GoF Observer + Strategy), Componentes e Casos de Uso:** [1.1.3.1. Modelagem — Observer (Moderação)](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md). Fonte vetorial SVG e PNG em `assets/diagramas/`.
- **Diagrama de Sequência UML (Pipeline Reativo de Moderação), Máquina de Estados e Atividades:** [1.1.3.2. Sequência — Observer (Moderação)](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md).

#### Foco 2: Autenticação — Chain of Responsibility (Hugo Freitas Silva)

**Chain of Responsibility — classes.** Diagrama "antes" (recorte do diagrama de autenticação da Entrega 02) e "depois" (padrão aplicado), correspondência entre participantes GoF e classes, regras A1–A8 e evidências: [1.1.3.3. Modelagem — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md). Fonte editável em PlantUML e exportações PNG/SVG em <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/chain-of-responsibility-classes-v1.puml" target="_blank" rel="noopener"><code>assets/chain-of-responsibility/</code></a>. Autoria: Hugo Freitas Silva.

**Chain of Responsibility — sequência.** Login de uma criadora com segundo fator, com o ponto de parada de cada recusa, o desafio TOTP e a volta pelo `RateLimitHandler`: [1.1.3.4. Sequência — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md). Fonte editável em <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/chain-of-responsibility-sequencia-v1.puml" target="_blank" rel="noopener"><code>chain-of-responsibility-sequencia-v1.puml</code></a>. Autoria: Hugo Freitas Silva.

![Diagrama de classes do Chain of Responsibility](assets/chain-of-responsibility/chain-of-responsibility-classes-v1.png)

*Figura 1 — Diagrama de classes do Chain of Responsibility aplicado à autenticação, v1. Autoria: Hugo Freitas Silva, 2026.*

#### Foco 3: Chat em Tempo Real (Philipe Amâncio Reis Caetano)

**Pendente:** Diagramas de classes e de sequência do padrão comportamental aplicado ao chat a serem adicionados pelo integrante responsável.

---

### Implementação (código)

#### Foco 1: Moderação Reativa (Eduardo Lôbo Moreira)

Concluído e integrado no [repositório de código da SubEquipe_03](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/feat/moderacao-observerBehavioralGoF), mantido separado deste repositório para que código e testes não interfiram na publicação do GitHub Pages:
- `src/patterns/observer/StreamChannel.ts`: ConcreteSubject e Context.
- `src/patterns/observer/interfaces.ts`: interfaces `ISubject`, `IObserver`, `StreamEvent`.
- `src/patterns/observer/observers/`: observadores especializados (`AutoModObserver`, `SafetyVisionModerationObserver`, `CopyrightDMCAAudioObserver`, `HumanModeratorDashboardObserver`, `ChatRaidShieldObserver`, `PiracyVideoRestreamObserver`).
- `src/patterns/strategy/`: estratégias de despacho síncrona e assíncrona concorrente.
- `src/interactive.ts`: console interativo REPL com comandos em tempo real (**Iniciativa Extra**).
- `src/__tests__/observer.test.ts`: 13 testes unitários automatizados cobrindo ciclo de vida e moderação (`npm test`).

#### Foco 2: Autenticação — Chain of Responsibility (Hugo Freitas Silva)

Código em <a href="https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main/" target="_blank" rel="noopener"><code>g6-streaming-entrega03-subgrupo03-codigo</code></a> — repositório de código dedicado da subequipe, pasta `src/autenticacao/` da `main`, onde convive com o Observer de Eduardo e o chat de Philipe. Foi desenvolvido na branch `feat/autenticacao-chainOfResponsibilityBehavioralGoF` e integrado pelo [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/2). TypeScript sem dependência de execução: a criptografia (scrypt, HMAC, SHA-256) vem do módulo `node:crypto`; `tsx`, `typescript` e `@types/node` são só de desenvolvimento. Um arquivo por participante:

| Participante | Arquivo | Trecho que realiza o padrão |
| --- | --- | --- |
| Handler | `src/autenticacao/cadeia/authentication-handler.ts` | interface `AuthenticationHandler` (`setNext`, `handle`); `AbstractAuthenticationHandler.handle` registra o elo na trilha e chama `next.handle`; sem sucessor, recusa com `UNHANDLED` |
| ConcreteHandler | `rate-limit-handler.ts`, `client-integrity-handler.ts`, `password-handler.ts`, `account-status-handler.ts`, `leaked-password-handler.ts`, `two-factor-handler.ts` | cada `handle` verifica uma regra e devolve a recusa ou chama `super.handle(context)` |
| ConcreteHandler terminal | `session-issuer-handler.ts`, `step-up-grant-handler.ts` | tratam o pedido (sessão + token, ou desafio concluído) e não repassam |
| Client | `src/autenticacao/login-service.ts` | `login` e `confirmStepUp` entregam o contexto ao primeiro elo e registram a auditoria |
| Request | `src/autenticacao/cadeia/authentication-context.ts` | `AuthenticationRequest` e `AuthenticationContext` (conta, marcas e trilha) |
| Montagem | `src/autenticacao/cadeia/authentication-chains.ts` | `buildLoginChain` e `buildStepUpChain`, com `setNext` encadeado |

O [README do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/README.md) resume participantes e limites. O segundo fator é TOTP [1], construído sobre o HOTP [14]; a sessão recebe um JWT assinado com HMAC-SHA-256 [15]; a lista de senhas vazadas é um filtro de Bloom [2] com índices por hash duplo [16], e exigir a troca dessas senhas segue a recomendação de comparar senhas com listas de comprometidas [17]. São 56 testes: os elos isolados com um sucessor dublê, as duas cadeias montadas, o `LoginService`, o domínio e os vetores da RFC 6238.

#### Foco 3: Chat em Tempo Real (Philipe Amâncio Reis Caetano)

Integrado à `main` do repositório de código pelo [PR #1](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/1), em [`src/chat/`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main/src/chat) e [`src/moderation/`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main/src/moderation):
- `ChatRoom.ts`: Subject do **GoF Observer** (`subscribe`, `unsubscribe`, `publish`); só notifica os observadores quando a moderação aprova a mensagem.
- `ChatObserver.ts` e `ChatDeliveryService.ts`: contrato `update(message)` e observador que entrega as mensagens aprovadas.
- `src/moderation/`: `AutoModPipeline`, `ModerationDecision` (aprovada, quarentena, rejeitada) e `ModerationVerdict`; mensagens em quarentena vão para a `QuarantineQueue` e toda decisão é registrada no `ChatAuditService`.
- `tests/chat.test.ts`: 5 testes (entrega, quarentena, rejeição, inscrição sem duplicidade e cópias defensivas), executados por `npm test` e `npm run test:chat` com a correção proposta no [PR #4](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/4): depois da integração dos três focos, o arquivo original em JavaScript deixou de rodar no projeto.

Modelagem UML, contexto, justificativa e vídeo do chat: a cargo de Philipe; há um relatório em elaboração na branch [`feat/chat_BehavioralGoF_Observer`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/tree/feat/chat_BehavioralGoF_Observer).

---

### Execução e vídeo do padrão em funcionamento

#### Foco 1: Moderação Reativa (Eduardo Lôbo Moreira)

**Pré-requisitos:** Node.js v20+ e npm v10+.

Código no [repositório de código da SubEquipe_03](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/feat/moderacao-observerBehavioralGoF):

```bash
git clone https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo.git
cd g6-streaming-entrega03-subgrupo03-codigo
git checkout feat/moderacao-observerBehavioralGoF
npm install
npm run web          # Dashboard Web em Tempo Real (http://localhost:3333) - Iniciativa Extra
npm run interactive  # Console interativo REPL com comandos em tempo real - Iniciativa Extra
npm run demo         # Demonstração automatizada do GoF Observer e moderação reativa
npm run benchmark    # Teste de carga comparativo com 2.000 espectadores - Iniciativa Extra
npm test             # 13 testes unitários automatizados nativos
```

**Cenários Demonstrados na Moderação (`npm run demo`):**
1. **YouTube Live ([Sorashina Sopia](https://www.youtube.com/@SorashinaSopia/videos)):** Entrada ao vivo, push notifications e encerramento.
2. **Twitch (Dima Wallhacks):** Detecção de spam no chat via AutoMod, detecção de fonograma protegido por DMCA com silenciamento de áudio.
3. **Kick.com (eskimozin):** Detecção de sangue excessivo (Gore) via Visão Computacional em imagem PPM real, aplicação de aviso de conteúdo 18+ (*Content Warning*) e ação de moderador no ModView.

**Iniciativa Extra — Resultados Empíricos do Benchmark (2.000 Espectadores):**

| Estratégia Adotada | Espectadores | Bloqueio da Thread (ms) | Tempo Total (ms) | Vazão (Throughput) | Falhas Isoladas |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Síncrona Clássica** *(Slide 53 naive)* | 2.000 | 10.404,62 ms | 10.405,75 ms | 192,2 notif/s | Risco de cascata |
| **Assíncrona Concorrente** *(Iniciativa Extra)* | 2.000 | **6,66 ms** | **89,35 ms** | **22.383,7 notif/s** | **100% isoladas via `allSettled`** |
| **Otimização Obtida** | - | **1.561,7x mais rápido** 🚀 | **116,5x mais rápido** ⚡ | **+11.546%** | **Alta disponibilidade** |

O roteiro detalhado do vídeo encontra-se em [1.1.3.5. Vídeo](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md).

#### Foco 2: Autenticação — Chain of Responsibility (Hugo Freitas Silva)

**Pré-requisitos:** Node 20 ou superior e npm. Nenhuma outra dependência global; o TypeScript roda pelo `tsx`, sem etapa de build.

```bash
git clone https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo.git
cd g6-streaming-entrega03-subgrupo03-codigo
npm ci                        # instala as dependências travadas no package-lock
npm run check:autenticacao    # tipos (tsc --noEmit) e os 56 testes (node:test)
npm run demo:autenticacao     # demonstração no terminal
```

**Cenário demonstrado (`npm run demo:autenticacao`).** Cinco contas fictícias, relógio fixo e ids sequenciais, para a saída ser igual a cada execução:

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

O vídeo do Chain of Responsibility, com roteiro e forma de produção, está em [1.1.3.5. Vídeo](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md?id=_2-vídeo-de-autenticação-chain-of-responsibility).

---

## Rastreabilidade Bidirecional Formal & Elos Arquiteturais (E01 ➔ E02 ➔ E03)

A rastreabilidade bidirecional estabelece a coerência entre as necessidades de negócio elicitadas (**Entrega 01**), os modelos estáticos/dinâmicos em notação UML (**Entrega 02**) e os Padrões de Projeto GoF implementados (**Entrega 03**), garantindo conformidade com a rubrica metodológica da disciplina de Desenho de Software.

### 1. Rastreabilidade *Forward* (Dos Requisitos E01 e Modelos E02 para os Padrões GoF E03)

| Requisito de Origem (E01) | Modelo de Referência (E02) | Elemento GoF / Participante (E03) | Implementação no Repositório | Comprobatório de Execução e Testes |
| :--- | :--- | :--- | :--- | :--- |
| **RF01:** Iniciar e encerrar transmissões ao vivo multicanal | **UC01:** Transmitir ao Vivo · **DiagSeq02:** Abertura de Live | `ISubject` & `StreamChannel` (`goLive`, `endLive`) | [`StreamChannel.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/StreamChannel.ts) | `npm test` (Teste 2) · `npm run web` (Botão 1) |
| **RF15:** Notificação em tempo real de seguidores e comunidades | **DiagAtiv03:** Disparo de Alertas a Inscritos | `IObserver` (`PushNotificationObserver`, `DiscordWebhookObserver`) | [`PushNotificationObserver.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/observers/PushNotificationObserver.ts) · [`DiscordWebhookObserver.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/observers/DiscordWebhookObserver.ts) | `npm run demo` (Etapa 3) · Push FCM e Discord |
| **RF07:** Moderação automatizada de mensagens e toxicidade no chat | **UC04:** Moderar Canal · **DiagAtiv03:** Filtro de Chat | `AutoModObserver` & `TextEntropyAnalyzer` | [`AutoModObserver.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/observers/AutoModObserver.ts) · [`TextEntropyAnalyzer.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/engine/algorithms/TextEntropyAnalyzer.ts) | `npm test` (Teste 3) · Shannon Entropy real |
| **RF08:** Detecção e contenção de conteúdo sensível (Nudez/Gore) | **DiagSeq05:** Pipeline Reativo de Inspeção de Frame | `SafetyVisionModerationObserver` | [`SafetyVisionModerationObserver.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/observers/SafetyVisionModerationObserver.ts) | `npm test` (Testes 4 e 5) · Imagem PPM real |
| **RF12:** Fiscalização de Direitos Autorais e Diretrizes de DMCA | **DiagAtiv03:** Análise de Faixa de Áudio | `CopyrightDMCAAudioObserver` & `AcousticFingerprinter` | [`CopyrightDMCAAudioObserver.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/observers/CopyrightDMCAAudioObserver.ts) · [`AcousticFingerprinter.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/engine/algorithms/AcousticFingerprinter.ts) | `npm test` (Teste 6) · Audio Mute e Strike |
| **RF09:** Auditoria e Intervenção de Moderadores Humanos | **UC04:** Moderar Canal (ModView E02) | `HumanModeratorDashboardObserver` | [`HumanModeratorDashboardObserver.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/observers/HumanModeratorDashboardObserver.ts) | `npm run web` · `npm run interactive` (`mod`) |
| **RNF02:** Desacoplamento arquitetural e extensibilidade (OCP) | **DiagClasses:** Arquitetura em Camadas | Interfaces canônicas `ISubject` e `IObserver` | [`interfaces.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/interfaces.ts) | Adição de 8 observadores sem alterar `StreamChannel` |
| **RNF04:** Alta vazão e liberação de thread (Desempenho) | **ADR-003:** Observer Concorrente Twitch | GoF Strategy: `AsynchronousConcurrentDispatchStrategy` | [`AsynchronousConcurrentDispatchStrategy.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/strategy/AsynchronousConcurrentDispatchStrategy.ts) | `npm run benchmark` (Speedup de 116.5x e 6.66ms) |
| **Foco 2 (Autenticação):** login com MFA, limite de tentativas e step-up (O05–O07, C03) | Classes de autenticação E02 (COR-E06) | GoF Chain of Responsibility: `AuthenticationHandler` e oito ConcreteHandlers | [Repositório de código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main) | Matriz detalhada em [3. Foco 2](/Base/Relatórios/1.1.3.SubEquipe_03/README.md?id=_3-foco-2-autenticação-chain-of-responsibility) |
| **Foco 3 (Chat):** Mensageria e Distribuição de Salas | Modelagem de Mensageria E02 | GoF Observer: `ChatRoom` (Subject) e `ChatObserver` | [`src/chat/`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main/src/chat) | [`tests/`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main/tests) (5 testes do chat) |

---

### 2. Rastreabilidade *Backward* (Do Código e Padrões GoF E03 para as Decisões de Arquitetura E02/E01)

| Elemento do Código GoF (E03) | Padrão e Papel Canônico | Justificativa Arquitetural no Projeto (E02/E01) | Decisão Formal Registrada |
| :--- | :--- | :--- | :--- |
| `StreamChannel` | **ConcreteSubject** (GoF Observer) | Centraliza o ciclo de vida da live sem se acoplar às regras específicas de cada inteligência artificial de moderação | [ADR-003: Contexto e Decisão](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md?id=_3-decisão-tomada) |
| `attach()` / `detach()` | **Subject Operations** (Slide 53) | Permite plugar ou desplugar observadores em tempo de execução sem derrubar o canal de streaming | [1.1.3.1. Modelagem — Classes](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md) |
| `getState()` | **Subject State Inspector** (Slide 53) | Fornece snapshot imutável do canal para clientes externos, ModView e Dashboard Web | [`interfaces.ts#L30`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/patterns/observer/interfaces.ts) |
| `INotificationDispatchStrategy` | **Strategy Interface** (GoF Strategy) | Isola o algoritmo de entrega de notificações, permitindo chavear entre laço síncrono e Worker Pool concorrente | [ADR-003: Estratégias Alternativas](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md?id=_2-padrões-e-alternativas-consideradas-fundamentação-teórica) |
| `AutoModObserver` | **ConcreteObserver** (Moderação) | Responde ao RF07 da E01 eliminando overhead de regex tradicional através da Entropia de Shannon | [1.1.3.2. Sequência — Pipeline](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) |
| `SafetyVisionModerationObserver` | **ConcreteObserver** (Moderação) | Implementa salvaguarda legal automática (Content Warning 18+) em conformidade com o Termo de Uso UGC da E01 | [1.1.3.1. Modelagem — Casos de Uso](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md?id=_5-diagrama-de-casos-de-uso-da-plataforma-ugc) |
| `HumanModeratorDashboardObserver` | **ConcreteObserver** (ModView) | Materializa a interface de auditoria do moderador prevista no UC04 da E02 | [Dashboard Web ModView](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/feat/moderacao-observerBehavioralGoF/src/webServer.ts) |
| `AbstractAuthenticationHandler` | **Handler** (GoF Chain of Responsibility) | Coordena as verificações de autenticação que a E02 modelou como classes isoladas; o fim da cadeia recusa (falha fechada) | [ADR-004, D1 e D2](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_4-decisão) |
| `RateLimitHandler` … `TwoFactorHandler` | **ConcreteHandler** (Autenticação) | Cada um realiza uma regra derivada do NFR da E01 (O05–O07, C03) e do diagrama de autenticação da E02 | [1.1.3.3. Modelagem — regras A1–A8](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md) |
| `LoginService` | **Client** (Autenticação) | Entrega o pedido só ao primeiro elo e registra a auditoria prevista no `IAuditLogger` da E02 | [1.1.3.4. Sequência — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) |
| `ChatRoom` | **Subject** (GoF Observer, Chat) | Desacopla a publicação de mensagens da entrega aos participantes, depois da decisão da moderação | [`ChatRoom.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/chat/ChatRoom.ts) |

### 3. Foco 2: Autenticação — Chain of Responsibility

A [modelagem da SubEquipe_03 na Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.SubEquipe_03) e o [NFR Framework da SubEquipe_03 na Entrega 01](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_01/#/Base/Relatorios/1.1.3.SubEquipe_03/2.NFRFramework) são as origens das regras abaixo. Os links de código apontam para a `main`, onde a pasta estará após a integração do pull request.

| Problema ou requisito | Artefato de origem (link) | Elemento do modelo | Trecho de código (link) | Evidência de execução (link) |
| --- | --- | --- | --- | --- |
| Login e autenticação como fluxo da SubEquipe_03 | [Escopo do Produto, Entrega 01](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_01/#/Projeto/EscopoProduto) (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e03-e01-escopo-fluxo-login-subequipe03.png" target="_blank" rel="noopener">COR-E03</a>) | Client `LoginService` e cadeia de login | [`login-service.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/login-service.ts) · [`authentication-chains.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/authentication-chains.ts) | Demo, partes 1 e 2 · teste `é montada na ordem decidida no ADR-004` |
| Ordem e coordenação do login não modeladas | [Modelagem Dinâmica, Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica) (delimitação) | Handler e [sequência](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.4.SequenciaChainOfResponsibility.md) | [`authentication-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/authentication-handler.ts) | Linhas `passou por` da demo |
| A1 — rate limiting no login (O07) | NFR, Entrega 01 (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e04-e01-nfr-o05-o06-o07.png" target="_blank" rel="noopener">COR-E04</a>) | `RateLimitHandler`, `LoginRateLimiter` | [`rate-limit-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/rate-limit-handler.ts) | Demo, parte 6 · teste `cinco falhas bloqueiam a sexta tentativa…` |
| A2 — atestação antes do hash (DE01) | Classes de autenticação, Entrega 02 (<a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e06-e02-classes-autenticacao.png" target="_blank" rel="noopener">COR-E06</a>) | `ClientIntegrityHandler`, `ClientIntegrityAttestation` | [`client-integrity-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/client-integrity-handler.ts) | Demo, parte 5 (webdriver) · testes `recusa atestação …` |
| A3 — mesma resposta para e-mail inexistente e senha errada | OWASP *Authentication Cheat Sheet* [3]; `Credential` da Entrega 02 (COR-E06) | `PasswordHandler` | [`password-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/password-handler.ts) | Demo, parte 5 · teste `e-mail inexistente e senha errada têm a mesma recusa` |
| A4 — estado da conta só após a senha | `AccountStatus`, Entrega 02 (COR-E06) | `AccountStatusHandler` | [`account-status-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/account-status-handler.ts) | Demo, parte 5 (conta suspensa) · teste `conta suspensa só é revelada a quem prova a senha` |
| A5 — senha vazada marca troca (DE02) | `LeakedPasswordBloomFilter`, Entrega 02 (COR-E06) | `LeakedPasswordHandler` | [`leaked-password-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/leaked-password-handler.ts) | Demo, parte 4 |
| A6 — MFA de criadores (O05, C03) | NFR, Entrega 01 (COR-E04, <a href="Base/Relatórios/1.1.3.SubEquipe_03/assets/chain-of-responsibility/evidencias/cor-e05-e01-nfr-conflito-c03.png" target="_blank" rel="noopener">COR-E05</a>) | `TwoFactorHandler`, `Account.requiresMfa` | [`two-factor-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/two-factor-handler.ts) | Demo, partes 3 e 5 · testes de `TwoFactorHandler` |
| A7 — TOTP ±1 passo, sem reuso | RFC 6238 §5.2 [1]; `TwoFactorAuth`, Entrega 02 | `TwoFactorAuth.verifyToken` | [`two-factor-auth.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/dominio/two-factor-auth.ts) | Demo, parte 3 (reuso) · vetores da RFC 6238 |
| A8 — fim da cadeia recusa | [ADR-004, D2](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-004-chain-of-responsibility-autenticacao.md?id=_4-decisão) | `AbstractAuthenticationHandler` | [`authentication-handler.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/authentication-handler.ts) | Demo, parte 8 · teste `sem sucessor, recusa com UNHANDLED` |
| Step-up antes de ação sensível | `StepUpAuthChallenge`, `StepUpTrigger`, Entrega 02 (COR-E06) | `buildStepUpChain`, `StepUpGrantHandler` | [`authentication-chains.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/cadeia/authentication-chains.ts) | Demo, parte 7 · teste `conclui o desafio com senha e código` |
| Auditoria de eventos de segurança | `IAuditLogger`, `SecurityEventType`, Entrega 02 (COR-E06) | Client `LoginService` | [`login-service.ts`](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/autenticacao/login-service.ts) | Demo, parte 9 · testes de `LoginService` |

As evidências COR-E01–COR-E06 são capturas arquivadas em [Modelagem — Chain of Responsibility](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.3.ModelagemChainOfResponsibility.md?id=evidências), cada uma com fonte e data no rodapé.

## Senso Crítico

### Foco 1: Moderação — Observer (Eduardo Lôbo Moreira)


**Benefícios (Moderação / Observer):** Desacoplamento estrito entre emissão de eventos e regras de moderação; adição de novos observadores sem modificar o `StreamChannel` (OCP); tolerância a falhas transitórias de socket em notificações remotas.

**Custos e limites:** Concorrência requer dimensionamento explícito do Worker Pool para evitar esgotamento de *file descriptors* no sistema operacional; consistência eventual na ordem de entrega de notificações assíncronas.

---

### Foco 2: Autenticação — Chain of Responsibility (Hugo Freitas Silva)

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

---

## Referências

### Foco 1: Moderação — Observer


1. **GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; VLISSIDES, John.** *Design Patterns: Elements of Reusable Object-Oriented Software*. Reading: Addison-Wesley, 1995.
2. **LARMAN, Craig.** *Utilizando UML e Padrões: Uma Introdução à Análise e ao Projeto Orientado a Objetos*. 3ª edição. Porto Alegre: Bookman, 2007.
3. **SOMMERVILLE, Ian.** *Engenharia de Software*. 8ª edição. São Paulo: Pearson Addison-Wesley, 2007.
4. **SERRANO, Milene.** *Arquitetura e Desenho de Software: Aula - GoFs Comportamentais*. Material didático da disciplina FGA0208. Universidade de Brasília (UnB Gama), [2019?].
5. **TWITCH DEVELOPERS.** *Twitch EventSub Documentation*. Disponível em: `https://dev.twitch.tv/docs/eventsub/`.
6. **GOOGLE DEVELOPERS.** *WebSub & Firebase Cloud Messaging*. Disponível em: `https://pubsubhubbub.appspot.com/`.

### Foco 2: Autenticação — Chain of Responsibility

As citações numéricas entre colchetes deste relatório (Metodologia e seções do Foco 2) remetem a esta lista; as obras do Foco 1 são citadas pelo nome do autor.

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

---

## Versionamentos & Participações

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| :---: | :---: | :--- | :--- | :--- | :---: |
| 0.1 | 16/10/2026 | Eduardo Lôbo Moreira | Modelagem do GoF Observer (foco Moderação), diagrama de classes e sequência, ADR-003 e código do StreamChannel | A preencher | Commit inicial SubEquipe 03 |
| 0.2 | 17/10/2026 | Eduardo Lôbo Moreira | Estruturação da divisão em 3 focos (Moderação, Autenticação e Chat) no padrão da SubEquipe 01, relato de IA e suíte de testes | A preencher | PR `docs/subequipe-03-modelagem-observer` |
| 0.3 | 18/10/2026 | Eduardo Lôbo Moreira | Implementação do console interativo REPL (`npm run interactive`) | A preencher | Commit `6ec8a38` |
| 0.4 | 18/10/2026 | Eduardo Lôbo Moreira | Implementação do Web ModView Dashboard (`npm run web`) e Matriz de Rastreabilidade Bidirecional Formal (E01 ➔ E02 ➔ E03) | A preencher | Commit `2af97fd` |
| 0.5 | 19/10/2026 | Eduardo Lôbo Moreira | Separação do código e testes em repositório dedicado (`g6-streaming-entrega03-subgrupo03-codigo`), alinhado ao padrão da SubEquipe 01 | A preencher | Branch `docs/subequipe-03-modelagem-observer` |
| 0.6 | 19/10/2026 | Eduardo Lôbo Moreira | Publicação do código na branch `feat/moderacao-observerBehavioralGoF` do repositório da organização UnBArqDsw2026-2-Turma01 | A preencher | Branch `docs/subequipe-03-modelagem-observer` |
| 1.0 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Código do Chain of Responsibility: domínio derivado da Entrega 02, Handler, oito ConcreteHandlers, montagem das cadeias de login e step-up, `LoginService`, 56 testes, demonstração e manual do código | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): execução de `npm run check` e `npm run demo`; conferência de cada elo contra as regras A1–A8 e dos testes de ordem e de ponto de parada da cadeia | [`6b7cdba`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/6b7cdba) · [`21ee94d`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/21ee94d) · [`076bd49`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/076bd49) · [`38bf862`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/38bf862) |
| 1.1 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | ADR-004: contexto, regras A1–A8, sete alternativas, decisão e decisões D1–D9 | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência das regras A1–A8 contra a Entrega 01 (O05–O07, C03) e a Entrega 02, das alternativas descartadas e das decisões D1–D9 | [`7363f87`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/7363f87) |
| 1.2 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Diagrama de classes (PlantUML, SVG, PNG), correspondência com a Entrega 02 e evidências COR-E01 a COR-E06 | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência dos participantes e relações do diagrama contra o código, da correspondência com as classes de autenticação da Entrega 02 e das evidências COR-E01 a COR-E06 | [`b671baf`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/b671baf) |
| 1.3 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Diagrama de sequência do login com segundo fator | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência da ordem das mensagens contra `buildLoginChain` e dos caminhos de recusa, desafio e sucesso | [`ff624e6`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/ff624e6) |
| 1.4 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Este relatório: estado, estrutura, relato de IA de Hugo, metodologia do padrão, contexto, escolha, modelagem, implementação, execução, vídeo do padrão em funcionamento (2 min 20 s), rastreabilidade, senso crítico e referências em ABNT | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): leitura do relatório, conferência dos links de rastreabilidade, dos comandos de execução e do vídeo | [`6b738dd`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/6b738dd) · [`4e802a1`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/4e802a1) |
| 1.5 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Navegação, visão geral do módulo, checklist e quadro de participações atualizados com o Chain of Responsibility | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência da navegação e do estado da SubEquipe_03 na visão geral, no checklist e no quadro de participações | [`49c371c`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/49c371c) |
| 1.6 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Referências refeitas no formato da SubEquipe_03 na Entrega 01: lista numerada pela ordem de citação, citações numéricas no texto, sem a coluna de fundamentação e sem os artefatos do próprio grupo; o mesmo no ADR-004 e na legenda da modelagem | [@EduLoboM](https://github.com/EduLoboM) e [@Phill-Chill](https://github.com/Phill-Chill): conferência do formato das referências com o da Entrega 01, das citações numéricas e dos links | [`555c4a9`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/555c4a9) |
| 1.7 | 18/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Revisão de Eduardo Lôbo Moreira e Philipe Amâncio Reis Caetano registrada nas versões 1.0 a 1.6, no ADR-004 (status aceito) e nas páginas de modelagem e sequência; revisão por pares acrescentada à metodologia | Não se aplica (registro da revisão) | [`2c57706`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/2c57706) |
| 1.8 | 19/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Código migrado para o repositório dedicado da subequipe (branch `feat/autenticacao-chainOfResponsibilityBehavioralGoF`), no padrão dos repositórios de Philipe e da SubEquipe_01; links, estrutura e passo a passo atualizados; novo vídeo com narração, roteiro atualizado e visualizador interativo com zoom nas figuras do padrão; relato individual no modelo da Entrega 01 | A revisar | [PR do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/tree/main) |
| 1.9 | 19/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Integração com a `main` (Observer de Eduardo): Chain of Responsibility como Foco 2 nas seções do relatório, quadro de focos, estrutura, rastreabilidade, senso crítico e referências; vídeo movido para 1.1.3.5 e relato de IA para 1.1.3.6; participações da SubEquipe_03 preenchidas | A revisar | [PR #12](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/12) |
| 1.10 | 19/10/2026 | [Hugo Freitas Silva](https://github.com/HugoFreitass) | Revisão da subequipe após a integração dos três focos: código de autenticação e chat apontando para a `main`; foco de Chat com o Observer integrado (estado, integrantes, estrutura, implementação, rastreabilidade); metodologia com o fluxo de PRs e revisões cruzadas; rastreabilidade *backward* com o Chain of Responsibility e o chat; links internos do Foco 1 corrigidos; data da aula alinhada entre as listas de referências; vídeo com a narração gravada por Hugo | A revisar | [PR da revisão](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pulls) · [PR #4 do código](https://github.com/UnBArqDsw2026-2-Turma01/g6-streaming-entrega03-subgrupo03-codigo/pull/4) |

O quadro consolidado de participações está em [1.2. Participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
