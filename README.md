# Testes de Integração com Inteligência Artificial Generativa

Atividade desenvolvida para a Especialização em Engenharia de Software: Automação e Inovação com Inteligência Artificial Generativa – UFG.

## Objetivo

Avaliar como diferentes tipos de prompt podem apoiar uma LLM na elaboração de casos de teste de integração.

## Cenário de integração

O cenário escolhido envolve dois serviços REST:

- Order Service: responsável pela criação de pedidos.
- Inventory Service: responsável pela consulta e reserva de estoque.

Fluxo:

```text
Cliente -> Order Service -> Inventory Service
```

Ao receber um pedido, o Order Service solicita ao Inventory Service a reserva dos produtos. O pedido somente deve ser confirmado quando a reserva for realizada com sucesso.

## Estrutura do repositório

```text
testes-integracao-genai/
├── README.md
├── prompts/
│   ├── prompt-01-cenarios-integracao.md
│   └── prompt-02-erros-dados-limite.md
└── tests/
    └── casos-de-teste.md
```

## Tipos de prompt utilizados

1. Prompt para geração de cenários funcionais de integração
   - Foco em comunicação entre serviços, códigos HTTP, propagação de dados, persistência e consistência.

2. Prompt para geração de cenários negativos e condições de borda
   - Foco em indisponibilidade, timeout, respostas inesperadas, duplicidade, dados inválidos e falhas parciais.

## Principais conclusões

Os prompts iniciais geraram resultados úteis, porém genéricos. Após o refinamento, com maior contexto sobre endpoints, responsabilidades dos serviços, códigos HTTP e estrutura esperada da resposta, os casos de teste ficaram mais objetivos e diversificados.

A LLM foi especialmente útil para sugerir cenários de exceção e riscos típicos de sistemas distribuídos. Entretanto, os resultados ainda precisam ser analisados por uma pessoa que conheça os requisitos e a arquitetura do sistema.

Assim, GenAI pode atuar como copiloto na construção de suítes de testes de integração, ampliando a cobertura e ajudando a identificar cenários que poderiam ser esquecidos em uma análise inicial.
