# Casos de Teste de Integração Gerados com auxílio de LLM

## CT-01 – Criação de pedido com estoque disponível

Pré-condição: produto 500 possui pelo menos 10 unidades disponíveis.

Entrada:

```json
{
  "customerId": 1001,
  "items": [
    {
      "productId": 500,
      "quantity": 2
    }
  ]
}
```

Resultado esperado:

- Order Service recebe a solicitação.
- Order Service envia a solicitação de reserva ao Inventory Service.
- Inventory Service retorna HTTP 201.
- Duas unidades são reservadas.
- O pedido é persistido.
- Order Service retorna sucesso ao cliente.

Risco validado: falha na comunicação ou propagação incorreta dos dados entre os serviços.

---

## CT-02 – Pedido com estoque insuficiente

Pré-condição: produto 500 possui apenas uma unidade disponível.

Entrada: quantidade solicitada igual a 2.

Resultado esperado:

- Order Service solicita a reserva.
- Inventory Service retorna HTTP 409.
- Nenhuma reserva é criada.
- O pedido não é persistido.
- Order Service informa que o pedido não pode ser processado.

Risco validado: criação de pedido sem disponibilidade real de estoque.

---

## CT-03 – Produto inexistente

Entrada:

```json
{
  "productId": 999999,
  "quantity": 1
}
```

Resultado esperado:

- Inventory Service rejeita a solicitação.
- Nenhuma reserva é criada.
- O pedido não é persistido.
- O erro recebido pelo Order Service é tratado adequadamente.

Risco validado: inconsistência de cadastro entre os serviços.

---

## CT-04 – Quantidade igual a zero

Entrada:

```json
{
  "productId": 500,
  "quantity": 0
}
```

Resultado esperado: a requisição deve ser rejeitada e nenhuma reserva ou pedido deve ser criado.

Risco validado: propagação de dados inválidos entre componentes.

---

## CT-05 – Quantidade negativa

Entrada:

```json
{
  "productId": 500,
  "quantity": -2
}
```

Resultado esperado: a requisição deve ser rejeitada sem alteração de estoque ou persistência do pedido.

Risco validado: ausência de validação de dados antes da integração.

---

## CT-06 – Inventory Service indisponível

Comportamento simulado: chamada retorna HTTP 503.

Resultado esperado:

- pedido não é confirmado;
- nenhuma reserva é considerada concluída;
- erro é tratado pelo Order Service;
- não existe inconsistência entre pedido e estoque.

Risco validado: confirmação de pedido quando uma dependência está indisponível.

---

## CT-07 – Timeout na comunicação

Cenário: Inventory Service demora mais que o limite configurado para responder.

Resultado esperado:

- Order Service identifica o timeout;
- pedido não é considerado concluído;
- nenhuma confirmação falsa de reserva ocorre;
- aplicação retorna uma resposta de erro controlada.

Risco validado: estado indefinido provocado por falha de rede ou lentidão do serviço integrado.

---

## CT-08 – Resposta HTTP inesperada

Cenário: Inventory Service retorna HTTP 500 durante a tentativa de reserva.

Resultado esperado:

- Order Service não persiste o pedido como concluído;
- falha é registrada e tratada;
- nenhuma confirmação de sucesso é retornada ao cliente.

Risco validado: tratamento inadequado de respostas não previstas.

---

## CT-09 – Requisição duplicada

Cenário: a mesma solicitação é enviada duas vezes devido a retry ou repetição do cliente.

Resultado esperado: o sistema deve impedir que uma repetição não intencional resulte em duas reservas e dois pedidos equivalentes, considerando o mecanismo de idempotência adotado pela aplicação.

Risco validado: duplicação de transações.

---

## CT-10 – Falha após reserva do estoque

Cenário: Inventory Service realiza a reserva corretamente, mas ocorre uma falha no Order Service antes da persistência definitiva do pedido.

Resultado esperado: o sistema deve possuir uma estratégia que impeça o estoque de permanecer reservado indefinidamente sem um pedido correspondente, como compensação, cancelamento da reserva ou mecanismo equivalente definido pela arquitetura.

Risco validado: inconsistência causada por falha parcial em uma operação distribuída.

---

# Síntese do experimento

O primeiro prompt concentrou-se no fluxo funcional e no contrato entre os serviços. Foi útil para identificar cenários relacionados a códigos HTTP, transmissão de dados, criação do pedido e reserva do estoque.

O segundo prompt aumentou a diversidade ao solicitar explicitamente falhas de comunicação, timeout, duplicidade e inconsistência entre sistemas.

Os prompts iniciais eram corretos, mas superficiais. Após adicionar contexto, endpoints, códigos HTTP, responsabilidades dos serviços e formato esperado da resposta, a LLM passou a gerar casos mais objetivos.

Outro ajuste importante foi pedir explicitamente que os cenários fossem testes de integração. Sem essa restrição, parte das sugestões se aproximava de testes unitários de validação de campos.
