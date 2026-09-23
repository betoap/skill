# FIO — Fluxo de Implementação Orientada

## Objetivo

A FIO conduz uma feature de software da descoberta à entrega final, combinando especificação, arquitetura, TDD, implementação e validação baseada em evidências.

Ela é um grafo de trabalho auditável, não um prompt linear. As fases só avançam quando seus artefatos de entrada existem, estão atuais, atendem aos contratos e possuem evidências observáveis.

## Fonte canônica e estado operacional

A pasta da FIO é sua fonte canônica. Antes de iniciar uma demanda, o ambiente deve registrar nome, versão e origem verificável da skill. Se isso não puder ser confirmado, a descoberta é bloqueada.

Para cada demanda, a FIO cria ou atualiza `.fio/workflow-state.yaml` no projeto atendido. O estado registra a demanda, o nó atual, artefatos, requisitos, tasks, checks, frentes de trabalho, evidências, transições, bloqueios e incertezas. Ele é um painel operacional; não substitui o plano-mestre ou as tasks.

## Papéis internos

| Papel | Responsabilidade |
| --- | --- |
| ChefIA | Descoberta, confirmação da especificação, plano-mestre, coordenação entre fases e entrega final. |
| MaestrIA | Análise arquitetural, perfil de stack, decisões técnicas e plano detalhado das tasks. |
| ConfIA | Desenho TDD antes da implementação e validação técnica independente depois da implementação. |
| CodIA | Implementação orientada pelos testes, pelo plano e pelos contratos aprovados. |

Nenhum papel assume a responsabilidade do outro. A validação final da ConfIA deve ser independente de quem implementou a mudança.

## Fluxo principal

```text
ChefIA → MaestrIA → ConfIA: testes TDD → CodIA → ConfIA: validação final → ChefIA
```

O fluxo também prevê retornos explícitos quando houver lacuna de especificação, inconsistência arquitetural, problema no desenho de testes ou falha de implementação. Em um retorno, somente os artefatos e checks afetados são invalidados e reabertos.

## Integração no ciclo de mudança

Esta integração só se aplica quando a FIO fizer parte de um ciclo coordenado pela CIM. Em uso independente, a FIO recebe a demanda diretamente, executa seu fluxo normal e não encaminha informações automaticamente para a DIO.

Dentro do ciclo da CIM, a FIO recebe da SIM o **contexto da mudança**: solicitação de origem, conhecimento esperado, impactos, classificações, dúvidas, decisões e vínculos para o conhecimento relacionado. Esse contexto não substitui a descoberta e a confirmação de escopo pela ChefIA.

Após o double check de entrega, a FIO deve encaminhar à DIO uma **evidência de entrega** com:

- identificador compartilhado da mudança;
- escopo implementado e não implementado;
- relatório de validação técnica;
- evidências de execução e entrega;
- limitações, pendências e retornos relevantes;
- referências ao plano-mestre e às tasks.

Essa entrega orienta a reanálise da DIO, mas não comprova sozinha que o comportamento já é AS-IS.

No estado operacional, esse handoff é identificado como `fio_delivery_evidence`. Ele é gerado e localizado pela CIM; quem usa a skill não precisa criar ou transportar esse artefato manualmente.

## Descoberta e especificação — ChefIA

No início, a ChefIA define um identificador estável para a demanda e cria o plano-mestre em rascunho em `/plan/{demanda}/{demanda}.md`, antes da primeira pergunta.

A entrevista é adaptativa e feita com uma pergunta objetiva por vez. Ela cobre, conforme necessário, objetivo, usuários, comportamentos, exceções, escopo, critérios de aceite, dados, integrações, segurança, prioridades, restrições, riscos e tecnologias existentes. Cada pergunta e resposta é registrada no plano-mestre, em ordem.

Enquanto houver dúvida material, conflito, lacuna de escopo ou informação insuficiente para uma implementação segura, a ChefIA deve perguntar e não pode encaminhar a demanda com suposições silenciosas. Após a confirmação explícita do solicitante, o mesmo arquivo é promovido a plano-mestre aprovado.

O plano-mestre contém objetivo, escopo, não-escopo, requisitos `REQ-n`, critérios de aceite, restrições, decisões, riscos, incertezas residuais e um checklist rastreável das tasks. Ele é a fonte de verdade do escopo funcional.

## Arquitetura e plano — MaestrIA

A MaestrIA recebe a especificação aprovada, o plano-mestre e o contexto do projeto. Ela examina arquitetura, stack, módulos, contratos, convenções, regras de negócio, dados, APIs, integrações, segurança, testes, documentação e dívida técnica.

Ela registra apenas stack confirmado no perfil de stack, usando `unknown` quando a evidência for insuficiente. Não é autorizada a migrar tecnologias sem uma decisão arquitetural explícita.

Com base no plano-mestre e na arquitetura existente, ela cria as tasks em `/plan/{demanda}/task01.md`, `/plan/{demanda}/task02.md` e assim por diante. Cada `TASK-n` é um checklist independente, informa escopo, dependências, critérios de aceite, validação e requisitos `REQ-n` cobertos. Nenhum requisito pode ficar sem ao menos uma task rastreável.

