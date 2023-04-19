We've made this lightweight, easy-to-digest guide on what you need to know about our latest `.NET 6` (ASP.NET Core) project template, and how to maintain code structure and best practices.

---

1. Interfaces should be **"abstract"**, and must be kept on the `Infrastructure` project
   - When creating interfaces

2. All services (interfaces) must return `Response<T>`. You **should not create** custom response classes in the Infra

3. Web Responses found in the API project (aka web models) are responsible for **translating error codes** returned by the services **into HTTP status code** that is valuable for the clients. (See Identity Web Response examples)

4. **Helper** classes should **not** have interfaces; if you are creating an interface **just for testability**, you are most likely doing something wrong
   - helper class can declare their methods `virtual` so that you can easily stub them using `Moq`


5. Use **constructors** for models
   - for example when converting from one model to another, use constructor to set properties. This forces a compile error when values are not passed correctly


6. Services **should** return **Anemic Models** (only getters setters) a.k.a `DTOs`, and not `entities`. This **decouples** presentation from logic

7. There is already an `AsyncStep` class available to use if you want to **implement logic as sequential steps**. See `IdentityService` for working example