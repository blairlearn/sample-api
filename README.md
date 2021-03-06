# placeholder api
This is a template repository for creating a dotnet API. It contains the common files and directory structures, but does not include the actual API project.

## Steps for creating an API project.

1. Create a new GitHub repository, using this repository (dotnet-api-template) as the template.
2. Clone the new repository locally.
3. Rename the solution file.
   ```
   git mv placeholder-api.sln my-cool-api.sln
   ```
3. Create the API project
   ```
   dotnet new webapi --no-https --name NCI.OCPL.API.MyCoolProject --output src/NCI.OCPL.API.MyCoolProject
   ```
4. Add the API project to the solution
   ```
   dotnet sln add src/NCI.OCPL.Api.MyCoolProject/
   ```
6. Replace the generated `appsettings.json` with the placeholder file.
   ```
   rm src/NCI.OCPL.Api.MyCoolProject/appsettings.json
   git mv placeholder-files/appsettings.json src/NCI.OCPL.Api.MyCoolProject/appsettings.json
   ```
5. Copy the placeholder `web.config` to the API project (be sure to replace the placeholder name in the file with the real name).
   ```
   git mv placeholder-files/web.config src/NCI.OCPL.Api.MyCoolProject/
   ```
6. Add the API project to source control
   ```
   git add src/NCI.OCPL.Api.MyCoolProject/
   ```
7. Rename the placeholder test project and add it to the solution.
   ```
   git mv test/NCI.OCPL.Api.Placeholder.Tests/ test/NCI.OCPL.Api.MyCoolProject.Tests/
   git mv test/NCI.OCPL.Api.Placeholder.Tests/NCI.OCPL.Api.Placeholder.Tests.csproj test/NCI.OCPL.Api.MyCoolProject.Tests/NCI.OCPL.Api.MyCoolProject.Tests.csproj
   dotnet sln add test/NCI.OCPL.Api.MyCoolProject.Tests/
   ```
8. Reference the API project from the test project.
   ```
   dotnet add test/NCI.OCPL.Api.MyCoolProject.Tests/ project src/NCI.OCPL.Api.MyCoolProject/
   ```
9. Rename the integration tests docker folder to match the api.
   ```
   git mv integration-tests/docker-placeholder-api/ integration-tests/docker-my-cool-api/
   ```
10. Update integration test files to match API and project file names:
    * `integration-tests/docker-placeholder-api/api/Dockerfile`
      * solution file name
      * docker directory name
      * executable name
    * `integration-tests/docker-placeholder-api/docker-compose.yml`
      * docker network name (networks entries for elasticsearch, api and main)
      * path to API Dockerfile
11. Update GitHub Actions workflow file (.github/workflows/workflow.yml)
    * `test_build_release` job:
      * Uncomment Publish and Upload steps
      * Project name in the Publish step
      * Artifact name in the publish step
    * Uncomment and update `integration_tests` job
      * Artifact name in the "Download Published Artifact" step
      * `APP_ASSEMBLY` name in the "Start API" step.
12. Get the Karate.jar file (GH templates don't allow files greater than 10 MB.)
    ```
    curl -L -X GET https://github.com/intuit/karate/releases/download/v0.9.5/karate-0.9.5.jar  -o integration_tests/bin/karate.jar
    git add integration_tests/bin/karate.jar
    ```