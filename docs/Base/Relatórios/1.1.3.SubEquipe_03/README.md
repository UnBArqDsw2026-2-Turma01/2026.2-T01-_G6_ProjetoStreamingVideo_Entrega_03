# 1.1.3. SubEquipe_03 — GoFs Comportamentais + IA Generativa

**Estado:** em elaboração. A SubEquipe 03 aborda os **Padrões de Projeto GoF Comportamentais** divididos em três focos funcionais complementares da plataforma de streaming:

1. **Moderação Reativa e Segurança de Transmissão:** modelagem e implementação do padrão **GoF Observer** aplicado ao ciclo de vida de lives e ao pipeline reativo de moderação no `StreamChannel` (elaborado por **Eduardo Lôbo Moreira**), registrado em [1.1.3.1. Modelagem — Observer (Moderação)](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md), [1.1.3.2. Sequência — Observer (Moderação)](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) e em [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md).
2. **Autenticação:** padrão GoF comportamental focado no fluxo de autenticação, verificação de credenciais e permissões de sessão, a ser definido e modelado por **Hugo Freitas Silva**.
3. **Chat em Tempo Real:** padrão GoF comportamental focado na mediação, distribuição e políticas de mensageria da sala de chat, a ser definido e modelado por **Philipe Amâncio Reis Caetano**.

Este relatório reúne os espaços necessários à Entrega 03. O conteúdo técnico do foco de **Moderação** já está modelado, implementado e testado; os demais focos e relatos individuais serão integrados pelos integrantes responsáveis.

---

## Integrantes e Divisão de Focos

