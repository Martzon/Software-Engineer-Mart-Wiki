# Project Seeding
is the process of setting up project pre-requisites such as `Azure DevOps`, `Repositories`, `Azure Subscription`, `Release Pipelines`, and etc. so that the project and the `Core Team` can proceed seamlessly towards it's delivery.

***Note** that you must read through the individual sections to accomplish checklist
***Also Note** that our (this) Azure DevOps contains sample Code Repositories and CI-CD that can serve as your working guide. If you don't have access (Basic License) please reach out to the Software Engineering Head


# Project Seeding Checklist

## Before Start
The project typically has a kickoff meeting before the first sprint planning starts. These items are needed to be set up before the first sprint. These items take away all setup dependencies or blockers a team might encounter once the first sprint has started. 

## Backend
- Database Connectivity from the code level
- IoC container or Dependency Injection in the API project
- Configuration using appSettings.json
- Database Project and publish functionalities
- Unit Test Project that uses Moq or Stubs for dependencies
- Logging to Application Insights
- Exception Handling per layer (Data and Service Exceptions. try-catch-wrap-rethrow)
- Test runSettings for code coverage
- Reusable helpers, base classes such as:
- Specification<T>
- SqlHelper

## Frontend
- Environments
- Scripts in package.json (start-local, build-dev, and etc)
- Configuration in angular.json for environments
- Common Dependencies
- Routing
- Bootstrap - NgBootstrap
- Fontawesome

## DevOps
- Git repositories for both Frontend and Backend - Dev branch
- Branch Policies and/or Gated Check-ins and the following are ran:
- Tslint
- StyleCop
- Unit Tests
- Comments are required to be resolved in Pull Requests
- Dev-CI for both Frontend and Backend
- Dev-CD and Promote to Staging for both Frontend and Backend
- Wiki - include details as much as possible such as:
- Link to prototypes
- Link to the Dev environment
- Architecture Diagram
- Database Credentials
- Azure Portal
- AppServices, Databases, Application Insights and other resources needed for the Dev environment


## During the Project
- Ensure coding standards are in place. Review PRs and provide feedback
- Facilitate Sprint Planning Meetings and Retrospectives
- Ensure correct branching strategies
- Work hand-in-hand with the Project Lead to set up DevOps for the staging environment


## Post-Seeding
- Follow up Code Reviews every X months (Interval TBD)
