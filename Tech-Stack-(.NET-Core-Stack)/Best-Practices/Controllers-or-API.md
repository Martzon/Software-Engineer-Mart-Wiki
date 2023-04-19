The entry point of the application; Usually, each method should only consist of 3 lines that:
- Accepts a request from the client
- Calls the service and passes the requests
- Returns the response to the client

Controllers are in the ASP.NET project and should be treated as a microservice like any other regular services (e.g. it should have it’s own models)

Other notes for the web api project:
- It can reference services
- It should always be setup with Dependency Injection (see guide below)

