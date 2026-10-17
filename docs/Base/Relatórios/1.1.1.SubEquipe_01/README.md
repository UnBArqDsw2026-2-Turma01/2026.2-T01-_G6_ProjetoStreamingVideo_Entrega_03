# 1.1.1. SubEquipe_01 — GoFs Criacionais + IA Generativa

**Estado:** em elaboração. O planejamento da SubEquipe_01 v1.0 (08/10/2026) propõe **Builder** para `StreamConfig` como padrão principal e **Factory Method** para a hierarquia `UserContent` como segundo padrão; a proposta ainda depende de validação dos quatro integrantes na reunião da subequipe. A modelagem do Builder já está registrada em [1.1.1.1. Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md) e em [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md).

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
| Matheus Lemes Amaral | A preencher pelo integrante | A preencher pelo integrante |
| Pedro Druck Montalvão Reis | A preencher pelo integrante | A preencher pelo integrante |
| Heitor Macedo Ricardo | A preencher pelo integrante | A preencher pelo integrante |

## Metodologia

**A preencher.** Descrever como a subequipe trabalhou: divisão de atividades, reuniões, estudos, ferramentas, debates e revisões. Relacionar atas e gravações, quando houver, aos [registros de reuniões](/Projeto/Atas/README.md).

## GoF Criacional

### Contexto (problema)

Na Entrega 02, `LiveStreamService.createStream(userId, config: StreamConfig)` recebe a configuração de uma transmissão ao vivo. No diagrama de classes v3, `StreamConfig` é um `«value object»` com quatro atributos — `title`, `visibility`, `latencyMode` e `recordAutomatically` — enquanto resolução, taxa de quadros e bitrate aparecem em `QualityVariant` (decisão DE08) e são tratados como responsabilidade do encoder do cliente.

O problema de criação só existe de fato quando os parâmetros de vídeo entram em `StreamConfig`: aí a configuração passa a ter sete campos, vários opcionais e **interdependentes** — latência baixa não convive com 2160p, e o bitrate mínimo depende da combinação resolução × taxa de quadros. Um construtor único com sete argumentos fica ilegível e aceita combinações inválidas sem um ponto onde essas regras sejam verificadas.

Essa incorporação é uma **revisão declarada** do modelo da Entrega 02 (decisão D1 do ADR-001) e precisa de aceite do grupo. O levantamento completo do problema, com as evidências que sustentam cada interdependência, está em [ADR-001 §1–§2](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_1-contexto).

**Pendente:** contexto do Factory Method (dupla Matheus + Pedro).

### Escolha e justificativa

**Builder** (padrão criacional GoF) para `StreamConfig`: a construção é feita passo a passo por uma interface fluente, todas as regras de combinação são verificadas em um único `build()`, e o produto devolvido é imutável. Isso separa a montagem da representação final e permite que um `StreamConfigDirector` ofereça presets (baixa latência, alta qualidade, móvel) sem duplicar validação em cada cliente.

Alternativas consideradas e descartadas, com o argumento de cada uma — construtor de sete parâmetros, literal de objeto com campos opcionais, funções estáticas nomeadas e Builder sem Director — estão em [ADR-001 §3](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_3-alternativas-consideradas), junto das sete decisões de projeto derivadas (D1–D7) e das cinco regras de validação (R1–R5).

**Limite declarado:** com os quatro atributos do v3, o Builder teria ganho pequeno e um construtor simples bastaria. A justificativa do padrão depende do aceite da revisão D1.

**Pendente:** escolha e justificativa do Factory Method (dupla Matheus + Pedro).

### Modelagem (notação UML)

**Builder — concluído.** Diagrama de classes "antes" (recorte do v3 da Entrega 02) e "depois" (Builder aplicado), correspondência entre participantes GoF e classes do domínio, regras de validação e as doze evidências que as sustentam: [1.1.1.1. Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md). Fonte editável em PlantUML e exportações PNG/SVG ficam em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/" target="_blank" rel="noopener">assets/builder/</a>. Autoria: Lucas Andrade Zanetti.

**Builder — sequência concluída.** Diagrama de sequência do preset montado pelo `StreamConfigDirector` (Client → Director → Builder → `build()`), com o caminho de erro de validação e a correspondência mensagem a mensagem com o código: [1.1.1.2. Sequência — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.2.SequenciaBuilder.md). Fonte editável em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/builder-sequencia-v1.puml" target="_blank" rel="noopener"><code>builder-sequencia-v1.puml</code></a>. Autoria: Heitor Macedo Ricardo.

