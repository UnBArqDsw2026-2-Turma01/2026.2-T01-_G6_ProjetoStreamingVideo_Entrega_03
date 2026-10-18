# Reunião S2_04 — Apresentação do código e integração da Entrega 3 · SubEquipe_02

| Item | Valor |
| -- | -- |
| **Data** | 16/10/2026 |
| **Horário** | 9h25 às 9h42 (17 min) |
| **Local** | [Microsoft Teams (reunião gravada e transcrita)](https://youtu.be/BzkZGvL6hbM) |
| **Pauta** | Apresentação do que cada frente produziu, definição do padrão da Doação (F2) após consulta à professora, integração das frentes e divisão da documentação |
| **Relator** | Davi Severiano Freitas |


## 1. Participantes

| Membro | Presença |
| -- | -- |
| Davi Severiano Freitas | ✅ Presente |
| Daniel de Oliveira Lira | ✅ Presente |
| Mateus Rodrigues Barreto | ✅ Presente |
| Pedro Henrique Freire Rodrigues | ✅ Presente |

## 2. Contexto

Reunião prevista na [Ata S2_03](./ata-S2-03-2026-10-13.md) para apresentar o código de cada frente e preparar a integração. Depois da reunião, as datas de integração foram reajustadas pela equipe no grupo de WhatsApp; esta ata já registra os prazos ajustados (D02 e D03).

## 3. Situação das entregas

Situação atualizada em 17/10/2026.

| Entrega prevista | Situação | Observação |
| -- | -- | -- |
| E01 · Diagrama da F2 | ✅ Concluída em 17/10 | Diagrama final da Facade com o Mediator |
| E02 · Definição do padrão da F2 | ✅ Concluída em 16/10 | Decidido aliar a Facade ao Mediator, como extra, por se tratar de padrão comportamental (D01) |
| E03 · Diagrama e código da F1 | ✅ Concluída em 15/10 · revisada em 17/10 | Adapter, Proxy e Decorator implementados, com integração a APIs de pagamento; diagramas e código revisados pela equipe em 17/10 |
| E04 · Diagramas e código da F2 | ✅ Concluída em 17/10 | Facade e Mediator implementados, com testes |
| E05 · Diagrama e código da F3 | ✅ Concluída em 16/10 | Decorator da mensagem destacada, com diagrama de classes |
| E06 · Integração das frentes | 🟡 Em andamento | Responsável e prazo redefinidos (D02) |

## 4. Discussões

**F1 · Recarga.** Davi Severiano Freitas informou que os três padrões da frente (Adapter, Proxy e Decorator) estão implementados, com integração a APIs de pagamento, e que o código já está no GitHub.

**Padrão da F2 · orientação da professora.** Pedro Henrique Freire Rodrigues consultou a professora sobre o uso do Proxy para evitar duplicação no repasse. A orientação foi que a forma planejada **não corresponde a uma implementação correta do Proxy**, pois o Proxy precisaria implementar a mesma interface (Subject) do objeto que protege, e não apenas usá-la. Diante disso, a equipe decidiu **não adotar o Proxy na F2** e **aliar a Facade ao Mediator**: a Facade continua como padrão principal da frente, e o Mediator, por ser um padrão **comportamental**, entra como extra.

**F2 · Doação e repasse — implementação.** Daniel de Oliveira Lira apresentou o código, feito a partir do diagrama de Pedro Henrique Freire Rodrigues:

| Elemento | Responsabilidade |
| -- | -- |
| `Doacao` | Especializa `Transacao`, nasce pendente, valida o limite de texto pela faixa de destaque e calcula o valor líquido do repasse ao criador |
| `DoacaoController` | Comunica-se exclusivamente com a Facade e formata o retorno no terminal |
| `FaixaDestaque` | Regras de negócio que associam a quantidade de moeda virtual à cor, ao tempo de exibição e ao limite progressivo de caracteres |
| `ServicoDoacao` | **Facade**: concentra o fluxo da doação e esconde os subsistemas; verifica a elegibilidade do canal e a maioridade do doador, transfere os saldos em operação atômica pelo `ServicoFinanceiro` e avisa o chat |
| Demonstração | Executa no terminal uma doação com sucesso e repasse, e o bloqueio de canais não monetizados |

Após a reunião, a F2 foi alterada para incorporar o Mediator, com as classes `MediatorDoacao` e `MediatorDoacaoComMensagem` e a nova `DoacaoComMensagem`, conforme o [repositório de código](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_SubEquipe02_Codigo/tree/main/src/f2-doacao) e o diagrama [`doacao-visao-geral.puml`](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_SubEquipe02_Codigo/blob/main/docs/doacao-visao-geral.puml).

**F3 · Mensagem destacada.** Mateus Rodrigues Barreto apresentou, em vídeo, os testes da mensagem destacada no chat, que usa o padrão Decorator.

**Integração.** A integração depende dos pull requests da F2 e da F3. A reorganização interna da F2 com o Mediator não impede a integração, porque não altera a forma como a doação é usada pelas demais frentes.

**Documentação.** As páginas das frentes (Recarga, Doação e Mensagem Destacada) serão finalizadas no domingo, 18/10, mas cada responsável já pode registrar o que foi decidido. Também é preciso preparar a página de IA Generativa, consolidar as referências e atualizar o README da subequipe, por exemplo, para refletir o uso do Mediator na F2.

## 5. Decisões

| # | Decisão | Justificativa |
| -- | -- | -- |
| **D01** | **F2 alia a Facade ao Mediator; o Proxy não é adotado na F2** e permanece apenas na F1. O Mediator é registrado como extra, por ser padrão comportamental. | Orientação da professora: a forma planejada não era um Proxy correto. A Facade continua como padrão estrutural principal da frente. |
| **D02** | **Integração do código e front-end a cargo de Mateus Rodrigues Barreto, até 18/10/2026 às 12h.** | Prazo redefinido pela equipe no grupo de WhatsApp, após a reunião. |
| **D03** | **Vídeos gravados somente depois da integração.** | Os vídeos devem mostrar o sistema integrado. |
| **D04** | **Páginas das frentes finalizadas em 18/10/2026**, podendo ser preenchidas desde já com o que foi decidido. | O conteúdo final depende da conclusão de todo o trabalho. |
| **D05** | **Molde da página de IA Generativa preparado até 17/10/2026**, para que cada integrante preencha o seu relato. | Organiza a página antes do preenchimento individual. |
| **D06** | **Referências consolidadas no momento da entrega**, reunindo as de cada frente. | Evita duplicação e registra apenas as fontes efetivamente usadas. |

## 6. Encaminhamentos

| # | Ação | Responsável | Prazo | Situação |
| -- | -- | -- | -- | -- |
| E01 | Abrir pull request da F2 | Daniel de Oliveira Lira e Pedro Henrique Freire Rodrigues | 17/10/2026 | ✅ Concluído |
| E02 | Abrir pull request da F3 | Mateus Rodrigues Barreto | 17/10/2026 | ✅ Concluído |
| E03 | Integrar o código das frentes e desenvolver o front-end | Mateus Rodrigues Barreto | 18/10/2026, 12h | 🟡 Em andamento |
| E04 | Preparar o molde da página de IA Generativa | Daniel de Oliveira Lira | 17/10/2026 | 🟡 Em andamento |
| E05 | Atualizar o README da subequipe, incluindo o uso do Mediator na F2 | Daniel de Oliveira Lira | 17/10/2026 | 🟡 Em andamento |
| E06 | Preencher a página da própria frente e o relato de IA Generativa | Cada responsável de frente | 18/10/2026 | 🟡 Em andamento |
| E07 | Gravar os vídeos das frentes | Cada responsável de frente | Após a integração | ⚪ Não iniciado |
| E08 | Consolidar as referências | Todos | 18/10/2026 | ⚪ Não iniciado |

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) | Revisor(es) |
| -- | -- | -- | -- | -- |
| 1.0 | 17/10/2026 | Criação da ata da reunião de apresentação do código e integração da Entrega 3, com os prazos reajustados pela equipe após a reunião | Davi Severiano Freitas | |