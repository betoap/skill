# Contratos de artefatos

Todo artefato usa um identificador estável, produtor, status (`draft`, `current`, `invalidated` ou `approved`), fontes de evidência e incertezas. Não preencha campos sem base observável.

## Especificação aprovada

- identificador da demanda e objetivo;
- requisitos funcionais identificados (`REQ-n`), critérios de aceite e não-escopo;
- regras de negócio, exceções, integrações, restrições e riscos;
- confirmação explícita do solicitante;
- itens desconhecidos ou dependentes de decisão.
- registro ordenado da entrevista, com cada pergunta da ChefIA e a resposta correspondente do solicitante.

## Arquitetura e plano

- decisões e justificativas, módulos, contratos, impacto e compatibilidade;
- plano-mestre do ChefIA em `/plan/{demanda}/{demanda}.md`, com escopo confirmado, requisitos, critérios de aceite e checklist rastreável de tasks;
- tarefas (`TASK-n`) em `/plan/{demanda}/taskNN.md`, com dependências, escopo, critérios de aceite, requisitos cobertos e checks por fase;
- perfil de stack e evidências de leitura do projeto;
- riscos e decisões que exigiriam retorno a ChefIA.

## Estratégia de testes e matriz de rastreabilidade

Para cada `REQ-n`, registre cenários positivos, negativos, bordas, segurança e integração quando aplicáveis. Cada cenário referencia pelo menos um teste (`TEST-n`), e cada teste referencia os requisitos que cobre. Registre também o que não será testado e a justificativa.

## Evidências de teste e implementação

Registre comando ou ação executada, ambiente, resultado observado, data lógica da execução, arquivos envolvidos e vínculo com `TEST-n` ou `TASK-n`. Para testes vermelhos, registre o motivo esperado da falha; para verdes, registre a saída que demonstra sucesso. Uma alegação sem evidência fica como `unknown`, nunca como aprovação.

Quando houver referência visual aprovada, registre também a referência, o contexto ou viewport comparado, a implementação renderizada, os aspectos avaliados e o resultado da comparação lado a lado. Sem essa evidência, a task não pode receber aprovação visual.

## Relatório de validação

Inclua matriz requisito → cenário → teste → evidência → status, resultados de regressão, achados, limitações, artefatos invalidados e a decisão `approved`, `rejected` ou `conditional`. Uma decisão condicional lista pendências, responsável e condição de encerramento.

## Relatório de entrega

Produzido pela ChefIA somente após o double check de entrega. Registre a versão da especificação conferida, o relatório de validação técnica da ConfIA e os checklists finalizados consultados, a confirmação de que não há pendências obrigatórias ou tasks abertas, o resultado `approved` ou `blocked`, achados e a comunicação final. Um relatório `blocked` não é entrega concluída e deve indicar o retorno necessário.
