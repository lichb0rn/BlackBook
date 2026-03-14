---
up:
  - "[[20 Software Architecture]]"
related: "[[Clean Architecture]]"
created: 2025-05-21
aliases:
  - ports and adapters
---
The layers we usually use are **adapters**, **ports**, **application**, and **domain**.

## Adapters
- An adapter is how your application talks to the external world. You have to adapt your internal structures to what the external API expects. Think **SQL queries**, HTTP or gRPC clients, file readers and writers, **Pub/Sub message publishers**.

## Ports
- A port is an input to your application, and the only way the external world can reach it. It could be an **HTTP or gRPC server**, a CLI command, or a **Pub/Sub message subscriber**.

## Application
- The application logic is a thin layer that “glues together” other layers. It’s also known as “**use cases**”. If you read this code and can’t tell what database it uses or what URL it calls, it’s a good sign. Sometimes it’s very short, and that’s fine. Think about it as an orchestrator.

## Domain
- If you also follow [[Domain-Driven Design]], you can introduce a domain layer that holds just the business logic.