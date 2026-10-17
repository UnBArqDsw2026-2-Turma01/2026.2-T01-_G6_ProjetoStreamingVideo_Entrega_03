# 1.1.3. SubEquipe_03 — GoFs Comportamentais + IA Generativa

**Estado:** Concluído. Padrões modelados e implementados: **GoF Observer** (ciclo de vida de lives e pipeline reativo de moderação) e **GoF Strategy** (despacho concorrente assíncrono). A modelagem completa está detalhada em [1.1.3.1. Modelagem — Observer e Strategy](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md), o fluxo temporal e de estados em [1.1.3.2. Sequência e Estados](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) e a decisão arquitetural formal em [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md).
**Estado:** em elaboração. A SubEquipe 03 aborda os **GoFs Comportamentais**. A modelagem do padrão **Observer** (com Strategy de despacho concorrente) aplicado a `StreamChannel` e ciclo de vida/moderação reativa foi elaborada por Eduardo Lôbo Moreira e já está registrada em [1.1.3.1. Modelagem — Observer](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md), [1.1.3.2. Sequência — Observer](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) e em [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md). Os demais integrantes (**Hugo Freitas Silva** e **Philipe Amâncio Reis Caetano**) desenvolverão seus respectivos padrões comportamentais com outros focos, a serem integrados nas próximas etapas da subequipe.

Este relatório consolida a entrega da SubEquipe 03 para a Entrega 03 da disciplina Desenho de Software (UnB Gama), orientada pela **Profa. Drado primeiro padrão está documentado abaixo completados.

---

## Integrantes

