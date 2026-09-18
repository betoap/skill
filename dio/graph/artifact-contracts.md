# Contratos de artefatos

Todo artefato usa identificador estável, produtor, status (`draft`, `current`, `invalidated`, `validated` ou `blocked`), classificação, fontes de evidência e incertezas. Não preencha campos sem base observável.

## Escopo e inventário de fontes

- identificador da demanda, caminho do projeto e caminho do vault;
- objetivo e limites da análise;
- documentação adicional e contexto livre recebidos, com origem e status;
- permissões ou bloqueios para leitura e publicação;
- exclusões explícitas, inclusive código de implementação que não deve ser documentado.

## Achados AS-IS e conhecimento preliminar

- finalidade, atores, funcionalidades, regras de negócio, fluxos, conceitos, integrações e arquitetura em alto nível, quando houver evidência;
- comportamento observável e a fonte que o sustenta;
- classificação `observado`, `inferido`, `confirmado` ou `a_confirmar` por afirmação material;
- limitações da análise e itens ainda desconhecidos;
- distinção explícita entre AS-IS e esperado quando ambos forem conhecidos.

Quando o esperado vier de uma solicitação de mudança, registre também sua origem e vínculo rastreável. Esse vínculo não permite promover, remover ou alterar o AS-IS sem evidência posterior no repositório.

## Registro de divergências e questionário

Para cada divergência, registre fontes em conflito, descrição objetiva, impacto, classificação e a pergunta necessária. Não peça ao usuário para definir o AS-IS se ele é observável. Ofereça, quando adequado, interpretações como: implementação correta; documentação desatualizada; documentação representa o esperado e a implementação precisa ser corrigida; regra alterada ou falta de informação; outra interpretação; ou não sei.

## Conhecimento validado e decisões

Registre cada resposta humana, responsável ou origem, data lógica, decisão, escopo afetado e efeito sobre o AS-IS, esperado ou incerteza. Uma resposta ausente mantém o item como `a_confirmar`; não a substitua por inferência.

## Baseline e relatório de consolidação

Registre modo de execução (`incremental` ou `explicit_rebuild`), notas criadas ou atualizadas, relações internas criadas, conteúdo preservado por validação humana, divergências abertas e resultado `published`, `partial` ou `blocked`. O relatório deve permitir identificar o que foi consolidado sem duplicar o conteúdo das notas.

No modo `explicit_rebuild`, registre também a autorização escrita do usuário, o escopo autorizado e cada nota substituída. Sem esses três elementos, trate a execução como `incremental`.

## Revalidação AS-IS para a CIM

Quando a execução estiver vinculada a uma CIM, registre um handoff com o `cycle_id` compartilhado, conhecimentos esperados avaliados, evidência observável no repositório, resultado por item (`confirmado`, `parcial`, `nao_encontrado` ou `bloqueado`), atualizações ou preservação da baseline, pendências e retorno necessário. Sem ciclo identificado, este artefato não é produzido nem encaminhado.
