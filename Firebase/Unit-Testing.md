It is **important** to note that in a `Firebase` project, we won't necessarily test our functions (sometimes we will), but instead we will test our `*.ts` service code that will contain the business logic.

**This guide assumes that:**
1. Your `functions` work similar to a `controller` where it just calls/passes the request to a `Service` class
2. Your `Services` should make use of it's constructor to inject dependencies and not just by straight import using `require` or `import`
    - For example, if your service uses a 3rd party npm package, you can easily `import * as package from 'package'` that library and use it using the `package` variable throughout the file/class. There should technically a way to stub this, but the more intuitive way to practice `DI` is to assign the variable to the class' `constructor`

**Correct**
```
import { MailService } from '@sendgrid/mail';

public class EmailService {
  constructor (
    client: MailService 
  ) {}

  async sendSomething(...): Promise<void> {
    ...
    await this.client.sendMail(...);
    ...
  }
}
``` 

**Avoid**

```
import { MailService } from '@sendgrid/mail';

public class EmailService {
  constructor (/* note the empty constructor */) {}

  async sendSomething(...): Promise<void> {
    ...
    const service = new MailService(key);
    await service.sendMail(...);
    ...
  }
}
```  

3. You have knowledge on how `Stubs` or `Mocks` work to test classes with `dependencies`
4. 