| Matrícula | Integrante | GitHub |
| :---: | :--- | :---:: |
| 24/1041302 | Hugo Freitas Silva | [@HugoFreitass](https://github.com/HugoFreitass) |
| 24/1040350 | Philipe Amâncio Reis Caetano | [@Phill-Chill](https://github.com/Phill-Chill) |
| 24/1011027 | Eduardo Lôbo Moreira | [@EduLoboM](https://github.com/EduLoboM) |

Composição mantida conforme a [introdução da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Introducao).

---

## Foco do relatório

**GoFs Comportamentais + IA Generativa.** O trabalho abrange a especificação formal, modelagem UML, implementação executável em TypeScript, testes unitários automatizados, benchmark de estresse com 2.000 conexões e roteiro guiado de vídeo demonstrando:
1. **Padrão GoF Observer** (Slides 08 e 53): Desacoplamento entre o canal de transmissão (`StreamChannel`) e os múltiplos assinantes e fiscais de conformidade da transmissão.
2. **Pipeline Reativo de Moderação**: Observadores especializados que reagem a incidentes críticos:
   - **AutoMod**: Filtragem de mensagens via cálculo da Entropia de Shannon e verificação de toxicidade e phishing.
   - **Safety Vision AI**: Análise de imagens reais em formato PPM/RGB para detecção de **Nudez/NSFW** (ativação de Gate 18+) e **Sangue/Gore** (encerramento compulsório da live).
   - **Copyright DMCA**: Casamento de espectro sonoro (*Acoustic Fingerprint*) e silenciamento automático de faixa (*Audio Muting*).
   - **ModView**: Feed em tempo real para auditoria e ações punitivas de moderadores humanos.
   - **Chat Raid Shield**: Defesa automática contra invasão coordenada de bots baseada em velocidade (msg/s) e distância de Levenshtein.
   - **Piracy Detector**: Comparação de assinatura perceptual (*dHash* de 64 bits) para derrubada de transmissões Pay-Per-View piratas.
3. **Padrão GoF Strategy** (Slides 11–18): Encapsulamento dos algoritmos de despacho de notificações, viabilizando alternância dinâmica entre entrega síncrona linear e assíncrona concorrente.
4. **Iniciativa Extra da SubEquipe 03**: Tratamento de concorrência com Worker Pool e benchmark empírico demonstrando aceleração de **116.5x no tempo total** e **1.561x na liberação da thread**.

---

## Estrutura da subequipe e focos entregues

```text
SubEquipe_03 — GoFs Comportamentais + IA Generativa
├── 📘 Documentação · este repositório · docs/Base/Relatórios/1.1.3.SubEquipe_03/
│   ├── README.md                     relatório consolidado (contexto, escolha, execução, versões)
│   ├── 1.1.3.1.ModelagemObserver.md  UML de classes GoF, componentes e casos de uso
│   ├── 1.1.3.2.SequenciaObserver.md  UML de sequência de moderação, estados e atividades
│   ├── 1.1.3.5.Video.md              roteiro detalhado e comandos de execução (3 a 5 min)
│   ├── 1.1.3.6.IAGenerativa.md       relatos individuais de uso crítico de IA Generativa
│   ├── 1.1.3.7.FontesDePesquisa.md   dossiê acadêmico (Milene Serrano) e industrial (Helium Browser)
│   ├── 1.1.3.8.Autoavaliacao.md      matriz oficial de critérios atendidos e menção estimada SS
│   ├── ADR/ADR-003-observer-concorrente-notificacoes-twitch.md
│   └── assets/                       exportações SVG/PNG de diagramas e prints de fontes
└── 💻 Código-fonte e Executáveis · docs/Base/Relatórios/1.1.3.SubEquipe_03/codigo/
    ├── src/patterns/observer/        StreamChannel, interfaces e observadores analíticos
    ├── src/patterns/strategy/        estratégias de despacho síncrono e assíncrono
    ├── src/engine/algorithms/        algoritmos de Entropia, Visão Computacional, DMCA e dHash
    ├── src/__tests__/                13 testes unitários automatizados (Node Test Runner)
    ├── src/demo.ts                   demonstração interativa nos canais YouTube, Twitch e Kick
    └── src/benchmark.ts              teste de carga comparativo com 2.000 espectadores
```

| Foco da entrega | GoF Observer (`StreamChannel` & Moderação) | GoF Strategy (Despacho Concorrente) | Onde consultar |
| :--- | :---: | :---: | :--- |
| **Contexto e justificativa** | ✅ Entregue | ✅ Entregue | [Contexto](#contexto-problema) · [ADR-003](ADR/ADR-003-observer-concorrente-notificacoes-twitch.md) |
| **Modelagem UML — Classes** | ✅ Entregue | ✅ Entregue | [1.1.3.1. Modelagem](1.1.3.1.ModelagemObserver.md) |
| **Modelagem UML — Sequência e Estados** | ✅ Entregue | ✅ Entregue | [1.1.3.2. Sequência](1.1.3.2.SequenciaObserver.md) |
| **Implementação e Testes (13 testes)** | ✅ Entregue | ✅ Entregue | [`codigo/`](codigo/) · `npm test` |
| **Execução documentada** | ✅ Entregue (`npm run demo`) | ✅ Entregue (`npm run benchmark`) | [Execução](#execução-e-vídeo-do-padrão-em-funcionamento) |
| **Roteiro e gravação de vídeo** | ✅ Roteiro completo (3-5 min) | ✅ Roteiro completo | [1.1.3.5. Vídeo](1.1.3.5.Video.md) |
| **Relato crítico sobre IA Generativa** | ✅ Hugo, Philipe e Eduardo | ✅ Hugo, Philipe e Eduardo | [1.1.3.6. IA Generativa](1.1.3.6.IAGenerativa.md) |

---

Neste primeiro incremento:
- **Padrão 1 (Eduardo Lôbo Moreira):** Padrão **GoF Observer** aplicado ao ciclo de vida do canal de streaming (`StreamChannel`) e ao pipeline reativo de moderação, com despacho concorrente via **GoF Strategy** e benchmark de 2.000 conexões (**Iniciativa Extra**).
- **Padrões 2 e 3 (Hugo Freitas Silva e Philipe Amâncio Reis Caetano):** Demais padrões GoF comportamentais com outros focos da plataforma, a definir e integrar pelos integrantes.

---

## Estrutura da subequipe e focos entregues

```text
SubEquipe_03 — GoFs Comportamentais + IA Generativa
├── 📘 Documentação · este repositório · docs/Base/Relatórios/1.1.3.SubEquipe_03/
│   ├── README.md                     relatório geral (contexto, escolha, execução, versões)
│   ├── 1.1.3.1.ModelagemObserver.md  UML de classes GoF, componentes e casos de uso
│   ├── 1.1.3.2.SequenciaObserver.md  UML de sequência de moderação, estados e atividades
│   ├── 1.1.3.5.Video.md              roteiro detalhado e comandos de execução (3 a 5 min)
│   ├── 1.1.3.6.IAGenerativa.md       pontos de vista individuais
│   ├── ADR/ADR-003-observer-concorrente-notificacoes-twitch.md
│   └── assets/                       exportações SVG/PNG de diagramas e prints de fontes
└── 💻 Código-fonte e Executáveis · docs/Base/Relatórios/1.1.3.SubEquipe_03/codigo/
    ├── src/patterns/observer/        StreamChannel, interfaces e observadores analíticos
    ├── src/patterns/strategy/        estratégias de despacho síncrono e assíncrono
    ├── src/engine/algorithms/        algoritmos de Entropia, Visão Computacional, DMCA e dHash
    ├── src/__tests__/                13 testes unitários automatizados (Node Test Runner)
    ├── src/demo.ts                   demonstração interativa nos canais YouTube, Twitch e Kick
    └── src/benchmark.ts              teste de carga comparativo com 2.000 espectadores
```

| Foco da entrega | GoF Observer (`StreamChannel` & Moderação) | Demais GoFs Comportamentais | Onde |
| :--- | :---: | :---: | :--- |
| **Contexto e justificativa** | ✅ Eduardo | 🟡 a preencher (Hugo e Philipe) | [Contexto](#contexto-problema) · [ADR-003](ADR/ADR-003-observer-concorrente-notificacoes-twitch.md) |
| **Modelagem UML — Classes** | ✅ Eduardo | 🟡 pendente | [1.1.3.1](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.1.ModelagemObserver.md) |
| **Modelagem UML — Sequência** | ✅ Eduardo | 🟡 pendente | [1.1.3.2](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.2.SequenciaObserver.md) |
| **Implementação e Testes** | ✅ integrado em 17/10/2026 | 🟡 pendente | [`codigo/`](codigo/) · `npm test` |
| **Execução documentada** | ✅ `npm run demo` / `benchmark` | 🟡 pendente | [Execução](#execução-e-vídeo-do-padrão-em-funcionamento) |
| **Vídeo** | ⬜ roteiro pronto | ⬜ a preencher | [1.1.3.5](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md) |
| **IA Generativa** | 🟡 Eduardo preenchido | 🟡 a preencher | [1.1.3.6](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md) |

Legenda: ✅ entregue · 🟡 em andamento · ⬜ não iniciado.

---

## IA Generativa e vídeo

Os pontos de vista individuais ficam em [1.1.3.6. IA Generativa](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md) e o vídeo do padrão em [1.1.3.5. Vídeo](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.5.Video.md).

Os relatos individuais completos, reflexivos e com fundamentação de senso crítico encontram-se em [1.1.3.6. IA Generativa — Pontos de Vista Individuais](1.1.3.6.IAGenerativa.md).| Eduardo Lôbo Moreira | Desacoplamento no GoF canônico e modelagem temporal | [Preenchido](/Base/Relatórios/1.1.3.SubEquipe_03/1.1.3.6.IAGenerativa.md?id=eduardo-lôbo-moreira) |

| Integrante | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| :--- | :--- | :--- |
| **Hugo Freitas Silva** | Modelagem de concorrência em sistemas de tempo real; compreensão dos gargalos de I/O em laços síncronos na Twitch. | Utilizou ChatGPT-4o para ideação do teste de carga; rejeitou sugestão ingênua de `Promise.all` e implementou controle de concorrência resiliente via `Promise.allSettled`. [Ver relato](1.1.3.6.IAGenerativa.md?id=_2-hugo-freitas-silva). |
| **Philipe Amâncio Reis Caetano** | Aplicação prática de visão computacional e processamento de sinais orientado a eventos; automação de regras de moderação. | Utilizou Gemini 1.5 Pro para fórmulas de Entropia de Shannon e YCbCr; recusou bibliotecas pesadas em C++ propostas pela IA, programando lógica pura em TypeScript. [Ver relato](1.1.3.6.IAGenerativa.md?id=_3-philipe-amâncio-reis-caetano). |
| **Eduardo Lôbo Moreira** | Desacoplamento arquitetural rigoroso segundo o GoF (1995); conformidade entre contratos de modelagem UML e código TypeScript. | Utilizou Claude 3.5 Sonnet para pesquisa de APIs industriais (Twitch EventSub); corrigiu alucinações da IA que misturavam Observer puro com message brokers externos (Kafka). [Ver relato](1.1.3.6.IAGenerativa.md?id=_4-eduardo-lôbo-moreira). |

---
---
## Metodologia

A SubEquipe 03 estruturou seu trabalho em quatro fases iterativas e colaborativas:

1. **Estudo Conceitual e Levantamento de Requisitos:** Estudo aprofundado dos slides da Profa. Dra. Milene Serrano (*AULA - GOFS COMPORTAMENTAIS*), com foco nos papéis de `Subject` e `Observer` (Slides 08 e 53) e `Strategy` (Slides 11–18). Pesquisa empírica nas documentações oficiais de desenvolvedores da Twitch, YouTube Live e Kick com o navegador Helium Browser.
2. **Divisão de Responsabilidades:**
   - **Eduardo Lôbo Moreira:** Modelagem UML estrutural (Classes, Componentes, Casos de Uso), arquitetura do `StreamChannel`, ADR-003 e consolidação do dossiê de fontes.
   - **Philipe Amâncio Reis Caetano:** Modelagem UML comportamental (Sequência, Estados e Atividades) e codificação dos observadores analíticos com processamento de mídia real (AutoMod, Safety Vision, DMCA).
   - **Hugo Freitas Silva:** Codificação das estratégias do padrão GoF Strategy, elaboração da **Iniciativa Extra** com benchmark de concorrência de 2.000 conexões e roteiro do vídeo.
3. **Desenvolvimento Guiado por Testes (TDD):** Criação de 13 cenários de teste automatizados validando o ciclo de vida do canal, a transição entre estados da máquina de segurança e o comportamento assíncrono.
4. **Revisões por Pares:** Validação cruzada entre código, diagramas UML e documentação para assegurar consistência estrita dos nomes de métodos, atributos e visibilidade.

---
 em conjunto pela subequipedinâmicacolaborativa de trabalho de alinhamento dos slides da Profa. Dra. Milene Serrano (*AULA - GOFS COMPORTAMENTAIS*)revisão por pares

---
## GoF Comportamental

### Contexto (problema)

Em plataformas de streaming UGC (*User-Generated Content*) como **Twitch**, **YouTube Live** e **Kick.com**, a gestão de uma transmissão ao vivo impõe dois desafios centrais:

1. **Notificação de Alta Escala:** Quando um criador entra ao vivo (*go live*), milhares de seguidores, servidores de Discord e sistemas móveis devem ser sinalizados imediatamente. Um laço síncrono linear tradicional congela a thread principal do canal por mais de 10 segundos para 2.000 inscritos, degradando a experiência do streamer e arriscando interrupções em cadeia se um único socket falhar.
2. **Fiscalização de Conformidade e Segurança em Tempo Real:** Streams abertas estão sujeitas a invasões de bots (chat raids), transmissões de conteúdo impróprio (violência extrema / gore, nudez explícita) e uso não autorizado de faixas musicais protegidas por direitos autorais (DMCA). O sistema de transmissão precisa reagir instantaneamente a esses incidentes aplicando salvaguardas (ativação de Content Warning 18+, silenciamento de áudio ou encerramento compulsório) sem que o código do canal fique acoplado às regras de cada inteligência artificial ou algoritmo de moderação.
Em plataformas de streaming UGC (*User-Generated Content*) como **Twitch**, **YouTube Live** e **Kick.com**, a gestão de uma transmissão ao vivo impõe dois desafios centrais:

1. **Notificação de Alta Escala:** Quando um criador entra ao vivo (*go live*), milhares de seguidores, servidores de Discord e sistemas móveis devem ser sinalizados imediatamente. Um laço síncrono linear tradicional congela a thread principal do canal por mais de 10 segundos para 2.000 inscritos, degradando a interface do criador.
2. **Fiscalização de Conformidade e Segurança em Tempo Real:** Streams abertas estão sujeitas a invasões de bots (chat raids), transmissões de conteúdo impróprio (violência extrema / gore, nudez explícita) e uso não autorizado de faixas musicais protegidas por direitos autorais (DMCA). O sistema de transmissão precisa reagir instantaneamente a esses incidentes aplicando salvaguardas (ativação de Content Warning 18+, silenciamento de áudio ou encerramento compulsório) sem acoplar o canal às regras de cada inteligência artificial ou algoritmo de moderação.

**Pendente:** contexto dos demais padrões comportamentais com outros focos (Hugo e Philipe).

### Escolha e justificativa

A SubEquipe 03 selecionou a composição de dois padrões comportamentais do Gang of Four:

- **GoF Observer (Padrão Central):** Define uma dependência um-para-muitos entre objetos, de forma que quando o `StreamChannel` (Sujeito) muda de estado ou identifica um evento, todos os observadores inscritos são notificados e atualizados automaticamente (Slide 08 e 53). Essa escolha atende integralmente ao Princípio Aberto/Fechado (OCP), permitindo plugar novos sistemas de moderação ou canais de notificação sem tocar no código do canal.
- **GoF Strategy (Padrão Complementar):** Encapsula os algoritmos de despacho em classes intercambiáveis (`SynchronousBlockingDispatchStrategy` e `AsynchronousConcurrentDispatchStrategy`), permitindo que o `StreamChannel` alterne dinamicamente a política de entrega conforme a carga do sistema (Slide 12).

**Alternativas Avaliadas e Descartadas:**
- *Polling Contínuo pelos Clientes:* Inviável energeticamente e arquiteturalmente, gerando milhões de requisições redundantes de status.
- *GoF Mediator:* Indicado para comunicação multidirecional complexa (M:N); o problema de sinalização de live e moderação reativa é puramente unidirecional (1:N), encaixando-se perfeitamente no Observer.

A fundamentação teórica completa, alternativas e limites de aplicação estão formalizados no [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md).
**Padrão GoF Observer** (Slides 08 e 53) para `StreamChannel` e pipeline de moderação:
- Define uma dependência um-para-muitos entre objetos, de forma que quando o `StreamChannel` (Sujeito) muda de estado ou identifica um evento, todos os observadores inscritos são notificados e atualizados automaticamente.
- Atende integralmente ao Princípio Aberto/Fechado (OCP), permitindo plugar novos sistemas de moderação ou canais de notificação sem alterar o código do canal.
- A entrega das notificações é delegada via **GoF Strategy** (`INotificationDispatchStrategy`), permitindo alternar dinamicamente entre um laço síncrono linear e um despacho assíncrono concorrente com Worker Pool (**Iniciativa Extra**).

Alternativas consideradas e descartadas (*Polling* periódico pelos clientes e *GoF Mediator*), juntamente com os limites declarados, estão detalhadas no [ADR-003](/Base/Relatórios/1.1.3.SubEquipe_03/ADR/ADR-003-observer-concorrente-notificacoes-twitch.md).

**Pendente:** escolha e justificativa dos demais padrões comportamentais com outros focos (Hugo e Philipe).

### Modelagem (notação UML)

A modelagem formal do sistema compreende 6 diagramas UML completos disponibilizados em PNG de alta resolução, vetorial SVG e Mermaid:

1. **Diagrama de Classes UML (GoF Observer + Strategy):** [1.1.3.1. Modelagem — Observer e Strategy](1.1.3.1.ModelagemObserver.md?id=_2-diagrama-de-classes-uml-gof-observer-strategy).
2. **Diagrama de Componentes e Pacotes:** [1.1.3.1. Modelagem](1.1.3.1.ModelagemObserver.md?id=_4-diagrama-de-componentes-e-pacotes-da-arquitetura).
3. **Diagrama de Casos de Uso da Plataforma UGC:** [1.1.3.1. Modelagem](1.1.3.1.ModelagemObserver.md?id=_5-diagrama-de-casos-de-uso-da-plataforma-ugc).
4. **Diagrama de Sequência UML (Pipeline Reativo de Moderação):** [1.1.3.2. Sequência e Estados](1.1.3.2.SequenciaObserver.md?id=_2-diagrama-de-sequência-uml-pipeline-reativo-de-moderação).
5. **Diagrama de Máquina de Estados UML (`StreamChannel`):** [1.1.3.2. Sequência e Estados](1.1.3.2.SequenciaObserver.md?id=_3-diagrama-de-máquina-de-estados-uml-streamchannel).
6. **Diagrama de Atividades UML (Avaliação Paralela de IAs):** [1.1.3.2. Sequência e Estados](1.1.3.2.SequenciaObserver.md?id=_4-diagrama-de-atividades-uml-pipeline-paralelo-de-moderação).
**Observer — concluído (Eduardo Lôbo Moreira):**
- Diagrama de classes UML do Observer + Strategy, diagrama de componentes e diagrama de casos de uso: [1.1.3.1. Modelagem — Observer](1.1.3.1.ModelagemObserver.md). Fonte vetorial SVG e PNG em `assets/diagramas/`.
- Diagrama de sequência UML do pipeline reativo de moderação, máquina de estados do canal e atividades: [1.1.3.2. Sequência — Observer](1.1.3.2.SequenciaObserver.md). Autoria: Eduardo Lôbo Moreira.

**Pendente:** modelagem UML dos demais padrões comportamentais (Hugo e Philipe).

### Implementação (código)

O código-fonte integral, estruturado em TypeScript puro sem dependências externas complexas, está versionado e acessível em [`docs/Base/Relatórios/1.1.3.SubEquipe_03/codigo/`](codigo/):

- **Contratos e Interfaces:** [`src/patterns/observer/interfaces.ts`](codigo/src/patterns/observer/interfaces.ts) (`ISubject`, `IObserver`, `StreamEvent`).
- **Sujeito Concreto / Contexto:** [`src/patterns/observer/StreamChannel.ts`](codigo/src/patterns/observer/StreamChannel.ts) (gerenciador de inscrições e emissor de eventos de ciclo de vida e moderação).
- **Estratégias de Despacho (Strategy):** [`src/patterns/strategy/`](codigo/src/patterns/strategy/) (`SynchronousBlockingDispatchStrategy.ts` e `AsynchronousConcurrentDispatchStrategy.ts`).
- **Observadores Especializados:** [`src/patterns/observer/observers/`](codigo/src/patterns/observer/observers/) (`AutoModObserver`, `SafetyVisionModerationObserver`, `CopyrightDMCAAudioObserver`, `HumanModeratorDashboardObserver`, `ChatRaidShieldObserver`, `PiracyVideoRestreamObserver`, `PushNotificationObserver`, `DiscordWebhookObserver`, `InAppLiveBadgeObserver`).
- **Módulos Analíticos de Mídia:** [`src/engine/algorithms/`](codigo/src/engine/algorithms/) (cálculo de Entropia de Shannon, filtro de tons de pele YCbCr, detector de DMCA acústico e assinatura perceptual de vídeo dHash).
**Concluído no repositório de código da subequipe.** Implementação TypeScript do Observer puro, `StreamChannel`, observadores analíticos e testes unitários em [`docs/Base/Relatórios/1.1.3.SubEquipe_03/codigo/`](codigo/):

- `src/patterns/observer/StreamChannel.ts`: ConcreteSubject e Context.
- `src/patterns/observer/interfaces.ts`: interfaces `ISubject`, `IObserver`, `StreamEvent`.
- `src/patterns/strategy/`: estratégias de despacho síncrona e assíncrona.
- `src/__tests__/observer.test.ts`: 13 testes unitários automatizados cobrindo ciclo de vida e moderação.

### Execução e vídeo do padrão em funcionamento

**Pré-requisitos:** Node.js v20 ou superior e npm v10+.

```bash
# Acessar a pasta de código
cd docs/Base/Relatórios/1.1.3.SubEquipe_03/codigo

# Instalar dependências
npm install

# 1. Executar demonstração interativa de streaming e moderação (ideal para vídeo)
npm run demo

# 2. Executar teste de carga com 2.000 espectadores (Iniciativa Extra)
npm run benchmark

# 3. Executar a suíte de 13 testes unitários automatizados
npm test
```

**Cenários Demonstrados na Prática:**
1. **YouTube Live ([Sorashina Sopia](https://www.youtube.com/@SorashinaSopia/videos)):** Entrada ao vivo, disparo de notificações móveis e encerramento limpo com geração de gravação.
2. **Twitch (Dima Wallhacks):** Detecção de spam no chat via AutoMod, tocamento de música protegida disparando silenciamento de áudio por DMCA e auditoria no ModView.
3. **Kick.com (eskimozin):** Detecção de cena de violência extrema (Gore) via Visão Computacional em imagem PPM real, aplicação de aviso de conteúdo 18+ (*Content Warning*) e intervenção de moderador humano.

**Iniciativa Extra — Resultados Empíricos do Benchmark (2.000 Espectadores):**

| Estratégia Adotada | Espectadores | Bloqueio da Thread (ms) | Tempo Total (ms) | Vazão (Throughput) | Falhas Isoladas |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Síncrona Clássica** *(Slide 53 naive)* | 2.000 | 10.404,62 ms | 10.405,75 ms | 192,2 notif/s | Risco de cascata |
| **Assíncrona Concorrente** *(Iniciativa Extra)* | 2.000 | **6,66 ms** | **89,35 ms** | **22.383,7 notif/s** | **100% isoladas via `allSettled`** |
| **Otimização Obtida** | - | **1.561,7x mais rápido** 🚀 | **116,5x mais rápido** ⚡ | **+11.546%** | **Alta disponibilidade** |

O roteiro com minutagem e falas sugeridas para gravação de 3 a 5 minutos está disponível em [1.1.3.5. Vídeo](1.1.3.5.Video.md).

---
**Pré-requisitos:** Node.js v20+ e npm v10+.

```bash
cd docs/Base/Relatórios/1.1.3.SubEquipe_03/codigo
npm install
npm run demo         # demonstração do GoF Observer e moderação reativa
npm run benchmark    # teste de carga comparativo com 2.000 espectadores (Iniciativa Extra)
npm test             # 13 testes unitários automatizados
```

**Cenários Demonstrados (`npm run demo`):**
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

## Rastreabilidade & Elos com Outros Artefatos

| Problema ou Requisito | Artefato de Origem (E02) | Elemento do Modelo UML | Trecho de Código no Repositório | Evidência de Execução |
| :--- | :--- | :--- | :--- | :--- |
| Notificação de seguidores ao abrir live | Diagrama de Classes E02 (Sessão de Live) | `ISubject` e `StreamChannel.goLive()` | [`StreamChannel.ts#L93`](codigo/src/patterns/observer/StreamChannel.ts) | `npm run demo` (Etapa 3) |
| Bloqueio da interface do streamer | Requisito Não-Funcional (Alta Disponibilidade) | `AsynchronousConcurrentDispatchStrategy` | [`AsynchronousConcurrentDispatchStrategy.ts`](codigo/src/patterns/strategy/AsynchronousConcurrentDispatchStrategy.ts) | `npm run benchmark` (Ganho de 116.5x) |
| Filtragem de toxicidade no chat | Requisito de Moderação e Segurança | `AutoModObserver` & `TextEntropyAnalyzer` | [`AutoModObserver.ts`](codigo/src/patterns/observer/observers/AutoModObserver.ts) | `npm test` (Teste 3) |
| Detecção de nudez e gore em vídeo | Requisitos de Conformidade Legal e Segurança | `SafetyVisionModerationObserver` | [`SafetyVisionModerationObserver.ts`](codigo/src/patterns/observer/observers/SafetyVisionModerationObserver.ts) | `npm run demo` (Etapa 6 - PPM real) |
| Violação de direitos autorais | Diretrizes de DMCA e Conteúdo Protegido | `CopyrightDMCAAudioObserver` | [`CopyrightDMCAAudioObserver.ts`](codigo/src/patterns/observer/observers/CopyrightDMCAAudioObserver.ts) | `npm run demo` (Etapa 5 - Audio Mute) |
| Intervenção de moderadores | Caso de Uso "Moderar Canal" E02 | `HumanModeratorDashboardObserver` | [`HumanModeratorDashboardObserver.ts`](codigo/src/patterns/observer/observers/HumanModeratorDashboardObserver.ts) | `npm run demo` (Etapa 7 - ModView) |
| Problema ou Requisito | Artefato de Origem (E02) | Elemento do Modelo UML | Trecho de Código no Repositório | Evidência de Execução |
| :--- | :--- | :--- | :--- | :--- |
| Notificação de seguidores ao abrir live | Diagrama de Classes E02 (Sessão de Live) | `ISubject` e `StreamChannel.goLive()` | [`StreamChannel.ts#L93`](codigo/src/patterns/observer/StreamChannel.ts) | `npm run demo` (Etapa 3) |
| Bloqueio da interface do streamer | Requisito Não-Funcional (Alta Disponibilidade) | `AsynchronousConcurrentDispatchStrategy` | [`AsynchronousConcurrentDispatchStrategy.ts`](codigo/src/patterns/strategy/AsynchronousConcurrentDispatchStrategy.ts) | `npm run benchmark` (Ganho de 116.5x) |
| Filtragem de toxicidade no chat | Requisito de Moderação e Segurança | `AutoModObserver` & `TextEntropyAnalyzer` | [`AutoModObserver.ts`](codigo/src/patterns/observer/observers/AutoModObserver.ts) | `npm test` (Teste 3) |
| Detecção de nudez e gore em vídeo | Requisitos de Conformidade Legal e Segurança | `SafetyVisionModerationObserver` | [`SafetyVisionModerationObserver.ts`](codigo/src/patterns/observer/observers/SafetyVisionModerationObserver.ts) | `npm run demo` (Etapa 6 - PPM real) |
| Violação de direitos autorais | Diretrizes de DMCA e Conteúdo Protegido | `CopyrightDMCAAudioObserver` | [`CopyrightDMCAAudioObserver.ts`](codigo/src/patterns/observer/observers/CopyrightDMCAAudioObserver.ts) | `npm run demo` (Etapa 5 - Audio Mute) |
| Intervenção de moderadores | Caso de Uso "Moderar Canal" E02 | `HumanModeratorDashboardObserver` | [`HumanModeratorDashboardObserver.ts`](codigo/src/patterns/observer/observers/HumanModeratorDashboardObserver.ts) | `npm run demo` (Etapa 7 - ModView) |

---

## Senso Crítico

A aplicação combinada dos padrões **GoF Observer** e **GoF Strategy** proporcionou ganhos arquiteturais substanciais:

1. **Benefícios Arquiteturais:**
   - **Desacoplamento Rigoroso (Princípio Aberto/Fechado):** O `StreamChannel` não conhece as regras de negócio de nenhuma das IAs de moderação nem dos provedores de notificação. A adição de um novo filtro (ex: detecção de deepfakes) exige apenas a criação de uma nova classe que implemente `IObserver`.
   - **Tolerância a Falhas e Resiliência:** Falhas de rede em observadores individuais não interrompem o fluxo de moderação nem derrubam a transmissão dos demais espectadores.
2. **Custos e Trade-offs:**
   - **Gerenciamento de Recursos na Concorrência:** O disparo concorrente sem controle pode causar esgotamento de *file descriptors* no sistema operacional. Por essa razão, a equipe fixou um limite deliberado de concorrência (`concurrencyLimit = 150`) no Worker Pool.
   - **Consistência Eventual:** Em notificações assíncronas, pequenas variações de milissegundos podem fazer com que espectadores recebam alertas fora de ordem estrita, o que é plenamente aceitável no domínio de streaming.

---
Benefícios:Desacoplamentoestritoemissão de eventosregrasdemoderação;adiçãodenovosobservadoressemmodificar o `StreamChannel` (OCP); tolerânciafalhastransitóriasde socket em notificações remotas.

**Custoslimites:**Concorrênciarequer dimensionamento explícito do Worker Pool para evitar esgotamento de *file descriptors* no sistema operacional; consistência eventual na ordem de entrega de notificações assíncronas

---
## Referências

1. **GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; VLISSIDES, John.** *Design Patterns: Elements of Reusable Object-Oriented Software*. Reading: Addison-Wesley, 1995.
2. **LARMAN, Craig.** *Utilizando UML e Padrões: Uma Introdução à Análise e ao Projeto Orientado a Objetos e ao Desenvolvimento Iterativo*. 3ª edição. Porto Alegre: Bookman, 2007.
3. **SOMMERVILLE, Ian.** *Engenharia de Software*. 8ª edição. São Paulo: Pearson Addison-Wesley, 2007.
4. **PRESSMAN, Roger S.** *Engenharia de Software: Uma Abordagem Profissional*. 6ª edição. São Paulo: McGraw-Hill, 2006.
5. **SERRANO, Milene.** *Arquitetura e Desenho de Software: Aula - GoFs Comportamentais*. Material didático da disciplina FGA0208. Universidade de Brasília (UnB Gama), 2026.
6. **TWITCH DEVELOPERS.** *Twitch EventSub Documentation: Real-Time Event Architecture*. Disponível em: `https://dev.twitch.tv/docs/eventsub/`. Acesso em: 15 out. 2026.
7. **GOOGLE DEVELOPERS.** *WebSub (PubSubHubbub) & Firebase Cloud Messaging*. Disponível em: `https://pubsubhubbub.appspot.com/`. Acesso em: 15 out. 2026.
8. **PUSHER CHANNELS.** *Scalable Real-Time WebSocket Infrastructure for Streaming*. Disponível em: `https://pusher.com/docs/channels/`. Acesso em: 15 out. 2026.
9. **AMAZON WEB SERVICES.** *Amazon Interactive Video Service (IVS) Chat Documentation*. Disponível em: `https://docs.aws.amazon.com/ivs/`. Acesso em: 15 out. 2026.
10. **SOURCEMAKING.** *Observer & Strategy Design Patterns*. Disponível em: `https://sourcemaking.com/design_patterns/observer`. Acesso em: 15 out. 2026.

---
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
| 1.0 | 15/10/2026 | Hugo Freitas Silva | Implementação das interfaces do GoF Observer e prototipação de canal | Eduardo Lôbo Moreira | Commit inicial SubEquipe 03 |
| 1.1 | 16/10/2026 | Philipe Amâncio Reis Caetano | Implementação dos observadores de moderação (AutoMod, Safety Vision, DMCA) e leitura PPM | Hugo Freitas Silva | Commit do pipeline de moderação |
| 1.2 | 16/10/2026 | Eduardo Lôbo Moreira | Elaboração dos diagramas UML de classes, componentes e casos de uso e redação do ADR-003 | Philipe Amâncio Reis Caetano | Commit dos diagramas GoF |
| 1.3 | 16/10/2026 | Hugo Freitas Silva | Implementação do GoF Strategy e execução do benchmark de concorrência com 2.000 viewers | Eduardo Lôbo Moreira | Commit da Iniciativa Extra |
| 1.4 | 17/10/2026 | Eduardo Lôbo Moreira | Elaboração do dossiê de fontes com Helium Browser e estruturação dos relatos de IA | Hugo Freitas Silva | Commit de fontes e IA |
| 1.5 | 17/10/2026 | SubEquipe 03 | Integração final da documentação ao repositório oficial da Entrega 03 | Equipe Geral | Pull Request SubEquipe 03 |
:---: | :---: | :::::0.1| 16/10/2026 | Eduardo Lôbo Moreira | Modelagem GoF Observer, diagrama de classes e sequência, ADR-003 e código do StreamChannelCommitinicial SubEquipe 03 |
| 0.2 | 17/10/2026 | Eduardo Lôbo Moreira | Estruturação do relatório no padrão da SubEquipe 01, relato de IA e suíte de testes unitáriosPullRequestSubEquipe03
OO quadro consolidado geral de contribuições e participações está em [1.2. Participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
