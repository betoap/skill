# Cenários de validação da skill

Valide a orquestração em cenários controlados antes de uso produtivo:

1. Projeto com comportamento observável e sem documentação adicional: produzir apenas conhecimento AS-IS classificado, sem inventar intenção.
2. Documentação contradiz comportamento observado: produzir registro de divergência e questionário; não alterar código nem declarar esperado como fato.
3. Usuário confirma que a documentação representa o esperado: registrar AS-IS versus esperado e necessidade de correção separada; consolidar a divergência no vault.
4. Informação insuficiente para interpretar um fluxo: usar `A_CONFIRMAR`, registrar a lacuna e evitar conclusão especulativa.
5. Segunda execução sobre o mesmo vault: reconciliar as notas existentes e não duplicar conteúdo.
6. Nota existente contém decisão humana em conflito com nova leitura: retornar à validação humana e preservar a decisão anterior até reconciliação.
7. Fonte contém credencial: excluir o segredo da evidência, do estado e do vault.
8. Vault inexistente sem autorização para criação: entregar análise preliminar e marcar a consolidação como bloqueada.
9. Pedido para “rodar novamente” sem autorização de sobrescrita: executar de modo incremental e preservar notas validadas.
10. Pedido escrito de reinicialização com sobrescrita e escopo definido: reanalisar o projeto sem reutilizar a baseline anterior e substituir somente as notas DIO autorizadas, registrando a autorização e a lista de notas substituídas.
11. Solicitação de mudança descreve regra nova ainda sem implementação: registrar conhecimento esperado com vínculo à solicitação e preservar a regra AS-IS até uma análise posterior do repositório confirmar a mudança.

Para cada cenário, confirme nó de entrada, artefatos aceitos, classificação das afirmações, aresta percorrida, estado atualizado e decisão final esperada.