**Pendente.** Diagrama de classes e de sequência do Factory Method (Matheus e Pedro).

### Implementação (código)

**Concluído no código integrado à `main` em 16/10/2026.** Implementação TypeScript do Builder, `StreamConfigDirector`, validação acumulada e testes estão no [repositório de código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo), integrado pelo [PR #1](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/1).

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

**Pendente.** Execução do Factory Method (`npm run demo:factory-method`, dupla Matheus + Pedro). O vídeo do padrão em funcionamento tem página própria: [1.1.1.5. Vídeo](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.5.Video.md).

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

As evidências E01–E12 são capturas de tela arquivadas em [Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md?id=evidências); cada linha acima aponta para as que sustentam a escolha. Os links de código apontam para a `main` do repositório de código. Rastreabilidade do Factory Method: **pendente** (Matheus e Pedro).

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

## Referências

Fontes efetivamente consultadas, com a decisão ou artefato que cada uma fundamenta.

| Fonte | Fundamenta | Observação |
| --- | --- | --- |
| GAMMA, E.; HELM, R.; JOHNSON, R.; VLISSIDES, J. *Padrões de Projeto: soluções reutilizáveis de software orientado a objetos*. Porto Alegre: Bookman, 2000 | Builder: participantes, estrutura e consequências ([ADR-001 §3–§4](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md?id=_3-alternativas-consideradas)) | **Páginas ainda a confirmar** no exemplar consultado; não foram verificadas |
| Entrega 02, SubEquipe_01 — [Modelagem Estática](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) e [Evidências da Modelagem Dinâmica](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.2.1.Foco02.Evidencias) | `StreamConfig` do v3, `QualityVariant`, sequência de `createStream` (E02–E07) | Fonte primária do "antes" |
| Planejamento da SubEquipe_01, v1.0, 08/10/2026 | Escolha do Builder, divisão de entregas e pares de revisão | Premissa conferida contra o modelo (E01) |
| Documentação pública de uma plataforma de transmissão ao vivo (ajuda do criador e configurações do encoder) | R3, R4 e R5 (E08–E11) | Plataforma **diferente** da de referência da Entrega 02; capturas arquivadas |
| Documentação pública da plataforma de referência da Entrega 02 | Bitrate por resolução (E12) | Convergência com a anterior sustenta tratar R5 como regra de domínio |
| Node.js. [`process.memoryUsage()`](https://nodejs.org/api/process.html) | Medida de `heapUsed` no [benchmark](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) | Documentação oficial; versão do Node usada: v26.8.1 |
| Node.js. [Opções de linha de comando](https://nodejs.org/api/cli.html) (`--expose-gc`, `--max-semi-space-size`) | Coleta de lixo forçada e semi-space grande na fase de memória | Documentação oficial |

## Versionamentos & Participações

Registrar apenas alterações efetivamente realizadas, incluindo autoria, revisão e links para commits ou pull requests.

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| --- | --- | --- | --- | --- | --- |
| 1.0 | 15/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Modelagem do Builder (diagrama antes/depois), ADR-001 e evidências; contexto, escolha e justificativa neste relatório | Pedro Druck Montalvão Reis (ADR-001) e Matheus Lemes Amaral (diagrama), conforme pares de revisão do planejamento | [`3c19fce`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/3c19fce) · [`550571e`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/550571e) |
| 1.1 | 15/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Diagrama de sequência do Builder (PlantUML) e presets do Director; seção Execução deste relatório; quadro de participações | A preencher (Pedro Druck Montalvão Reis, sequência) | [`b00ad0c`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/b00ad0c) |
| 1.2 | 16/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Imagem e links da sequência compatíveis com o roteador do Docsify | @1emes (revisão do [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2)) | [`14126fa`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/14126fa) |
| 1.3 | 16/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Diagrama de classes alinhado ao código integrado (`VideoSettings`, `fromBuilder`, R2 estrutural) | @1emes (revisão do [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2)) | [`3b6aefc`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/3b6aefc) |
| 1.4 | 17/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Links 404 do ADR-001 corrigidos; históricos de versão atualizados com a autoria de Heitor; páginas de Vídeo e IA Generativa; estrutura visual da subequipe; relato de IA do Lucas | A preencher | PR `docs/subequipe-01-versionamento-ia` |
| 1.5 | 17/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Rastreabilidade, senso crítico e referências preenchidos; iniciativa extra: [benchmark de tempo e memória](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.7.BenchmarkBuilder.md) (script Python e relatório gerado no repositório de código) | A preencher | PR `docs/subequipe-01-rastreabilidade-benchmark` |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
