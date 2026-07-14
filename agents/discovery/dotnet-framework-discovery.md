# Discovery Plugin: .NET Framework

Plugin id: `dotnet-framework-discovery`

Use when `project-config.yml` includes:

```text
dotnet-framework
dotnet-framework-4.6.1
aspnet-mvc
webforms
```

Detect:

- `.sln`, `.csproj`, `packages.config`, `web.config`
- ASP.NET MVC controllers, areas, filters, views
- WebForms pages, controls, master pages, code-behind files
- legacy config transforms and binding redirects
- authentication modules, forms auth, OWIN, or custom auth
- repositories, services, data access, and SQL usage

Output notes:

- flag global state, static helpers, and tightly coupled code
- flag upgrade risks for .NET 8 rewrite
- identify migration candidates for services, controllers, and shared libraries
