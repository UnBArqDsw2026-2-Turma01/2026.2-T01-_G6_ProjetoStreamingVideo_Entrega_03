# Reunião S2_01 — Planejamento da Entrega 3 · SubEquipe_02

> **Data**: 06/10/2026 · Primeira reunião da Entrega 3.
>
> **Tema da entrega**: Desenho de Software — Padrões de Projeto GoF + IA Generativa.
>
> **Atribuição da SubEquipe_02**: **Padrões Estruturais**.
>
> **Participantes previstos**: Davi Severiano Freitas, Daniel de Oliveira Lira, Mateus Rodrigues Barreto e Pedro Henrique Freire Rodrigues.
>
> **Status**: 🔵 Planejamento — documento de apoio, a ser consolidado em ata ao final da reunião.
>
---

## 1. Pauta

1. Ponto de partida: o que as Entregas 1 e 2 já nos entregam (§2)
2. Escolha dos padrões estruturais (§3)
3. Divisão de responsabilidades (§4)
4. Entrega mínima e definições técnicas (§5)
5. Iniciativas extras (§6)
6. Cronograma e marcos (§7)
7. Decisões a registrar em ata (§8)
8. Encaminhamentos: responsáveis e prazos

---

## 2. Ponto de partida: o que já temos

Esta entrega não começa do zero. A subequipe acumula, ao longo de duas entregas, uma base de requisitos não funcionais operacionalizados, achados empíricos e modelos consolidados.

A consequência prática: **não precisamos inventar um caso de uso para encaixar um padrão**. Vários padrões estruturais já estão latentes nos nossos modelos, e — mais importante — o NFR Framework já descreve, em linguagem de requisito, exatamente o que esses padrões resolvem.

### 2.1 Insumos da Entrega 1

| Insumo | O que ele nos entrega agora |
| -- | -- |
| **NFR Framework**, com 19 operacionalizações (O01–O19) sobre Confiabilidade e Disponibilidade | Critério objetivo de escolha: cada padrão deve operacionalizar um softgoal já documentado |
| **BPMN — Compra de moeda virtual** | Fluxo de checkout com processadores externos, origem do caso do Adapter |
| **BPMN — Chat ao vivo** | Fluxo de envio com decisão sobre bloqueio da mensagem, origem do caso do Decorator |
| **BPMN — Recuperação de falha de transmissão** | Tolerância a falhas, fora do escopo dos padrões escolhidos |
| **Artefato Generalista (Rich Picture)** | Visão de contexto: carteira virtual, gateway de pagamento e instituições externas |
| **Engenharia Reversa (regras RN01–RN09)** | Regras observadas no fluxo de monetização, úteis como justificativa adicional nos ADRs |

### 2.2 Insumos da Entrega 2

| Insumo | O que ele nos entrega agora |
| -- | -- |
| Interface `GatewayPagamento`, com `iniciarCheckout`, `solicitarTransferencia` e `validarWebhook` | Um *Target* pronto para múltiplos processadores externos |
| Nó "Processador de Pagamentos" no diagrama de implantação | Dois caminhos distintos já desenhados: chamada de API e retorno por webhook |
| `FaixaDestaque`, com cor, tempo de fixação e limite de caracteres | Comportamento que se acumula sobre uma mensagem de chat |
| `ServicoModeracao`, com `avaliarSpam`, `verificarPermissoes` e `aplicarRegras` | Cadeia de validações sobre a mesma mensagem |
| Achados SQ11, SQ12, SQ14, SC01, SC02 e SC06 | Lastro empírico para cada padrão candidato |
| Tabelas de decisões e refinamentos A01–A11 | Base quase pronta para ADRs: problema, alternativas e justificativa já escritos |
| Código TypeScript de referência (domínio, serviços, controllers) | Base de implementação coerente com os diagramas |

---

## 3. Padrões candidatos

A coluna de operacionalização liga cada padrão ao NFR Framework. É o que transforma a escolha em decisão de arquitetura, e não em exercício de livro.

