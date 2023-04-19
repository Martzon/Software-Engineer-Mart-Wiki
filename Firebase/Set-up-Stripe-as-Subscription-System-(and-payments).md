In this guide, we will setup your Firebase App (in firebase console) to integrate with Stripe so that it can handle your Payments and your customers' Subscription. As you may have predicted, you need to have an already setup Stripe account with valid `publishable key` and `secret keys`. While following this guide, make sure to use Stripe's `Test Mode` i.e. also, get only **TEST** `api keys`


1. Get everything from `Stripe`; The image below points to 2 different things that are equally important. First, the toggle button to the left should be toggled to `Viewing test data`. Also notice the orange text. Second, in the main part of the screen, find the `Get your test API keys` section and look for `Publishable key` and `Secret key`. The beginning of these keys should have `pk_test` and `sk_test`. In `live` mode, the keys should say `pk_live` and `sk_live`.

**Pro tip:** Make sure to switch your keys eventually through configuration

![image.png](/.attachments/image-311ebcad-713d-4fa7-92f5-2df70e355be1.png)


2. Go to `Firebase Console` and hit the `Extensions` menu item in the bottom. Next, find the `Run Subscription Payments with Stripe`. Hit `Install`

![image.png](/.attachments/image-d5e729fd-8ce7-4378-ae97-148f4dcaf53a.png)


3. In the `Configure Extension` step, take note of the encircled fields. The `users` should be the `collection` name where you duplicate your users in `Firebase Authentication`. The second encircled field about `Sync` says that every time a product is created in `Stripe`, it will automatically be synced to your `products` collection. This will allow you to show these products in your frontend along with their respective prices. The third and last encircled field is the `publishable key` you'll get from `Stripe`. Make sure to switch from `test` to `live` keys at some point.

![image.png](/.attachments/image-c30ecf33-0871-46b6-8b4e-3a37cefeb864.png)

![image.png](/.attachments/image-06dfa95f-f267-4dd0-a886-78d1f9b395ad.png)


4. From here on, once installed, follow the guide provided by the extension. It's more comprehensive but straightforward. Next, you'll need to create a webhook in `Stripe` and so on

![image.png](/.attachments/image-9fa8be74-e901-47c4-b780-e91f16ed7b70.png)