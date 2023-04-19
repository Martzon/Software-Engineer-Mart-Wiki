# To get started:
![image.png](/.attachments/image-8f289e0c-d576-48fe-a8a8-14fa0ac85760.png)

# Writing rules
All Cloud Firestore Security Rules consist of match statements, which identify documents in your database, and allow expressions, which control access to those documents:
![image.png](/.attachments/image-fd1141dd-a96b-447c-a8be-1d86f3a8fddd.png)

<hr/>

# Authentication
One of the most common security rule patterns is controlling access based on the user's authentication state. For example, your app may want to allow only signed-in users to write data:
![image.png](/.attachments/image-c3935d7a-69f2-4ba7-814b-e2225b7767b5.png)

Another common pattern is to make sure users can only read and write their own data:
![image.png](/.attachments/image-cbb1c77c-d411-4426-8d3a-56a04e39ae74.png)

If your app uses Firebase Authentication, the request.auth variable contains the authentication information for the client requesting data. For more information about request.auth, see the [reference documenttation](https://firebase.google.com/docs/reference/rules/rules.firestore.Request#auth).

<hr/>

# Custom functions
Using functions in your security rules makes them more maintainable as the complexity of your rules grows.

![image.png](/.attachments/image-7072071a-d7a7-4192-9ba0-f585d845ff5f.png)

In the above example I create an `IsAdminUser()` function that checks whether the requesting user is an admin or not.
The `exists()` function is a built in cloud function same with `get()`
<hr/>

# Queries and security rules
For example you want to get the collection of path `/institution/{institutionId}/forms` but you want to only allow users if they are the author of form (eg: `form.author = uid`; `uid` being the **userId** in **Authentication**)
<pre>
match /forms/{formId} {
  allow read: if request.auth.uid == resource.data.author;
}
</pre>
In your angular code for example, when you try this: 
`firestore.collection("forms").get();` - this will fail even if the user is the author of some forms. This is because some of the forms are restricted to the user. Remember the firestore rules is not a **Query**.

To be able to access if you should add filter to your code. As for the above example it should be: 
`db.collection("forms").where("author", "==", uidOfUser).get()`
<hr/>

This is the basic of what you can do in Firestore Security Rules. For in depth guide please see [Firebase Firestore Security Rules](https://firebase.google.com/docs/firestore/security/get-started)