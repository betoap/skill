# Contratos de artefatos

Todo artefato usa identificador estável, produtor, status (`draft`, `current`, `invalidated`, `validated` ou `blocked`), ciclo relacionado, fontes de evidência e incertezas. Não preencha campos sem base verificável.

## Registro do ciclo

- identificador compartilhado e solicitação de origem;
- projeto e vault relacionados;
- estado atual, nó atual, responsável e bloqueios;
- referências verificáveis para SIM, FIO e DIO;
- relação com ciclos anteriores, quando houver.
- modo de entrada: `new`, `resume` ou `assumed_partial`; uma entrada parcial registra dependências e riscos.
- alvo de confirmação: `repositorio`, `homologacao` ou `producao`, evidência disponível e maior estágio confirmado.
- para cada pendência ou bloqueio: responsável, próxima ação e data ou condição de revisão.

## Handoff da SIM

- identificador compartilhado e solicitação de origem;
- conhecimento esperado ou planejado;
- análise de impacto e classificação de certeza;
- divergências, dúvidas, decisões humanas e pendências;
- referências às notas e ao histórico da solicitação.

## Handoff da FIO

- identificador compartilhado e referência ao contexto recebido da SIM;
- especificação aprovada, escopo implementado e não implementado;
- plano, relatório de validação técnica e evidências de execução e entrega;
- limitações, pendências, retornos e referências ao plano-mestre e às tasks.

## Handoff da DIO

- identificador compartilhado e conhecimentos esperados avaliados;
- evidência observável no repositório;
- resultado por item: `confirmado`, `parcial`, `nao_encontrado` ou `bloqueado`;
- atualizações ou preservação da baseline AS-IS;
- incertezas, pendências e ação de retorno, quando aplicável.

## Relatório de ciclo

Registre a trilha de handoffs, o resultado final, itens confirmados, parciais ou não confirmados, evidências consultadas, pendências, próximos responsáveis e vínculos com o histórico da solicitação. Um relatório de ciclo não substitui os relatórios técnicos da FIO nem a revalidação da DIO.
