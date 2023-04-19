Are model classes used to represent input and output. The client sends a request to the server, and the server responds with a response. For example:

You want to get all payments made by a user. Then you will create `GetPaymentsByUser` request and response. The request at least contains the `UserId`, and maybe a start date of payments to query. The response class will have an array of payments.

## Note: All Request/Response Models should belong to the Infrastructure project and are meant to be shared across Services/Projects or the API project. The concept is that these models represents how your solution responds whenever a client requests for something
