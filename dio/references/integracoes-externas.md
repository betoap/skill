# Integrações externas

Trate uma integração como parte do comportamento do produto quando ela altera, viabiliza, consulta ou confirma uma decisão de negócio. Inclua APIs, eventos, filas, arquivos, webhooks, provedores e sistemas internos ou de terceiros.

## Registro por integração

Para cada integração relevante, consolide uma seção ou nota com:

- **Sistema ou domínio integrado:** nome conhecido ou descrição neutra quando o nome não for seguro ou estiver ausente.
- **Propósito de negócio:** qual capacidade do produto a interação viabiliza ou qual decisão ela apoia.
- **Gatilho e ator:** evento, etapa do fluxo ou ator que causa a interação.
- **Pré-condições e regras:** condições para chamar, critérios que impedem a chamada e regras que dependem da resposta.
- **Informação de negócio trocada:** categorias de dados necessárias e resultado consumido; nunca valores sensíveis, credenciais ou payloads completos.
- **Resultado e efeito:** como sucesso, recusa, ausência de resposta ou retorno parcial afetam o usuário, o processo e os próximos passos.
- **Assincronia e recuperação:** eventos posteriores, confirmação, repetição, compensação ou ação manual, quando houver evidência.
- **Evidência e certeza:** fontes observadas e classificação `observado`, `inferido`, `confirmado` ou `a_confirmar`.

## Profundidade adequada

Explique a intenção e a regra de negócio, não a implementação do cliente de integração. Um bom registro permite responder “por que o produto consulta esse sistema, quando faz isso e o que ocorre conforme a resposta”, sem expor endpoint, biblioteca, método, token ou estrutura interna de código.

Se a existência da chamada estiver observável, mas seu propósito ou regra não estiver claro, registre a interação e mantenha o propósito como `A_CONFIRMAR`. Não deduza intenções apenas pelo nome técnico de uma rota, classe ou variável.
