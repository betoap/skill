# Cenários de validação da CIM

Valide a orquestração em cenários controlados antes de uso produtivo:

1. Solicitação clara percorre SIM, FIO e DIO; a DIO confirma a implementação no repositório e o ciclo encerra como `confirmada_asis`.
2. SIM identifica ambiguidade material; a CIM mantém o ciclo em decisão pendente e não inicia a FIO.
3. FIO encontra alteração material de escopo; a CIM retorna o contexto à SIM ou ao recebimento, preservando o identificador.
4. FIO conclui tecnicamente, mas a DIO não encontra a mudança no repositório; a CIM preserva o AS-IS e retorna para entrega corretiva ou encerra como não confirmada.
5. DIO confirma somente parte do conhecimento esperado; a CIM encerra como `parcial` e mantém os itens pendentes rastreáveis.
6. Reexecução do mesmo ciclo após interrupção: a CIM localiza o último handoff válido e não cria segundo histórico, plano ou atualização no vault.
7. Handoff sem identificador compartilhado ou evidência: a CIM bloqueia a transição e encaminha ao produtor correto.
8. Uma das skills coordenadas está indisponível ou com fonte não verificável: a CIM bloqueia antes de substituí-la por execução própria.

Para cada cenário, confirme nó de entrada, handoffs aceitos, guarda percorrida, estado atualizado, itens invalidados e resultado final esperado.