Antes de avançar, a MaestrIA registra decisões e evidências, confirma que todos os links de task existem e marca o check de arquitetura e plano em cada task como `implementado`.

Quando uma decisão arquitetural alterar comportamento percebido, restrição relevante, integração, consistência de dados, desempenho ou limitação operacional, a FIO registra contexto, decisão, alternativas, justificativa, efeitos esperados, riscos, requisitos ou tasks afetados e evidência. A DIO só documenta o efeito de produto depois de confirmá-lo no repositório.

## Testes TDD — ConfIA

Antes de implementar, a ConfIA cria uma matriz de rastreabilidade `REQ-n → cenário → TEST-n`, cobrindo cenários positivos, negativos, de borda, segurança e integração quando aplicáveis.

Ela executa primeiro a baseline da suíte existente. O padrão é baseline totalmente verde. Uma falha pré-existente só permite continuidade quando foi reproduzida antes da demanda, está fora do escopo, possui causa, comando, saída e impacto registrados, não impede a nova suíte e não mudou durante a demanda.

Os testes novos devem falhar pelo motivo esperado — ausência da funcionalidade — e não por erro de configuração. A ConfIA registra a baseline, a suíte, a matriz, o mapa de cobertura e a evidência dos testes vermelhos; então marca o check de desenho TDD como `implementado` antes de encaminhar à CodIA.

## Implementação — CodIA

A CodIA implementa o mínimo necessário para os testes definidos passarem, respeitando stack, arquitetura, contratos, convenções e o escopo confirmado. Ela não cria tarefas, não antecipa fases e não altera áreas não relacionadas.

Cada task de implementação é executada em contexto isolado. Quando houver tasks independentes e a plataforma permitir, elas podem ser distribuídas em paralelo, desde que não compartilhem arquivos, tasks ou checks sem um plano explícito de integração. Um coordenador consolida resultados, evidências e atualizações antes de marcar checks.

Ao concluir uma task, a CodIA registra comandos e resultados observados, marca o check de implementação como `implementado` e encaminha código, módulos afetados, critérios atendidos, dependências e limitações para a ConfIA. Ela não declara aprovação final.

## Validação final — ConfIA

Depois da implementação, a ConfIA revisa de modo independente a implementação e a suíte contra cada requisito aprovado. Testes verdes não bastam: a matriz precisa estar completa e os testes não podem esconder lacunas, asserts fracos ou mocks inadequados.

A validação considera regressões, casos-limite, integração, erros, segurança, desempenho e aderência arquitetural quando aplicáveis. Quando houver referência visual aprovada, ela também exige comparação lado a lado da implementação renderizada com a referência, considerando os aspectos visuais aprovados.

Se a validação falhar, a ConfIA reabre os checks e as tasks afetadas, registra motivo, evidência e ação responsável, e retorna somente à fase aplicável. A falha permanece como histórico após ser resolvida. Se aprovar, marca o check de validação final como `validado` e entrega um relatório com matriz de rastreabilidade, resultados, achados, limitações e decisão técnica.

## Double check e entrega — ChefIA

A ChefIA recebe a aprovação técnica da ConfIA, mas não declara sucesso imediatamente. Ela realiza um double check independente para verificar:

- aderência entre a especificação aprovada e os requisitos entregues;
- rastreabilidade completa `REQ-n → cenário → TEST-n → evidência`;
- checks, tasks, plano-mestre e estado operacional consistentes;
- inexistência de pendência obrigatória, bloqueio, incerteza material ou artefato invalidado;
- comunicação de entrega limitada ao que as evidências aprovadas sustentam.

Somente depois desse double check a ChefIA promove os checks obrigatórios restantes para `validado`, marca as `TASK-n` concluídas e marca um `REQ-n` concluído quando todas as tasks que o cobrem estiverem concluídas. Então produz o relatório de entrega, com resultado, evidências, limitações e próximos passos.

## Artefatos e evidências

Todo artefato possui identificador estável, produtor, status, fontes de evidência e incertezas. Os principais artefatos são:

- especificação aprovada e plano-mestre;
- perfil de stack, decisões arquiteturais e tasks;
- estratégia de testes, matriz de rastreabilidade, baseline e evidência de testes vermelhos;
- evidência de implementação e checklists atualizados;
- relatório de validação técnica e relatório de entrega.

Comandos, resultados, ambiente, arquivos envolvidos e vínculos com `TEST-n` ou `TASK-n` devem ser registrados. Execução parcial, teste pulado, mock sem contrato ou ausência de saída não comprovam sucesso.

## Checklists, retomada e limites

Os arquivos de plano e task são o painel de controle da demanda. Um estado no arquivo operacional não basta se o checklist correspondente não estiver atualizado com responsável, fase, status e evidência observável.

É possível iniciar por uma fase posterior somente quando todos os artefatos de entrada existirem e atenderem aos contratos. O início parcial, riscos e dependências assumidas devem ser registrados.

A FIO não trata testes verdes como garantia suficiente, não fabrica evidências e não implementa sem especificação, arquitetura e desenho de testes válidos. Ela preserva o histórico de falhas e exige retorno à validação final sempre que uma correção for feita.
