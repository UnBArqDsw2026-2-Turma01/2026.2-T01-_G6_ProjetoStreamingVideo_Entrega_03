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

## Participantes no foco — lições aprendidas e IA Generativa

| Integrante | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| --- | --- | --- |
| Lucas Andrade Zanetti | A preencher pelo integrante | A preencher pelo integrante |
| Matheus Lemes Amaral | A preencher pelo integrante | A preencher pelo integrante |
| Pedro Druck Montalvão Reis | A preencher pelo integrante | A preencher pelo integrante |
| Heitor Macedo Ricardo | A preencher pelo integrante | A preencher pelo integrante |

Cada integrante deverá explicar o que aprendeu, como colaborou e, caso tenha usado IA, qual ferramenta utilizou, o apoio recebido, como validou os resultados e quais limitações encontrou. Informar também quando não houver uso de IA.

## Metodologia

**A preencher.** Descrever como a subequipe trabalhou: divisão de atividades, reuniões, estudos, ferramentas, debates e revisões. Relacionar atas e gravações, quando houver, aos [registros de reuniões](/Projeto/Atas/README.md).

## GoF Criacional

### Contexto (problema)

Na Entrega 02, `LiveStreamService.createStream(userId, config: StreamConfig)` recebe a configuração de uma transmissão ao vivo. No diagrama de classes v3, `StreamConfig` é um `«value object»` com quatro atributos — `title`, `visibility`, `latencyMode` e `recordAutomatically` — enquanto resolução, taxa de quadros e bitrate aparecem em `QualityVariant` (decisão DE08) e são tratados como responsabilidade do encoder do cliente.

O problema de criação só existe de fato quando os parâmetros de vídeo entram em `StreamConfig`: aí a configuração passa a ter sete campos, vários opcionais e **interdependentes** — latência baixa não convive com 2160p, e o bitrate mínimo depende da combinação resolução × taxa de quadros. Um construtor único com sete argumentos fica ilegível e aceita combinações inválidas sem um ponto onde essas regras sejam verificadas.

Essa incorporação é uma **revisão declarada** do modelo da Entrega 02 (decisão D1 do ADR-001) e precisa de aceite do grupo. O levantamento completo do problema, com as evidências que sustentam cada interdependência, está em [ADR-001 §1–§2](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md#1-contexto).

**Pendente:** contexto do Factory Method (dupla Matheus + Pedro).

### Escolha e justificativa

**Builder** (padrão criacional GoF) para `StreamConfig`: a construção é feita passo a passo por uma interface fluente, todas as regras de combinação são verificadas em um único `build()`, e o produto devolvido é imutável. Isso separa a montagem da representação final e permite que um `StreamConfigDirector` ofereça presets (baixa latência, alta qualidade, móvel) sem duplicar validação em cada cliente.

Alternativas consideradas e descartadas, com o argumento de cada uma — construtor de sete parâmetros, literal de objeto com campos opcionais, funções estáticas nomeadas e Builder sem Director — estão em [ADR-001 §3](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md#3-alternativas-consideradas), junto das sete decisões de projeto derivadas (D1–D7) e das cinco regras de validação (R1–R5).

**Limite declarado:** com os quatro atributos do v3, o Builder teria ganho pequeno e um construtor simples bastaria. A justificativa do padrão depende do aceite da revisão D1.

**Pendente:** escolha e justificativa do Factory Method (dupla Matheus + Pedro).

### Escolha e justificativa

**A definir.** Registrar o padrão escolhido, alternativas consideradas, justificativa apoiada na literatura e limites de aplicação.

### Modelagem (notação UML)

**Builder — concluído.** Diagrama de classes "antes" (recorte do v3 da Entrega 02) e "depois" (Builder aplicado), correspondência entre participantes GoF e classes do domínio, regras de validação e as doze evidências que as sustentam: [1.1.1.1. Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md). Fonte editável em PlantUML e exportações PNG/SVG ficam em [`assets/builder/`](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/builder-classes-depois-v1.puml). Autoria: Lucas Andrade Zanetti.

**Pendente.** Diagrama de sequência do Builder (Heitor); diagrama de classes e de sequência do Factory Method (Matheus e Pedro).

### Implementação (código)

**Pendente.** Acrescentar o link para o código versionado no repositório e explicar os trechos associados aos participantes do padrão. Linguagem e dependências serão informadas pela subequipe.

### Execução e vídeo do padrão em funcionamento

**Pendente.** Documentar pré-requisitos, comandos, cenário demonstrado e resultado esperado. Inserir o link para o vídeo mostrando o padrão em execução, com identificação dos participantes.

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
| 1.0 | 15/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Modelagem do Builder (diagrama antes/depois), ADR-001 e evidências; contexto, escolha e justificativa neste relatório | Pedro Druck Montalvão Reis (ADR-001) e Matheus Lemes Amaral (diagrama), conforme pares de revisão do planejamento | PR da branch `docs/subequipe-01-modelagem-builder` |
| A preencher | A preencher | A preencher | A preencher | A preencher | A preencher |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