| Padrão | Operacionalização atendida (Entrega 1) | Âncora no modelo (Entrega 2) | Esforço | Força |
| -- | -- | -- | -- | -- |
| **Adapter** | **O07** — fallback automático para gateways secundários: rotear a transação para um processador de backup quando o principal cai | `GatewayPagamento`; achados SQ11 e SQ12 (processadores com contratos, prazos e taxas distintos) | Médio | ⭐⭐⭐ |
| **Decorator** | **O05** — limitação de taxa; **O06** — degradação graciosa por feature flags | `ServicoModeracao` (validações encadeadas) ou `FaixaDestaque` (SC01, SC02) | Médio | ⭐⭐⭐ |
| **Proxy** | **O11** — chave de idempotência; **O14** — verificação de autenticidade do webhook; **O10** — cache de estado para elegibilidade | Confirmação de webhook nos fluxos de Recarga e Saque; acesso protegido ao repasse (SQ14) | Baixo | ⭐⭐⭐ |
| **Composite** | — | Thread de respostas sob a mensagem fixada (SC06) | Médio | ⭐⭐ |
| **Flyweight** | **O06** — eficiência de processamento sob estresse | Emotes e emblemas repetidos em milhares de mensagens | Alto | ⭐⭐ |
| **Facade** | — | `ServicoFinanceiro`, que já encapsula débito, crédito, commit e rollback | Muito baixo | ⭐ |

**Observação relevante**: o Proxy subiu de posição. As operacionalizações O11 e O14 descrevem literalmente um objeto que intercepta a requisição antes do serviço real — verificando duplicidade e autenticidade do webhook —, que é a definição do padrão. Como o esforço é baixo e já modelamos a idempotência nos diagramas de sequência, ele deixou de ser um extra condicional e virou candidato forte.

**Proposta para discussão**: implementar **Adapter** (Monetização) e **Decorator** (Chat), com **Proxy** como terceiro padrão se o cronograma permitir. Adapter e Proxy são complementares no mesmo módulo: um troca o processador, o outro protege a confirmação.

---

## 4. Proposta de divisão

| Dupla | Módulo | Padrão | Entregáveis sob sua responsabilidade |
| -- | -- | -- | -- |
| Davi Severiano Freitas e Mateus Rodrigues Barreto | Monetização | **Adapter** (+ Proxy, se houver folga) | Diagrama, implementação, mocks dos processadores, suíte de testes com cobertura, trecho do vídeo |
| Pedro Henrique Freire Rodrigues e Daniel de Oliveira Lira | Chat | **Decorator** | Diagrama, implementação, cenários de combinação, trecho do vídeo |
| Todos | — | — | Relato individual de IA Generativa; revisão cruzada entre duplas |

A revisão cruzada foi o que mais agregou nas entregas anteriores e deve ser mantida: cada dupla revisa o artefato da outra antes do commit final.

---

## 5. Entrega mínima (obrigatória para menção MM)

| # | Item | Observação para a nossa subequipe |
| -- | -- | -- |
| E1 | **Modelo** — diagrama do padrão escolhido | Mostrar o *antes* (modelo da Entrega 2) e o *depois* (com o padrão aplicado), evidenciando a evolução |
| E2 | **Código** — implementação real, com link direto e acessível | TypeScript, reaproveitando as classes já modeladas; pasta própria no repositório novo |
| E3 | **Execução** — vídeo curto com o código rodando | Um trecho por padrão, narrado por quem implementou |
| E4 | **IA Generativa** — relato individual, crítico e fundamentado | Um por membro; é o item que mais costuma ficar para o fim |

### Definições técnicas a fechar hoje

| Item | Proposta |
| -- | -- |
| Linguagem | TypeScript, por continuidade com o código de referência |
| Testes | Jest, com meta de cobertura a definir |
| Diagramação | Mesmas ferramentas das entregas anteriores (Miro para consolidação, PlantUML para versionar) |
| Estrutura de pastas | Uma pasta por padrão, com `src/` e `tests/` |
| Anonimização | Manter `<plataforma>`, "moeda virtual" e "mensagem paga destacada" desde o primeiro commit — inclusive em nomes de variáveis, arquivos e mensagens de commit |
| Referência teórica | Incluir no catálogo do novo repositório: GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; VLISSIDES, John. **Padrões de Projeto: soluções reutilizáveis de software orientado a objetos**. Porto Alegre: Bookman, 2000. |

---

## 6. Iniciativas extras viáveis

