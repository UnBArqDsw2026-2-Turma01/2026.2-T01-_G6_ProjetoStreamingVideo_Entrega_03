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

**Factory Method — `UserContent`.** Na Entrega 02, `LiveStream`, `RecordedVideo` e `Clip` herdam de `UserContent` (decisão DE03) e nascem em três pontos diferentes do fluxo `LiveStream → RecordedVideo → ClipRequest → Clip`: `LiveStreamService.createStream`, `MediaProcessingService.persistRecording` e a extração do clipe coordenada por `ClipService`. O v3 oferece os elementos de um caminho comum de registro — `ContentRepository.save(content: UserContent)`, `PolicyService.moderate(contentId)` e a regra 8 da nota "Regras do fluxo de clipes", segundo a qual publicar exige moderação aprovada e mídia pronta para qualquer conteúdo —, mas não desenha esse fluxo. Aplicada a regra 8 aos três tipos, o caminho ficaria repetido em cada serviço, e o código que registra conteúdo precisaria conhecer a classe concreta criada.

Ao contrário do Builder, o padrão não exige revisar atributos do v3: os três pontos de criação e a hierarquia aparecem no diagrama e nas evidências FM-E01 a FM-E03; o caminho comum é proposta desta entrega ([ADR-002 §1](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_1-contexto)).

### Escolha e justificativa

**Builder** (padrão criacional GoF) para `StreamConfig`: a construção é feita passo a passo por uma interface fluente, todas as regras de combinação são verificadas em um único `build()`, e o produto devolvido é imutável. Isso separa a montagem da representação final e permite que um `StreamConfigDirector` ofereça presets (baixa latência, alta qualidade, móvel) sem duplicar validação em cada cliente.

