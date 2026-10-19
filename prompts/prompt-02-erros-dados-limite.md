# Prompt 02 – Geração de erros e condições de borda

## Tipo de prompt

Prompt direcionado à geração de cenários negativos, falhas de integração e condições de borda.

## Prompt inicial

> Gere casos de erro para a integração entre uma API de pedidos e uma API de estoque.
>
> Inclua também dados inválidos e casos extremos.

## Resultado observado

O modelo apresentou alguns erros comuns, como ausência de estoque e campos inválidos, mas deixou de explorar problemas típicos de sistemas distribuídos, como timeout, indisponibilidade temporária, processamento duplicado e falha parcial.

Por isso, o prompt foi refinado.

## Prompt refinado

> Atue como engenheiro de qualidade responsável por testar integrações entre microsserviços REST.
>
> Analise a integração:
>
> Order Service -> Inventory Service.
>
> O Order Service recebe `POST /orders` e chama `POST /reservations` no Inventory Service.
>
> Considere principalmente cenários negativos e condições de borda.
>
> Gere casos envolvendo, quando aplicável:
>
> - estoque insuficiente;
> - produto inexistente;
> - quantidade zero;
> - quantidade negativa;
> - campo obrigatório ausente;
> - serviço de estoque indisponível;
> - timeout;
> - resposta HTTP inesperada;
> - requisição duplicada;
> - falha após a reserva do estoque;
> - risco de inconsistência entre pedido e estoque.
>
> Para cada caso informe:
>
> 1. cenário;
> 2. dados utilizados;
> 3. comportamento simulado;
> 4. resultado esperado;
> 5. risco de integração que o teste procura identificar.
>
> Evite repetir testes equivalentes.
>
> Priorize problemas que surgem especificamente da comunicação entre os componentes, e não testes unitários internos de cada serviço.

## Influência na diversidade dos casos

Esse prompt aumentou significativamente a diversidade dos testes ao direcionar a LLM para problemas de integração distribuída, incluindo falhas de rede, timeout, duplicidade e inconsistência entre serviços.
