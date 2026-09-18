# Protocolo de evidências

Use somente fatos observados no projeto, em documentos fornecidos, no contexto explícito do usuário ou em ferramentas executadas. Diferencie claramente **observado**, **inferido**, **confirmado** e **a confirmar**.

- Não invente funcionalidades, regras, atores, integrações, decisões de produto, resultados ou aprovações.
- O código é evidência do AS-IS, mas não prova sozinho de que o comportamento é o esperado pelo produto.
- Documentação adicional e contexto livre são fontes comparáveis, não substitutos automáticos para o comportamento observado.
- Uma solicitação de mudança ou critério de aceite é evidência de comportamento esperado ou planejado; nunca é, por si só, evidência para promover uma mudança a AS-IS.
- Somente uma análise posterior do repositório, com comportamento observável, pode promover conhecimento esperado para AS-IS.
- Quando uma informação necessária não puder ser verificada, mantenha-a como `A_CONFIRMAR` e registre a lacuna ou o bloqueio.
- Evidências devem permitir localizar a fonte sem expor secrets, credenciais ou dados sensíveis.
- Não copie blocos de código, listas de classes ou detalhes de implementação para o vault como forma de evidência.
- Uma decisão humana resolve somente a divergência declarada e deve preservar as fontes e o motivo da decisão.
- Alterações em conhecimento validado exigem evidência nova e registro da reconciliação; nunca apague histórico de divergência apenas porque foi resolvida.
- Uma execução que ignore a baseline anterior exige autorização escrita e explícita para `explicit_rebuild`, com vault ou escopo identificado. Sem essa autorização, “executar novamente” significa execução incremental e idempotente.
