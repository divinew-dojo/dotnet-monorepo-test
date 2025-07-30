# **.NET Monorepo Template**

## **Overview**
This is a Backstage Software template that creates a new .NET monorepo on Github.

The output repository is structures to support multiple services, shared libraries, and end-to-end tests from a single solution files. 
It comes pre-configured with a basic CI/CD pipelie powered by GitHub Actions to build and test your code.

## **Details**

This Software Template creates a repository with the following structure:

1. `services/example-service`
A sample "Hello World" web application that serves as a blueprint for creating new services. It includes both a source project (`src/`) and a test project (`test/`).

2. `common/Shared.Library`
A class library project intended for code that needs to be shared across multiple services within the monorepo.

3. `e2e/`
A dedicated folder for housing end-to-end integration tests that may span multiple services.

4. `.github/workflows`
Contains a suite of CI/CD workflows for building, testing, and deploying your services in the monorepo.

5. **Solution File** (`${{ values.domain }}.sln`):
The main solution file is dynamically names based on the domain you select, tying all projects together

## **Usage**
1. **Navigate to this Software Template on Backstage.**
   *add direct link to template here*

2. **Fill in the required details.**
- **Domain**: Using the picker, select the Domain and System that this monorepo will belong to. The name of the Domain you choose will be used to name the new GitHub repository and the solution (`.sln`) file.
- **Owner**: Select the Tribe and Squad that will own this new component.

3. **Click "Create".**

4. **Access Your New Repository.**

## **CI/CD Setup**

The generated repository includes a suite of GitHub Actions workflows located in the `.github/workflows` directory to automate your development lifecycle.

- `build-branch.yaml`: Triggered on pushes to feature branches. It builds the solution, runs all unit tests, and ensures the code integrates correctly.

- `release-production.yaml`: Handles the deployment of your services to the production environment.

- `rollback-production.yaml`: Provides a mechanism to roll back a production deployment in case of issues.

- `e2e-html-reporting.yaml`: Runs the end-to-end tests and generates an HTML report of the results.

- `standalone-security-scans.yaml`: Performs security vulnerability scans on your codebase to identify potential risks.

- `synchronize-translations.yaml`: Manages localization and translation files, ensuring they are kept up to date.

