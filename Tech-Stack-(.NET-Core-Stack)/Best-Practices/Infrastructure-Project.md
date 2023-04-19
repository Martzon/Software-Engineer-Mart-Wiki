The only shared project across the solution. It can contain reusable functionalities that have nothing to do with the business or the problem that a solution is trying to solve. Examples:

- Loggers
- Helper Classes - database helpers such as SqlHelper that wraps the native .NET sql classes for testability
- Extension Methods - such as `GuidExtensions` that has methods to check if `Guid` is valid and etc
- Base classes - such as `Specification<T>`
- Messaging Classes i.e. Request-Response objects/models
