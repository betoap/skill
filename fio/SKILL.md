---
name: fio
version: 1.2.1
description: Fluxo de Implementação Orientada para conduzir uma feature da descoberta à validação final, combinando arquitetura, TDD, implementação e controle de evidências. Use para executar ou retomar o fluxo completo de uma feature.

author:
  name: Adalberto Ap. Silva
  alias: Beto
  email: betoap@msn.com
---

# FIO — Fluxo de Implementação Orientada

## Distribuição e versão

Esta pasta é a fonte canônica da FIO. Ambientes de execução devem referenciá-la diretamente, preferencialmente por link simbólico, e nunca manter uma cópia editável independente. Antes de iniciar uma demanda, registre no estado `skill_name`, `skill_version` e `skill_source`; se a versão ou a origem em uso não puderem ser verificadas, bloqueie o fluxo antes da descoberta. Uma atualização da skill é concluída somente quando o ambiente de execução volta a resolver para esta mesma fonte canônica.

Conduza a demanda como um grafo de trabalho auditável. Esta é uma skill única, mas cada fase mantém os limites de responsabilidade originais: descoberta e orquestração (ChefIA), arquitetura e plano (MaestrIA), desenho/validação de testes (ConfIA) e implementação (CodIA). Não omita fases, nem faça uma fase assumir responsabilidades de outra.

## Preparação obrigatória

Antes de atuar, leia o [contrato do grafo](graph/README.md), os [contratos de artefatos](graph/artifact-contracts.md), o [protocolo de evidências](graph/evidence-protocol.md) e o [grafo de workflow](graph/workflow.yaml). Crie ou atualize o estado da demanda conforme definido no contrato do grafo. O grafo é a fonte de verdade para nós, artefatos, condições de transição, retornos e invariantes.

Identifique o ponto de entrada. Só inicie uma fase quando todos os artefatos declarados para ela estiverem presentes, atuais e aderentes aos seus contratos. Quando uma entrada parcial for válida, registre as dependências assumidas e os riscos das etapas puladas; quando não for válida, redirecione ao nó produtor. Antes de cada transição, atualize o estado compartilhado e registre a evidência da condição da aresta. Reconcilie o estado com o plano-mestre e as tasks antes de transicionar: caminhos, requisitos, checks, status e evidências devem coincidir. Registre cada artefato declarado como entrada ou saída de um nó de forma estruturada no estado, incluindo identificador, produtor, status, caminho ou referência, contexto de criação, incertezas e evidências observáveis. Registre também cada check de fase individualmente, com task, responsável, status e evidência. Texto livre em uma transição não substitui esses registros.

## Plano por demanda

O ChefIA só encaminha a demanda após confirmar com o usuário que não restam dúvidas materiais sobre o que será implementado. Ele deve conduzir perguntas objetivas enquanto houver ambiguidade, conflito, lacuna de escopo, comportamento, critério de aceite ou restrição que impeça uma implementação segura. Registre respostas, decisões e não-escopo na especificação aprovada.

Antes da primeira pergunta da entrevista, o ChefIA define `{demanda}` como identificador estável e cria o plano-mestre em rascunho em `/plan/{demanda}/{demanda}.md`. Ele registra ali cada pergunta e resposta; após a confirmação explícita, promove o mesmo arquivo a plano-mestre aprovado. Esse arquivo é um checklist do escopo confirmado, dos requisitos e do acompanhamento das tasks; ele é a fonte de verdade do escopo funcional.

Este é um artefato novo e exclusivo da demanda: não reutilize, renomeie, complete ou marque como evidência um plano geral, um README, uma task de outra demanda ou qualquer documento preexistente. Se o identificador ou o diretório ainda não estiverem definidos, não avance para MaestrIA. Crie primeiro o diretório `/plan/{demanda}/` e o plano-mestre exatamente nesse caminho, a partir do modelo de plano. Cada requisito e cada task deve aparecer como item de checklist não concluído; uma marcação só pode mudar com o responsável, a fase e a evidência observável registrados no próprio documento.

Com base exclusivamente nesse plano-mestre e na arquitetura existente, o MaestrIA cria todas as tasks necessárias em `/plan/{demanda}/task01.md`, `/plan/{demanda}/task02.md` e assim por diante. Cada task é um checklist independente e deve referenciar os `REQ-n` que cobre. Nenhum requisito confirmado pode ficar sem uma task rastreável.

Não substitua essas tasks por uma lista narrativa, uma task avulsa em outro diretório ou documentação global do projeto. Antes da transição para ConfIA, confirme por inspeção que o plano-mestre existe, que todas as tasks referenciadas existem no mesmo diretório da demanda e que todo `REQ-n` possui ao menos uma task vinculada.

