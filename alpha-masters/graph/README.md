# Contrato do grafo de trabalho

O fluxo é um grafo dirigido de nós especializados, não um prompt linear. As arestas só podem ser percorridas quando sua condição estiver comprovada pelos artefatos de saída e pelo [protocolo de evidências](evidence-protocol.md).

No início de uma demanda, crie ou atualize `.alpha-masters/workflow-state.yaml` no projeto atendido a partir do [template](workflow-state.template.yaml). Registre demanda, nó atual, artefatos disponíveis, checks, evidências, última transição e bloqueios. Mantenha somente estado operacional verificável.

Depois que ChefIA definir a demanda, o estado deve registrar `plan_directory` e `master_plan_path`, apontando para `/plan/{demanda}/` e `/plan/{demanda}/{demanda}.md`. As listas `requirements`, `tasks`, `checks` e `workstreams` começam vazias e só recebem registros reais. Mantenha uma entrada por requisito com seu `REQ-n`, status e tasks vinculadas; uma entrada por task com seu `TASK-n`, caminho, requisitos cobertos, status e checks de fase; e uma entrada por check com status, responsável e evidência. Ao delegar trabalho paralelo, registre em `workstreams` o responsável, fase, task ou cenários atribuídos, arquivos ou módulos, dependências, status e evidências. O estado não substitui os documentos de checklist: ele deve apontar para eles e reproduzir apenas o estado necessário para auditar a transição.

Antes de qualquer transição, compare o estado com o plano-mestre e as tasks no disco. Se um caminho não existir, uma referência divergir ou um check tiver status ou evidência diferente, trate o estado como desatualizado, corrija a inconsistência e bloqueie a transição até a reconciliação.

É permitido iniciar em qualquer nó quando os artefatos de entrada existirem e cumprirem seus [contratos](artifact-contracts.md). Registre início parcial e riscos de fases puladas. Em retornos, invalide apenas os artefatos afetados e reabra seus checks. Use os [cenários de validação](validation-scenarios.md) para testar a própria suite.

## Execução local

O executor auditável da suite, quando provisionado junto ao ambiente da skill, valida o YAML do grafo, controla o estado por demanda, aplica contratos mínimos dos artefatos e bloqueia entradas ou arestas sem evidência observável. Ele não substitui a skill nem fabrica provas: um host integrado chama a skill do nó atual, registra os artefatos devolvidos e solicita a transição correspondente.
