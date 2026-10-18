# 1.1.3. SubEquipe_03 — GoFs Comportamentais + IA Generativa

**Estado:** relatório coletivo da SubEquipe 03, com as frentes de
**Moderação (Eduardo)**, **Autenticação (Hugo)** e **Chat (Philipe)**. A
contribuição documentada nesta versão é a aplicação do padrão **Observer** à
feature de chat. O código executável será mantido em repositório separado e
ainda aguarda vinculação.

Este relatório reúne os espaços necessários à Entrega 03. O conteúdo técnico e
os relatos individuais serão produzidos pelos integrantes abaixo.

## Integrantes

| Matrícula | Integrante | GitHub |
| --- | --- | --- |
| 24/1041302 | Hugo Freitas Silva | [@HugoFreitass](https://github.com/HugoFreitass) |
| 24/1040350 | Philipe Amâncio Reis Caetano | [@Phill-Chill](https://github.com/Phill-Chill) |
| 24/1011027 | Eduardo Lôbo Moreira | [@EduLoboM](https://github.com/EduLoboM) |

Composição mantida conforme a [introdução da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/#/Introducao).

## Foco do relatório

**GoFs Comportamentais + IA Generativa.** Este relatório consolida as três
frentes comportamentais da subequipe. Nesta versão, a seção técnica detalhada
é a contribuição de Philipe: o padrão Observer aplicado ao chat de uma
transmissão, incluindo contexto, UML, rastreabilidade, execução esperada e
avaliação crítica. As seções específicas de Moderação e Autenticação devem ser
preenchidas por Eduardo e Hugo, respectivamente.

## Participantes no foco — lições aprendidas e IA Generativa

| Integrante | Lições aprendidas | Uso da IA Generativa (senso crítico) |
| --- | --- | --- |
| Hugo Freitas Silva | A preencher pelo integrante | A preencher pelo integrante |
| Philipe Amâncio Reis Caetano | O principal aprendizado foi entender que receber uma mensagem não significa publicá-la. Antes de chegar aos participantes, a `ChatMessage` passa pelo `AutoModPipeline`, que pode aprová-la, colocá-la em quarentena ou rejeitá-la. O **Observer** notifica apenas as mensagens aprovadas e não é responsável pela moderação. Também aprendi a separar as responsabilidades dos componentes. A `ChatRoom` usa a interface `ChatObserver` para registrar e notificar observadores sem depender de cada serviço específico. O `ChatDeliveryService` participa desse mecanismo, enquanto o `ChatAuditService` registra os resultados e a `QuarantineQueue` guarda mensagens para revisão. Por fim, mantive `ChatRoom`, `ChatMessage` e o fluxo DYN-01 como base da Entrega 02.  | Usei o Copilot como apoio para consultar o Observer no Refactoring.Guru, localizar os elementos correspondentes na Entrega 02, revisar a coerência do diagrama e adaptar a documentação para PlantUML. O uso da IA não substituiu a análise dos artefatos: comparei as sugestões com a fonte consultada e com o modelo anterior, corrigi nomes genéricos, separei as responsabilidades de Chat e Moderação e mantive pendentes as evidências ainda inexistentes, como repositório externo, commit e vídeo. |
| Eduardo Lôbo Moreira | A preencher pelo integrante | A preencher pelo integrante |

Cada integrante deverá explicar o que aprendeu, como colaborou e, caso tenha
usado IA, qual ferramenta utilizou, o apoio recebido, como validou os
resultados e quais limitações encontrou. Informar também quando não houver uso
de IA.

## Metodologia

A subequipe dividiu o foco comportamental em três frentes de domínio:
**Eduardo — Moderação**, **Hugo — Autenticação** e **Philipe — Chat**. Cada
integrante deve modelar e documentar o comportamento de sua própria feature,
preservando os vínculos com os artefatos da Entrega 02. Nesta versão, a frente
de Chat foi organizada em quatro etapas: identificação do problema de
atualização, estudo do Observer na referência consultada, mapeamento dos
participantes para `ChatRoom` e `ChatMessage` e preparação do diagrama UML.
A implementação foi deliberadamente separada deste repositório.

Não há ata ou gravação vinculada a esta versão. Registros futuros devem ser
adicionados em [Atas e reuniões](/Projeto/Atas/README.md).

## GoF Comportamental — Observer (Feature Chat)

**Responsável pela frente:** Philipe Amâncio Reis Caetano.

Esta seção trata exclusivamente da feature de Chat.

### Contexto (problema)

Na Entrega 02, `ChatRoom` e `ChatMessage` já representam, respectivamente, a
sala e a mensagem do chat. O fluxo **DYN-01 — Inspeção e encaminhamento de
mensagens** também registra que o `AutoModPipeline` inspeciona a mensagem antes
da publicação. O problema desta etapa é definir como uma mensagem aprovada
chega aos componentes interessados sem que `ChatRoom` conheça cada classe
concreta consumidora.

Uma solução em que o publicador chama diretamente cada componente cria
acoplamento e exige alterações no publicador quando um novo interessado é
adicionado. A solução proposta usa uma lista de observadores: cada interessado
pode se inscrever ou se remover, e o publicador notifica todos por uma
interface comum.

O requisito funcional tratado nesta etapa é: **quando uma nova mensagem for
aprovada pelo fluxo de moderação e publicada no `ChatRoom`, todos os
observadores registrados devem receber a notificação; observadores removidos
não devem receber novas notificações**.

O contexto geral está registrado em [Projeto](/Projeto/Projeto.md). Os
artefatos anteriores utilizados são a
[modelagem estática da SubEquipe 03 na Entrega 02](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/blob/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.1.Foco01.ModelagemEstatica.md),
a [modelagem dinâmica da SubEquipe 03 na Entrega 02](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/blob/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica.md)
e, especificamente, o fluxo DYN-01 de inspeção e encaminhamento.

### Escolha e justificativa

O **Observer** foi escolhido porque, conforme a referência consultada, ele
define um mecanismo de inscrição para notificar múltiplos objetos sobre eventos
do objeto observado. No vocabulário usado pela referência:

- o **Publisher** mantém a infraestrutura de assinaturas e notifica os
  assinantes quando ocorre um evento;
- o **Subscriber** expõe uma operação de notificação comum, normalmente
  `update`;
- os **Concrete Subscribers** reagem à notificação sem que o publicador
  conheça suas classes concretas;
- o **Client** cria os objetos e registra os assinantes.

No domínio existente, `ChatRoom` assume o papel de **Publisher** e
`ChatMessage` transporta o contexto da notificação. A interface proposta
`ChatObserver` define `update`, e `ChatDeliveryService` é o observador concreto
responsável por receber a mensagem publicada. `ChatAuditService`,
`QuarantineQueue` e `AutoModPipeline` não são observadores: são dependências
usadas pela sala para registrar o resultado, encaminhar mensagens retidas e
avaliar a mensagem antes da publicação. `ChatSetup` assume o papel de cliente,
montando essas dependências e inscrevendo o serviço de entrega.

Os nomes e operações de assinatura são uma extensão deste desenho, não uma
afirmação de que já existiam na Entrega 02. O `AutoModPipeline` continua
responsável pela inspeção anterior à publicação, conforme DYN-01, e a
integração com ele permanece separada do mecanismo de notificação do
Observer.

O padrão não define persistência, autenticação, transporte de rede, ordenação,
filtragem ou moderação das mensagens. Esses comportamentos não fazem parte
desta demonstração e não são atribuídos ao Observer.

### Modelagem (notação UML)

![UML](./assets/chatGoFObserver.png)

#### Correspondência entre UML e Observer

| Participante da referência | Elemento do chat | Responsabilidade |
| --- | --- | --- |
| Publisher | `ChatRoom` (extensão proposta) | Manter observadores, permitir inscrição e remoção e chamar `update` para cada observador. |
| Subscriber | `ChatObserver` (extensão proposta) | Definir a interface comum de notificação. |
| Concrete Subscriber | `ChatDeliveryService` (extensão proposta) | Receber a mensagem publicada por meio de `update`. |
| Evento/contexto | `ChatMessage` (Entrega 02) | Transportar a mensagem publicada para `update`. |
| Dependências do Publisher | `AutoModPipeline`, `ChatAuditService` e `QuarantineQueue` | Avaliar, registrar e encaminhar o resultado da moderação. |
| Client | `ChatSetup` (extensão proposta) | Fornecer as dependências à sala e registrar o observador. |

O diagrama representa a chamada indireta do `ChatRoom` para
`ChatDeliveryService`: a sala mantém objetos que implementam `ChatObserver` e
os notifica por `update`. `ChatAuditService` recebe uma chamada específica
`record(message, verdict)` e, portanto, não é um Subscriber. A notificação é
privada (`notify`) e só ocorre para uma mensagem aprovada; mensagens
quarentenadas são encaminhadas à `QuarantineQueue` e mensagens rejeitadas não
são entregues.

### Implementação (código)

O código TypeScript será versionado em repositório separado. A escolha de
TypeScript mantém a coerência tecnológica com a Entrega 02, que utiliza essa
linguagem como referência, e permite representar diretamente as interfaces,
tipos de mensagem e contratos do modelo. Até que a URL seja informada, o elo
versionado permanece explicitamente pendente:

- **Responsável pelo código:** Philipe Amâncio Reis Caetano;
- **Repositório:** a informar;
- **arquivo executável:** a informar;
- **commit da implementação:** a informar.

O código deverá preservar os participantes e operações do modelo:
`ChatRoom.subscribe`, `ChatRoom.unsubscribe`, `ChatRoom.publish`,
`ChatRoom.notify`, `ChatObserver.update` e `ChatDeliveryService`. Também deve
representar as dependências `AutoModPipeline`, `ChatAuditService` e
`QuarantineQueue`, sem transformar esses serviços em observadores. A
implementação de Chat não incorpora a lógica interna de moderação de Eduardo:
ela apenas consome o `ModerationVerdict` retornado pela avaliação para decidir
entre notificar, registrar ou encaminhar para quarentena.

### Execução e vídeo do padrão em funcionamento

Esta documentação não contém o código, portanto o comando executável e o
resultado observado ainda não podem ser declarados como evidência. Após a
vinculação do repositório externo, preencher:

```text
Pré-requisito: Node.js e dependências do projeto TypeScript
Comando: [comando real do repositório externo]
Vídeo: [link para a demonstração]
```

O cenário mínimo a demonstrar é:

1. o `ChatSetup` configura um `ChatRoom`, suas dependências e um
   `ChatDeliveryService`;
2. o serviço de entrega é registrado por `subscribe`;
3. o `ChatRoom.publish` solicita a avaliação ao `AutoModPipeline`;
4. para uma decisão `APPROVED`, a sala registra o resultado em
   `ChatAuditService` e chama `notify`, que executa `update` no serviço de
   entrega;
5. para uma decisão `QUARANTINED`, a sala registra o resultado e encaminha a
   mensagem e o veredito para `QuarantineQueue`, sem notificar o observador;
6. para uma decisão `REJECTED`, a sala registra a decisão e não entrega a
   mensagem;
7. após `unsubscribe`, uma nova mensagem aprovada não deve mais chamar
   `update` nesse observador.

Os itens acima são o roteiro verificável da execução, não uma afirmação de
que ela já foi executada neste repositório.

## Rastreabilidade & Elos com Outros Artefatos

A [modelagem estática](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/blob/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.1.Foco01.ModelagemEstatica.md)
e a [modelagem dinâmica](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/blob/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica.md)
da SubEquipe 03 na Entrega 02 são os artefatos de origem. O Observer é uma
extensão de desenho desta entrega, não uma funcionalidade declarada como
existente na Entrega 02.

| Problema ou requisito | Artefato de origem (link) | Elemento do modelo | Trecho de código (link) | Evidência de execução (link) |
| --- | --- | --- | --- | --- |
| Mensagem aprovada deve ser distribuída sem acoplamento do `ChatRoom` ao serviço concreto de entrega | [ChatMessage, ChatRoom e DYN-01 na Entrega 02](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/blob/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica.md) | `ChatRoom`, `ChatMessage`, `ChatObserver`, `ChatDeliveryService` | Repositório externo — URL, arquivo e commit a informar | Vídeo e saída do programa — a informar |
| Inscrição e remoção devem controlar quais objetos recebem novas notificações | [Observer — mecanismo de assinatura](https://refactoring.guru/design-patterns/observer) | `ChatRoom.subscribe`, `ChatRoom.unsubscribe`, `ChatRoom.notify`, `ChatObserver.update` | Repositório externo — a informar | Demonstração do cenário de inscrição e remoção — a informar |
| Mensagens devem ser avaliadas antes da publicação e encaminhadas conforme o veredito | [DYN-01 e DYN-02 da Entrega 02](https://github.com/UnBArqDsw2026-2-Turma01/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/blob/main/docs/Base/Relat%C3%B3rios/1.1.3.SubEquipe_03/1.1.3.2.Foco02.ModelagemDinamica.md) | `AutoModPipeline`, `ModerationVerdict`, `ModerationDecision`, `QuarantineQueue`, `ChatAuditService` | Repositório externo — a informar | Cenários `APPROVED`, `QUARANTINED` e `REJECTED` — a informar |
| As dependências e o observador devem ser montados e registrados pelo cliente | [Observer — papel do Client](https://refactoring.guru/design-patterns/observer) | `ChatSetup` | Repositório externo — a informar | Demonstração da configuração — a informar |

As lacunas estão marcadas como pendentes para não transformar uma URL,
commit, arquivo ou execução inexistentes em comprobatórios fictícios.

## Senso Crítico

O Observer reduz o acoplamento entre o publicador e os componentes que
consomem eventos do chat. Também permite adicionar novos assinantes sem
alterar o publicador, desde que implementem a mesma interface. A inscrição e
a remoção em tempo de execução representam diretamente a necessidade de
participantes entrarem ou saírem do acompanhamento da transmissão.

Como custos, o publicador passa a manter uma coleção de assinantes e uma
notificação pode disparar várias ações em sequência. O padrão, isoladamente,
não resolve falhas de um assinante, concorrência, ordenação, persistência ou
entrega por rede. Esses limites devem ser tratados por outras decisões de
arquitetura, sem atribuí-los ao Observer.

A coerência do modelo será validada contra o código externo quando o
repositório for vinculado. Nesta versão, o UML é a especificação da
implementação esperada, e não uma evidência de execução.

## Referências

1. Refactoring.Guru. **Observer**. Descrição do padrão comportamental,
   incluindo intenção, problema, solução, estrutura, pseudocódigo e
   aplicabilidade. Consulta realizada em 16 out. 2026.
   <https://refactoring.guru/design-patterns/observer>. Fundamenta a escolha
   do mecanismo de assinatura, a separação entre Publisher e Subscriber, a
   operação `update` e a notificação com dados de contexto.
2. Grupo 06. **Documentação da Entrega 02**. Artefatos anteriores da
   plataforma de streaming. Disponível em:
   <https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/>.
   Fundamenta a continuidade do domínio; o artefato específico da feature
   ainda precisa ser apontado.

## Versionamentos & Participações

Registrar apenas alterações efetivamente realizadas, incluindo autoria,
revisão e links para commits ou pull requests.

| Versão | Data | Integrante | Contribuição | Revisor | Comprobatório (commit/PR) |
| --- | --- | --- | --- | --- | --- |
| 0.1 | 16/10/2026 | [@Philipe Amâncio Reis Caetano](https://github.com/Phill-Chill)| Documentação do Observer para o chat, diagrama PlantUML, rastreabilidade e roteiro de execução | [@Eduardo Lôbo Moreira](https://github.com/EduLoboM), [@Hugo Freitas Silva](https://github.com/HugoFreitass) | A vincular após commit/PR |

Atualizar também o [quadro consolidado de participações](/Base/1.2.ParticipacoesPadroesDeProjeto.md)
quando houver evidência versionada.


 