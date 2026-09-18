---
name: dio
version: 1.0.1
description: Analisa um projeto existente e cria ou atualiza uma baseline AS-IS de conhecimento no Obsidian, distinguindo fatos observados, inferências, confirmações e pontos a confirmar. Use para bootstrap de conhecimento de projeto; não use para implementar funcionalidades ou documentar detalhes de código.

author:
  name: Adalberto Ap. Silva
  alias: Beto
  email: betoap@msn.com
---

# DIO — Documentação Inicial Obsidian

## Distribuição e versão

Esta pasta é a fonte canônica da skill. Ambientes de execução devem referenciá-la diretamente, preferencialmente por link simbólico, e nunca manter uma cópia editável independente. Antes de iniciar, registre no estado `skill_name`, `skill_version` e `skill_source`. Se a versão ou a origem não puderem ser verificadas, bloqueie o fluxo antes da análise.

Conduza a demanda como um grafo de conhecimento auditável. O repositório é a fonte de verdade da implementação AS-IS; o vault do Obsidian é a base de conhecimento de projeto. A implementação pode ser examinada para sustentar conclusões, mas classes, métodos, funções, testes, lint e outros detalhes de implementação não devem ser copiados para o vault.

## Preparação obrigatória

Antes de atuar, leia o [contrato do grafo](graph/README.md), os [contratos de artefatos](graph/artifact-contracts.md), o [protocolo de evidências](graph/evidence-protocol.md) e o [grafo de workflow](graph/workflow.yaml). Crie ou atualize o estado da demanda conforme o contrato do grafo. O grafo é a fonte de verdade para nós, artefatos, condições de transição, retornos e invariantes.

Defina os limites do trabalho antes da análise: projeto, caminho do vault, documentação adicional e contexto fornecido. Se o caminho do vault não existir, ou se não houver autorização para criá-lo ou alterá-lo, consolide apenas o relatório preliminar e bloqueie a publicação. Nunca registre secrets ou credenciais.

## Princípios de conhecimento

- Trate o comportamento observável no projeto como AS-IS, não como confirmação de que o produto está correto.
- Diferencie sempre o que existe do que deveria existir, do que é inferido e do que ainda não é conhecido.
- Classifique cada afirmação material como `observado`, `inferido`, `confirmado` ou `a_confirmar`.
- Não transforme inferências em fatos automaticamente. Quando faltarem evidências, use `A_CONFIRMAR` ou `INFERIDO` de forma explícita.
- Confronte código, documentação adicional e contexto fornecido. Não tente reconstruir a intenção original sem base observável.
- Não pergunte qual é o AS-IS quando ele puder ser observado. Pergunte ao usuário somente como interpretar divergências materiais ou lacunas que bloqueiem a consolidação.

## Fronteira com Solicitações de Mudança

A DIO é a única responsável por criar ou revalidar a baseline AS-IS. Solicitações de mudança, planos, critérios de aceite e outros materiais que descrevam alteração pretendida são fontes de conhecimento esperado, não evidência de que o comportamento atual já mudou.

Quando uma fonte descreve uma mudança futura, mantenha-a vinculada à sua origem e registre-a como `esperado`, `planejado` ou `a_confirmar`, conforme a evidência disponível. Não substitua, remova ou reclassifique uma afirmação AS-IS por causa dessa fonte. A promoção para AS-IS só ocorre após evidência observável no repositório durante uma nova análise da DIO.

## Roteamento por fase

- Para inventariar fontes, delimitar escopo e produzir conhecimento preliminar, siga [análise AS-IS](references/analise-asis.md).
- Para confrontar fontes e conduzir a validação humana de divergências, siga [confronto e validação](references/confronto-validacao.md).
- Para organizar e publicar conhecimento no vault sem duplicação, siga [consolidação no Obsidian](references/consolidacao-obsidian.md).

Siga esta sequência e as condições do grafo:

```text
Descoberta → Análise AS-IS → Confronto de fontes → Validação humana → Consolidação no Obsidian
```

Uma validação humana só é necessária quando houver divergência material, interpretação de esperado, ou incerteza que impeça uma afirmação segura. Se não houver itens a confirmar, a fase de validação pode registrar `not_required` e avançar. Não corrija a implementação automaticamente: quando o esperado divergir do AS-IS, registre a divergência e a necessidade de uma demanda de correção separada.

## Estrutura progressiva do vault

Crie somente notas que representem conhecimento realmente consolidado. Uma baseline pode começar por `Projeto.md` e `Produto.md`, complementadas por notas de funcionalidades, regras de negócio, fluxos, arquitetura em alto nível, integrações, conceitos, incertezas e divergências quando houver conteúdo suficiente.

Use links internos apenas para relações reais de conhecimento. Use front matter somente quando melhorar a recuperação futura. Preserve notas validadas por humanos: uma nova execução deve reconciliar conteúdo, registrar mudanças e nunca duplicar conteúdo ou sobrescrever silenciosamente uma decisão humana.

### Reinicialização explícita

O comportamento padrão é idempotente: leia as notas existentes, reconcilie o conhecimento e preserve decisões humanas. A DIO só pode ignorar a baseline anterior e reconstruir suas notas quando o usuário fizer um pedido explícito, por escrito, de **reinicialização com sobrescrita** e identificar o vault ou escopo-alvo.

Esse modo não é inferido de pedidos como “rode novamente”, “atualize” ou “comece de novo”. Antes de escrever, registre no estado o texto da autorização, o escopo afetado e a data lógica. Reanalise as fontes do projeto do zero e substitua somente as notas que pertencem ao escopo declarado da DIO; não apague nem altere notas não relacionadas do vault. O relatório de consolidação deve declarar que a execução ocorreu em modo de reinicialização e listar cada nota substituída.

## Integração opcional pela CIM

Por padrão, a DIO cria ou revalida a baseline AS-IS e encerra sua execução sem acionar outra skill. Quando for acionada pela CIM, receba o `cycle_id`, o contexto de mudança da SIM e a evidência de entrega da FIO apenas como guia de reanálise. A confirmação continua baseada em evidência observável no repositório.

Ao concluir a reanálise dentro desse ciclo, produza a **revalidação AS-IS** para a CIM: conhecimentos esperados avaliados, evidência observável, resultado por item (`confirmado`, `parcial`, `nao_encontrado` ou `bloqueado`), atualizações ou preservação da baseline e pendências ou retorno necessário. Só registre esse handoff quando houver ciclo CIM identificado.

## Recursos operacionais

- Use o [template de estado](graph/workflow-state.template.yaml) para iniciar o estado operacional no projeto analisado.
- Use os [cenários de validação](graph/validation-scenarios.md) para verificar o comportamento da skill em casos controlados.
