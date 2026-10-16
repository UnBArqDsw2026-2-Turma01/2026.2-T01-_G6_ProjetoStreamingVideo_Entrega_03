# ADR-002 — Factory Method para a hierarquia `UserContent`

| Campo | Valor |
| --- | --- |
| Status | Proposta (aguarda revisão de um integrante da outra dupla, conforme o `CONTRIBUTING.md` do repositório de código) |
| Data | 16/10/2026 |
| Autor | Matheus Lemes Amaral |
| Revisor | A preencher |
| Escopo | Modelagem (diagramas de classes e de sequência) e decisões do padrão. Implementação e testes ficam no [repositório de código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo), pasta `src/criacionais/factory-method/`. |

> Como o [ADR-001](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md), este registro segue a ordem do raciocínio. Cada afirmação sobre o modelo da Entrega 02 aponta para uma evidência (`FM-E01`–`FM-E03`) arquivada em <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/evidencias/fm-e01-v3-recorte-conteudo-ugc.png" target="_blank" rel="noopener"><code>assets/factory-method/evidencias/</code></a>; o que não tem evidência está marcado como *decisão de projeto*.

## 1. Contexto

O planejamento da SubEquipe_01 v1.0 (08/10/2026, seção 2) aponta o segundo problema de criação do modelo: `UserContent` (abstrata) e suas subclasses `LiveStream`, `RecordedVideo` e `Clip` — decisão DE03 — são "três tipos de conteúdo com identidade, título, visibilidade e autoria comuns, criados em pontos diferentes da cadeia `LiveStream → RecordedVideo → ClipRequest → Clip`", e "o código que publica conteúdo não deveria conhecer a classe concreta que está criando" (<a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e01-planejamento-premissa-streamconfig.png" target="_blank" rel="noopener">E01 do ADR-001</a>, segunda linha da tabela).

**Conferindo contra o modelo, a afirmação se sustenta em parte:**

| Afirmação do planejamento | O que o diagrama v3 mostra | Evidência |
| --- | --- | --- |
| Os três herdam de `UserContent` e compartilham identidade, título, visibilidade e autoria | `UserContent` concentra `id`, `ownerId`, `title`, `visibility`, `publicationStatus`, `moderationStatus` e `createdAt`, além de `publish()`, `unpublish()`, `applyModeration()` e `isPublished()` | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/evidencias/fm-e01-v3-recorte-conteudo-ugc.png" target="_blank" rel="noopener">FM-E01</a> |
| Os três nascem em pontos diferentes | `LiveStreamService.createStream(...): LiveStream`; `MediaProcessingService.persistRecording(streamId): RecordedVideo`; `MediaProcessingService.extractClip(...): Clip`, coordenado por `ClipService` | <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/evidencias/fm-e02-v3-servicos-que-criam-conteudo.png" target="_blank" rel="noopener">FM-E02</a> |
| Depois de criados, podem passar pelo mesmo caminho | O v3 **não** desenha um fluxo único de registro. Ele oferece os elementos: `ContentRepository.save(content: UserContent)` aceita qualquer conteúdo; `PolicyService` aparece em `LiveStreamService` e `ClipService`, mas não em `MediaProcessingService`; e a regra 8 da nota vale para qualquer conteúdo: "publish exige moderação APPROVED e mídia pronta". O caminho comum é **proposta desta entrega**, apoiada nesses elementos | FM-E02, <a href="Base/Relatórios/1.1.1.SubEquipe_01/assets/factory-method/evidencias/fm-e03-v3-regras-do-fluxo-de-clipes.png" target="_blank" rel="noopener">FM-E03</a> |

O problema, portanto, não é montar um objeto complicado — os produtos têm poucos campos —, e sim **onde fica o caminho comum de registro** e **quem decide qual classe instanciar**. No v3, cada um dos três serviços cria a sua subclasse; ao aplicar a regra 8 a todos eles, cada serviço teria de repetir o mesmo trecho: persistir, pedir moderação pelo id, registrar o veredito e publicar só se a moderação aprovou e a mídia está pronta.

Diferente do ADR-001, este padrão **não exige revisão dos atributos do diagrama v3** para se justificar: os três pontos de criação e a hierarquia já estão no modelo da Entrega 02. O que esta entrega acrescenta é a decisão de dar a todo conteúdo o mesmo caminho de registro (DF2).

## 2. Regras de domínio envolvidas

As regras não foram inventadas para o padrão: vêm da nota "Regras do fluxo de clipes" (FM-E03), introduzida na revisão v2 do diagrama de classes da Entrega 02 (UGC e clipagem, Matheus Lemes Amaral e Pedro Druck Montalvão Reis) e mantida no v3. O prefixo `F` evita confusão com `R1`–`R5` do Builder.

| Id | Regra | Origem | Onde é verificada |
| --- | --- | --- | --- |
| F1 | Título não vazio | *Decisão de projeto*, simétrica à R1 do ADR-001 | construtor de `UserContent` |
| F2 | Gravação só nasce de transmissão existente, encerrada (`ENDED`) e com gravação automática habilitada | Regra 2 da nota (FM-E03); encerramento pela máquina M4 da Entrega 02 | `RecordedVideoCreator` (existência) e construtor de `RecordedVideo` |
| F3 | `READY` exige duração, `storageUri` e `availableAt` | Regra 9 da nota (FM-E03), **sem** o manifesto, que não é representado; duração positiva e data válida são *refinamentos de projeto* | `RecordedVideo.markReady` |
| F4 | Clipe só nasce de gravação `READY` da transmissão | Regra 1 da nota (FM-E03) | `ClipCreator` (existência) e construtor de `Clip` |
| F5 | `0 ≤ início < fim ≤ duração da gravação` | Regra 4 da nota (FM-E03) | construtor de `Clip` |
| F6 | Publicar exige moderação `APPROVED` e mídia pronta | Regra 8 da nota (FM-E03) | `UserContent.publish` |

A regra 7 da nota ("preservar o proprietário da origem"; no clipe, `createdByUserId` é quem pediu o corte) não ganhou id: ela não é verificada, é **garantida pela construção** (decisão DF3). A regra 5 (`/durationSeconds` derivado) vira propriedade calculada de `Clip`.

## 3. Alternativas consideradas

| # | Alternativa | A favor | Contra |
| --- | --- | --- | --- |
| A | `new` direto em cada serviço, caminho comum repetido (como está no v3) | Nenhuma classe nova | O trecho persistir → moderar → publicar fica copiado três vezes; uma mudança na regra 8 exige editar três serviços e lembrar dos três |
| B | Fábrica simples: uma função com `switch` sobre o tipo de conteúdo | Um só ponto de criação; com sobrecargas, o retorno pode manter o tipo concreto | Não é padrão GoF; a função conhece as três classes concretas e é editada a cada tipo novo; a entrada vira uma união de três formatos |
| C | Abstract Factory | Cria famílias de objetos relacionados | Não há família: cada ponto do fluxo cria **um** produto. Seria uma interface com três métodos em que cada fábrica concreta só implementaria um |
| D | Builder (como no ADR-001) | Já conhecido pela subequipe | Resolve montagem passo a passo de um objeto com muitos campos interdependentes; aqui o objeto é simples e a variação é *qual classe* criar |
| **E** | **Factory Method: Creator com a operação comum e um método-fábrica por subclasse** | **Caminho comum escrito uma vez, só com `UserContent`; cada ConcreteCreator decide a classe e de onde vêm os dados; tipo novo entra como subclasse, sem editar o Creator** | **Uma hierarquia de criadores paralela à de produtos (três classes a mais); o método-fábrica precisa de entrada diferente por tipo** |
| F | Composição: uma função comum `registrar(criar, entrada)` que recebe a função de criação como parâmetro | Menos classes; mesma separação entre o caminho comum e a criação | Equivale ao padrão sem a hierarquia: perde o lugar nomeado para cada criador (com o repositório que ele consulta para achar a origem) e o vocabulário GoF que a disciplina pede para modelar em UML; seria a escolha natural num código sem esse objetivo didático |

## 4. Decisão

Adotar **E**: Factory Method para a hierarquia `UserContent`.

| Participante GoF | Classe | Arquivo no código |
| --- | --- | --- |
| Product | `UserContent` (abstrata) | `user-content.ts` |
| ConcreteProduct | `LiveStream`, `RecordedVideo`, `Clip` | `live-stream.ts`, `recorded-video.ts`, `clip.ts` |
| Creator | `UserContentCreator<TInput, TContent>` — `submit` (operação) e `createContent` (método-fábrica) | `user-content-creator.ts` |
| ConcreteCreator | `LiveStreamCreator`, `RecordedVideoCreator`, `ClipCreator` | `live-stream-creator.ts`, `recorded-video-creator.ts`, `clip-creator.ts` |
| Client | função `registrar` da demonstração (no sistema, os serviços do v3) | `demo.ts` |

Cada ConcreteCreator ocupa o lugar de um ponto de criação do v3:

| ConcreteCreator | No lugar de | Entrada | Produto nasce em |
| --- | --- | --- | --- |
| `LiveStreamCreator` | `LiveStreamService.createStream(userId, config)` | dono, canal e `StreamConfig` (produto do Builder, ADR-001) | `CREATED` |
| `RecordedVideoCreator` | `MediaProcessingService.persistRecording(streamId)` | id da transmissão | `PROCESSING` |
| `ClipCreator` | extração coordenada por `ClipService` / `MediaProcessingService.extractClip` | `ClipRequestInput` do v3 | pronto |

### Decisões de projeto derivadas

| # | Decisão | Motivo | Impacto na Entrega 02 |
| --- | --- | --- | --- |
| DF1 | O Creator é genérico na entrada (`TInput`) | Cada tipo precisa de dados diferentes (uma `StreamConfig`, o id de uma transmissão, um pedido de recorte). É uma **adaptação tipada**, não a variante de métodos-fábrica parametrizados do GoF, em que o parâmetro identifica o produto: aqui o parâmetro só carrega dados e quem decide a classe é a subclasse. Consequência: os criadores não são intercambiáveis entre si; o comum é `submit` e o retorno `UserContent` | Nenhum |
| DF2 | `submit` = `createContent` → `save` → `moderate(id)` → `applyModeration` → `publish` se `APPROVED` e mídia pronta → `save` | `PolicyService.moderate` recebe o **id** no v3, então o conteúdo precisa estar persistido antes da moderação | Nenhum; usa as interfaces do v3 como estão |
| DF3 | `RecordedVideo` e `Clip` recebem a **origem inteira** (a live, a gravação), e não `ownerId` | Garante a regra 7 por construção: o dono vem da origem, sem chance de o chamador passar outro | Os atributos do v3 continuam os mesmos (`sourceStreamId`, `sourceVideoId`, `ownerId`); muda só a forma de criar |
| DF4 | As regras moram no **produto**; o criador só localiza a origem | Um `new Clip(...)` escrito fora do padrão também não consegue criar clipe inválido; o método-fábrica fica com uma responsabilidade só | — |
| DF5 | Conteúdo cuja mídia ainda não está pronta é registrado e **não** publicado, sem erro | Uma live em `CREATED` e uma gravação em `PROCESSING` são estados normais do fluxo, não falhas; publicar é um passo posterior | Torna explícito o gancho `isMediaReady()` em `UserContent`, que no v3 aparecia só como texto da regra 8 |
| DF6 | `ContentVisibility` e `LatencyMode` reaproveitados do Builder, sem duplicar | Duas enumerações iguais seriam tipos incompatíveis em TypeScript; a `StreamConfig` do Builder não alimentaria a `LiveStream` | — |
| DF7 | Clipe herda a visibilidade da gravação | *Decisão de projeto*: um clipe de gravação privada não pode nascer público | O v3 não definia a visibilidade do clipe |
| DF8 | Pedido de clipe sem gravação pronta é **recusado** com F4 | A espera em `WAITING_RECORDING` e o reprocessamento pelo evento `RecordingAvailable` (DE04, DE05) são do `ClipService`, fora do escopo de um padrão de criação | Limite declarado; o fluxo assíncrono do v3 continua válido |
| DF9 | Uma gravação por transmissão: o `RecordedVideoCreator` recusa a segunda | Com duas gravações da mesma live, `findRecordingByStream` poderia devolver a que falhou e o `ClipCreator` recusaria um recorte válido | O v3 sugere a unicidade (`RecordingHandle.expectedVideoId`), sem declará-la como regra |

## 5. Consequências

**Fica mais fácil:** mudar o caminho de registro (por exemplo, a regra de publicação) em um só lugar; acrescentar um tipo de conteúdo como uma subclasse nova de produto e de criador, sem editar o Creator nem os outros criadores; testar o caminho comum com um criador dublê, sem depender das três classes concretas.

**Fica mais difícil / custo:**

- Três classes de criador a mais, numa hierarquia paralela à de produtos. O GoF aponta essa consequência do padrão: para criar um produto concreto, é preciso criar também uma subclasse do Creator.
- A operação `submit` faz o papel de um Template Method sobre o método-fábrica (o GoF observa que métodos-fábrica costumam ser chamados de dentro de Template Methods). Quem lê o código precisa reconhecer os dois papéis no mesmo método.
- **Sem transação.** Pela ordem `save → moderate → save` (DF2), se a política ou o segundo `save` lançar erro, o erro sobe e o conteúdo fica registrado como `PENDING` e fora do ar. É um estado válido (conteúdo aguardando moderação) e pode ser moderado de novo pelo id, mas repetir o `submit` cria outro conteúdo.
- O custo da indireção (chamada ao método-fábrica e acesso aos colaboradores pelo Creator) é **hipótese** até o benchmark: o cenário `factory-method` compara `ClipCreator.submit` com os mesmos passos escritos em linha. Este ADR não afirma número.

**Riscos e limites declarados**

- O ganho depende de o caminho comum continuar comum. Se cada tipo passar a ter regras de publicação muito diferentes, a operação do Creator vira um conjunto de exceções e o padrão perde sentido.
- Os construtores dos produtos são públicos (TypeScript não tem visibilidade de pacote), como `StreamConfig.fromBuilder` no Builder. O padrão garante o caminho de `submit`; as regras F1–F6 valem nos dois caminhos porque moram no produto (DF4).
- `LiveStream` e `RecordedVideo` têm só as transições de estado que a demonstração usa; as máquinas completas estão no diagrama de estados da Entrega 02.

## 6. Referências

- GAMMA, E.; HELM, R.; JOHNSON, R.; VLISSIDES, J. *Padrões de Projeto: soluções reutilizáveis de software orientado a objetos*. Porto Alegre: Bookman, 2000 — Factory Method, capítulo de padrões de criação (intenção, aplicabilidade, consequências e a variação de métodos-fábrica parametrizados). **Páginas a confirmar** no exemplar consultado; não foram verificadas neste registro.
- Entrega 02, SubEquipe_01: [Conteúdo Gerado pelo Usuário e Clipagem](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.2.Foco01.ConteudoGeradoUsuario) (DE03, regras do fluxo de clipes) e [Modelagem Estática](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) (DE03–DE05, DE09).
- [ADR-001 — Builder para `StreamConfig`](/Base/Relatórios/1.1.1.SubEquipe_01/ADR/ADR-001-builder-stream-config.md): produto consumido pelo `LiveStreamCreator`.
- Planejamento da SubEquipe_01, v1.0, 08/10/2026 (seção 2).
