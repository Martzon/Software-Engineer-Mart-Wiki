The guide will teach you to migrate your Monolith App with Services (currently as .dlls) to Microservices using Azure Function Apps

## Code Changes

### Pre-requisites
 - All service interfaces e.g. IDocumentService should be placed in the Infrastructure project under the Interfaces folder
 - All Request-Response classes and relevant model classes should be in the Infrastructure project and foldered per service e.g. Infrastructure/Messages/{ServiceName}. Both Services and Clients will share the same models/contract. This will allow us to easily setup path filters in our release pipelines later on

### Function Apps
 - Create Function Apps for each Service you have. [1]
 - In the newly created Function App, add the Service Project as reference
 - The Function App template comes with default Function1. Rename it based on requirements. Attempt to instantiate the Service Class to be used in the Run method. You may configure Dependency Injection later. [2]
 - Run the project; The default port for function apps is 7071. Ensure that on the launched command prompt that you are able to see routes. E.g. localhost:7071/api/functionName. We will soon configure port numbers so that you are able to run multiple function apps at the same time. [3]

[1] Note that some Services can be combined together into one function app depending on the domain, the problem it solves, or their bounded contexts. E.g. user, and authentication service can be combined into one function app just having 2 different functions/endpoints and still use the same IService implementation.

[2] Since your Service adheres to Request-Response pattern and Http-trigger function apps accepts _HttpRequest_ you need to create an [extension method](https://gist.github.com/amcpanaligan/20583c281a0427b52070ad702fd84d1c) to convert it to your models

[3] Please follow this [link](https://stackoverflow.com/questions/44976890/how-to-run-azure-function-app-on-a-different-port-in-visual-studio) to change ports

### Clients (Implements `IService` interfaces)
We will consume a function app/service using a _Client_ class. These classes only send Http requests to the function apps. Note that each function app/service should only have one Client class.
 - The clients should have separate class libraries AND implements the same interface of the service it’s wrapping. E.g. `DocumentService` implements `IDocumentService`, so as `DocumentClient`.
   - This will allow us to easily swap implementations of `IDocumentService` in the API controllers
 - The client class should accept the function app endpoint, and keys through its constructor since each client will now represent a function app/service
 - The client class should only use the HttpClient class to issue http requests. RestSharp is an option but stay away from it unless otherwise required. [1]

[1] Install the NuGet package Microsoft.AspNet.WebApi.Client for extension methods such as PostAsJsonAsync<T>, and ReadAs<T>

### Web API
 - All controllers should now depend on the Client implementation of Services e.g. `DocumentClient` than `DocumentService` for `IDocumentClient`
 - The `appSettings` should contain relevant function app endpoints and keys for injection
 - Configure/change dependency injection in Startup.cs for your client classes. [1]

[1] Since the constructors of client classes accept strings, you need to inject them from the configuration [like this](https://gist.github.com/amcpanaligan/581907a387006f01aa3508021b2eabd7) 

### Securing Function Apps
 - In azure portal, navigate to the function app. You should be able to see “Keys” and copy them
 - Put these keys in the Api’s configuration together with that function app’s respective URL
 - These function keys will be appended to the headers for every http requests that the client class performs with key: `x-function-keys`
 - Change the AuthorizationLevel from Anonymous to Admin
 - Note that all Function Keys shall only be put in the Server Side and kept secret all the time like any other connection strings


### Function Apps Dependency Injection
https://docs.microsoft.com/en-us/azure/azure-functions/functions-dotnet-dependency-injection


## Release Pipelines
### General Guidelines
 - Each Service or Function App should have a corresponding CI-CD or Release Pipeline Setup (1:1)
   - Changes in DocumentService should not affect UserService. Only the Document Service’s Release Pipeline should trigger.
 - A build (CI) and release (CD) shall be triggered when relevant code changes are pushed that affect the service Even changes as little as adding a property to a request class needs a rebuild and redeploy. We will set up the CI to trigger when certain directories or paths, and files have changed. Some of the files and folders are:
   - Models/Requests/Responses etc (e.g.    -    -    - 
   - Infra/Document/Messages)
   - The Client project
   - The Service project itself
   - The Service interface
   - The Service function app equivalent
   - Service dependency e.g. this service uses another service
 - The Web API project itself is a Service on its own. Any code changes require redeployment

### One service one pipeline setup
Create the CI, configure the triggers and path filters. Follow the guide above of which paths to put

<IMG  src="https://lh6.googleusercontent.com/1XTi8VzK0mG6Z2sNAX_sCsd8-TGUW3-uqzHsUUOBmM_vr2Qz30ht5B1D82yWlL07qEI6cayhbmeEMenhGQqdg3dqC8Ic1dTY6t-DgSicVIIEA0O6VeOaNrnHD-hXoq1R8J4nyeZA"/>

The next steps are:
 - In the CI's Build step, it should only run build the `Functions.Document.csproj`
 - In the CI's Publish step, it should only publish the `Functions.Document.csproj`. The published project gets deployed to the actual Function App resource in Azure
 - CD should use the CI as the artifact to deploy to the corresponding function app/azure resource

### Which paths are needed to be included in the CI trigger?
Start with one Service and Identify all the dependencies (projects used/.dlls imported). Most of the time these are:
 - The `Infra` project specifically `Models`, `Interfaces`, `Messages (Request-Response)` used by the Service
 - Other `Services` imported
 - The `Functions` Project (path to `csproj`)

**IMPORTANT**: The thinking behind these filters is to track changes that a Service use. If any of the dependencies change, the service should be rebuilt and potentially redeployed. Each services' deployment can be isolated from each other despite being stored in the repository using this approach

### Additional Notes and Tips
 - When determining which functions to start with, instead of looking at the architecture, it’s better to refer to the Web API Controller. You want to be able to do an end to end implementation from the Web API to the service, there could be some services in the architecture that don't have any endpoint in the Web API but are used by other services e.g. Email Service.