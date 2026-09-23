# Tarefa: Criar Skill de Knowledge Bootstrap AS-IS para Obsidian

## Objetivo

Criar uma nova skill cuja responsabilidade seja analisar um projeto de software existente e construir uma base inicial de conhecimento sobre esse projeto no Obsidian. Esta etapa é um bootstrap inicial.

## Separação de Responsabilidades

O repositório continua sendo a fonte de verdade da implementação, e o Obsidian será a base de conhecimento sobre o projeto.

Portanto, não armazenar no Obsidian classes, métodos, funções, testes, lint ou detalhes de implementação. Esses elementos podem ser analisados, mas não documentados.

O foco é conhecimento de projeto:

- finalidade;
- funcionalidades;
- regras de negócio;
- fluxos;
- atores;
- conceitos;
- integrações;
- arquitetura em alto nível;
- comportamentos observados;
- comportamentos esperados, quando conhecidos;
- incertezas e divergências.

Para regras materiais, a DIO documenta gatilho, pré-condições, decisão, exceções, efeito no produto e evidência. Para cada integração externa relevante, documenta propósito de negócio, momento de chamada, regras, resultados, impacto no fluxo e recuperação observável, sem publicar detalhes técnicos ou dados sensíveis.

### Regra fundamental

O código é a fonte de verdade do AS-IS. Isso não significa que ele está correto do ponto de vista de produto. Diferenciar sempre AS-IS e esperado.

### Fronteira com Solicitações de Mudança

Esta skill é a única responsável por criar ou revalidar a baseline AS-IS a partir do repositório. Uma solicitação de mudança pode descrever comportamento esperado, mas não altera automaticamente o conhecimento de comportamento atual.

Conhecimento esperado só pode ser promovido a AS-IS quando houver evidência observável no repositório ou quando esta skill executar uma nova análise do projeto. A skill de Solicitações de Mudança deve preservar a ligação entre a mudança proposta e o conhecimento esperado, sem substituir a baseline AS-IS.

### Handoff para encerramento pela CIM

Este handoff só se aplica quando a DIO for acionada dentro de um ciclo coordenado pela CIM. Em uso independente, a DIO cria ou revalida a baseline AS-IS e encerra sua execução sem encaminhar informações automaticamente para a CIM.

Dentro do ciclo, a DIO usa a solicitação, o conhecimento esperado e a evidência de entrega apenas como contexto para saber o que avaliar. A confirmação continua baseada na observação do repositório.

Ao concluir a reanálise, a DIO deve entregar à CIM uma **revalidação AS-IS** com:

- identificador compartilhado da mudança;
- conhecimentos esperados avaliados;
- evidência observável no repositório;
- resultado por item: `confirmado`, `parcial`, `não_encontrado` ou `bloqueado`;
- atualizações ou preservação da baseline AS-IS;
- pendências e retorno necessário, quando aplicável.

No estado operacional, esse handoff é identificado como `dio_as_is_revalidation`. Ele é gerado e localizado pela CIM; quem usa a skill não precisa criar ou transportar esse artefato manualmente.

### Fontes de entrada

A skill deve aceitar obrigatoriamente o projeto como fonte. Opcionalmente, pode receber documentação adicional e contexto adicional em texto livre. Essas fontes devem ser confrontadas com o comportamento observado no projeto.

### Regra de não alucinação

Quando não houver informação suficiente, não inventar. Usar `A_CONFIRMAR` ou `INFERIDO` de forma explícita. Não tentar reconstruir a intenção original sem base.

### Classificação inicial

Utilizar as classificações `observado`, `inferido`, `confirmado` e `a confirmar`. Inferências nunca viram fato automaticamente.

### Confronto e divergências

Após consolidar o AS-IS e comparar com a documentação e o contexto, identificar divergências e apresentar um questionário consolidado ao usuário.

Não perguntar qual é o AS-IS. Perguntar como a divergência deve ser interpretada. Exemplos de opções:

- implementação correta;
- documentação desatualizada;
- documentação representa o esperado e a implementação precisa ser corrigida;
- regra alterada ou falta de informação;
- outra interpretação;
- não sei.

### Resultados possíveis

Se o código estiver correto, consolidar o conhecimento e, se for o caso, registrar que existe documentação externa potencialmente desatualizada.

Se a implementação estiver incorreta, registrar explicitamente a divergência entre AS-IS e esperado e indicar necessidade de correção. Não corrigir automaticamente.

## Estrutura do Vault

Utilizar uma estrutura inicial simples e progressiva. Como exemplo conceitual: `Projeto.md`, `Produto.md` e pastas ou notas para funcionalidades, regras de negócio, fluxos, arquitetura, integrações, conceitos, incertezas e divergências.

- Não criar arquivos vazios apenas por estrutura.
- Organizar progressivamente.
- Usar links internos apenas quando houver relação real de conhecimento.
- Usar front matter somente quando ajudar na recuperação futura.
- Nunca armazenar secrets ou credenciais.

### Idempotência

Executar mais de uma vez não deve duplicar conteúdo nem sobrescrever silenciosamente conhecimento validado por humano.

### Fora de escopo

- Não processar solicitações de mudança como fonte de atualização automática do AS-IS.
- Não implementar RAG, embeddings ou banco vetorial agora.
- Não alterar a skill de implementação atual.
- Esta etapa trata apenas da criação da primeira baseline de conhecimento AS-IS.

## Processo conceitual

1. Analisar o projeto.
2. Analisar a documentação opcional e o contexto adicional.
3. Consolidar conhecimento preliminar.
4. Identificar divergências.
5. Conduzir validação humana.
6. Só então, consolidar no Obsidian.

### Princípio final

Manter sempre explícito o que existe, o que deveria existir, o que não sabemos e o que está divergente.
