# **.NET Monorepo**

This repository is a .NET monorepo designed to house multiple microservices and shared libraries.

## **Repository Structure**

The repository is organized to separate shared code, services, and end-to-end tests. The example-service is provided as a blueprint for creating new services.
```
.  
├── ${{ values.domain }}.sln  
├── README.md  
├── catalog-info.yaml  
├── common/  
│   └── Shared.Library/  
│       ├── Class1.cs  
│       └── Shared.Library.csproj  
├── e2e/  
│   └── README.md  
└── services/  
    └── example-service/  
        ├── orchestra.yaml  
        ├── src/  
        │   └── ExampleService/  
        │   ├── ExampleService.csproj  
        │   └── Program.cs  
        └── test/  
            └── ExampleService.Tests/  
                ├── ExampleService.Tests.csproj  
                └── ExampleServiceTests.cs
```
## **The Example Service**

The `example-service` included in this repository serves as a template and a guide. When you create a new service, you should follow its structure:

- **`src/` directory:** Contains the main project for the service.
- **`test/` directory:** Contains the corresponding unit test project.
- **Configuration files:** Includes other necessary configuration files like `orchestra.yaml`.

## **Managing Services**

Service management can be done using the `dotnet` command-line interface (CLI) from the **root directory** of this repository (the same folder that contains the `.sln` file).

### **Adding a New Service**

Follow these steps to add a new microservice. For this guide, we will use the name `MyNewService`. Replace this with your intended service name in all commands.

1. **Create the Main Service Project**  
   This command creates a new ASP.NET Core Web API project in the correct directory (`services/MyNewService/src/`).
```bash
   dotnet new web -n MyNewService -o services/MyNewService/src/MyNewService
```
2. **Create the Test Project**  
   This creates an xUnit test project for your new service.
```bash
   dotnet new xunit -n MyNewService.Tests -o services/MyNewService/test/MyNewService.Tests
```
3. **Add the New Projects to the Solution**  
   This links your new projects to the main solution file, making them discoverable by build tools and IDEs.
```bash
   # Add the main service project  
   dotnet sln add services/MyNewService/src/MyNewService/MyNewService.csproj  
   
   # Add the test project  
   dotnet sln add services/MyNewService/test/MyNewService.Tests/MyNewService.Tests.csproj
```
4. **(Optional) Add a Reference to the Shared Library**  
   If your service needs to use code from `Shared.Library`, run this command:
```bash
   dotnet add services/MyNewService/src/MyNewService/MyNewService.csproj reference common/Shared.Library/Shared.Library.csproj
```
### **Removing a Service**

To safely remove a service, you must first unlink it from the solution file and then delete its directory.

1. **Remove Projects from the Solution**  
   Use the `dotnet sln remove` command to unlink the projects. 
```bash
   # Remove the main service project  
   dotnet sln remove services/MyNewService/src/MyNewService/MyNewService.csproj  
   
   # Remove the test project  
   dotnet sln remove services/MyNewService/test/MyNewService.Tests/MyNewService.Tests.csproj
```
2. **Delete the Service Directory**  
   Once the projects are removed from the solution, you can safely delete the service's folder. 
```bash
   # On macOS or Linux  
   rm -rf services/MyNewService  
   
   # On Windows PowerShell  
   Remove-Item -Recurse -Force services/MyNewService
```
## **Important Notes on Naming**

- **Consistency is Key:** The name you provide with the `-n` flag (e.g., `MyNewService`) is used to name the project file (`.csproj`), the project's root folder, and the default namespace in the C# code. It is best practice to keep these consistent.
- **C# Naming Conventions:** Use **PascalCase** for service and project names (e.g., `OrderProcessor`, not `order-processor`).
- **Avoid Manual Renaming:** Manually renaming a project folder after it has been created will break the reference in the `.sln` file. If you need to rename a service, it is safer to remove it and re-create it with the correct name using the steps above.

## **Building the Project**

After adding or removing services, you can verify that the solution is still in a good state by running a build from the root directory.
```bash
  dotnet build
```
If the build succeeds, your changes have been correctly integrated.
