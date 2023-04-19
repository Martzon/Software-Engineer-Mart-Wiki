We follow the request-response pattern for service communication. For every request, a corresponding response will be returned. These are all just models/classes that have properties.

At some point, a request might be invalid or might be unsuccessful and we will need to communicate these issues to the requestor i.e. the one that called or used our class.

Summary:
1. Create your custom WebResponse classes by inheriting from `WebResponse`
2. Override `StatusCodeMap` to match error codes to status code (http)

---

The api project has a base `WebResponse` class. You may derive your custom response models from here so that you'll inherit the `StatusCodeMap` map. It should look something like this:

![image.png](/.attachments/image-5a427aa4-4a1c-4293-94b4-d4efb755a440.png)

Two things about the image above
1. The `StatusCodeMap` provisions a way to return error codes (string) and it's intended status code (int) for the consumers to use. There's a `SetError` method to set code
2. This gets read/processed in the Api/Controller code so that the response `statusCode` and `errorCode` will be set 


Notice the `IdentityServiceErrorCodes`. This is just a class that holds constant values to avoid typographical errors because these error codes will also be used by the client (in our case, Angular Frontends) to identify what happened on the request, or for example use the code to display an appropriate error message. See example below

![image.png](/.attachments/image-ec4ffcc8-feb7-43c8-a18f-7970353c1cb7.png)

Once the two above are set in place. Your custom `WebResponse` class will be processed by the controller as seen in the code below

![image.png](/.attachments/image-06443d5a-cb98-4f33-b962-64efb9825a54.png)