Antes de concluir uma fase de uma task, a fase responsável marca o check correspondente no próprio `taskNN.md`, registra o estado e acrescenta a evidência observável. MaestrIA, ConfIA no desenho TDD e CodIA registram suas entregas como `implementado`; ConfIA registra a validação técnica final como `validado`. No encerramento, ChefIA faz o double check de integridade e somente então promove todos os checks obrigatórios da task para `validado` e marca a task correspondente no plano-mestre como concluída.

Trate os arquivos de plano e task como o painel de controle da demanda: eles devem permanecer legíveis e atuais durante todo o fluxo. Não comunique conclusão de fase, task ou entrega se os respectivos checklists não refletirem esse estado. Se um check ou evidência estiver ausente, mantenha-o pendente e bloqueie a transição aplicável.

Um `REQ-n` do plano-mestre só pode ser marcado como concluído pela ChefIA no double check final quando todas as tasks que o cobrem estiverem concluídas e validadas. Se uma task vinculada a esse requisito for reaberta por falha, desmarque também o `REQ-n` até que a correção complete novamente o ciclo de validação.

## Roteamento por fase

- Para descoberta, confirmação da especificação, criação do plano-mestre, coordenação entre fases e entrega, siga integralmente [ChefIA](references/chefia.md).
- Para análise do projeto, decisões técnicas, perfil de stack e plano de execução, siga integralmente [MaestrIA](references/maestria.md) e o [modelo de plano](references/plano.md).
- Para o desenho TDD antes da implementação ou para a validação final independente, siga integralmente [ConfIA](references/confia.md).
- Para implementar uma tarefa ou fase depois do desenho TDD, siga integralmente [CodIA](references/codia.md).

Ao executar o fluxo completo, siga esta sequência e as condições exatas do grafo:

```text
ChefIA → MaestrIA → ConfIA (testes TDD) → CodIA → ConfIA (validação final) → ChefIA
```

Em qualquer retorno, percorra somente a aresta de retorno aplicável, invalide apenas os artefatos afetados e reabra os checks correspondentes. Não declare uma aprovação baseada apenas em testes verdes: mantenha a rastreabilidade `REQ-n → cenário → TEST-n → evidência`, a revisão final independente da ConfIA contra a especificação aprovada e o double check de entrega da ChefIA antes de comunicar sucesso.

## Contextos isolados e trabalho paralelo

Cada task de implementação deve ser executada em contexto isolado — por exemplo, sessão, agente, worktree ou ambiente equivalente — separado de qualquer outra task. Antes de iniciar, CodIA registra no estado a task, o contexto atribuído, os arquivos ou módulos permitidos e suas dependências. Se a plataforma não oferecer contexto isolado, registre essa limitação, execute uma única task por vez e bloqueie qualquer paralelismo.

Quando houver duas ou mais tasks independentes e a plataforma suportar agentes, CodIA deve distribuí-las entre múltiplos agentes. Antes de delegar, divida por task, módulo, arquivo ou conjunto de cenários sem sobreposição e registre no estado o responsável, escopo e dependências de cada frente. Não delegue em paralelo mudanças no mesmo arquivo, na mesma task ou no mesmo check sem um plano explícito de integração.

Cada fase mantém um agente coordenador responsável por consolidar os resultados, verificar as evidências, resolver conflitos e atualizar a task, o plano-mestre e o estado. Agentes delegados não concluem tasks, não marcam checks globais e não autorizam transições: eles devolvem alterações, testes e evidências ao coordenador. A ConfIA que faz a validação final deve permanecer independente da implementação que está aprovando.

Use paralelismo apenas quando as dependências declaradas permitirem. Se o resultado de uma frente alterar o contrato, os requisitos, a arquitetura, a matriz de testes ou os arquivos de outra frente, interrompa as frentes afetadas, reconcilie o plano e retome somente depois da atualização correspondente.

## Integração opcional pela CIM

Por padrão, a FIO recebe uma demanda diretamente, executa seu fluxo completo e encerra com o relatório de entrega. Ela não aciona a DIO automaticamente.

Quando for acionada pela CIM, receba o **contexto da mudança** da SIM e o `cycle_id` compartilhado. Registre-os como contexto de entrada, sem pular a descoberta nem substituir a confirmação de escopo pela ChefIA. Após o double check da ChefIA, produza a **evidência de entrega** para a CIM encaminhar à DIO: escopo implementado e não implementado, relatório de validação técnica, evidências de execução e entrega, limitações, pendências e referências ao plano-mestre e às tasks. Só registre esse handoff quando houver ciclo CIM identificado; ele não prova AS-IS por si só.

## Recursos operacionais

- Use [perfil de stack](graph/stack-profile.md) para registrar apenas o stack confirmado no projeto; divergências exigem retorno à fase arquitetural.
- Use [cenários de validação](graph/validation-scenarios.md) para validar a própria suite em casos controlados.
- O [template de estado](graph/workflow-state.template.yaml) define o formato inicial do estado operacional.
