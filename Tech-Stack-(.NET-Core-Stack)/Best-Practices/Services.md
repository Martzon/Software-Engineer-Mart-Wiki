A class that contains all the complexity of the business that a solution is trying to solve. Ideally practices the SRP and should solve one aspect of the problem. These can also use classes (that are inspired by other design patterns) to accomplish their goal. Examples:
- `EmailService` - sending emails can be written as a separate service as it solves email-related problems. This will also be easily testable
- `SmsService` - same with emails
- `ProductService`
