# Tarefa: Criar Skill de Orquestração do Ciclo de Mudança

## Objetivo

Criar uma nova skill responsável por orquestrar o ciclo completo de uma solicitação de mudança entre as skills SIM, FIO e DIO.

Essa skill não substitui nem mistura as responsabilidades das outras. Ela mantém o estado do ciclo, a rastreabilidade e as transições entre as skills, garantindo que uma mudança só seja encerrada após a confirmação AS-IS pela DIO.

## Papel de cada skill

| Skill | Responsabilidade exclusiva |
| --- | --- |
| SIM | Interpretar a solicitação de mudança e consolidar conhecimento esperado ou planejado, com impacto e rastreabilidade. |
| FIO | Esclarecer, planejar, implementar e validar tecnicamente a mudança. |
| DIO | Observar o repositório e criar ou revalidar a baseline AS-IS no Obsidian. |
| Skill orquestradora | Coordenar o ciclo, preservar o identificador comum, validar handoffs e encerrar a mudança. |

## Princípio fundamental

A skill não assume a responsabilidade da outra.

- A SIM propõe e registra o conhecimento esperado.
- A FIO implementa e valida a demanda.
- A DIO confirma o que existe no repositório e promove conhecimento para AS-IS quando houver evidência.
- A skill orquestradora apenas coordena essas passagens e registra o estado do ciclo.

## Identificador compartilhado

Cada ciclo deve ter um identificador estável de mudança. Esse identificador deve aparecer:

- no registro da solicitação da SIM;
- no plano-mestre e nas tasks da FIO;
- na revalidação e no relatório da DIO;
- no estado operacional da skill orquestradora.

Nenhuma skill deve criar um segundo ciclo para a mesma solicitação sem registrar explicitamente a relação entre eles.

## Ciclo de mudança

1. Receber uma solicitação de mudança.
2. Encaminhar a solicitação para a SIM.
3. Validar que a SIM produziu registro da solicitação, conhecimento esperado, análise de impacto, classificações e pendências.
4. Encaminhar o contexto consolidado da SIM para a FIO.
5. Validar que a FIO produziu especificação aprovada, plano, evidências de implementação e validação técnica.
6. Encaminhar a evidência de entrega da FIO para a DIO.
7. Validar que a DIO reanalisou o repositório e classificou o resultado como confirmado, parcial, não encontrado ou bloqueado.
8. Encerrar o ciclo e atualizar o histórico da solicitação com o resultado final.

## Handoffs obrigatórios

Os handoffs possuem nomes e objetivos explícitos, mas são obrigatórios somente dentro de um ciclo iniciado ou assumido pela CIM. Uma execução isolada de SIM, FIO ou DIO não cria handoff nem aciona outra skill automaticamente.

Dentro do ciclo da CIM, os handoffs são:

- **Contexto da mudança:** SIM → FIO.
- **Evidência de entrega:** FIO → DIO.
- **Revalidação AS-IS:** DIO → CIM.

Todos preservam o mesmo identificador compartilhado. Eles não criam uma etapa adicional para o usuário; apenas tornam verificável a passagem de contexto entre as skills.

### SIM para FIO

A SIM deve entregar um contexto de mudança contendo:

- identificador compartilhado;
- solicitação de origem;
- conhecimento esperado ou planejado;
- análise de impacto;
- classificações de certeza;
- divergências, dúvidas e decisões humanas;
- vínculos para as notas e o histórico relevantes.

A FIO pode pedir esclarecimentos ou devolver a mudança para revisão, mas não pode perder o vínculo com a solicitação de origem.

### FIO para DIO

A FIO deve entregar uma evidência de implementação contendo:

- identificador compartilhado;
- escopo implementado e não implementado;
- relatório de validação técnica;
- evidências de execução e de entrega;
- limitações, pendências e retornos relevantes.

Essa evidência é um gatilho para reanálise pela DIO, não uma prova automática de AS-IS.

### DIO para encerramento

A DIO deve entregar uma revalidação do repositório contendo:

