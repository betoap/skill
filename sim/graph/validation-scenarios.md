# Cenários de validação da SIM

Valide a orquestração em cenários controlados antes de uso produtivo:

1. Solicitação clara de regra nova: consolidar como conhecimento esperado, com vínculo à solicitação, sem confirmação humana obrigatória.
2. Solicitação altera regra existente, mas o repositório ainda não mudou: registrar esperado e preservar o AS-IS atual.
3. Solicitação pede remoção de comportamento atual: registrar remoção esperada e não apagar a nota AS-IS.
4. Solicitação ambígua com duas interpretações plausíveis: produzir pergunta objetiva e bloquear a consolidação afetada até decisão humana.
5. Solicitação contradiz conhecimento confirmado: registrar divergência e solicitar interpretação humana, sem sobrescrever a nota existente.
6. Segunda execução da mesma solicitação: reconciliar seu histórico e suas notas, sem duplicar conteúdo.
7. Solicitação contém credencial: excluir o segredo de estado, evidência, histórico e notas.
8. Solicitação sem projeto ou vault identificável: registrar bloqueio antes de publicar.

Para cada cenário, confirme nó de entrada, artefatos aceitos, classificação, aresta percorrida, atualização do estado e resultado esperado.
