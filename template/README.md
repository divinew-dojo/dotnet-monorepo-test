# .NET Monorepo

This repository contains a .NET monorepo designed to house multiple microservices and shared libraries.


## Adding New Services to Your Monorepo

### 1.
This creates a new ASP .NET Core Web API project in the current directory structure called 'MyNewService'

```bash
dotnet new webapi -n MyNewService -o services/MyNewService/src/MyNewService
```

### 2.
This creates an xUnit test project for your new service inside the 

```bash
dotnet new xunit -n MyNewService.Tests -o services/MyNewService/test/MyNewService.Tests
```