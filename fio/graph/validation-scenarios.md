# Cenários de validação da suite

Valide a orquestração com cenários controlados antes de uso produtivo:

1. Feature simples com requisito e teste positivos, negativos e de borda.
2. Requisito ambíguo detectado por ConfIA antes da implementação; deve retornar a ChefIA.
3. Contrato arquitetural inconsistente detectado no desenho de testes; deve retornar a MaestrIA.
4. Teste novo falha por configuração, não por ausência da feature; CodIA não pode iniciar.
5. CodIA encontra teste insuficiente; deve retornar à ConfIA de desenho de testes.
6. Testes verdes, mas cenário da especificação não está coberto; validação final deve reprovar.
7. Regressão em teste existente; validação final deve reprovar e reabrir os checks afetados.
8. Início direto em CodIA sem artefatos obrigatórios; ChefIA deve impedir ou redirecionar o fluxo.

Para cada cenário, confirme nó de entrada, artefatos aceitos, aresta percorrida, estado atualizado e decisão final esperada.
