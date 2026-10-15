# ADR-001 — Builder para `StreamConfig`

| Campo | Valor |
| --- | --- |
| Status | Proposta (aguarda revisão de Heitor Macedo Ricardo, conforme o [planejamento](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md#fontes-do-planejamento)) |
| Data | 15/10/2026 |
| Autor | Lucas Andrade Zanetti |
| Revisor | A preencher (Heitor Macedo Ricardo) |
| Escopo | Modelagem (diagrama de classes e regras). Implementação e testes ficam no [repositório de código](https://github.com/Bappoz/g6-streaming-entrega03-subgrupo01-codigo). |

> Este ADR registra o **processo de decisão**, na ordem em que o raciocínio aconteceu. Cada afirmação factual aponta para uma evidência (`E01`–`E12`) arquivada em [`assets/builder/evidencias/`](/Base/Relatórios/1.1.1.SubEquipe_01/1.1.1.1.ModelagemBuilder.md#evidencias). O que **não** tem evidência está marcado como *decisão de projeto*.

## 1. Contexto

O `LiveStreamService.createStream(userId, config: StreamConfig)` da Entrega 02 recebe a configuração da transmissão ([E02](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e02-v3-streamconfig-quatro-atributos.png), [E04](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e04-e02-livestreamservice-recebe-streamconfig.png), [E07](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e07-e02-sequencia-createstream.png)). No diagrama v3, `StreamConfig` é um `«value object»` com **quatro** atributos: `title`, `visibility`, `latencyMode` e `recordAutomatically`.

O planejamento da SubEquipe_01 ([E01](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e01-planejamento-premissa-streamconfig.png)) afirma que a configuração tem "muitos parâmetros, vários opcionais e interdependentes (resolução, fps, bitrate, latência, gravação, visibilidade)". **Conferindo contra o modelo, essa afirmação está só parcialmente sustentada**:

| Parâmetro citado no planejamento | Está em `StreamConfig` v3? | Onde existe no modelo |
| --- | --- | --- |
| visibilidade, latência, gravação, título | Sim ([E02](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e02-v3-streamconfig-quatro-atributos.png)) | `StreamConfig` |
| resolução, fps, bitrate | **Não** | `QualityVariant` ([E03](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e03-v3-enumeracoes-e-qualityvariant.png), DE08 em [E05](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e05-e02-decisoes-de01-de03-de08.png)) |

Além disso, a Entrega 02 diz que preset, resolução, fps e bitrate são responsabilidade do **encoder do cliente**, fora do `MediaProcessingService` ([E06](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e06-e02-encoder-parametros-do-cliente.png)), e que a sequência de início da transmissão envia `StreamConfig` na mensagem 1 e configura o encoder na mensagem 11 ([E07](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e07-e02-sequencia-createstream.png)).

Com 4 atributos, quase todos enumerações ou booleanos, um construtor simples bastaria. O problema só passa a justificar um Builder se o modelo **incorporar os parâmetros de vídeo ao `StreamConfig`** e se houver regras de interdependência reais. Isto é uma **revisão do modelo da Entrega 02**, declarada abaixo (D1).

## 2. Evidências das interdependências

Para não inventar regras, buscou-se documentação pública que mostrasse dependências reais entre esses parâmetros:

| Regra | Fonte | Evidência |
| --- | --- | --- |
| Latência baixa/ultra-baixa não suporta 4K; latência normal suporta todas as resoluções | documentação de uma plataforma de transmissão ao vivo (ajuda do criador) | [E08](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e08-latencia-baixa-incompativel-com-4k.png) |
| Em 4K a otimização para baixa latência não está disponível; tudo vai para latência normal | mesma plataforma, página de configurações do encoder | [E09](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e09-4k-forca-latencia-normal.png) |
| Faixa de bitrate recomendada depende de codec, resolução **e** taxa de quadros | mesma página | [E10](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e10-bitrate-depende-de-codec-resolucao-fps.png) |
| Taxa de quadros: até 60 fps | mesma página | [E11](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e11-taxa-de-quadros-ate-60-e-codecs.png) |
| Resolução maior exige bitrate maior (1080p60 → 6000 kbps; 1080p30 → 4500 kbps; 720p30 → 3000 kbps) | plataforma de referência da Entrega 02 | [E12](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e12-plataforma-a-bitrate-por-resolucao.png) |

**Limite declarado.** E08–E11 vêm de uma plataforma que **não** é a de referência da Entrega 02; E12 vem da de referência. A convergência entre as duas é o que sustenta tratar "bitrate depende de resolução × fps" como regra de domínio e não de um fornecedor. Os **valores numéricos** são de referência e não são normativos para o nosso sistema.

## 3. Alternativas consideradas

| # | Alternativa | A favor | Contra |
| --- | --- | --- | --- |
| A | Construtor único com 7 parâmetros | Zero classes novas | Ordem de argumentos ilegível; opcionais viram `undefined`; aceita combinação inválida |
| B | Literal de objeto com campos opcionais | Idiomático em TypeScript; sem boilerplate | Nenhum ponto único de validação; objeto mutável escapa; com `exactOptionalPropertyTypes` o "ausente" ≠ `undefined` vira armadilha |
| C | Funções estáticas (`StreamConfig.lowLatency(...)`) | Nomeadas, curtas | Explosão de variações; não resolve montagem parcial passo a passo |
| **D** | **Builder fluente + `build()` validando e devolvendo objeto imutável** | **Validação centralizada; produto imutável; legível; separa construção de representação** | **Mais classes; custo por instância (medido no benchmark, não presumido)** |
| E | Builder sem Director | Menos classes | Presets repetidos em cada cliente; o planejamento já atribui o Director ao Heitor |

## 4. Decisão

Adotar **D**: Builder para `StreamConfig`, validação em `build()`, Director fora do escopo desta modelagem (Heitor).

| Participante GoF | Classe | Responsável |
| --- | --- | --- |
| Product | `StreamConfig` (imutável, construtor privado) | Lucas |
| Builder | interface `StreamConfigBuilder` | Lucas |
| ConcreteBuilder | `DefaultStreamConfigBuilder` | Lucas |
| Director | `StreamConfigDirector` | Heitor (contrato apenas) |
| Client | `LiveStreamService` / `demo.ts` | — |

### Decisões de projeto derivadas

| # | Decisão | Motivo | Impacto na Entrega 02 |
| --- | --- | --- | --- |
| D1 | `StreamConfig` ganha `resolution`, `framesPerSecond` e `bitrateBps` | Sem eles não há interdependência a validar (seção 1) | **Altera o diagrama v3.** `QualityVariant` permanece como vocabulário (DE08), mas deixa de ser a única casa desses valores |
| D2 | `Resolution` passa a ser enumeração (`R360P`…`R2160P`) em vez de `string` | `QualityVariant.resolution` é `string` no v3 ([E03](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e03-v3-enumeracoes-e-qualityvariant.png)); regra R4 compara com 2160p e `string` não impede `"4k"`, `"2160"`, `"3840x2160"` | Sugere trocar o tipo em `QualityVariant` num próximo ciclo; **não** feito aqui |
| D3 | Padrão `recordAutomatically = true` | A nota "Regras do fluxo de clipes" do v3 (regra 2) rejeita clipe sem gravação habilitada; padrão `false` tornaria clipagem inviável por omissão. Fonte: `foco01-classes-modelo-estatico-v3.drawio`, nota `y-9E5nLQ_uyiijW86kDa-213` — **sem print**, pois é texto do `.drawio` | Nenhum |
| D4 | Validar tudo em `build()`, não em cada `with*()` | Regras R2–R5 envolvem pares de campos; validar por campo não as enxerga | — |
| D5 | `build()` acumula **todas** as violações em `InvalidStreamConfigError.violations` | Quem monta uma configuração quer ver todos os erros de uma vez | — |
| D6 | `reset()` na interface | Permite reutilizar o builder pelo Director sem alocar outro | Efeito medido no benchmark |
| D7 | `title` sem valor padrão | Obrigatório; inventar título geraria dado falso | — |

### Regras de validação

| Id | Regra | Base |
| --- | --- | --- |
| R1 | `title` não vazio | D7 |
| R2 | `resolution`, `framesPerSecond` e `bitrateBps` informados **juntos** (nenhum ou todos) | [E10](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e10-bitrate-depende-de-codec-resolucao-fps.png) |
| R3 | `framesPerSecond` ≤ 60 | [E11](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e11-taxa-de-quadros-ate-60-e-codecs.png) |
| R4 | `latencyMode ∈ {LOW, ULTRA_LOW}` incompatível com `R2160P` | [E08](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e08-latencia-baixa-incompativel-com-4k.png), [E09](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e09-4k-forca-latencia-normal.png) |
| R5 | `bitrateBps` ≥ mínimo da faixa (resolução × fps) | [E10](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e10-bitrate-depende-de-codec-resolucao-fps.png), [E12](/Base/Relatórios/1.1.1.SubEquipe_01/assets/builder/evidencias/b-e12-plataforma-a-bitrate-por-resolucao.png) |

Mínimos usados em R5 (coluna "mínimo, H.264" de E10, Mbps): 2160p60 = 14 · 2160p30 = 11 · 1440p60 = 8 · 1440p30 = 7 · 1080p60 = 6 · 1080p30 = 5 · 720p60 = 3 · 720p30 = 3 · 480p = 0,4 · 360p = 0,4. Para fps entre 31 e 60 usa-se a linha "60"; até 30, a linha "30". **Configuráveis**, não normativos.

## 5. Consequências

**Fica mais fácil:** testar regras de combinação em um só ponto; passar `StreamConfig` adiante sabendo que é válido e imutável; adicionar um preset sem tocar o serviço.

**Fica mais difícil / custo:** o modelo cresce em 5 tipos (interface, builder, director, erro, enumeração); o diagrama v3 deixa de ser a fonte única de `StreamConfig`; mais código para um objeto de 7 campos.

**Riscos e limites declarados**

- O ganho do padrão com 4 atributos seria pequeno; ele aparece de fato com D1. Se o grupo preferir **não** alterar o v3, a alternativa honesta é B ou A (seção 3) e o Builder perde justificativa.
- R4 e R5 vêm de documentação de plataformas externas; não há garantia de que valem para o sistema modelado.
- O custo em tempo e memória do Builder frente ao construtor direto é **hipótese** até o benchmark rodar; este ADR não afirma número.

## 6. Referências

- GAMMA, E.; HELM, R.; JOHNSON, R.; VLISSIDES, J. *Padrões de Projeto: soluções reutilizáveis de software orientado a objetos*. Porto Alegre: Bookman, 2000 — Builder, capítulo de padrões de criação. **Páginas a confirmar** pelo autor no exemplar consultado; não foram verificadas neste registro.
- Entrega 02, SubEquipe_01: [Modelagem Estática](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.1.Foco01.ModelagemEstatica) e [Evidências da Modelagem Dinâmica](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Base/Relat%C3%B3rios/1.1.1.SubEquipe_01/1.1.1.2.1.Foco02.Evidencias).
- Planejamento da SubEquipe_01, v1.0, 08/10/2026 (seções 2, 3 e 6).
