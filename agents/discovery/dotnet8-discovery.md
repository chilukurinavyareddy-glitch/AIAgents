# Discovery Plugin: .NET 8

Plugin id: `dotnet8-discovery`

Use when the application uses .NET 8 or targets .NET 8.

Detect:

- solution and project layout
- API startup project
- minimal API or controller routing
- dependency injection registration
- middleware pipeline
- options/configuration patterns
- health checks, Swagger, logging, auth, tests, and publish targets

Output notes:

- confirm `dotnet build`, `dotnet test`, and `dotnet publish` targets
- identify shared backend locks such as API startup and dependency injection
- identify service, repository, domain, and common project boundaries
