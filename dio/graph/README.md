# Contrato do grafo de conhecimento

No início de uma demanda, crie ou atualize `.dio/workflow-state.yaml` no projeto analisado a partir do [template](workflow-state.template.yaml). Registre identificador da demanda, projeto, vault, fontes, nó atual, nome, versão e origem verificável da skill, artefatos, evidências, última transição, decisões humanas, incertezas e bloqueios.

O estado mantém somente informação operacional verificável. Cada artefato declarado como entrada ou saída de um nó deve ter uma entrada própria com identificador, produtor, status, caminho ou referência, contexto de criação, classificação, incertezas e evidências. O estado não substitui as notas do vault nem o relatório de análise: ele aponta para eles e registra o necessário para auditar transições.

Antes de qualquer transição, reconcilie estado, fontes consultadas e notas que serão atualizadas. Se uma nota tiver confirmação ou decisão humana que entre em conflito com a nova análise, não a sobrescreva: registre a divergência e retorne à validação humana.

Materiais de solicitação de mudança podem ser inventariados como fontes de comportamento esperado, mas não podem invalidar nem substituir a baseline AS-IS sem nova evidência observável no repositório. Registre a origem da solicitação e a ligação com cada conhecimento esperado afetado.

É permitido iniciar diretamente em um nó apenas quando os artefatos de entrada existirem, estiverem atuais e atenderem aos [contratos](artifact-contracts.md). Registre o início parcial, as fases puladas e os riscos. Em retornos, invalide somente os artefatos afetados.

## Idempotência

Antes de criar uma nota, procure uma nota existente que cubra o mesmo assunto. Atualize-a de forma reconciliada ou registre uma divergência; não crie duplicatas por conveniência. Uma alteração em conteúdo validado por humano exige evidência nova e validação humana explícita. Nunca remova a evidência histórica de uma divergência resolvida.

## Reinicialização com sobrescrita

O estado deve registrar `execution_mode: incremental` por padrão. O valor `explicit_rebuild` só é válido se houver autorização escrita e explícita do usuário para ignorar a baseline anterior e sobrescrever o escopo identificado. Registre a autorização, o escopo e as notas substituídas em entradas próprias de evidência e relatório.

Mesmo em `explicit_rebuild`, inventarie as notas existentes apenas para delimitar o escopo e proteger conteúdo não relacionado. Não reutilize seu conteúdo como fonte da nova baseline e não altere fora do escopo autorizado.
