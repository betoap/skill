# Modelo de plano e tasks por demanda

## Plano-mestre do ChefIA — `/plan/{demanda}/{demanda}.md`

# {demanda}

**Objetivo:** resultado observável confirmado pelo usuário.

## Registro da entrevista

Registre cada pergunta objetiva da ChefIA e a resposta correspondente, na ordem em que ocorreram. Faça a próxima pergunta somente após receber e registrar a resposta anterior.

1. **Pergunta:** ...
   **Resposta:** ...

**Escopo confirmado:** requisitos, comportamentos e limites incluídos.

**Não-escopo:** comportamentos e limites excluídos.

**Critérios de aceite:** condições verificáveis associadas a `REQ-n`.

**Restrições e decisões confirmadas:** dados, integrações, segurança, compatibilidade e demais limites relevantes.

**Riscos e incertezas residuais não bloqueantes:** itens conhecidos que não impedem o início.

## Checklist de requisitos

- [ ] REQ-01 — requisito confirmado — concluído somente quando todas as tasks vinculadas estiverem concluídas no double check da ChefIA

## Checklist de tasks

- [ ] TASK-01 — nome orientado ao resultado — `task01.md` — cobre `REQ-01`

Uma task só recebe check no plano-mestre quando todos os seus checks obrigatórios forem marcados como `validado` pela ChefIA no double check final. Um requisito só recebe check quando todas as tasks que o cobrem estiverem concluídas. Ao atualizar qualquer item, registre junto dele ou na seção de evidências: responsável, fase, status e referência à evidência observável. Não use este modelo para substituir documentação preexistente de outra demanda.

## Task do MaestrIA — `/plan/{demanda}/taskNN.md`

## TASK-N — Nome orientado ao resultado

**Objetivo:** resultado observável.

**Dependências:** etapas, decisões, serviços ou dados necessários.

**Escopo:** módulos, contratos e comportamentos alterados.

**Critérios de aceite:** condições verificáveis de sucesso.

**Requisitos cobertos:** identificadores `REQ-n` atendidos por esta tarefa.

**Validação:** testes e verificações relevantes.

**Referência visual aprovada (quando aplicável):** arquivo, tela, protótipo ou especificação a comparar; contextos ou viewports relevantes.

**Evidências esperadas:** comandos, arquivos, relatórios ou observações que poderão comprovar a conclusão.

### Checklist

- [ ] Arquitetura e plano da task — pendente
- [ ] Desenho de testes TDD — pendente
- [ ] Implementação — pendente
- [ ] Validação final — pendente

Cada responsável deve atualizar o check da sua fase antes de solicitar a transição. Estados permitidos: **pendente**, **em andamento**, **implementado** e **validado**. MaestrIA, ConfIA no desenho TDD e CodIA registram seus checks como `implementado`; ConfIA marca a validação técnica final como `validado`; ChefIA promove todos os checks obrigatórios para `validado` no double check de entrega. Quando houver referência visual aprovada, o check de validação final exige a comparação lado a lado e aderência total aos aspectos visuais aprovados. Se ConfIA encontrar uma falha, deve desmarcar os checks invalidados e adicionar diretamente abaixo deles a observação `Falha de validação — status: aberta`, contendo somente motivo, evidência e ação responsável. Após a correção aprovada, altere somente o status para `resolvida`; não remova o registro. O check de implementação não substitui a validação; a task encerra somente com todos os itens obrigatórios validados. Nenhum check pode ser marcado sem uma evidência observável registrada na task.
