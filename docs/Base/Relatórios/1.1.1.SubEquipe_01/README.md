# 1.1.1. SubEquipe_01 — GoFs Criacionais + IA Generativa

**Estado:** em elaboração. O planejamento da SubEquipe_01 v1.0 (08/10/2026) propõe **Builder** para `StreamConfig` como padrão principal e **Factory Method** para a hierarquia `UserContent` como segundo padrão; a proposta ainda depende de validação dos quatro integrantes na reunião da subequipe. A modelagem do Builder já está registrada em [1.1.1.1. Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md) e em [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md); a do Factory Method, em [1.1.1.3. Modelagem — Factory Method](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.3.ModelagemFactoryMethod.md) e em [ADR-002](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md).

Este relatório reúne os espaços necessários à Entrega 03. O conteúdo técnico e os relatos individuais serão produzidos pelos integrantes abaixo.

## Integrantes

| Matrícula | Integrante | GitHub |
| --- | --- | --- |
| 24/1039645 | Lucas Andrade Zanetti | [@Bappoz](https://github.com/Bappoz) |
| 24/1031852 | Matheus Lemes Amaral | [@1emes](https://github.com/1emes) |
| 24/1040332 | Pedro Druck Montalvão Reis | [@pedruck](https://github.com/pedruck) |
| 24/1039073 | Heitor Macedo Ricardo | [@HeitorM50](https://github.com/HeitorM50) |

Composição mantida conforme a [introdução da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Introducao).

## Foco do relatório

**GoFs Criacionais + IA Generativa.** A entrega mínima deste foco inclui um padrão criacional, modelo UML, código e vídeo demonstrando sua execução, além dos pontos de vista individuais.

## Estrutura da subequipe e focos entregues

```text
SubEquipe_01 — GoFs Criacionais + IA Generativa
├── 📘 Documentação · este repositório · docs/Base/Relatórios/1.1.1.SubEquipe_01/
│   ├── README.md                     relatório geral (contexto, escolha, execução, versões)
│   ├── 1.1.1.1.ModelagemBuilder.md   UML de classes antes/depois + evidências E01–E12
│   ├── 1.1.1.2.SequenciaBuilder.md   UML de sequência (Director → Builder → build())
│   ├── 1.1.1.5.Video.md              vídeo do padrão em funcionamento
│   ├── 1.1.1.6.IAGenerativa.md       pontos de vista individuais
│   ├── 1.1.1.7.BenchmarkBuilder.md   iniciativa extra: tempo e memória (padrão × manual)
│   ├── ADR/ADR-001-builder-stream-config.md
│   └── assets/builder/               .puml, .svg, .png e evidências
└── 💻 Código · repositório separado · g6-streaming-entrega03-subgrupo01-codigo
    ├── src/criacionais/builder/      Product, Builder, ConcreteBuilder, Director, demo.ts
    ├── bench/                        medidor TypeScript (cenários, rodadas, gc)
    └── benchmark/                    Python: gerar_relatorio.py, gráficos, relatório
```

| Foco da entrega | Builder (`StreamConfig`) | Factory Method (`UserContent`) | Onde |
| --- | --- | --- | --- |
| Contexto e justificativa | ✅ | 🟡 pendente (Matheus e Pedro) | [Contexto](/Base/Relatórios/1.1.1.SubEquipe_01/README.md?id=contexto-problema) · [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md) |
| Modelagem UML — classes | ✅ Lucas | 🟡 pendente | [1.1.1.1](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md) |
| Modelagem UML — sequência | ✅ Heitor | 🟡 pendente | [1.1.1.2](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.2.SequenciaBuilder.md) |
| Implementação e testes | ✅ integrado em 16/10/2026 | 🟡 pendente | [Repositório de código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo) |
| Execução documentada | ✅ `npm run demo:builder` | 🟡 pendente | [Execução](/Base/Relatórios/1.1.1.SubEquipe_01/README.md?id=execução-e-vídeo-do-padrão-em-funcionamento) |
| Vídeo | ⬜ a preencher | ⬜ a preencher | [1.1.1.5](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.5.Video.md) |
| Iniciativa extra — benchmark | ✅ tempo e memória | ⬜ sem cenário | [1.1.1.7](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) |
| IA Generativa | 🟡 Lucas preenchido | 🟡 a preencher | [1.1.1.6](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.6.IAGenerativa.md) |

Legenda: ✅ entregue · 🟡 em andamento · ⬜ não iniciado.

## IA Generativa e vídeo

Os pontos de vista individuais ficam em [1.1.1.6. IA Generativa](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.6.IAGenerativa.md) e o vídeo do padrão em [1.1.1.5. Vídeo](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.5.Video.md).

| Integrante | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| --- | --- | --- |
| Lucas Andrade Zanetti | A preencher pelo integrante | [Preenchido](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.6.IAGenerativa.md?id=lucas-andrade-zanetti) |
| Matheus Lemes Amaral | Implementar o Factory Method sobre a hierarquia `UserContent`, que eu e o Pedro modelamos na Entrega 02, mostrou que o padrão vale pelo que fica **em comum**, e não pela criação em si: o ganho foi escrever uma vez o caminho de registro (persistir, moderar e publicar sob a regra 8 do v3) no `submit()` do Creator e deixar cada subclasse decidir só qual classe instanciar. Aprendi a diferença prática entre Factory Method e uma fábrica simples com `switch`, o custo das hierarquias paralelas (um criador por produto) e que `submit()` acaba sendo também um Template Method sobre o método-fábrica. Também aprendi a pôr as regras no construtor do produto, para nem um `new` fora do padrão criar conteúdo inválido, e a conferir diagrama e código lado a lado: o diagrama de classes foi desenhado depois do código e precisou ser corrigido quando o código mudou. Na revisão do PR do Builder, aprendi que o Docsify resolve imagens a partir da pasta da página e captura links de arquivo como rota, o que quebrava o site. | Usei o **Claude** (Claude Code) no Factory Method como auxiliar nas partes que eu não sabia fazer: estruturar o Creator genérico em TypeScript, escrever os testes com Vitest, gerar os diagramas em PlantUML e organizar o ADR-002. Depois revisei o código e alterei as partes que considerei incorretas, e pedi uma segunda revisão independente ao GPT (Codex). Essa revisão apontou problemas reais que o primeiro resultado tinha deixado passar — live encerrada continuava publicada, gravação podia nascer de live que nem tinha começado e ser criada duas vezes, datas expostas por referência — e afirmações do ADR mais fortes do que o diagrama v3 sustentava; as correções estão nos commits `fix(...)` do PR #2 do código e na revisão do ADR-002. Validei o resultado com os testes (131, com 100% de cobertura), executando a demo e conferindo regra por regra contra a nota "Regras do fluxo de clipes" do v3. **Limite:** a IA produz rápido muito código e texto que parecem certos; sem conferir contra o modelo da Entrega 02 e sem a segunda revisão, erros de regra de negócio e exageros na justificativa teriam passado. |
| Pedro Druck Montalvão Reis | A preencher pelo integrante | A preencher pelo integrante |
| Heitor Macedo Ricardo | A preencher pelo integrante | A preencher pelo integrante |

## Metodologia

**A preencher.** Descrever como a subequipe trabalhou: divisão de atividades, reuniões, estudos, ferramentas, debates e revisões. Relacionar atas e gravações, quando houver, aos [registros de reuniões](/Projeto/Atas/README.md).

## GoF Criacional

### Contexto (problema)

Na Entrega 02, `LiveStreamService.createStream(userId, config: StreamConfig)` recebe a configuração de uma transmissão ao vivo. No diagrama de classes v3, `StreamConfig` é um `«value object»` com quatro atributos — `title`, `visibility`, `latencyMode` e `recordAutomatically` — enquanto resolução, taxa de quadros e bitrate aparecem em `QualityVariant` (decisão DE08) e são tratados como responsabilidade do encoder do cliente.

O problema de criação só existe de fato quando os parâmetros de vídeo entram em `StreamConfig`: aí a configuração passa a ter sete campos, vários opcionais e **interdependentes** — latência baixa não convive com 2160p, e o bitrate mínimo depende da combinação resolução × taxa de quadros. Um construtor único com sete argumentos fica ilegível e aceita combinações inválidas sem um ponto onde essas regras sejam verificadas.

Essa incorporação é uma **revisão declarada** do modelo da Entrega 02 (decisão D1 do ADR-001) e precisa de aceite do grupo. O levantamento completo do problema, com as evidências que sustentam cada interdependência, está em [ADR-001 §1–§2](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_1-contexto).

**Factory Method — `UserContent`.** Na Entrega 02, `LiveStream`, `RecordedVideo` e `Clip` herdam de `UserContent` (decisão DE03) e nascem em três pontos diferentes do fluxo `LiveStream → RecordedVideo → ClipRequest → Clip`: `LiveStreamService.createStream`, `MediaProcessingService.persistRecording` e a extração do clipe coordenada por `ClipService`. O v3 oferece os elementos de um caminho comum de registro — `ContentRepository.save(content: UserContent)`, `PolicyService.moderate(contentId)` e a regra 8 da nota "Regras do fluxo de clipes", segundo a qual publicar exige moderação aprovada e mídia pronta para qualquer conteúdo —, mas não desenha esse fluxo. Aplicada a regra 8 aos três tipos, o caminho ficaria repetido em cada serviço, e o código que registra conteúdo precisaria conhecer a classe concreta criada.

Ao contrário do Builder, o padrão não exige revisar atributos do v3: os três pontos de criação e a hierarquia aparecem no diagrama e nas evidências FM-E01 a FM-E03; o caminho comum é proposta desta entrega ([ADR-002 §1](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_1-contexto)).

### Escolha e justificativa

**Builder** (padrão criacional GoF) para `StreamConfig`: a construção é feita passo a passo por uma interface fluente, todas as regras de combinação são verificadas em um único `build()`, e o produto devolvido é imutável. Isso separa a montagem da representação final e permite que um `StreamConfigDirector` ofereça presets (baixa latência, alta qualidade, móvel) sem duplicar validação em cada cliente.

Alternativas consideradas e descartadas, com o argumento de cada uma — construtor de sete parâmetros, literal de objeto com campos opcionais, funções estáticas nomeadas e Builder sem Director — estão em [ADR-001 §3](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_3-alternativas-consideradas), junto das sete decisões de projeto derivadas (D1–D7) e das cinco regras de validação (R1–R5).

**Limite declarado:** com os quatro atributos do v3, o Builder teria ganho pequeno e um construtor simples bastaria. A justificativa do padrão depende do aceite da revisão D1.

**Factory Method** (padrão criacional GoF) para a hierarquia `UserContent`: o Creator abstrato `UserContentCreator` escreve uma vez a operação comum (`submit`: criar, persistir, moderar, publicar quando possível) e delega ao **método-fábrica** `createContent` de cada subclasse — `LiveStreamCreator`, `RecordedVideoCreator`, `ClipCreator` — a decisão de qual classe instanciar e de onde vêm os dados. É a intenção do padrão no GoF: deixar as subclasses decidirem qual classe instanciar. O `LiveStreamCreator` recebe o `StreamConfig` montado pelo Builder, o que liga os dois padrões da subequipe.

Alternativas descartadas — `new` em cada serviço com o caminho repetido (como no v3), fábrica simples com `switch` sobre o tipo, composição com uma função de criação, Abstract Factory e Builder — estão em [ADR-002 §3](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_3-alternativas-consideradas), junto das nove decisões derivadas (DF1–DF9) e das regras F1–F6. F2 a F6 vêm da nota do v3 (F2 também da máquina M4); F1 e alguns refinamentos de F3 são decisões de projeto.

**Limites declarados:** a entrada do método-fábrica é tipada por genéricos (adaptação, não a variante parametrizada do GoF); cada produto novo custa também um criador novo (hierarquias paralelas); e o pedido de clipe feito antes de a gravação ficar pronta é recusado, e não enfileirado como no v3, porque a fila é responsabilidade do `ClipService`.

### Modelagem (notação UML)

**Builder — concluído.** Diagrama de classes "antes" (recorte do v3 da Entrega 02) e "depois" (Builder aplicado), correspondência entre participantes GoF e classes do domínio, regras de validação e as doze evidências que as sustentam: [1.1.1.1. Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md). Fonte editável em PlantUML e exportações PNG/SVG ficam em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/" target="_blank" rel="noopener">assets/builder/</a>. Autoria: Lucas Andrade Zanetti.

**Builder — sequência concluída.** Diagrama de sequência do preset montado pelo `StreamConfigDirector` (Client → Director → Builder → `build()`), com o caminho de erro de validação e a correspondência mensagem a mensagem com o código: [1.1.1.2. Sequência — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.2.SequenciaBuilder.md). Fonte editável em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/builder-sequencia-v1.puml" target="_blank" rel="noopener"><code>builder-sequencia-v1.puml</code></a>. Autoria: Heitor Macedo Ricardo.

**Factory Method — concluído.** Diagrama de classes desenhado a partir do código, recorte "antes" do componente UGC do v3, correspondência entre participantes GoF, serviços do v3 e classes, regras F1–F6 e evidências: [1.1.1.3. Modelagem — Factory Method](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.3.ModelagemFactoryMethod.md). Diagrama de sequência de `ClipCreator.submit`, separando o método-fábrica da operação comum, com os caminhos de erro: [1.1.1.4. Sequência — Factory Method](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.4.SequenciaFactoryMethod.md). Fontes em PlantUML e exportações PNG/SVG ficam em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/factory-method-classes-v1.puml" target="_blank" rel="noopener"><code>assets/factory-method/</code></a>. Autoria: Matheus Lemes Amaral.

### Implementação (código)

**Builder — concluído no código integrado à `main` em 16/10/2026.** Implementação TypeScript do Builder, `StreamConfigDirector`, validação acumulada e testes estão no [repositório de código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo), integrado pelo [PR #1](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/1).

**Factory Method.** Código em [`src/criacionais/factory-method/`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method) do repositório de código (TypeScript, sem dependência de execução; [PR #2 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/2), aguardando revisão; os links apontam para o commit `a7ae60e` da branch do PR). Um arquivo por participante:

| Participante | Arquivo | Trecho que realiza o padrão |
| --- | --- | --- |
| Product | `user-content.ts` | classe abstrata `UserContent`; `publish()` aplica F6 com o gancho abstrato `isMediaReady()` |
| ConcreteProduct | `live-stream.ts`, `recorded-video.ts`, `clip.ts` | cada um implementa `isMediaReady()`; `RecordedVideo` e `Clip` recebem a origem e verificam F2–F5 |
| Creator | `user-content-creator.ts` | `submit()` chama `this.createContent(input)` e segue só com `UserContent`; `createContent` é `protected abstract` |
| ConcreteCreator | `live-stream-creator.ts`, `recorded-video-creator.ts`, `clip-creator.ts` | sobrescrevem `createContent` com o `new` da classe concreta e a busca da origem no repositório |
| Client | `demo.ts` | `registrar(creator, input)` aceita qualquer `UserContentCreator` |

O README do padrão, no repositório de código, explica as decisões de estrutura e os limites. São 78 testes do Factory Method (131 no total), com 100% de cobertura de linhas, ramos e funções no código instrumentado (demos e benchmark ficam fora da medição).

### Execução e vídeo do padrão em funcionamento

Código no [repositório de código da SubEquipe_01](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo), separado deste para que código e testes não interfiram no GitHub Pages.

**Pré-requisitos:** Node 22 ou superior e npm. Nenhuma outra dependência global; o TypeScript roda direto pelo `tsx`, sem etapa de build.

```bash
git clone https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo.git
cd g6-streaming-entrega03-subgrupo01-codigo
npm ci                # instala as dependências travadas no package-lock
npm run check         # formatação → lint → tipos → testes (a mesma sequência da CI)
npm run demo:builder  # demonstração do Builder no terminal
```

**Cenário demonstrado (`demo:builder`).** Um único builder, reaproveitado do início ao fim:

1. **Presets do Director** — `lowLatency`, `highQuality` e `mobile`, cada um impresso com título, perfil de vídeo, latência, visibilidade, gravação e a confirmação de que o objeto é imutável.
2. **Configuração sob medida** — o Client usa o builder direto, sem Director (1080p, não listada, gravação desligada).
3. **Configuração inválida** — título vazio, 4K com latência `ULTRA_LOW`, 75 fps e 2 Mbps. O `build()` rejeita e lista **as quatro violações de uma vez**, cada uma com o id da regra do [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md).

**Resultado esperado** (trecho da parte 3, saída real):

```text
=== 3. Configuração inválida rejeitada no build() ===

Título vazio + 4K com latência ULTRA_LOW + 75 fps + 2 Mbps (abaixo do piso de 4K):
  InvalidStreamConfigError: 4 violações
  - R1 título é obrigatório e não pode ser vazio
  - R3 taxa de quadros não pode passar de 60 (recebido: 75)
  - R4 latência ULTRA_LOW é incompatível com R2160P; use STANDARD ou reduza a resolução
  - R5 bitrate 2000000 bps está abaixo do mínimo de 14000000 bps para R2160P a 75 fps
```

`npm run check` deve terminar sem erro. O Builder foi integrado à `main` em 16/10/2026 ([PR #1](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/1)), com 53 testes passando e 100% de cobertura de linhas, ramos e funções (`npm run coverage`).

**Factory Method (`demo:factory-method`).** Mesmos pré-requisitos e repositório; enquanto o [PR #2 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/2) não for integrado à `main`, rode `git checkout feat/factory-method-user-content` antes do `npm ci`.

```bash
npm run demo:factory-method  # live → gravação → clipe pela mesma função cliente
```

**Cenário demonstrado.** Um repositório em memória e uma política de moderação que recusa o termo "spoiler" são compartilhados pelos três criadores:

1. **`LiveStreamCreator`** — cria a live a partir do preset `highQuality` do Builder. Ela é aprovada, mas fica fora do ar até `markLive()`, porque a mídia ainda não existe (F6).
2. **`RecordedVideoCreator`** — cria a gravação da live encerrada em `PROCESSING`; com `markReady()` (evento `RecordingAvailable`), ela é publicada.
3. **`ClipCreator`** — um espectador recorta 30 s da gravação; o clipe nasce publicado, com o dono da gravação e o espectador em `createdByUserId`.
4. **Pedidos recusados** — clipe com termo bloqueado (criado, mas `REJECTED` e fora do ar), recorte além do fim da gravação (F5), gravação de live sem gravação automática (F2) e clipe de transmissão sem gravação (F4).

**Resultado esperado** (trecho das partes 3 e 4, saída real):

```text
=== 3. ClipCreator — um espectador recorta a gravação ===
  classe:        Clip
  id:            conteudo-03
  título:        O refrão do show
  dono:          criadora
  visibilidade:  PUBLIC
  moderação:     APPROVED
  mídia pronta:  sim
  publicação:    PUBLISHED
  pedido por:    espectador (30 s de recorte)

=== 4. Pedidos recusados ===
...
Clipe que passa do fim da gravação (3600 s):
  ContentRuleViolationError: F5 recorte 3590s–3700s fora de 0 ≤ início < fim ≤ 3600s

Gravação de uma live com gravação automática desligada:
  ContentRuleViolationError: F2 a transmissão conteudo-06 não tem gravação automática habilitada

Clipe de uma transmissão que não tem gravação:
  ContentRuleViolationError: F4 a transmissão conteudo-06 não tem gravação para recortar
```

O id `conteudo-05` não aparece porque o recorte recusado por F5 chegou a reservar um id antes de o construtor de `Clip` rejeitá-lo; nada foi persistido.

**Vídeo do Factory Method em funcionamento** (1 min 44 s, sem áudio; apresentação: Matheus Lemes Amaral). Gravação de um terminal executando os comandos reais do roteiro: participantes do padrão, `submit()` do Creator, `createContent()` do `ClipCreator`, `npm run check` (131 testes) e a demonstração completa, com os pedidos recusados por F5, F2 e F4. A digitação dos comandos é simulada por script, para manter o ritmo legível; as saídas são as dos comandos executados.

<video controls preload="metadata" width="100%" src="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/video/factory-method-demo.mp4"></video>

<a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/video/factory-method-demo.mp4" target="_blank" rel="noopener">Abrir o vídeo (MP4)</a>

**Pendente.** Vídeo do Builder em funcionamento. O vídeo do padrão em funcionamento tem página própria: [1.1.1.5. Vídeo](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.5.Video.md).

## Rastreabilidade & Elos com Outros Artefatos

A [modelagem da SubEquipe_01 na Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.SubEquipe_01) é um ponto de partida. A equipe deverá indicar quais artefatos e elementos sustentam efetivamente sua decisão nesta etapa.

| Problema ou requisito | Artefato de origem (link) | Elemento do modelo | Trecho de código (link) | Evidência de execução (link) |
| --- | --- | --- | --- | --- |
| `StreamConfig` com sete parâmetros interdependentes cria combinações inválidas (D1) | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e01-planejamento-premissa-streamconfig.png" target="_blank" rel="noopener">E01</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e02-v3-streamconfig-quatro-atributos.png" target="_blank" rel="noopener">E02</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e04-e02-livestreamservice-recebe-streamconfig.png" target="_blank" rel="noopener">E04</a> · [ADR-001 §1](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_1-contexto) | Product `StreamConfig` («value object» revisado) | [`stream-config.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/stream-config.ts) | `npm run demo:builder`, parte 1 |
| R1 — título obrigatório (D7) | [ADR-001 §4](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_4-decisão) | ConcreteBuilder · `validate()` | [`default-stream-config-builder.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/default-stream-config-builder.ts#L115) | Parte 3 do demo (`R1 título é obrigatório…`) · testes `R1 — título obrigatório` |
| R2 — resolução, fps e bitrate informados juntos | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e10-bitrate-depende-de-codec-resolucao-fps.png" target="_blank" rel="noopener">E10</a> | `VideoSettings` (garantia pelo tipo, não por `validate()`) | [`video-settings.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/video-settings.ts) | Teste `deixa os três campos de vídeo indefinidos quando não há perfil (R2)` |
| R3 — taxa de quadros até 60 fps | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e11-taxa-de-quadros-ate-60-e-codecs.png" target="_blank" rel="noopener">E11</a> | ConcreteBuilder · `validate()` | [`default-stream-config-builder.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/default-stream-config-builder.ts#L129) | Parte 3 do demo (75 fps rejeitado) · testes `R3 — teto de taxa de quadros` |
| R4 — latência baixa incompatível com 4K | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e08-latencia-baixa-incompativel-com-4k.png" target="_blank" rel="noopener">E08</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e09-4k-forca-latencia-normal.png" target="_blank" rel="noopener">E09</a> | ConcreteBuilder · `validate()` | [`default-stream-config-builder.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/default-stream-config-builder.ts#L135) | Parte 3 do demo (`ULTRA_LOW` + 2160p) · testes `R4` |
| R5 — bitrate mínimo por resolução × fps | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e10-bitrate-depende-de-codec-resolucao-fps.png" target="_blank" rel="noopener">E10</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e12-plataforma-a-bitrate-por-resolucao.png" target="_blank" rel="noopener">E12</a> | `minimumBitrateBps` (tabela de pisos) | [`bitrate-floor.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/bitrate-floor.ts#L49) | Parte 3 do demo (`2000000 bps … mínimo de 14000000`) · `bitrate-floor.test.ts` |
| Presets de transmissão sem repetir validação em cada cliente | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e06-e02-encoder-parametros-do-cliente.png" target="_blank" rel="noopener">E06</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e07-e02-sequencia-createstream.png" target="_blank" rel="noopener">E07</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e12-plataforma-a-bitrate-por-resolucao.png" target="_blank" rel="noopener">E12</a> · [Sequência](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.2.SequenciaBuilder.md) | Director `StreamConfigDirector` | [`stream-config-director.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/stream-config-director.ts) | Parte 1 do demo (3 presets) · teste `chama reset() primeiro e build() por último` |
| Início da transmissão envia `StreamConfig` ao serviço (Client) | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e04-e02-livestreamservice-recebe-streamconfig.png" target="_blank" rel="noopener">E04</a>, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e07-e02-sequencia-createstream.png" target="_blank" rel="noopener">E07</a> | Client `LiveStreamService` / `demo.ts` | [`demo.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/src/criacionais/builder/demo.ts) | `npm run demo:builder` completo |
| Custo do padrão e decisão D6 eram hipóteses no ADR-001 | [ADR-001 §5](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_5-consequências) | Cenário de benchmark, três braços | [`bench/cenarios/builder.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/bench/cenarios/builder.ts) · [`gerar_relatorio.py`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/benchmark/gerar_relatorio.py) | [1.1.1.7. Benchmark](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) · [relatório gerado](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/main/benchmark/relatorio/relatorio-benchmark.md) |
| Factory Method: conteúdo nasce em três serviços e passa pelo mesmo caminho de registro | [Modelagem Estática da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) (FM-E02) | `UserContentCreator.submit` / `createContent` | [`user-content-creator.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/user-content-creator.ts) | Demo, partes 1–3 |
| Hierarquia `UserContent` (DE03) | [Conteúdo Gerado pelo Usuário](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.2.Foco01.ConteudoGeradoUsuario) (FM-E01) | Product e ConcreteProducts | [`user-content.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/user-content.ts), [`clip.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/clip.ts) | Demo, linha `classe:` de cada conteúdo |
| Regra 8: publicar exige `APPROVED` e mídia pronta (F6) | Nota "Regras do fluxo de clipes" do v3 (FM-E03) | `UserContent.publish`, `isMediaReady` | [`user-content.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/user-content.ts) | Demo, partes 1 e 2 e clipe `REJECTED` da parte 4 |
| Regras 1, 2, 4 e 7: origem e janela do recorte, dono preservado (F2, F4, F5) | Nota do v3 (FM-E03) | Construtores de `RecordedVideo` e `Clip` | [`clip.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/clip.ts), [`recorded-video.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/recorded-video.ts) | Demo, partes 3 e 4 |
| `createStream(userId, config: StreamConfig)` liga Builder e Factory Method | [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md) e diagrama v3 | `LiveStreamCreator` | [`live-stream-creator.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/live-stream-creator.ts) | Demo, parte 1 |

As evidências E01–E12 são capturas de tela arquivadas em [Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md?id=evidências); cada linha acima aponta para as que sustentam a escolha. Os links de código do Builder apontam para a `main` do repositório de código; os do Factory Method, para o commit `a7ae60e` do [PR #2 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/2), ainda fora da `main`.

## Senso Crítico

**Benefícios que as evidências sustentam.**

- A validação ficou em um só ponto: `build()` executa R1, R3, R4 e R5 e devolve **todas** as violações de uma vez, e o produto sai imutável. A demonstração da parte 3 mostra quatro violações simultâneas, cada uma com o id da regra do ADR-001.
- A cobertura é verificável: 53 testes passando e 100% de cobertura de linhas, ramos e funções (`npm run coverage`).
- O Director concentra os presets sem duplicar validação: um título vazio num preset sai como `InvalidStreamConfigError` com R1.

**Custos medidos.** O [benchmark](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) mostrou que o Builder custa de 2,2× a 2,9× a instanciação manual em tempo (cerca de 82 a 135 ns por instância, conforme N) e 326 B contra 80 B por instância em memória (N = 100 mil). Como a configuração é criada uma vez por transmissão, o custo é irrelevante para o sistema. O braço manual não valida nada; a diferença inclui, portanto, o custo das regras, e as duas parcelas não foram separadas.

**Decisões revistas ao longo do trabalho.**

- **D1 é uma revisão do modelo da Entrega 02.** A premissa do planejamento ("muitos parâmetros interdependentes") só se sustentava depois de mover resolução, fps e bitrate para `StreamConfig`. Com os quatro atributos do v3 o Builder teria ganho pequeno; esse limite continua declarado e depende do aceite do grupo.
- **R2 deixou de ser verificação.** O código agrupou os três campos de vídeo em `VideoSettings`, e a regra passou a ser garantida pelo tipo. O diagrama de classes divergiu do código e a divergência foi apontada na revisão do PR #2; o diagrama foi corrigido a partir do código integrado.
- **D6 perdeu a justificativa de desempenho.** O resultado preliminar do benchmark (reutilizado quase 2× mais lento) era ruído de amostra curta, e a medição pareada não achou diferença de tempo. A decisão se sustenta por design (o Director reaproveita o builder que recebe) e por `reset()` ser exigido por correção. O benchmark em Python acrescentou uma economia de memória de cerca de 17%, que não era a vantagem prometida.

**Coerência entre UML e implementação.** Diagrama de classes, sequência e código foram conferidos entre si: a ordem `reset → withTitle → withLatencyMode → withVideo → build` do diagrama de sequência é verificada por um teste com builder dublê. Divergências remanescentes conhecidas: nenhuma registrada até esta data; a conferência do Factory Method depende da dupla responsável.

**Limites.** R4 e R5 vêm de documentação pública de plataformas externas, não do nosso sistema; os valores numéricos são de referência e configuráveis. Os números do benchmark valem para uma máquina e uma versão do Node: a razão entre braços mudou de cerca de 3,9× (máquina do Heitor) para 2,9× (esta execução), então não deve ser tomada como constante.

**Factory Method.** O ganho é concreto e localizado: a regra 8 do v3 passou a existir em um só lugar (`submit` + `publish`), e um tipo novo de conteúdo entra como subclasse, sem tocar no Creator. O custo é a hierarquia de criadores paralela à de produtos — três classes a mais para três produtos — e um método que faz dois papéis (Template Method sobre o método-fábrica). Decisões revistas durante o trabalho: as regras saíram do criador e foram para o construtor dos produtos (DF4), para que nem um `new` fora do padrão crie conteúdo inválido; o pedido de clipe sem gravação pronta passou a ser recusado, e não enfileirado (DF8), uma simplificação declarada do fluxo assíncrono do v3; e uma revisão independente do código levou a despublicar a live ao encerrar, exigir live encerrada e gravação única em F2 (DF9), validar a data de F3 e copiar as datas dos produtos. O diagrama de classes foi desenhado depois do código e conferido contra ele; a ordem das mensagens do diagrama de sequência é verificada por teste. Detalhes em [ADR-002 §5](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_5-consequências).

## Referências

Fontes efetivamente consultadas, com a decisão ou artefato que cada uma fundamenta.

| Fonte | Fundamenta | Observação |
| --- | --- | --- |
| GAMMA, E.; HELM, R.; JOHNSON, R.; VLISSIDES, J. *Padrões de Projeto: soluções reutilizáveis de software orientado a objetos*. Porto Alegre: Bookman, 2000 | Builder: participantes, estrutura e consequências ([ADR-001 §3–§4](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_3-alternativas-consideradas)) | **Páginas ainda a confirmar** no exemplar consultado; não foram verificadas |
| Entrega 02, SubEquipe_01 — [Modelagem Estática](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) e [Evidências da Modelagem Dinâmica](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.2.1.Foco02.Evidencias) | `StreamConfig` do v3, `QualityVariant`, sequência de `createStream` (E02–E07) | Fonte primária do "antes" |
| Planejamento da SubEquipe_01, v1.0, 08/10/2026 | Escolha do Builder e do Factory Method, divisão de entregas e pares de revisão | Premissa do Builder conferida contra o modelo (E01) |
| Documentação pública de uma plataforma de transmissão ao vivo (ajuda do criador e configurações do encoder) | R3, R4 e R5 (E08–E11) | Plataforma **diferente** da de referência da Entrega 02; capturas arquivadas |
| Documentação pública da plataforma de referência da Entrega 02 | Bitrate por resolução (E12) | Convergência com a anterior sustenta tratar R5 como regra de domínio |
| Node.js. [`process.memoryUsage()`](https://nodejs.org/api/process.html) | Medida de `heapUsed` no [benchmark](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) | Documentação oficial; versão do Node usada: v26.8.1 |
| Node.js. [Opções de linha de comando](https://nodejs.org/api/cli.html) (`--expose-gc`, `--max-semi-space-size`) | Coleta de lixo forçada e semi-space grande na fase de memória | Documentação oficial |
| GAMMA, E.; HELM, R.; JOHNSON, R.; VLISSIDES, J. *Padrões de Projeto: soluções reutilizáveis de software orientado a objetos*. Porto Alegre: Bookman, 2000 | Factory Method: intenção, aplicabilidade, consequências e a variação de métodos-fábrica parametrizados ([ADR-002 §3–§4](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_3-alternativas-consideradas), decisões DF1 e DF2) | **Páginas ainda a confirmar** no exemplar consultado; não foram verificadas |
| Entrega 02, SubEquipe_01 — [Conteúdo Gerado pelo Usuário e Clipagem](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.2.Foco01.ConteudoGeradoUsuario) e [Modelagem Estática](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) | Hierarquia `UserContent` (DE03), os três serviços que criam conteúdo e a nota "Regras do fluxo de clipes", origem das regras F2–F6 (FM-E01 a FM-E03) | Fonte primária do "antes" do Factory Method |
| Entrega 02, SubEquipe_01 — [Diagrama de Máquina de Estados](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.10.Extra.DiagramaEstados), máquinas M2 (clipagem) e M4 (transmissão e gravação) | F2 (a gravação nasce do encerramento da live) e estados iniciais `CREATED` e `PROCESSING` dos produtos | Citada no ADR-002 e no README do padrão no repositório de código |

## Versionamentos & Participações

Registrar apenas alterações efetivamente realizadas, incluindo autoria, revisão e links para commits ou pull requests.

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| --- | --- | --- | --- | --- | --- |
| 1.0 | 15/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Modelagem do Builder (diagrama antes/depois), ADR-001 e evidências; contexto, escolha e justificativa neste relatório | @1emes ([revisão do PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2#pullrequestreview-5554232012)): diagrama de classes e conferência geral, incluindo o ADR-001 | [`3c19fce`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/3c19fce) · [`550571e`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/550571e) |
| 1.1 | 15/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Diagrama de sequência do Builder (PlantUML) e presets do Director; seção Execução deste relatório; quadro de participações | @1emes ([revisão do PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2#pullrequestreview-5554232012)): conferência geral, incluindo a sequência | [`b00ad0c`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/b00ad0c) |
| 1.2 | 16/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Imagem e links da sequência compatíveis com o roteador do Docsify | @1emes (revisão do [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2)) | [`14126fa`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/14126fa) |
| 1.3 | 16/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Diagrama de classes alinhado ao código integrado (`VideoSettings`, `fromBuilder`, R2 estrutural) | @1emes (revisão do [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2)) | [`3b6aefc`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/3b6aefc) |
| 1.4 | 17/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Links 404 do ADR-001 corrigidos; históricos de versão atualizados com a autoria de Heitor; páginas de Vídeo e IA Generativa; estrutura visual da subequipe; relato de IA do Lucas | Sem revisão registrada no PR | [`84b35b4`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/84b35b4) · [PR #4](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/4) |
| 1.5 | 17/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Rastreabilidade, senso crítico e referências preenchidos; iniciativa extra: [benchmark de tempo e memória](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) (script Python e relatório gerado no repositório de código) | Sem revisão registrada no PR | [`1d7c1b0`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/1d7c1b0) · [PR #5](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/5) · [PR #3 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/3) |
| 1.6 | 16/10/2026 | [Matheus Lemes Amaral](https://github.com/1emes) | Factory Method: diagramas de classes e de sequência (PlantUML), ADR-002, evidências FM-E01 a FM-E03; contexto, escolha e justificativa, modelagem, implementação, execução, rastreabilidade e senso crítico do padrão neste relatório; implementação, testes, demo e cenário de benchmark no repositório de código | @HeitorM50 ([comentários no ADR-002](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/3#pullrequestreview-5555487760), sem aprovação) · @pedruck ([aprovação do PR #3](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/3#pullrequestreview-5560570331)) | [PR #3](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/3) · [PR #2 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/2) |
| 1.7 | 17/10/2026 | [Pedro Druck Montalvão Reis](https://github.com/pedruck) | Conflitos do PR #3 com a `main` resolvidos sem descartar conteúdo (barra lateral, quadro de participações e este relatório: Builder e Factory Method lado a lado) e integração do PR #3 | Sem revisão registrada | [`a48982e`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/a48982e) · [PR #3](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/3) |
| 1.8 | 17/10/2026 | [Pedro Druck Montalvão Reis](https://github.com/pedruck) | Factory Method no código: correções nos ConcreteCreators a partir da revisão do PR #2 do código — gravação `FAILED` deixa de bloquear a transmissão, `submit` repetido após falha da moderação testado e documentado, perfil de vídeo do `StreamConfig` declarado fora da `LiveStream` (6 commits, 6 testes novos) | Revisão solicitada a @HeitorM50 | [PR #4 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/4) |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