- identificador compartilhado;
- conhecimentos esperados avaliados;
- evidência observável no repositório;
- resultado por item: `confirmado`, `parcial`, `não_encontrado` ou `bloqueado`;
- atualizações da baseline AS-IS e itens que permaneceram esperados ou incertos.

## Estados do ciclo

Utilizar estados explícitos e rastreáveis:

- `recebida`;
- `em_analise_sim`;
- `aguardando_decisao`;
- `pronta_para_fio`;
- `em_execucao_fio`;
- `aguardando_revalidacao_dio`;
- `confirmada_asis`;
- `parcial`;
- `nao_confirmada`;
- `bloqueada`;
- `cancelada`.

Uma transição deve registrar o artefato que a sustenta, a evidência observável, os itens invalidados e o próximo responsável.

## Regras de transição

- Não iniciar a FIO sem contexto mínimo válido da SIM, salvo início parcial explicitamente registrado.
- Não acionar a DIO como confirmação final sem entrega validada da FIO, salvo quando houver evidência de repositório independente explicitamente registrada.
- Não encerrar o ciclo como `confirmada_asis` sem revalidação da DIO.
- Um resultado `parcial`, `não_confirmado` ou `bloqueado` não encerra o conhecimento esperado como realizado; deve preservar pendências e indicar o retorno necessário.
- Se a FIO alterar o escopo aprovado, a orquestradora deve devolver a mudança para a SIM ou para a etapa de esclarecimento aplicável antes de prosseguir.
- Se a DIO não encontrar a mudança no repositório, a orquestradora deve preservar o AS-IS, reabrir a mudança ou marcá-la como não confirmada, conforme a evidência.

## Idempotência e retomada

Executar novamente o mesmo ciclo deve localizar seu identificador e reconciliar o estado, sem duplicar planos, histórico, links ou atualizações no vault.

O ciclo pode ser retomado do último handoff válido quando seus artefatos existirem, estiverem atuais e forem consistentes. Uma reexecução não pode avançar por uma transição apenas porque há texto narrativo; ela exige os artefatos e evidências definidos.

### Artefato para continuar depois

Ao iniciar o ciclo, a CIM cria no projeto relacionado o arquivo `.cim/workflow-state.yaml`. Este é o artefato de continuidade: ele registra o identificador do ciclo e da solicitação, projeto e vault relacionados, etapa e status atuais, referências aos handoffs já concluídos, evidências, pendências, bloqueios, retornos e histórico.

A CIM aceita três modos de entrada: `new`, para uma solicitação ainda sem ciclo; `resume`, para continuar um ciclo já registrado; e `assumed_partial`, para assumir uma mudança iniciada fora da CIM. No último caso, ela vincula o resultado preexistente ao ciclo e só avança se o artefato da etapa anterior cumprir seu contrato; riscos e dependências permanecem registrados.

Para continuar no dia seguinte, basta solicitar à CIM a retomada da mesma mudança. A CIM localiza esse arquivo pelo projeto e pelo identificador do ciclo, confere o último handoff registrado contra seus artefatos de origem e segue pela próxima etapa válida.

Se a referência estiver ausente, o identificador não corresponder, a evidência for insuficiente ou o artefato estiver invalidado, a CIM não reinicia todo o ciclo: ela bloqueia apenas a transição afetada e informa o ponto que precisa ser retomado. Não criar um novo ciclo apenas porque a execução foi interrompida.

## Limites e fora de escopo

A skill orquestradora não deve:

- interpretar a solicitação no lugar da SIM;
- implementar, testar ou validar tecnicamente no lugar da FIO;
- analisar o repositório ou alterar a baseline AS-IS no lugar da DIO;
- alterar código, corrigir bugs ou tomar decisões de produto sem evidência e validação necessárias;
- integrar automaticamente com Kanban, sistemas de gestão de solicitações, RAG, embeddings, banco vetorial ou Figma.

## Princípio final

Uma mudança só é considerada concluída quando existe uma trilha verificável de solicitação, conhecimento esperado, implementação validada e confirmação observável no repositório. O conhecimento esperado e o AS-IS devem permanecer distintos até essa confirmação.
