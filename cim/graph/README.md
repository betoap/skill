# Contrato do grafo de orquestração

No início de um ciclo, crie ou atualize `.cim/workflow-state.yaml` no projeto relacionado a partir do [template](workflow-state.template.yaml). Registre identificador do ciclo, solicitação, projeto, vault, nó atual, estado, fontes verificáveis das skills, artefatos de handoff, transições, evidências, responsáveis, bloqueios e retornos. Registre também `entry_mode` como `new`, `resume` ou `assumed_partial`.

Cada handoff deve ter uma entrada própria com identificador, produtor, status, caminho ou referência, ciclo relacionado, escopo, pendências, evidências e incertezas. O estado da CIM não substitui os estados de SIM, FIO ou DIO; ele aponta para eles e registra apenas o necessário para auditar a passagem entre skills.

Antes de qualquer transição, compare o estado com os artefatos de origem. Uma referência ausente, identificador incompatível, resultado sem evidência, artefato inválido ou pendência obrigatória bloqueia a transição até a reconciliação.

## Retomada e encerramento

Uma retomada localiza o mesmo identificador de ciclo e o último handoff válido. Uma assunção parcial vincula um resultado preexistente ao ciclo e o valida antes de avançar. Não crie um novo ciclo para a mesma solicitação sem registrar a relação entre os ciclos.

O ciclo só pode encerrar como `confirmada_asis` quando a DIO registrar evidência observável no repositório e confirmar os conhecimentos esperados avaliados. Resultados `parcial`, `nao_confirmada` e `bloqueada` preservam pendências e informam o retorno necessário; eles não equivalem a entrega confirmada.
