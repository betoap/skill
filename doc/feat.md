# Tarefa: Criar Skill de Knowledge Incremental a partir de Solicitações de Mudança

## Objetivo

Criar uma nova skill responsável por receber informações de uma solicitação de mudança, interpretar a demanda, consultar a base de conhecimento no Obsidian, realizar análise de impacto sobre o conhecimento atual e consolidar alterações automaticamente sempre que houver segurança suficiente.

## Princípio fundamental

O objetivo é construir conhecimento persistente sobre o produto a partir de demandas temporárias.

- A solicitação de mudança é a origem temporária.
- Obsidian é o conhecimento persistente.
- O repositório continua sendo a fonte de implementação.

## Fronteira com a Baseline AS-IS

Esta skill é independente da skill de bootstrap inicial. A skill de bootstrap é responsável pela baseline AS-IS, criada ou revalidada a partir da evidência observável no repositório. Esta skill é responsável por interpretar a solicitação de mudança e registrar seu impacto esperado sobre o conhecimento do produto.

Uma solicitação de mudança não é evidência de que o comportamento atual já mudou. Portanto, esta skill não pode promover automaticamente conhecimento `esperado` ou `planejado` para `AS-IS`, nem substituir, remover ou reclassificar comportamentos atuais sem evidência posterior no repositório.

Quando a mudança for clara, a consolidação automática deve registrar a alteração como conhecimento esperado e vinculá-la à solicitação que a originou. A promoção para AS-IS ocorre somente após uma nova análise da skill de bootstrap ou outra evidência observável equivalente.

### Handoff para a FIO

Este handoff só se aplica quando esta skill participar de um ciclo coordenado pela CIM. Em uso independente, a SIM conclui sua própria análise e não encaminha informações automaticamente para a FIO.

Dentro do ciclo da CIM, ela deve entregar à FIO um **contexto da mudança** com:

- identificador compartilhado da mudança;
- solicitação de origem;
- conhecimento esperado ou planejado;
- análise de impacto e classificações de certeza;
- divergências, dúvidas, decisões humanas e pendências;
- vínculos com as notas e o histórico relevantes.

Esse contexto é apenas a entrada inicial da FIO. A FIO continua responsável por esclarecer dúvidas materiais e confirmar o escopo antes de implementar.

No estado operacional, esse handoff é identificado como `sim_change_context`. Ele é gerado e localizado pela CIM; quem usa a skill não precisa criar ou transportar esse artefato manualmente.

## Entrada

Receber dados colados manualmente pelo usuário a partir de uma solicitação de mudança, como descrição, critérios de aceite e metadados quando disponíveis.

- Não assumir estrutura fixa dentro dos campos.
- Tratar todo o conteúdo como texto.

## Processamento

Interpretar o texto da feature e identificar conhecimento sobre o produto:

- regras de negócio;
- fluxos;
- atores;
- conceitos;
- integrações;
- comportamentos descritos ou sugeridos.

Consultar o conhecimento relacionado já existente no Obsidian e realizar uma análise de impacto, classificando-o como:

- `novo`;
- `complementa`;
- `altera`;
- `remove`;
- `divergência`;
- `dúvida`.

Divergência ou dúvida não é o padrão. A validação humana só é necessária quando houver ambiguidade real ou mais de uma interpretação plausível. Não pedir confirmação por formalidade.

O tipo de impacto não substitui a classificação de certeza. Cada afirmação material também deve ser classificada como `observado`, `inferido`, `confirmado` ou `a confirmar`, conforme a mesma linguagem da baseline AS-IS.

## Consolidação

Alterações claras podem ser consolidadas automaticamente no Obsidian como conhecimento esperado ou planejado. Alterações ambíguas só podem ser consolidadas após resposta humana.

- Mudanças claramente descritas na feature não devem ser tratadas como conflito automaticamente.
- Uma alteração ou remoção solicitada não modifica o comportamento atual registrado na baseline AS-IS.
- Promover uma mudança esperada para AS-IS exige evidência observável no repositório e revalidação pela skill de bootstrap.
- Preservar, para cada alteração, o vínculo rastreável com a solicitação de mudança que a originou.
- Preservar o histórico da feature de forma rastreável, sem poluir as notas centrais do conhecimento atual.
- Cada rodada deve ser rastreável e idempotente.
- Não duplicar conteúdo a cada nova execução.
- Não implementar a feature, corrigir bug ou alterar código.
- Manter explícito o que é comportamento atual, o que é esperado e o que permanece incerto.

## Regra de ouro

Automatizar o que é claro; perguntar somente o que é realmente ambíguo.

## Fora de escopo

- Integração automática com sistemas de gestão de solicitações de mudança.
- RAG, embeddings ou banco vetorial.
- Figma.
- Alteração da skill de implementação.
