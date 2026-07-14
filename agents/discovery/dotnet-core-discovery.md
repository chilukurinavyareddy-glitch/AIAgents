# Discovery Plugin: .NET Core

Plugin id: `dotnet-core-discovery`

Use when the application uses ASP.NET Core before .NET 8.

Detect:

- `.sln`, SDK-style `.csproj`, `Program.cs`, `Startup.cs`
- controllers, minimal APIs, middleware, filters
- dependency injection registration
- appsettings and environment configuration
- EF Core or repository patterns
- authentication and authorization setup

Output notes:

- identify API startup project
- identify service boundaries
- identify build, test, and publish commands
