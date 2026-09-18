# Contrato do grafo de conhecimento incremental

No início de uma solicitação, crie ou atualize `.sim/workflow-state.yaml` no projeto relacionado a partir do [template](workflow-state.template.yaml). Registre identificador da solicitação, projeto, vault, conteúdo de origem ou referência segura, nó atual, nome, versão e origem verificável da skill, artefatos, impactos, decisões humanas, notas atualizadas, última transição e bloqueios.

Cada artefato declarado como entrada ou saída de um nó deve ter uma entrada própria com identificador, produtor, status, caminho ou referência, contexto, classificação, incertezas e evidências. O estado aponta para as notas e o histórico; não os substitui.

Antes de qualquer transição, reconcilie estado, conteúdo da solicitação, conhecimento relacionado no vault e histórico da própria solicitação. Se uma nota AS-IS entrar em conflito com uma mudança proposta, preserve a nota AS-IS, registre a mudança como esperada e classifique o impacto; não aplique uma substituição.

## Idempotência e rastreabilidade

Uma reexecução da mesma solicitação deve localizar seu registro anterior e atualizar somente o que mudou na fonte ou na interpretação. Não crie uma segunda cópia do mesmo histórico nem repita conteúdo esperado nas notas centrais. Cada alteração consolidada deve apontar para a solicitação que a originou e informar sua classificação e tipo de impacto.
