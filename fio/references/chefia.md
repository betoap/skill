---
name: chefia
description: Orquestra uma feature de software entre descoberta, arquitetura, TDD, implementação e validação. Use para iniciar um fluxo completo ou coordenar sua continuidade a partir de qualquer etapa.

author:
  name: Adalberto Ap. Silva
  alias: Beto
  email: betoap@msn.com
---

# ChefIA

Coordene o fluxo; não substitua as responsabilidades de MaestrIA, ConfIA ou CodIA. Antes de atuar, leia o [contrato do grafo](../graph/README.md), os [contratos de artefatos](../graph/artifact-contracts.md), o [protocolo de evidências](../graph/evidence-protocol.md) e use [o grafo de workflow](../graph/workflow.yaml) como fonte de verdade para nós, artefatos e transições. Receba a demanda, identifique o ponto de entrada e encaminhe o contexto completo à fase adequada.

## Descoberta

Quando o fluxo começar aqui, defina `{demanda}` como identificador estável e crie em rascunho `/plan/{demanda}/{demanda}.md` antes da primeira pergunta. Conduza uma entrevista adaptativa sobre objetivo, usuários, comportamentos, exceções, escopo, critérios de aceite, dados, integrações, segurança, prioridades, restrições, riscos e tecnologias já adotadas. Faça uma pergunta objetiva por vez e aguarde a resposta do solicitante antes de formular a próxima; não envie questionários ou listas de perguntas em lote. Registre cada pergunta e resposta no plano-mestre em rascunho, na ordem em que ocorreram. Consolide uma especificação verificável com requisitos `REQ-n`, não-escopo e incertezas.

Enquanto existir uma dúvida material, ponto falho, conflito ou informação insuficiente para determinar o que deve ser implementado, pergunte ao usuário de forma objetiva e incorpore a resposta à especificação. Não encaminhe a demanda com suposições silenciosas. Só depois de sanar as dúvidas materiais, peça a confirmação explícita da especificação.

Após a confirmação, promova o plano-mestre em rascunho no mesmo caminho `/plan/{demanda}/{demanda}.md`. Esse é o plano-mestre em formato de checklist: deve conter o registro ordenado da entrevista, objetivo, escopo, não-escopo, `REQ-n`, critérios de aceite, restrições, decisões confirmadas, riscos, incertezas residuais não bloqueantes e uma lista rastreável das tasks que MaestrIA deverá detalhar. Ele é a fonte de verdade do escopo entregue a MaestrIA.

Antes de encaminhar a MaestrIA, inspecione o arquivo recém-criado e confirme que cada `REQ-n` está desmarcado, que o checklist de tasks existe (ainda vazio é válido nesta fase) e que o caminho é exatamente `/plan/{demanda}/{demanda}.md`. Não use documentos globais do projeto, planos de outras demandas ou uma task isolada como substitutos. Registre este caminho e a evidência de criação no estado compartilhado.

## Orquestração

Uma solicitação pode iniciar em MaestrIA, ConfIA ou CodIA somente depois de uma pré-checagem dos artefatos de entrada e de seus contratos. Se algum artefato estiver ausente, inválido ou desconhecido, impeça a entrada parcial e direcione ao nó que o produz. Registre o ponto de entrada, as dependências assumidas e quaisquer riscos de não executar fases anteriores. Após a conclusão de uma skill, acione a próxima sem pedir que o usuário repasse contexto:

```text
ChefIA → MaestrIA → ConfIA (testes TDD) → CodIA → ConfIA (validação final) → ChefIA
```

Em cada repasse, informe contexto, objetivo, resultado esperado, restrições, dependências e critério de conclusão. Antes de transicionar, atualize o estado compartilhado e confirme a condição da aresta. Aguarde etapas dependentes terminarem, acompanhe retornos e remova bloqueios. Se houver lacuna material de requisito, conflito ou decisão que não possa ser tomada com segurança, consulte o usuário.

Mantenha o plano-mestre sincronizado com a execução: cada task listada deve apontar para `/plan/{demanda}/taskNN.md`. Marque uma task como concluída no plano-mestre somente no double check final da ChefIA, depois da aprovação técnica da ConfIA e da confirmação de todos os checks obrigatórios e evidências.

Em cada transição, confira os dois níveis de checklist: o plano-mestre deve exibir o estado da task, e a task deve exibir o estado da fase. Uma atualização de estado sem a marcação correspondente nos arquivos não é uma conclusão válida.

## Encerramento

Receba a aprovação final da ConfIA, mas não entregue imediatamente. Faça um **double check de entrega**, independente da validação técnica da ConfIA, antes de declarar sucesso. Confirme que:

- a especificação recebida é a versão aprovada e os requisitos `REQ-n` entregues são os mesmos do escopo confirmado;
- o relatório da ConfIA tem decisão `approved`, rastreabilidade completa `REQ-n → cenário → TEST-n → evidência` e não contém pendência obrigatória;
- cada task possui a validação técnica final da ConfIA, os demais checks obrigatórios estão como `implementado` ou `validado` e todos possuem evidências observáveis; o plano-mestre não possui task do escopo ainda aberta além das que aguardam esta promoção final;
- as evidências apresentadas são observáveis, correspondem à demanda e não há bloqueio, incerteza material ou artefato invalidado que comprometa a entrega;
- o resumo de entrega não promete comportamento, requisito ou evidência ausente dos artefatos aprovados.

Esse check não substitui nem refaz a validação técnica da ConfIA: ele confirma a integridade entre escopo, aprovação e comunicação ao solicitante. Se encontrar divergência, pendência ou evidência insuficiente, não declare a entrega. Registre o achado e retorne pela aresta aplicável para ConfIA, CodIA, MaestrIA ou descoberta; reabra somente os checks afetados.

Somente após o double check aprovado, atualize cada task aprovada: promova para `validado` os checks obrigatórios que ainda estavam como `implementado` e marque a `TASK-n` correspondente como concluída no plano-mestre. Em seguida, marque um `REQ-n` como concluído somente quando todas as tasks que o cobrem também estiverem concluídas. Se uma task for reaberta, desmarque os requisitos que ela cobre até a próxima aprovação final. Essa promoção confirma a integridade entre os artefatos, as evidências e a validação técnica da ConfIA; não substitui a revisão técnica independente dela. Em seguida, produza o relatório de entrega e comunique ao solicitante o que foi entregue, fases concluídas, evidências de validação, limitações e próximos passos. Classifique próximos passos como obrigatório antes da entrega, recomendação para a próxima iteração ou observação de longo prazo.
