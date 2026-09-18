---
name: cim
version: 1.0.1
description: Orquestra o ciclo de uma solicitação de mudança entre SIM, FIO e DIO, validando handoffs, rastreabilidade e encerramento após confirmação AS-IS. Use para coordenar uma mudança de ponta a ponta; não use para interpretar, implementar ou revalidar em lugar dessas skills.

author:
  name: Adalberto Ap. Silva
  alias: Beto
  email: betoap@msn.com
---

# CIM — Ciclo Integrado de Mudanças

## Distribuição e versão

Esta pasta é a fonte canônica da CIM. Ambientes de execução devem referenciá-la diretamente, preferencialmente por link simbólico, e nunca manter uma cópia editável independente. Antes de iniciar, registre no estado `skill_name`, `skill_version` e `skill_source`. Se a versão ou a origem não puderem ser verificadas, bloqueie o ciclo antes do recebimento.

## Papel da CIM

A CIM coordena o ciclo completo de uma solicitação de mudança entre:

- SIM, que interpreta a solicitação e consolida conhecimento esperado;
- FIO, que esclarece, planeja, implementa e valida tecnicamente a mudança;
- DIO, que reanalisa o repositório e confirma o AS-IS.

A CIM mantém o identificador compartilhado, o estado do ciclo, os artefatos de handoff e as transições. Ela não substitui nenhuma dessas responsabilidades, não altera código e não confirma AS-IS por conta própria.

SIM, FIO e DIO permanecem utilizáveis separadamente. A CIM só cria, exige ou encaminha handoffs quando iniciar ou assumir explicitamente um ciclo de mudança.

## Preparação obrigatória

Antes de atuar, leia o [contrato do grafo](graph/README.md), os [contratos de artefatos](graph/artifact-contracts.md), o [protocolo de evidências](graph/evidence-protocol.md) e o [grafo de workflow](graph/workflow.yaml). Crie ou atualize o estado conforme o contrato do grafo.

Confirme que SIM, FIO e DIO estão disponíveis em suas fontes canônicas e que a solicitação, projeto e vault relacionados estão identificados. Uma skill indisponível, uma origem não verificável ou um artefato obrigatório ausente bloqueia a transição aplicável; não substitua a skill ausente com uma execução improvisada.

## Identificador e handoffs

Defina um identificador estável de ciclo antes de encaminhar a solicitação à SIM. Esse identificador deve ser mantido no registro da solicitação, no plano-mestre e tasks da FIO, na revalidação da DIO e no estado da CIM.

Somente encaminhe uma fase quando o handoff anterior cumprir seu contrato:

- SIM → FIO: contexto da mudança, conhecimento esperado, impacto, certeza, pendências e vínculos de origem;
- FIO → DIO: escopo implementado, relatório técnico, evidências de execução e entrega, limitações e pendências;
- DIO → encerramento: evidência observável do repositório, resultado por item e atualização ou preservação da baseline AS-IS.

## Fluxo do ciclo

```text
Recebimento → SIM → FIO → DIO → Encerramento
```

1. Registre a solicitação e crie o ciclo.
2. Acione a SIM e valide sua saída antes de preparar a demanda da FIO.
3. Acione a FIO e valide a entrega técnica antes de solicitar a reanálise da DIO.
4. Acione a DIO para observar o repositório; a evidência de entrega da FIO é um gatilho, não uma prova de AS-IS.
5. Encerre somente depois de registrar o resultado da DIO: `confirmada_asis`, `parcial`, `nao_confirmada` ou `bloqueada`.

Quando a FIO alterar materialmente o escopo, retorne à SIM ou à etapa de esclarecimento aplicável. Quando a DIO não encontrar a mudança no repositório, preserve o AS-IS e reabra ou não confirme o ciclo conforme a evidência.

## Regras de orquestração

- Não inicie a FIO sem um handoff válido da SIM, salvo início parcial explicitamente registrado com riscos e dependências.
- Não solicite confirmação final à DIO sem entrega tecnicamente validada pela FIO, salvo evidência independente de repositório explicitamente registrada.
- Não marque uma mudança como realizada apenas porque a FIO entregou ou porque a SIM descreveu o comportamento esperado.
- Não encerre como `confirmada_asis` sem revalidação observável da DIO.
- Toda transição registra artefato, evidência, itens invalidados, próximo responsável e bloqueios.
- Ao retomar um ciclo, reconcilie o estado e os handoffs existentes; não duplique planos, histórico, vínculos ou atualizações no vault.
- Ao assumir uma mudança iniciada fora da CIM, crie ou atualize o estado do ciclo, vincule o resultado existente ao `cycle_id` e valide-o contra o contrato da etapa correspondente antes de avançar. Registre riscos e dependências se a entrada for parcial.

## Limites

A CIM não interpreta uma solicitação no lugar da SIM, não implementa ou valida tecnicamente no lugar da FIO e não cria ou altera a baseline AS-IS no lugar da DIO. Ela não integra automaticamente com Kanban ou outros sistemas de gestão, não usa RAG, embeddings, banco vetorial ou Figma, e não altera as skills coordenadas.

## Recursos operacionais

- Use o [template de estado](graph/workflow-state.template.yaml) para iniciar o estado operacional do ciclo.
- Use os [cenários de validação](graph/validation-scenarios.md) para verificar a orquestração em casos controlados.
