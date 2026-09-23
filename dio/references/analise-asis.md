# Análise AS-IS

Comece por inventariar fontes e definir os limites da análise. Examine o projeto para compreender comportamento, domínio e estrutura em alto nível, priorizando evidências que sustentem finalidade, atores, funcionalidades, regras, fluxos, integrações e conceitos.

Para cada comportamento material, registre a regra de negócio de maneira completa: o que o dispara, para quem se aplica, pré-condições, decisão tomada, exceções, resultado e efeito no fluxo. Prefira frases verificáveis a rótulos genéricos. Por exemplo, em vez de “valida pagamento”, registre qual condição permite ou impede o avanço do pedido, o que ocorre em cada resultado e qual evidência sustenta essa conclusão.

Mapeie também interações externas, incluindo chamadas HTTP, mensageria, arquivos, webhooks, provedores ou sistemas corporativos. Para cada uma, siga o contrato de [integrações externas](integracoes-externas.md). Uma integração sem propósito de negócio identificado deve permanecer como `a_confirmar`, não ser descrita como suposição.

Registre afirmações curtas e recuperáveis, associadas a sua fonte e classificação. Converta em `inferido` somente conclusões razoáveis sustentadas por evidência; se houver mais de uma interpretação plausível, use `a_confirmar`.

Evite transformar a análise em documentação técnica do código. Referencie a evidência de maneira localizável, mas descreva o conhecimento de projeto, não nomes de arquivos, métodos, classes, funções, testes ou detalhes internos. Nunca publique segredos, credenciais, tokens, URLs privadas, cabeçalhos de autenticação ou payloads completos.