| Iniciativa | Esforço | Por que vale |
| -- | -- | -- |
| **Mocks de processadores externos + testes com cobertura** | Médio | É o extra sugerido no enunciado para padrões estruturais; a lógica do Adapter é determinística e fácil de testar |
| **Cenário de fallback entre processadores** | Baixo | Demonstra a O07 na prática: derrubar o processador principal no mock e ver a transação seguir pelo secundário, sem alterar o serviço |
| **ADRs (Architecture Decision Records)** | Baixo | O conteúdo já existe nas tabelas de refinamentos A01–A11 e nas operacionalizações do NFR |
| **Rastreabilidade tripla: padrão ↔ operacionalização do NFR ↔ achado de engenharia reversa** | Baixo | Diferencial exclusivo nosso: liga as três entregas e mostra que o padrão operacionaliza um requisito não funcional documentado |
| **Terceiro padrão (Proxy de idempotência e validação de webhook)** | Baixo | Atende O11 e O14; reaproveita regra já modelada nos fluxos de Recarga e Saque |
| **Benchmark do Flyweight em emotes** | Alto | Atende O06, mas exige medição confiável; só com cronograma folgado |

---

## 7. Marcos propostos

As datas devem ser preenchidas na reunião, a partir do prazo oficial da Entrega 3.

| # | Marco | Responsável | Prazo |
| -- | -- | -- | -- |
| M1 | Padrões e divisão confirmados; este documento vira ata | Todos | 06/10/2026 |
| M2 | Repositório novo estruturado e ambiente de testes pronto | Davi | |
| M3 | Diagramas dos padrões (antes/depois) | Cada dupla | |
| M4 | Implementação do Adapter, com mocks | Davi e Mateus | |
| M5 | Implementação do Decorator | Pedro e Daniel | |
| M6 | Suíte de testes e relatório de cobertura | Davi e Mateus | |
| M7 | ADRs e rastreabilidade tripla | Todos | |
| M8 | Implementação do Proxy (condicional) | Davi e Mateus | |
| M9 | Revisão cruzada entre as duplas | Todos | |
| M10 | Gravação e edição do vídeo | A definir | |
| M11 | Relatos individuais de IA Generativa | Cada membro | |
| M12 | Documento final publicado e conferido no GitPages | Todos | |

---

## 8. Decisões a registrar em ata

| # | Questão | Opções |
| -- | -- | -- |
| D01 | Quais padrões estruturais a subequipe implementa? | Adapter + Decorator · os dois + Proxy · apenas um |
| D02 | A divisão por módulo (Monetização e Chat) se mantém? | Sim |
| D03 | O Decorator do Chat incide sobre a cadeia de moderação (O05, O06) ou sobre a mensagem destacada (SC01, SC02)? | Moderação · mensagem |
| D04 | Linguagem da implementação | TypeScript · outra |
| D05 | Ferramenta de testes e meta de cobertura | Jest · outra; meta percentual |
| D06 | Entregamos ADRs como iniciativa extra? | Sim · não |
| D07 | A rastreabilidade liga os padrões às operacionalizações do NFR Framework? | Sim · apenas aos achados da Entrega 2 |
| D08 | Formato do vídeo | Único com os trechos · um por padrão |
| D09 | Extensão e formato do relato individual de IA | A definir |

---

## 9. Riscos identificados

| Risco | Mitigação |
| -- | -- |
| Relatos individuais de IA deixados para o último dia | Prazo próprio, uma semana antes da entrega, cobrado na revisão cruzada |
| Implementação desacoplada dos modelos anteriores, parecendo exercício isolado | Toda classe nova deve referenciar uma classe, um achado ou uma operacionalização já documentada |
| Quebra da anonimização no repositório novo | Regra valendo desde o primeiro commit; conferir também nomes de arquivos e de variáveis |
| Escopo inflado com padrões demais | Fixar dois padrões obrigatórios; o terceiro só com cronograma folgado |
| Vídeo gravado sem o código rodando de fato | Ensaiar a execução antes de gravar; mostrar terminal e saída real |
| Texto prometendo correções que não serão feitas | Registrar limitações como definitivas no senso crítico, sem promessa de ajuste posterior |

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) | Revisor(es) |
| -- | -- | -- | -- | -- |
| 1.0 | 06/10/2026 | Criação do documento de apoio à reunião S3_01, com proposta de padrões ancorada nas operacionalizações do NFR Framework, divisão e cronograma | Davi Severiano Freitas | |