## Naming Conventions

- **Class** names should be in singular form and a **noun**. Unless creating classes that represent a command, or a handler (chain of responsibility). Examples:
   - `User`
   - `Product`
   - `CreateUserCommand`

- **Method** names should be a **verb**; Async methods should have `Async` in the end. Examples:
   - `InsertUserAsync`
   - `SendEmailAsync`

- **Database Tables** should be in plural form. Casing should be PascalCase. Examples:
   - Users
   - Products
   - UserRoles

- **Views** should start with vw_ and **Stored Procedures** should start with sp_. Examples:
   - `sp_InsertUser`
   - `sp_UpdateOrder`
   - `vw_AustralianUsers`
- **Data Gateways** and **SQL Command Factories** should start with the table name it transact against. Examples:
   - `ProductSqlDataGateway / ProductSqlCommandFactory`
   - `OrderSqlDataGateway / OrderSqlCommandFactory`