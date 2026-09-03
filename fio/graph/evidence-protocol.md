# Protocolo de evidências

Use somente fatos observados no projeto, em comandos, ferramentas ou documentos fornecidos. Diferencie claramente **observado**, **inferido** e **desconhecido**.

- Não invente arquivos, APIs, comandos, resultados, cobertura, métricas ou aprovações.
- Não trate um teste como prova de requisito se ele não estiver ligado a um `REQ-n` na matriz.
- Não trate execução parcial, teste pulado, mock sem contrato ou saída ausente como evidência de sucesso.
- Quando um dado for necessário e não puder ser verificado, registre-o como bloqueio ou risco e siga a aresta de retorno apropriada.
- Uma validação final deve comparar a implementação e a suíte de testes contra a especificação aprovada, não apenas contra o plano ou contra testes verdes.
- Uma falha registrada em uma task é evidência histórica: após a correção, marque-a como `resolvida`, mas não apague seu motivo, evidência ou ação responsável.
- Uma falha de baseline só pode ser tratada como pré-existente quando foi reproduzida antes da demanda, está fora de seu escopo, tem causa, comando, saída e impacto registrados e não impede a execução dos testes novos. Caso contrário, ela bloqueia o TDD.
