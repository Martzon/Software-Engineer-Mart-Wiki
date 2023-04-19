## Web App won’t Start
There are instances where an ASP.NET Core Application won’t start without showing relevant error messages. Here are some of the issues that may cause it for both local and cloud

- Dependency Injection Problem - Check your classes’ dependencies i.e. injected types through the constructor. When a dependency is added to a class’ constructor but was not injected properly in Startup.cs, the app won’t start

- Environment / Configuration Problem - Our structure relies on appSettings to configure values. There are instances wherein you need to set the ASPNETCORE_ENVIRONMENT to e.g. Development or Staging so that it could pick up the right appSetting. To do this:

   - Locally, right-click the API project > Properties > Debug > Environment Variables; Create if not exist a new entry for ASPNETCORE_ENVIRONMENT and put the required value
   - In the Cloud, navigate to the App Service where the API is deployed. Under Settings > Configuration > Application Settings; Add the ASPNETCORE_ENVIRONMENT value


---

## Application won’t connect to the Database
There are times that the local ASP.NET application is required to connect directly to a **database in the cloud**. But most of these databases will have a built-in security feature that will prevent this requirement
 - Double check Connection Strings in appSettings; Usually this can be found in the Project’s Wiki. Otherwise, you may also find it in Azure or where the Database is hosted
 - Microsoft SQL Server - Check firewall settings. Often times, the IP address of a computer/application needs to be whitelisted/allowed for it to be able to access the server


---
There are times when a request body, query, or basically any value passed by the Frontend won’t bind to the backend. Here are the common solutions:

- Check the `JsonProperty` attribute for case-sensitivity issues
- Check the controller method parameter(s)
  - Naturally if the request is a `POST` you would mark your controller parameter with a `[FromBody]` tag so that ASP.NET will know where the data will come from a request. This should also be the case for PATCH and PUT requests
  - Otherwise for `GET` requests that make use of query string parameters e.g. `/orders?id=25`. Make sure to add the `[FromQuery]` attribute beside the method’s parameter
  - Example: `CreateOrderAsync([FromBody] CreateOrderWebRequest request)`

---

## Requests bound properly from Front to Backend but not saved correctly in the Database
There are instances where requests are sent correctly but when saved to the database, there were missed out fields. It could be vice-versa that the data is selected and complete but when serialized to the frontend, there are missing fields/values
- Check model parsing **Extension Methods**; Models come in as Web Models from the Frontend and saved as Entities. When the Extension Method that converts to/from these models miss out one property then that might probably be the root cause

---
## Requests won’t go through the API -- Error 401
Controllers are secured using the `[Authorize]` attribute; Most of the time we use **JWT** as the authentication technique. The authorize attribute checks for the token and validates it, otherwise it returns 401 Unauthorized. Common issues below:
- The JWT/authentication token is not attached or sent through the request headers
- Check Network Tools; Double check if the token exist
- The token might be expired, or was issued by a different provider e.g. environment which may cause authentication issues. Usually requesting another one resolves the issue
- All authentication errors will return 401 regardless of the cause. This will be otherwise too difficult when you encounter it in a deployed environment.

---
## ModelState: [Required] Attribute is not working and potentially other attributes as well
The `[Required]` attribute works only for **Nullable** types (Nullables are denoted by the `?` character e.g. `int? Age`). For example if you Model wants to validate an int field say age. Declaring it as public int Age… and putting the `[Required]` attribute won’t work. This is because the default value of an int is 0 and therefore the `[Required]` attribute won’t catch it.
 - All types that you wish to validate using the [Required] attribute should be Nullable; In this case int should be declared as int? in the Web Model(s) for it to be validated properly

