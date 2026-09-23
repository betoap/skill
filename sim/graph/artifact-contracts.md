# Contratos de artefatos

Todo artefato usa identificador estável, produtor, status (`draft`, `current`, `invalidated`, `validated` ou `blocked`), fontes de evidência e incertezas. Não preencha campos sem base disponível.

## Registro da solicitação e escopo

- identificador estável, quando disponível, ou identificador local derivado de forma rastreável;
- texto de origem, referência segura ou resumo fiel do conteúdo recebido;
- projeto e vault relacionados;
- partes ausentes, limitações ou bloqueios de interpretação;
- indicação de que a fonte descreve proposta, não comportamento AS-IS.

## Conhecimento candidato e análise de impacto

- regras de negócio, fluxos, atores, conceitos, integrações e comportamentos de produto identificados;
- tipo de impacto: `novo`, `complementa`, `altera`, `remove`, `divergência` ou `dúvida`;
- dimensões de impacto aplicáveis: `funcional`, `dados`, `integração`, `segurança` e `experiência`, com evidência ou indicação `a_confirmar`;
- classificação de certeza: `observado`, `inferido`, `confirmado` ou `a_confirmar`;
- notas, conceitos ou conhecimentos relacionados consultados;
- distinção explícita entre comportamento atual, esperado e incerto.

## Proposta de consolidação e decisão humana

Para cada alteração, registre destino proposto, conteúdo esperado ou planejado, solicitação de origem, impacto, certeza, evidência e razão para consolidação automática ou validação humana. Uma decisão humana deve registrar resposta, escopo afetado e efeito sobre a proposta. Sem resposta necessária, mantenha o item como `a_confirmar` ou bloqueado.

## Atualização incremental e histórico

Registre notas criadas ou atualizadas, conhecimento esperado consolidado, vínculos internos criados, histórico da solicitação, itens pendentes e resultado `published`, `partial` ou `blocked`. O histórico deve permitir rastrear a rodada sem duplicar seu conteúdo nas notas centrais.

Uma atualização esperada não pode declarar alteração do AS-IS. A promoção posterior exige uma nova análise da DIO e evidência observável no repositório.

## Contexto da mudança para a CIM

Quando a execução estiver vinculada a uma CIM, registre um handoff com o `cycle_id` compartilhado, solicitação de origem, conhecimento esperado ou planejado, análise de impacto, classificações de certeza, dúvidas, decisões humanas, pendências e referências para as notas e o histórico. Sem ciclo identificado, este artefato não é produzido nem encaminhado.
