---
name: sim
version: 1.0.1
description: Interpreta uma solicitação de mudança e incrementa o conhecimento esperado do produto no Obsidian, com análise de impacto e rastreabilidade. Use para consolidar mudanças propostas; não use para criar ou alterar a baseline AS-IS, implementar código ou operar um sistema de gestão de demandas.

author:
  name: Adalberto Ap. Silva
  alias: Beto
  email: betoap@msn.com
---

# SIM — Solicitação Incremental de Mudança

## Distribuição e versão

Esta pasta é a fonte canônica da SIM. Ambientes de execução devem referenciá-la diretamente, preferencialmente por link simbólico, e nunca manter uma cópia editável independente. Antes de iniciar, registre no estado `skill_name`, `skill_version` e `skill_source`. Se a versão ou a origem não puderem ser verificadas, bloqueie o fluxo antes da interpretação.

Conduza cada solicitação como um grafo de conhecimento auditável. A solicitação de mudança é uma origem temporária; o vault do Obsidian mantém conhecimento persistente; o repositório continua sendo a fonte de implementação.

## Preparação obrigatória

Antes de atuar, leia o [contrato do grafo](graph/README.md), os [contratos de artefatos](graph/artifact-contracts.md), o [protocolo de evidências](graph/evidence-protocol.md) e o [grafo de workflow](graph/workflow.yaml). Crie ou atualize o estado conforme o contrato do grafo.

Receba o conteúdo colado manualmente pelo usuário, sem assumir estrutura fixa. Descrição, critérios de aceite e metadados podem estar presentes, mas todos os campos devem ser tratados como texto. Identifique projeto, vault e solicitação; se uma dessas referências for necessária e estiver ausente, registre o bloqueio antes de consolidar.

## Fronteira com a DIO

A DIO é a única responsável por criar ou revalidar a baseline AS-IS a partir de evidência observável no repositório. A SIM é independente e responsável somente por analisar a solicitação e registrar conhecimento `esperado`, `planejado` ou `a_confirmar`.

Uma solicitação não é evidência de que o comportamento atual já mudou. Portanto, a SIM nunca promove conteúdo para AS-IS, nem substitui, remove ou reclassifica uma afirmação atual. Uma mudança esperada só é promovida a AS-IS após uma nova análise da DIO ou evidência observável equivalente no repositório.

## Princípios de interpretação

- Extraia somente conhecimento de produto: regras de negócio, fluxos, atores, conceitos, integrações e comportamentos descritos ou sugeridos.
- Não documente classes, métodos, funções, testes, lint ou detalhes de implementação.
- Classifique o impacto em `novo`, `complementa`, `altera`, `remove`, `divergência` ou `dúvida`.
- Classifique também cada afirmação material como `observado`, `inferido`, `confirmado` ou `a_confirmar`; o tipo de impacto não substitui a classificação de certeza.
- Não trate uma mudança claramente descrita como conflito apenas por ser nova. Validação humana é necessária somente para ambiguidade real, mais de uma interpretação plausível ou divergência material.
- Não invente intenção, regra ou comportamento ausente da solicitação e do conhecimento disponível.

## Roteamento por fase

- Para interpretar a solicitação e identificar conhecimento potencial, siga [interpretação da solicitação](references/interpretacao.md).
- Para comparar a solicitação com o vault e classificar o impacto, siga [análise de impacto](references/analise-impacto.md).
- Para registrar conhecimento esperado e preservar histórico sem duplicação, siga [consolidação incremental](references/consolidacao.md).

Siga esta sequência e as condições do grafo:

```text
Recebimento → Interpretação → Análise de impacto → Validação humana, quando necessária → Consolidação incremental
```

## Consolidação e histórico

Alterações claras podem ser consolidadas automaticamente como conhecimento esperado ou planejado. Alterações ambíguas só podem ser consolidadas após resposta humana. Cada item consolidado deve manter vínculo rastreável com a solicitação que o originou.

Preserve o histórico da solicitação em uma nota ou registro próprio, sem transformar as notas centrais de conhecimento atual em um log de demandas. Antes de criar conteúdo, procure notas e registros existentes que cubram a mesma solicitação ou o mesmo conhecimento esperado. Reconcilie e atualize de forma idempotente; não duplique conteúdo a cada execução.

## Integração opcional pela CIM

Por padrão, a SIM é independente: conclui a análise e não encaminha informações automaticamente. Quando for acionada pela CIM, receba e preserve o `cycle_id` compartilhado no estado e nos artefatos relacionados.

Após a consolidação, produza o **contexto da mudança** para a CIM encaminhar à FIO. Ele deve referenciar a solicitação de origem, conhecimento esperado ou planejado, análise de impacto, classificações de certeza, dúvidas, decisões humanas, pendências e vínculos com notas e histórico. Só registre esse handoff quando houver ciclo CIM identificado; ele não substitui o resultado normal da SIM.

## Fora de escopo

- Implementar a solicitação, corrigir bugs ou alterar código.
- Alterar a baseline AS-IS ou promover automaticamente comportamento esperado para atual.
- Integração automática com sistemas de gestão de solicitações de mudança.
- RAG, embeddings, banco vetorial ou Figma.
- Alterar a DIO ou a FIO.

## Recursos operacionais

- Use o [template de estado](graph/workflow-state.template.yaml) para iniciar o estado operacional da solicitação.
- Use os [cenários de validação](graph/validation-scenarios.md) para verificar o comportamento da SIM em casos controlados.
