# Protocolo de evidências

Use somente o texto recebido da solicitação, o conhecimento existente no vault, contexto explícito do usuário e observações verificáveis em ferramentas. Diferencie claramente comportamento **atual**, **esperado**, **planejado** e **incerto**, além das classificações `observado`, `inferido`, `confirmado` e `a_confirmar`.

- Não invente regras, fluxos, atores, integrações, decisões ou critérios que não estejam sustentados pela solicitação ou pelo conhecimento disponível.
- A solicitação é evidência de mudança proposta, não de mudança implementada.
- Não trate uma mudança nova e clara como conflito somente porque ela não aparece na baseline AS-IS.
- Não altere a baseline AS-IS, ainda que a solicitação peça alteração ou remoção; registre o impacto esperado e a necessidade de confirmação posterior pelo repositório.
- Quando houver ambiguidade material ou mais de uma interpretação plausível, solicite decisão humana de forma objetiva.
- Preserve a origem de cada mudança consolidada, sem expor secrets, credenciais ou dados sensíveis.
- Não copie código, detalhes de implementação ou todo o texto da solicitação para notas centrais quando um resumo rastreável for suficiente.
