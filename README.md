# ShoopTree — Arquitetura de Microsserviços

Prova de conceito desenvolvida para demonstrar a aplicação de conceitos de arquitetura de software utilizando microsserviços, comunicação orientada a eventos e Design Pattern em Python.

## Sobre o projeto

A ShoopTree é uma plataforma de comércio eletrônico que originalmente utiliza uma arquitetura monolítica. Com o crescimento da plataforma, surgiram problemas relacionados à escalabilidade, manutenção, acoplamento entre módulos e evolução do sistema.

Este projeto apresenta uma prova de conceito de uma arquitetura baseada em microsserviços, utilizando Python e FastAPI, com comunicação orientada a eventos simulada por classes Python.

## Arquitetura

A solução é composta por dois serviços independentes:

* **Serviço de Produtos**: responsável pelo cadastro e consulta de produtos.
* **Serviço de Pagamentos**: responsável pelo cadastro e consulta de pagamentos.

Além dos serviços, a solução possui uma simulação de comunicação orientada a eventos.

O fluxo principal é:

```text
Compra realizada
        │
        ▼
Evento: CompraRealizada
        │
        ├──────────────► Pagamento Consumer
        │
        └──────────────► Notification Consumer
```

O evento é publicado por um produtor e consumido pelos componentes interessados.

## Serviços

### Serviço de Produtos

Responsável por gerenciar os produtos disponíveis na plataforma.

Endpoints:

```text
GET /produtos
POST /produtos
```

### Serviço de Pagamentos

Responsável por gerenciar os pagamentos associados às compras.

Endpoints:

```text
GET /pagamentos
POST /pagamentos
```

## Comunicação orientada a eventos

A comunicação entre os componentes é simulada utilizando classes Python, sem a necessidade de ferramentas externas como Kafka ou RabbitMQ.

O fluxo funciona da seguinte forma:

1. Uma compra é realizada.
2. Um evento `CompraRealizada` é criado.
3. O evento é publicado pelo produtor.
4. O `PagamentoConsumer` consome o evento.
5. O `NotificationConsumer` também consome o evento.

Essa abordagem permite demonstrar o conceito de comunicação desacoplada baseada em eventos.

## Design Pattern

O projeto utiliza o padrão de projeto **Factory Method**.

O padrão será utilizado para centralizar a criação dos objetos de eventos, evitando que diferentes partes do sistema precisem conhecer diretamente os detalhes de instanciação de cada tipo de evento.

A Factory será responsável por criar os eventos necessários para a comunicação da aplicação, mantendo a lógica de criação centralizada e facilitando futuras extensões.

## Estrutura do projeto

```text
arquitetura-software/
│
├── produto_service/
│
├── pagamento_service/
│
├── eventos/
│
├── diagrams/
│
├── docs/
│
├── README.md
│
├── requirements.txt
│
└── .gitignore
```

## Como executar

As instruções de instalação e execução serão adicionadas conforme os serviços forem implementados.

## Diagramas

Os diagramas arquiteturais serão disponibilizados na pasta `diagrams/` utilizando o C4 Model:

* Diagrama de Contexto;
* Diagrama de Containers.

## Documentação

A decisão arquitetural do projeto será registrada por meio de um ADR (Architecture Decision Record), contendo:

* problema arquitetural;
* alternativas avaliadas;
* decisão tomada;
* justificativa técnica;
* consequências da decisão.