| Matrícula | Integrante | GitHub | Foco Comportamental na Entrega 03 |
| :---: | :--- | :---: | :--- |
| 24/1011027 | Eduardo Lôbo Moreira | [@EduLoboM](https://github.com/EduLoboM) | **Moderação Reativa e Segurança de Transmissão** (Padrão: **GoF Observer**) |
| 24/1041302 | Hugo Freitas Silva | [@HugoFreitass](https://github.com/HugoFreitass) | **Autenticação e Sessão** (Padrão GoF Comportamental a definir) |
| 24/1040350 | Philipe Amâncio Reis Caetano | [@Phill-Chill](https://github.com/Phill-Chill) | **Chat em Tempo Real** (Padrão GoF Comportamental a definir) |

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
│   ├── 1.1.3.5.Video.md              roteiro detalhado e comandos de execução (3 a 5 min)
│   ├── 1.1.3.6.IAGenerativa.md       pontos de vista individuais (Eduardo preenchido; Hugo e Philipe a preencher)
│   ├── ADR/ADR-003-observer-concorrente-notificacoes-twitch.md
│   └── assets/                       exportações SVG/PNG de diagramas e prints de fontes
└── 💻 Código-fonte e Executáveis · repositório separado · g6-streaming-entrega03-subgrupo03-codigo
    ├── src/patterns/observer/        StreamChannel, interfaces e observadores de moderação
    ├── src/patterns/strategy/        estratégias de despacho síncrono e assíncrono
    ├── src/engine/algorithms/        algoritmos de Entropia, Visão Computacional, DMCA e dHash
    ├── src/__tests__/                13 testes unitários automatizados (Node Test Runner)
    ├── src/interactive.ts            console interativo REPL com comandos em tempo real (Iniciativa Extra)
    ├── src/webServer.ts              dashboard web de moderação em tempo real (Iniciativa Extra)
    ├── src/demo.ts                   demonstração automatizada nos canais YouTube, Twitch e Kick
    └── src/benchmark.ts              teste de carga comparativo com 2.000 espectadores (Iniciativa Extra)
```

| Foco da entrega | Moderação: Observer (`StreamChannel`) | Autenticação: GoF Comportamental | Chat: GoF Comportamental | Onde |
| :--- | :---: | :---: | :---: | :--- |
| **Contexto e justificativa** | ✅ Eduardo | 🟡 pendente (Hugo) | 🟡 pendente (Philipe) | [Contexto](#contexto-problema) · [ADR-003](ADR/ADR-003-observer-concorrente-notificacoes-twitch.md) |
| **Modelagem UML — Classes** | ✅ Eduardo | 🟡 pendente | 🟡 pendente | [1.1.3.1](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md) |
| **Modelagem UML — Sequência** | ✅ Eduardo | 🟡 pendente | 🟡 pendente | [1.1.3.2](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) |
| **Implementação e Testes** | ✅ integrado em 17/10/2026 | 🟡 pendente | 🟡 pendente | [Repositório de código](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo) · `npm test` |
| **Execução documentada** | ✅ `demo` · `benchmark` · `interactive` · `web` | 🟡 pendente | 🟡 pendente | [Execução](#execução-e-vídeo-do-padrão-em-funcionamento) |
| **Vídeo** | ⬜ roteiro pronto | ⬜ a preencher | ⬜ a preencher | [1.1.3.5](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md) |
| **IA Generativa** | 🟡 Eduardo preenchido | 🟡 a preencher | 🟡 a preencher | [1.1.3.6](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md) |

Legenda: ✅ entregue · 🟡 em andamento · ⬜ não iniciado.

---

## IA Generativa e vídeo

Os pontos de vista individuais ficam em [1.1.3.6. IA Generativa](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md) e os vídeos dos padrões em [1.1.3.5. Vídeo](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md).

| Integrante | Foco | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| :--- | :--- | :--- | :--- |
| **Eduardo Lôbo Moreira** | Moderação Reativa (Observer) | Desacoplamento no GoF canônico e modelagem temporal | [Preenchido](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md?id=eduardo-lôbo-moreira) |
| **Hugo Freitas Silva** | Autenticação | A preencher pelo integrante | A preencher pelo integrante |
| **Philipe Amâncio Reis Caetano** | Chat em Tempo Real | A preencher pelo integrante | A preencher pelo integrante |

---

## Metodologia

**A preencher em conjunto pela subequipe.** Descrever a dinâmica colaborativa de trabalho: divisão de atividades pelos três focos (Moderação, Autenticação e Chat), reuniões de alinhamento, estudos dos slides da Profa. Dra. Milene Serrano (*AULA - GOFS COMPORTAMENTAIS*), ferramentas e revisão por pares. Relacionar atas e gravações, quando houver, aos [registros de reuniões](/Projeto/Atas/README.md).

---

## GoF Comportamental

### Contexto (problema)

#### Foco 1: Moderação Reativa e Segurança de Transmissão (Eduardo Lôbo Moreira)

Em plataformas de streaming UGC (*User-Generated Content*) como **Twitch**, **YouTube Live** e **Kick.com**, a gestão de uma transmissão ao vivo impõe dois desafios centrais:

1. **Notificação de Alta Escala:** Quando um criador entra ao vivo (*go live*), milhares de seguidores, servidores de Discord e sistemas móveis devem ser sinalizados imediatamente. Um laço síncrono linear tradicional congela a thread principal do canal por mais de 10 segundos para 2.000 inscritos, degradando a interface do criador.
2. **Fiscalização de Conformidade e Segurança em Tempo Real:** Streams abertas estão sujeitas a invasões de bots (chat raids), transmissões de conteúdo impróprio (violência extrema / gore, nudez explícita) e uso não autorizado de faixas musicais protegidas por direitos autorais (DMCA). O sistema de transmissão precisa reagir instantaneamente a esses incidentes aplicando salvaguardas (ativação de Content Warning 18+, silenciamento de áudio ou encerramento compulsório) sem acoplar o canal às regras de cada inteligência artificial ou algoritmo de moderação.

#### Foco 2: Autenticação (Hugo Freitas Silva)

**Pendente:** Contexto e requisitos de autenticação de usuários, verificação de credenciais e gestão de sessão a preencher pelo integrante Hugo Freitas Silva.

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

#### Foco 2: Autenticação (Hugo Freitas Silva)

**Pendente:** Escolha e justificativa do padrão GoF comportamental aplicado à autenticação a preencher por Hugo Freitas Silva.

#### Foco 3: Chat em Tempo Real (Philipe Amâncio Reis Caetano)

**Pendente:** Escolha e justificativa do padrão GoF comportamental aplicado ao chat a preencher por Philipe Amâncio Reis Caetano.

---

### Modelagem (notação UML)

#### Foco 1: Moderação Reativa — GoF Observer (Eduardo Lôbo Moreira)

- **Diagrama de Classes UML (GoF Observer + Strategy), Componentes e Casos de Uso:** [1.1.3.1. Modelagem — Observer (Moderação)](1.1.3.1.ModelagemObserver.md). Fonte vetorial SVG e PNG em `assets/diagramas/`.
- **Diagrama de Sequência UML (Pipeline Reativo de Moderação), Máquina de Estados e Atividades:** [1.1.3.2. Sequência — Observer (Moderação)](1.1.3.2.SequenciaObserver.md).

#### Focos 2 e 3: Autenticação e Chat (Hugo e Philipe)

**Pendente:** Diagramas de classes, sequência e estados dos padrões comportamentais de autenticação e chat a serem adicionados pelos integrantes responsáveis.

---

### Implementação (código)

#### Foco 1: Moderação Reativa (Eduardo Lôbo Moreira)

Concluído e integrado no [repositório de código da SubEquipe_03](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo), mantido separado deste repositório para que código e testes não interfiram na publicação do GitHub Pages:
- `src/patterns/observer/StreamChannel.ts`: ConcreteSubject e Context.
- `src/patterns/observer/interfaces.ts`: interfaces `ISubject`, `IObserver`, `StreamEvent`.
- `src/patterns/observer/observers/`: observadores especializados (`AutoModObserver`, `SafetyVisionModerationObserver`, `CopyrightDMCAAudioObserver`, `HumanModeratorDashboardObserver`, `ChatRaidShieldObserver`, `PiracyVideoRestreamObserver`).
- `src/patterns/strategy/`: estratégias de despacho síncrona e assíncrona concorrente.
- `src/interactive.ts`: console interativo REPL com comandos em tempo real (**Iniciativa Extra**).
- `src/__tests__/observer.test.ts`: 13 testes unitários automatizados cobrindo ciclo de vida e moderação (`npm test`).

#### Focos 2 e 3: Autenticação e Chat (Hugo e Philipe)

**Pendente:** Implementação e testes unitários dos módulos de autenticação e chat.

---

### Execução e vídeo do padrão em funcionamento

**Pré-requisitos:** Node.js v20+ e npm v10+.

Código no [repositório de código da SubEquipe_03](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo):

```bash
git clone https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo.git
cd g6-streaming-entrega03-subgrupo03-codigo
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

---

## Rastreabilidade Bidirecional Formal & Elos Arquiteturais (E01 ➔ E02 ➔ E03)

A rastreabilidade bidirecional estabelece a coerência entre as necessidades de negócio elicitadas (**Entrega 01**), os modelos estáticos/dinâmicos em notação UML (**Entrega 02**) e os Padrões de Projeto GoF implementados (**Entrega 03**), garantindo conformidade com a rubrica metodológica da disciplina de Desenho de Software.

### 1. Rastreabilidade *Forward* (Dos Requisitos E01 e Modelos E02 para os Padrões GoF E03)

| Requisito de Origem (E01) | Modelo de Referência (E02) | Elemento GoF / Participante (E03) | Implementação no Repositório | Comprobatório de Execução e Testes |
| :--- | :--- | :--- | :--- | :--- |
| **RF01:** Iniciar e encerrar transmissões ao vivo multicanal | **UC01:** Transmitir ao Vivo · **DiagSeq02:** Abertura de Live | `ISubject` & `StreamChannel` (`goLive`, `endLive`) | [`StreamChannel.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/StreamChannel.ts) | `npm test` (Teste 2) · `npm run web` (Botão 1) |
| **RF15:** Notificação em tempo real de seguidores e comunidades | **DiagAtiv03:** Disparo de Alertas a Inscritos | `IObserver` (`PushNotificationObserver`, `DiscordWebhookObserver`) | [`PushNotificationObserver.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/observers/PushNotificationObserver.ts) · [`DiscordWebhookObserver.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/observers/DiscordWebhookObserver.ts) | `npm run demo` (Etapa 3) · Push FCM e Discord |
| **RF07:** Moderação automatizada de mensagens e toxicidade no chat | **UC04:** Moderar Canal · **DiagAtiv03:** Filtro de Chat | `AutoModObserver` & `TextEntropyAnalyzer` | [`AutoModObserver.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/observers/AutoModObserver.ts) · [`TextEntropyAnalyzer.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/engine/algorithms/TextEntropyAnalyzer.ts) | `npm test` (Teste 3) · Shannon Entropy real |
| **RF08:** Detecção e contenção de conteúdo sensível (Nudez/Gore) | **DiagSeq05:** Pipeline Reativo de Inspeção de Frame | `SafetyVisionModerationObserver` | [`SafetyVisionModerationObserver.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/observers/SafetyVisionModerationObserver.ts) | `npm test` (Testes 4 e 5) · Imagem PPM real |
| **RF12:** Fiscalização de Direitos Autorais e Diretrizes de DMCA | **DiagAtiv03:** Análise de Faixa de Áudio | `CopyrightDMCAAudioObserver` & `AudioAcousticFingerprinter` | [`CopyrightDMCAAudioObserver.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/observers/CopyrightDMCAAudioObserver.ts) · [`AudioAcousticFingerprinter.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/engine/algorithms/AudioAcousticFingerprinter.ts) | `npm test` (Teste 6) · Audio Mute e Strike |
| **RF09:** Auditoria e Intervenção de Moderadores Humanos | **UC04:** Moderar Canal (ModView E02) | `HumanModeratorDashboardObserver` | [`HumanModeratorDashboardObserver.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/observers/HumanModeratorDashboardObserver.ts) | `npm run web` · `npm run interactive` (`mod`) |
| **RNF02:** Desacoplamento arquitetural e extensibilidade (OCP) | **DiagClasses:** Arquitetura em Camadas | Interfaces canônicas `ISubject` e `IObserver` | [`interfaces.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/interfaces.ts) | Adição de 8 observadores sem alterar `StreamChannel` |
| **RNF04:** Alta vazão e liberação de thread (Desempenho) | **ADR-003:** Observer Concorrente Twitch | GoF Strategy: `AsynchronousConcurrentDispatchStrategy` | [`AsynchronousConcurrentDispatchStrategy.ts`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/strategy/AsynchronousConcurrentDispatchStrategy.ts) | `npm run benchmark` (Speedup de 116.5x e 6.66ms) |
| **Foco 2 (Autenticação):** Verificação de Sessão e Tokens | Modelagem de Sessão E02 | *GoF Comportamental a definir* | A preencher pelo integrante (**Hugo Freitas Silva**) | A preencher |
| **Foco 3 (Chat):** Mensageria e Distribuição de Salas | Modelagem de Mensageria E02 | *GoF Comportamental a definir* | A preencher pelo integrante (**Philipe Amâncio Reis Caetano**) | A preencher |

---

### 2. Rastreabilidade *Backward* (Do Código e Padrões GoF E03 para as Decisões de Arquitetura E02/E01)

| Elemento do Código GoF (E03) | Padrão e Papel Canônico | Justificativa Arquitetural no Projeto (E02/E01) | Decisão Formal Registrada |
| :--- | :--- | :--- | :--- |
| `StreamChannel` | **ConcreteSubject** (GoF Observer) | Centraliza o ciclo de vida da live sem se acoplar às regras específicas de cada inteligência artificial de moderação | [ADR-003: Contexto e Decisão](ADR/ADR-003-observer-concorrente-notificacoes-twitch.md#decisão) |
| `attach()` / `detach()` | **Subject Operations** (Slide 53) | Permite plugar ou desplugar observadores em tempo de execução sem derrubar o canal de streaming | [1.1.3.1. Modelagem — Classes](1.1.3.1.ModelagemObserver.md) |
| `getState()` | **Subject State Inspector** (Slide 53) | Fornece snapshot imutável do canal para clientes externos, ModView e Dashboard Web | [`interfaces.ts#L30`](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/patterns/observer/interfaces.ts) |
| `INotificationDispatchStrategy` | **Strategy Interface** (GoF Strategy) | Isola o algoritmo de entrega de notificações, permitindo chavear entre laço síncrono e Worker Pool concorrente | [ADR-003: Estratégias Alternativas](ADR/ADR-003-observer-concorrente-notificacoes-twitch.md#alternativas-consideradas) |
| `AutoModObserver` | **ConcreteObserver** (Moderação) | Responde ao RF07 da E01 eliminando overhead de regex tradicional através da Entropia de Shannon | [1.1.3.2. Sequência — Pipeline](1.1.3.2.SequenciaObserver.md) |
| `SafetyVisionModerationObserver` | **ConcreteObserver** (Moderação) | Implementa salvaguarda legal automática (Content Warning 18+) em conformidade com o Termo de Uso UGC da E01 | [1.1.3.1. Modelagem — Casos de Uso](1.1.3.1.ModelagemObserver.md#4-diagrama-de-casos-de-uso-da-plataforma-ugc) |
| `HumanModeratorDashboardObserver` | **ConcreteObserver** (ModView) | Materializa a interface de auditoria do moderador prevista no UC04 da E02 | [Dashboard Web ModView](https://github.com/EduLoboM/g6-streaming-entrega03-subgrupo03-codigo/blob/main/src/webServer.ts) |

## Senso Crítico

**Benefícios (Moderação / Observer):** Desacoplamento estrito entre emissão de eventos e regras de moderação; adição de novos observadores sem modificar o `StreamChannel` (OCP); tolerância a falhas transitórias de socket em notificações remotas.

**Custos e limites:** Concorrência requer dimensionamento explícito do Worker Pool para evitar esgotamento de *file descriptors* no sistema operacional; consistência eventual na ordem de entrega de notificações assíncronas.

---

## Referências

1. **GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; VLISSIDES, John.** *Design Patterns: Elements of Reusable Object-Oriented Software*. Reading: Addison-Wesley, 1995.
2. **LARMAN, Craig.** *Utilizando UML e Padrões: Uma Introdução à Análise e ao Projeto Orientado a Objetos*. 3ª edição. Porto Alegre: Bookman, 2007.
3. **SOMMERVILLE, Ian.** *Engenharia de Software*. 8ª edição. São Paulo: Pearson Addison-Wesley, 2007.
4. **SERRANO, Milene.** *Arquitetura e Desenho de Software: Aula - GoFs Comportamentais*. Material didático da disciplina FGA0208. Universidade de Brasília (UnB Gama), 2026.
5. **TWITCH DEVELOPERS.** *Twitch EventSub Documentation*. Disponível em: `https://dev.twitch.tv/docs/eventsub/`.
6. **GOOGLE DEVELOPERS.** *WebSub & Firebase Cloud Messaging*. Disponível em: `https://pubsubhubbub.appspot.com/`.

---

## Versionamentos & Participações

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| :---: | :---: | :--- | :--- | :--- | :---: |
| 0.1 | 16/10/2026 | Eduardo Lôbo Moreira | Modelagem do GoF Observer (foco Moderação), diagrama de classes e sequência, ADR-003 e código do StreamChannel | A preencher | Commit inicial SubEquipe 03 |
| 0.2 | 17/10/2026 | Eduardo Lôbo Moreira | Estruturação da divisão em 3 focos (Moderação, Autenticação e Chat) no padrão da SubEquipe 01, relato de IA e suíte de testes | A preencher | PR `docs/subequipe-03-modelagem-observer` |
| 0.3 | 18/10/2026 | Eduardo Lôbo Moreira | Implementação do console interativo REPL (`npm run interactive`) | A preencher | Commit `6ec8a38` |
| 0.4 | 18/10/2026 | Eduardo Lôbo Moreira | Implementação do Web ModView Dashboard (`npm run web`) e Matriz de Rastreabilidade Bidirecional Formal (E01 ➔ E02 ➔ E03) | A preencher | Commit `2af97fd` |
| 0.5 | 19/10/2026 | Eduardo Lôbo Moreira | Separação do código e testes em repositório dedicado (`g6-streaming-entrega03-subgrupo03-codigo`), alinhado ao padrão da SubEquipe 01 | A preencher | Branch `docs/subequipe-03-modelagem-observer` |

O quadro consolidado de participações está em [1.2. Participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
