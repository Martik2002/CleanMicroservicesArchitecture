# CleanMicroservicesArchitecture

> 🚧 **Work in progress** — the service skeletons are in place; business logic is being implemented.

A microservices system in .NET where every service follows **Clean Architecture** internally. The goal is to combine independent, separately deployable services with a consistent, testable structure inside each one.

## Services

| Service | Responsibility | Status |
|---------|----------------|--------|
| **IdentityService** | User registration, authentication, issuing JWT tokens | Scaffolded |
| **NotificationService** | Sending notifications (email, SMS, push) in response to events | Scaffolded |

## Architecture

Each service is self-contained, with its own database and the same layered structure:

```
Service/<ServiceName>/
├── src/
│   ├── Domain/          # Entities, value objects, domain events — no dependencies
│   ├── Application/     # Use cases (CQRS with MediatR), validation, interfaces
│   ├── Infrastructure/  # EF Core, external services, persistence
│   └── Web/             # ASP.NET Core API host
└── tests/               # Unit and functional tests
```

Dependencies point inward: `Web → Infrastructure → Application → Domain`. The domain and use cases never depend on frameworks or databases, which keeps business logic easy to test and change.

Each service is based on the [Clean Architecture template](https://github.com/jasontaylordev/CleanArchitecture) by Jason Taylor.

## Tech Stack

- .NET 9, ASP.NET Core
- MediatR (CQRS), FluentValidation, AutoMapper
- Entity Framework Core, SQL Server
- NUnit for tests

## Roadmap

- [x] Solution structure and service skeletons
- [ ] IdentityService: registration, login, JWT and refresh tokens
- [ ] NotificationService: email/SMS senders
- [ ] Asynchronous communication between services (message broker)
- [ ] API gateway
- [ ] Docker Compose setup for running all services together

## Running a Service

```bash
cd Service/IdentityService/src/Web
dotnet run
```

## License

[MIT](LICENSE)
