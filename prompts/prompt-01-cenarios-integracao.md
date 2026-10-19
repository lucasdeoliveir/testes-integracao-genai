# Prompt 01 – Geração de cenários funcionais de integração

## Tipo de prompt

Prompt estruturado e contextualizado para geração de cenários funcionais de integração.

## Prompt inicial

> Considere uma integração REST entre um serviço de pedidos e um serviço de estoque.
>
> Gere casos de teste de integração para verificar se os dois serviços estão se comunicando corretamente.
>
> Para cada teste, informe:
> - cenário;
> - entrada;
> - resultado esperado.

## Resultado observado

O prompt produziu cenários válidos, porém relativamente genéricos. Alguns resultados não especificavam códigos HTTP, pré-condições, estado final dos sistemas ou qual aspecto da integração deveria ser validado.

Por isso, foi necessário adicionar mais contexto e restrições.

## Prompt refinado

> Atue como engenheiro de software especializado em testes de integração de APIs REST.
>
> Considere o seguinte cenário:
>
> O Order Service disponibiliza:
>
> `POST /orders`
>
> Exemplo de requisição:
>
> ```json
> {
>   "customerId": 1001,
>   "items": [
>     {
>       "productId": 500,
>       "quantity": 2
>     }
>   ]
> }
> ```
>
> Durante o processamento, o Order Service chama o Inventory Service:
>
> `POST /reservations`
>
> Quando a reserva é realizada com sucesso, o Inventory Service responde HTTP 201.
>
> Caso não exista estoque suficiente, responde HTTP 409.
>
> O Order Service somente deve persistir o pedido após uma reserva bem-sucedida.
>
> Gere casos de teste de integração que validem:
>
> - comunicação entre os serviços;
> - códigos HTTP;
> - propagação dos dados;
> - persistência do pedido;
> - reserva do estoque;
> - consistência entre os sistemas.
>
> Para cada caso informe:
>
> 1. identificador;
> 2. objetivo;
> 3. pré-condição;
> 4. entrada;
> 5. comportamento esperado do Inventory Service;
> 6. comportamento esperado do Order Service;
> 7. resultado esperado.
>
> Não invente endpoints ou comportamentos diferentes dos especificados.

## Influência na qualidade dos casos

O refinamento tornou os casos mais objetivos, facilitou a validação do contrato entre os serviços e reduziu respostas vagas. A estrutura fixa também facilitou a comparação dos cenários gerados.
