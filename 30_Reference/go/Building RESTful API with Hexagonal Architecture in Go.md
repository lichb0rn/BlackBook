---
title: Building RESTful API with Hexagonal Architecture in Go
source: https://dev.to/bagashiz/building-restful-api-with-hexagonal-architecture-in-go-1mij
author:
  - "[[DEV Community]]"
published: 2023-09-27
created: 2025-03-30
description: I've been learning how to build web applications using different frameworks and languages for a while... Tagged with go, api, backend, architecture.
tags:
  - clippings
related: "[[Jet Spares Go]]"
github: https://github.com/bagashiz/go-pos/tree/main
---
I've been learning how to build web applications using different frameworks and languages for a while now, such as [Laravel](https://github.com/bagashiz/sea-cinema-tix) with its MVC architecture and [Node.js](https://github.com/bagashiz/openmusic-api) following the 'Hapi.js Way'. As I'm trying to create a new portfolio project using Go, I found myself contemplating over the ideal project structure. I wanted something that not only aligns with [the standard Go project layout](https://github.com/golang-standards/project-layout), but also makes the code both easy to write and understand. That's when I stumbled upon the concept of Hexagonal Architecture, as showcased in [Netflix's engineering blog](https://netflixtechblog.com/ready-for-changes-with-hexagonal-architecture-b315ec967749). The idea of seamlessly swapping infrastructures with minimal code changes fascinated me, and I decided to implement it in my new project.

Now, the remaining question was, *"what should I build?"* Fortunately, as I was casually scrolling through YouTube videos, I stumbled upon this hidden gem video titled [*'Ide Project untuk Upgrade Portfolio Backend Engineer'*](https://www.youtube.com/watch?v=uAR1kjyeDtg) by [Asdita Prasetya](https://www.youtube.com/@asditaprasetya). He recommended developing a RESTful Point of Sale API service. It felt like the perfect project to put my newfound architectural knowledge into practice. So, getting my coffee and keyboard ready, I started on this exciting learning journey!

## Hexagonal Architecture

> Create your application to work without either a UI or a database so you can run automated regression-tests against the application, work when the database becomes unavailable, and link applications together without any user involvement.

[Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture), also known as Ports & Adapters Architecture, is one of several ways to build decoupled software systems. It was popularized by [Alistair Cockburn](https://alistaircockburn.com/Bio), who is known as one of the initiators of the agile movement in software development. This way of organizing software is great for making applications that are easy to work on and can change without breaking.

The main idea behind Hexagonal Architecture is to separate the application's core business logic from the external stuff, such as databases, user interfaces, and other external services. It promotes a clean and modular structure that makes it easier to test, maintain, and scale the application.

### Core

The core is where the heart of the application lives. It contains the essential business logic and rules of the application. This is where things like processing orders, managing user accounts, and performing all the tasks of the application is designed for. The core should be independent of any external technologies or frameworks, making it highly portable and reusable.

There are two other essential concepts in Hexagonal Architecture: "ports" and "adapters". These concepts dictates how the "core" interacts with the external components.

### Ports

Think of ports as contracts or interfaces. They define how the application communicates with external systems or services. For example, a port could specify the rules for connecting to a database, interacting with another web services, or handling user interfaces. Ports belongs to the core, because the core defines which actions are required to achieve the business logic goals.

### Adapters

Adapters are the ones who implement the contracts or interfaces defined by ports. Adapters are responsible for making sure the application can interact to databases, web services, or other things. They handle the technical details.

### Driver Actors

Driver actors are the initiators of communication with the core. They reach out to the core to request specific services. Examples of driver actors can be HTTP request or command line interfaces (CLI).

### Driven Actors

Driven actors are the ones that triggered by the core. If the core needs something from external services, it sends a request to the adapter, instructing it to perform a particular action. For example, if the core needs to store data in a Postgres database, it triggers communication with the Postgres client to execute an INSERT query. In this scenario, the core initiates the communication.

## Implementation

### Requirements

Asdita had been kind enough to provide the [database schema design](https://hellodit.mayar.link/catalog/desain-database-aplikasi-pos) and [Postman API documentation](https://documenter.getpostman.com/view/4080490/2s93CSnAJa). So all I had to do was just structure my application to adhere to hexagonal architecture principles and start coding.

### Tech Stacks

For building the RESTful Point of Sale service API, I've considered and selected a combination of technologies that would work seamlessly together. For handling HTTP requests and responses, using the [Gin HTTP web framework](https://github.com/gin-gonic/gin) would make sense because I think it seems complete and popular among Go community too. To ensure data integrity and persistence, I'm using [PostgreSQL](https://www.postgresql.org/) database with [pgx](https://github.com/jackc/pgx) as the database driver, the reason I choose PostgreSQL because it is the most popular relational database to use in production and offers efficient Go integration. I'm also implementing caching using [Redis](https://redis.io/) with [go-redis](https://github.com/redis/go-redis) client library, which provides powerful in-memory data storage capabilities.

### Database Schema

[![Go-POS Schema](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F0dl588lkw6yuq7iapn0n.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F0dl588lkw6yuq7iapn0n.png)

- `users`: stores user information, including names, emails, passwords, roles (admin or cashier), and timestamps for creation and updates.
- `payments`: stores various payment methods. It tracks payment types, names, logos, and timestamps for creation and updates.
- `categories`: stores product categories, tracking category names and timestamps for creation and updates.
- `products`: stores essential product data, including category IDs, SKUs, names, stock levels, prices, images, and timestamps for creation and updates.
- `orders`: stores order details, such as user IDs, payment IDs, customer names, total prices, payments made, returns, receipt codes, and timestamps for creation and updates.
- `order_products`: stores record of products included in each order. It notes order and product IDs, quantities, total prices, and timestamps for creation and updates.

### Application Architecture

[![Go-POS Hexagonal Architecture](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F30x1jxedqgc970e4plm2.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F30x1jxedqgc970e4plm2.png)

The application follows Hexagonal Architecture, depicted as a hexagon. The `core` at its center houses `domain` and `service` containing business logic.

On the left side of core is a `driver port`, an entry point for driver adapter, while on the right side there are 2 `driven ports` that act as the gate for the core to interact with driven adapter.

Around the core, `adapters` bridge the core and external world. On the left, the `HTTP adapter` handles incoming HTTP requests. On the right, 2 adapters exist: `DB adapter` connects to PostgreSQL and `Cache adapter` works with Redis.

The `driver actors` and `driven actors` resides outside of the application. Nginx, on the left, serves as an HTTP server, the `driver actor`. On the right, PostgreSQL and Redis represent `driven actors` responding to core requests.

### Project Structure

```
.
├── bin
├── cmd
│   └── http
├── docs
└── internal
    ├── adapter
    │   ├── cache
    │   │   └── redis
    │   ├── handler
    │   │   └── http
    │   ├── repository
    │   │   └── postgres
    │   │       └── migrations
    │   └── token
    │       └── paseto
    └── core
        ├── domain
        ├── port
        ├── service
        └── util

21 directories
```
- `bin`: directory to store compiled executable binary.
- `docs`: directory to store project's documentation, such as swagger static files.
- `cmd`: directory for main entry points or commands of the application. The `http` sub-directory holds the main HTTP server entry point.
- `internal`: directory for containing application code that should not exposed to external packages.
- `core`: directory that contains the central business logic of the application. Inside it there are 4 sub-directories.
	- `domain`: directory that contains domain models/entities representing core business concepts.
	- `port`: directory that contains defined interfaces or contracts that adapters must follow.
	- `service`: directory that contains the business logic or services of the application.
	- `util`: directory that contains utility functions that reused in the `service` package.
- `adapters`: directory for containing external services that will interact with the core of application. There are 4 external services used in this application.
	- `handler/http`: directory that contains HTTP request and response handler.
	- `repository/postgres`: directory that contains database adapters for PostgreSQL.
	- `cache/redis`: directory that contains cache adapters for Redis.
	- `token/paseto`: directory that contains token generation and validation adapters using Paseto.

### Dev tools

I've used several tools to ease things out during development. These tools help in different ways.

#### Podman

[Podman](https://podman.io/) is a containerization tool similar to [Docker](https://www.docker.com/), it manages containers for the application. It simplifies tasks such as building, running, and maintaining containers. It is ideal for creating isolated development environments such as PostgreSQL and Redis instance.

#### DBDocs

[DBDocs](https://dbdocs.io/) serves as a database documentation generator. It automates the process of generating documentation for the database schema, aiding in comprehending and managing the database structure, especially when working with relational databases like PostgreSQL.

#### Taskfile

[Taskfile](https://taskfile.dev/) is a tool for streamlining repetitive development tasks. It helps automate activities like building, testing, and deploying applications. Unlike [Makefile](https://www.gnu.org/software/make/manual/make.html), Taskfile uses YAML for configuration, making it more readable and user-friendly.

#### Golang-migrate

[Golang-migrate](https://github.com/golang-migrate/migrate) is a database migration tool designed for Go applications. It helps manage and apply changes to the database schema as the application grows, ensuring that the code and database structure stay in sync.

#### Air

[Air](https://github.com/cosmtrek/air) is an automatic reloading tool for Go applications. It keeps an eye on code changes and automatically restarts the application, making development more efficient.

#### Swaggo

[Swaggo](https://github.com/swaggo/swag) is a tool that creates Swagger documentation for Go APIs. It makes documenting API endpoints easier, helping developers understand and use the API.

#### Golangci-lint

[Golangci-lint](https://github.com/golangci/golangci-lint) is a tool for checking Go code quality, finding issues, bugs, and style problems. It helps keep the code clean and maintainable.

#### Github Actions

[GitHub Actions](https://github.com/features/actions) is a platform linked with GitHub repositories for automating tasks like building, testing, and deploying applications. It simplifies development and ensures code quality.

### Deployment

I have created a GitHub Action workflow to automate the containerization process of the application and put it on [GitHub Container Registry](https://github.com/bagashiz/go-pos/pkgs/container/go-pos). Then I manually deployed it on my personal VPS with [Nginx](https://www.nginx.com/) as reverse proxy. I might consider writing another blog post to explain my VPS setup.

You can explore the application's Swagger documentation at this URL: [`https://gopos.bagashiz.me/docs/index.html`](https://gopos.bagashiz.me/docs/index.html)

[![Go-POS Swagger Live Documentation](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fg4c5awnunlu0fgpf3opt.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fg4c5awnunlu0fgpf3opt.png)

## Source Code

I don't want to make this post too long. So if you are interested, please check out the complete source code for this project on my [GitHub repository](https://github.com/bagashiz/go-pos). You can access and explore the code base, review the application's structure, and even contribute to its development.

## bagashiz / go-pos

### Simple RESTful Point of Sale (POS) Service API written in Go using Gin web framework, PostgreSQL database, and Redis cache. Proof of concept of implementing Hexagonal Architecture in Go.

## Go POS

## Description

A simple RESTful Point of Sale (POS) web service written in Go programming language. This project is a part of my learning process in understanding [Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture/) in Go.

It uses [Gin](https://gin-gonic.com/) as the HTTP framework and [PostgreSQL](https://www.postgresql.org/) as the database with [pgx](https://github.com/jackc/pgx/) as the driver and [Squirrel](https://github.com/Masterminds/squirrel/) as the query builder. It also utilizes [Redis](https://redis.io/) as the caching layer with [go-redis](https://github.com/redis/go-redis/) as the client.

This project idea was inspired by the [Ide Project untuk Upgrade Portfolio Backend Engineer](https://www.youtube.com/watch?v=uAR1kjyeDtg) video on YouTube by [Asdita Prasetya](https://www.youtube.com/@asditaprasetya), which provided valuable guidance and inspiration for its development.

## Getting Started

1. If you do not use devcontainer, ensure you have [Go](https://go.dev/dl/) 1.23 or higher and [Task](https://taskfile.dev/installation/) installed on your machine:
	```md
	go version && task --version
	```
2. Create a copy of the `.env.example` file and rename it to `.env`:
	```md
	cp .env.example .env
	```
	Update configuration values as needed.
3. Install all dependencies, run docker…

  
  

## Improvements

I admit that there are a few areas of this project that still have room for improvement:

- As of now, unit tests haven't been implemented yet.
- The project currently uses [`slog`](https://pkg.go.dev/log/slog) package from standard library for logging. But switching to a more advanced logger like [`zap`](https://github.com/uber-go/zap) could offer more flexibility and features.
- Instead of directly accessing environment variables with `os.Getenv()`, integrating a configuration handler like [`viper`](https://github.com/spf13/viper) might make it maintainable.

## References

- [Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture) by Alistair Cockburn
- [Ready for changes with Hexagonal Architecture](https://netflixtechblog.com/ready-for-changes-with-hexagonal-architecture-b315ec967749) by Netflix Technology Blog
- [Hexagonal Architecture in Go](https://medium.com/@matiasvarela/hexagonal-architecture-in-go-cfd4e436faa3) by Matias Varela