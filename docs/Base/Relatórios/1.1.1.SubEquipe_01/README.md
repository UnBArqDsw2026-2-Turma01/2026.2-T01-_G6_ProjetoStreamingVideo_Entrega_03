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
│   ├── ADR/ADR-001-builder-stream-config.md
│   └── assets/builder/               .puml, .svg, .png e evidências
└── 💻 Código · repositório separado · g6-streaming-entrega03-subgrupo01-codigo
    └── src/criacionais/builder/      Product, Builder, ConcreteBuilder, Director, demo.ts
```

| Foco da entrega | Builder (`StreamConfig`) | Factory Method (`UserContent`) | Onde |
| --- | --- | --- | --- |
| Contexto e justificativa | ✅ | 🟡 pendente (Matheus e Pedro) | [Contexto](/Base/Relatórios/1.1.1.SubEquipe_01/README.md?id=contexto-problema) · [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md) |
| Modelagem UML — classes | ✅ Lucas | 🟡 pendente | [1.1.1.1](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md) |
| Modelagem UML — sequência | ✅ Heitor | 🟡 pendente | [1.1.1.2](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.2.SequenciaBuilder.md) |
| Implementação e testes | ✅ integrado em 16/10/2026 | 🟡 pendente | [Repositório de código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo) |
| Execução documentada | ✅ `npm run demo:builder` | 🟡 pendente | [Execução](/Base/Relatórios/1.1.1.SubEquipe_01/README.md?id=execução-e-vídeo-do-padrão-em-funcionamento) |
| Vídeo | ⬜ a preencher | ⬜ a preencher | [1.1.1.5](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.5.Video.md) |
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
| A preencher | A preencher | A preencher | A preencher | A preencher |

## Senso Crítico

**A preencher.** Avaliar benefícios, custos e limitações do padrão, coerência entre UML e implementação e decisões revistas ao longo do trabalho. Relacionar a avaliação às evidências e à literatura consultada.

## Referências

**A preencher com fontes efetivamente consultadas.** Identificar autor, título, edição ou versão, ano e link quando disponível; relacionar as referências às decisões e artefatos que fundamentam.

## Versionamentos & Participações

Registrar apenas alterações efetivamente realizadas, incluindo autoria, revisão e links para commits ou pull requests.

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| --- | --- | --- | --- | --- | --- |
| 1.0 | 15/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Modelagem do Builder (diagrama antes/depois), ADR-001 e evidências; contexto, escolha e justificativa neste relatório | Pedro Druck Montalvão Reis (ADR-001) e Matheus Lemes Amaral (diagrama), conforme pares de revisão do planejamento | [`3c19fce`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/3c19fce) · [`550571e`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/550571e) |
| 1.1 | 15/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Diagrama de sequência do Builder (PlantUML) e presets do Director; seção Execução deste relatório; quadro de participações | A preencher (Pedro Druck Montalvão Reis, sequência) | [`b00ad0c`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/b00ad0c) |
| 1.2 | 16/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Imagem e links da sequência compatíveis com o roteador do Docsify | @1emes (revisão do [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2)) | [`14126fa`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/14126fa) |
| 1.3 | 16/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Diagrama de classes alinhado ao código integrado (`VideoSettings`, `fromBuilder`, R2 estrutural) | @1emes (revisão do [PR #2](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/pull/2)) | [`3b6aefc`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/commit/3b6aefc) |
| 1.4 | 17/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Links 404 do ADR-001 corrigidos; históricos de versão atualizados com a autoria de Heitor; páginas de Vídeo e IA Generativa; estrutura visual da subequipe; relato de IA do Lucas | A preencher | PR `docs/subequipe-01-versionamento-ia` |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