Alternativas consideradas e descartadas, com o argumento de cada uma — construtor de sete parâmetros, literal de objeto com campos opcionais, funções estáticas nomeadas e Builder sem Director — estão em [ADR-001 §3](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md#3-alternativas-consideradas), junto das sete decisões de projeto derivadas (D1–D7) e das cinco regras de validação (R1–R5).

**Limite declarado:** com os quatro atributos do v3, o Builder teria ganho pequeno e um construtor simples bastaria. A justificativa do padrão depende do aceite da revisão D1.

**Factory Method** (padrão criacional GoF) para a hierarquia `UserContent`: o Creator abstrato `UserContentCreator` escreve uma vez a operação comum (`submit`: criar, persistir, moderar, publicar quando possível) e delega ao **método-fábrica** `createContent` de cada subclasse — `LiveStreamCreator`, `RecordedVideoCreator`, `ClipCreator` — a decisão de qual classe instanciar e de onde vêm os dados. É a intenção do padrão no GoF: deixar as subclasses decidirem qual classe instanciar. O `LiveStreamCreator` recebe o `StreamConfig` montado pelo Builder, o que liga os dois padrões da subequipe.

Alternativas descartadas — `new` em cada serviço com o caminho repetido (como no v3), fábrica simples com `switch` sobre o tipo, composição com uma função de criação, Abstract Factory e Builder — estão em [ADR-002 §3](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_3-alternativas-consideradas), junto das nove decisões derivadas (DF1–DF9) e das regras F1–F6. F2 a F6 vêm da nota do v3 (F2 também da máquina M4); F1 e alguns refinamentos de F3 são decisões de projeto.

**Limites declarados:** a entrada do método-fábrica é tipada por genéricos (adaptação, não a variante parametrizada do GoF); cada produto novo custa também um criador novo (hierarquias paralelas); e o pedido de clipe feito antes de a gravação ficar pronta é recusado, e não enfileirado como no v3, porque a fila é responsabilidade do `ClipService`.

### Modelagem (notação UML)

**Builder — concluído.** Diagrama de classes "antes" (recorte do v3 da Entrega 02) e "depois" (Builder aplicado), correspondência entre participantes GoF e classes do domínio, regras de validação e as doze evidências que as sustentam: [1.1.1.1. Modelagem — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md). Fonte editável em PlantUML e exportações PNG/SVG ficam em [`assets/builder/`](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/builder-classes-depois-v1.puml). Autoria: Lucas Andrade Zanetti.

**Builder — sequência concluída.** Diagrama de sequência do preset montado pelo `StreamConfigDirector` (Client → Director → Builder → `build()`), com o caminho de erro de validação e a correspondência mensagem a mensagem com o código: [1.1.1.2. Sequência — Builder](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.2.SequenciaBuilder.md). Fonte editável em [`builder-sequencia-v1.puml`](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/builder-sequencia-v1.puml). Autoria: Heitor Macedo Ricardo.

**Factory Method — concluído.** Diagrama de classes desenhado a partir do código, recorte "antes" do componente UGC do v3, correspondência entre participantes GoF, serviços do v3 e classes, regras F1–F6 e evidências: [1.1.1.3. Modelagem — Factory Method](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.3.ModelagemFactoryMethod.md). Diagrama de sequência de `ClipCreator.submit`, separando o método-fábrica da operação comum, com os caminhos de erro: [1.1.1.4. Sequência — Factory Method](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.4.SequenciaFactoryMethod.md). Fontes em PlantUML e exportações PNG/SVG ficam em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/factory-method-classes-v1.puml" target="_blank" rel="noopener"><code>assets/factory-method/</code></a>. Autoria: Matheus Lemes Amaral.

### Implementação (código)

**Factory Method.** Código em [`src/criacionais/factory-method/`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method) do repositório de código (TypeScript, sem dependência de execução; [PR #2 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/2), aguardando revisão; os links apontam para o commit `a7ae60e` da branch do PR). Um arquivo por participante:

| Participante | Arquivo | Trecho que realiza o padrão |
| --- | --- | --- |
| Product | `user-content.ts` | classe abstrata `UserContent`; `publish()` aplica F6 com o gancho abstrato `isMediaReady()` |
| ConcreteProduct | `live-stream.ts`, `recorded-video.ts`, `clip.ts` | cada um implementa `isMediaReady()`; `RecordedVideo` e `Clip` recebem a origem e verificam F2–F5 |
| Creator | `user-content-creator.ts` | `submit()` chama `this.createContent(input)` e segue só com `UserContent`; `createContent` é `protected abstract` |
| ConcreteCreator | `live-stream-creator.ts`, `recorded-video-creator.ts`, `clip-creator.ts` | sobrescrevem `createContent` com o `new` da classe concreta e a busca da origem no repositório |
| Client | `demo.ts` | `registrar(creator, input)` aceita qualquer `UserContentCreator` |

O README do padrão, no repositório de código, explica as decisões de estrutura e os limites. São 78 testes do Factory Method (131 no total), com 100% de cobertura de linhas, ramos e funções no código instrumentado (demos e benchmark ficam fora da medição).

**Builder — pendente.** Acrescentar o link para o código versionado no repositório e explicar os trechos associados aos participantes do padrão.

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

> Enquanto o [PR #1](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/1) não for integrado à `main`, rode `git checkout feat/builder-stream-config` antes do `npm ci`.

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

`npm run check` deve terminar sem erro; em 15/10/2026 eram 53 testes do Builder passando, com 100% de cobertura de linhas, ramos e funções (`npm run coverage`).

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

**Pendente.** Vídeo do Builder em funcionamento.

## Rastreabilidade & Elos com Outros Artefatos

A [modelagem da SubEquipe_01 na Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.SubEquipe_01) é um ponto de partida. A equipe deverá indicar quais artefatos e elementos sustentam efetivamente sua decisão nesta etapa.

| Problema ou requisito | Artefato de origem (link) | Elemento do modelo | Trecho de código (link) | Evidência de execução (link) |
| --- | --- | --- | --- | --- |
| Factory Method: conteúdo nasce em três serviços e passa pelo mesmo caminho de registro | [Modelagem Estática da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) (FM-E02) | `UserContentCreator.submit` / `createContent` | [`user-content-creator.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/user-content-creator.ts) | Demo, partes 1–3 |
| Hierarquia `UserContent` (DE03) | [Conteúdo Gerado pelo Usuário](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.2.Foco01.ConteudoGeradoUsuario) (FM-E01) | Product e ConcreteProducts | [`user-content.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/user-content.ts), [`clip.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/clip.ts) | Demo, linha `classe:` de cada conteúdo |
| Regra 8: publicar exige `APPROVED` e mídia pronta (F6) | Nota "Regras do fluxo de clipes" do v3 (FM-E03) | `UserContent.publish`, `isMediaReady` | [`user-content.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/user-content.ts) | Demo, partes 1 e 2 e clipe `REJECTED` da parte 4 |
| Regras 1, 2, 4 e 7: origem e janela do recorte, dono preservado (F2, F4, F5) | Nota do v3 (FM-E03) | Construtores de `RecordedVideo` e `Clip` | [`clip.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/clip.ts), [`recorded-video.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/recorded-video.ts) | Demo, partes 3 e 4 |
| `createStream(userId, config: StreamConfig)` liga Builder e Factory Method | [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md) e diagrama v3 | `LiveStreamCreator` | [`live-stream-creator.ts`](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/blob/a7ae60ee0fb2299897e1ecde88086f3bdbc8c75a/src/criacionais/factory-method/live-stream-creator.ts) | Demo, parte 1 |
| Builder: a preencher | A preencher | A preencher | A preencher | A preencher |

## Senso Crítico

**A preencher.** Avaliar benefícios, custos e limitações do padrão, coerência entre UML e implementação e decisões revistas ao longo do trabalho. Relacionar a avaliação às evidências e à literatura consultada.

**Factory Method.** O ganho é concreto e localizado: a regra 8 do v3 passou a existir em um só lugar (`submit` + `publish`), e um tipo novo de conteúdo entra como subclasse, sem tocar no Creator. O custo é a hierarquia de criadores paralela à de produtos — três classes a mais para três produtos — e um método que faz dois papéis (Template Method sobre o método-fábrica). Decisões revistas durante o trabalho: as regras saíram do criador e foram para o construtor dos produtos (DF4), para que nem um `new` fora do padrão crie conteúdo inválido; o pedido de clipe sem gravação pronta passou a ser recusado, e não enfileirado (DF8), uma simplificação declarada do fluxo assíncrono do v3; e uma revisão independente do código levou a despublicar a live ao encerrar, exigir live encerrada e gravação única em F2 (DF9), validar a data de F3 e copiar as datas dos produtos. O diagrama de classes foi desenhado depois do código e conferido contra ele; a ordem das mensagens do diagrama de sequência é verificada por teste. Detalhes em [ADR-002 §5](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-002-factory-method-user-content.md?id=_5-consequências).

## Referências

**A preencher com fontes efetivamente consultadas.** Identificar autor, título, edição ou versão, ano e link quando disponível; relacionar as referências às decisões e artefatos que fundamentam.

- GAMMA, E.; HELM, R.; JOHNSON, R.; VLISSIDES, J. *Padrões de Projeto: soluções reutilizáveis de software orientado a objetos*. Porto Alegre: Bookman, 2000 — Factory Method (intenção, aplicabilidade, consequências e métodos-fábrica parametrizados): fundamenta a escolha e as decisões DF1 e DF2 do ADR-002. Páginas a confirmar no exemplar consultado.
- Entrega 02, SubEquipe_01 — [Conteúdo Gerado pelo Usuário e Clipagem](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.2.Foco01.ConteudoGeradoUsuario) e [Modelagem Estática](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica): origem do problema do Factory Method e das regras F2–F6.

## Versionamentos & Participações

Registrar apenas alterações efetivamente realizadas, incluindo autoria, revisão e links para commits ou pull requests.

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| --- | --- | --- | --- | --- | --- |
| 1.0 | 15/10/2026 | [Lucas Andrade Zanetti](https://github.com/Bappoz) | Modelagem do Builder (diagrama antes/depois), ADR-001 e evidências; contexto, escolha e justificativa neste relatório | Pedro Druck Montalvão Reis (ADR-001) e Matheus Lemes Amaral (diagrama), conforme pares de revisão do planejamento | PR da branch `docs/subequipe-01-modelagem-builder` |
| 1.1 | 15/10/2026 | [Heitor Macedo Ricardo](https://github.com/HeitorM50) | Diagrama de sequência do Builder (PlantUML) e presets do Director; seção Execução deste relatório | A preencher (Pedro Druck Montalvão Reis, sequência) | PR da branch `docs/subequipe-01-modelagem-builder` |
| 1.2 | 16/10/2026 | [Matheus Lemes Amaral](https://github.com/1emes) | Factory Method: diagramas de classes e de sequência (PlantUML), ADR-002, evidências FM-E01 a FM-E03; contexto, escolha e justificativa, modelagem, implementação, execução, rastreabilidade e senso crítico do padrão neste relatório; implementação, testes, demo e cenário de benchmark no repositório de código | A preencher | PR da branch `docs/subequipe-01-factory-method` · [PR #2 do código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo/pull/2) |
| A preencher | A preencher | A preencher | A preencher | A preencher | A preencher |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md).
