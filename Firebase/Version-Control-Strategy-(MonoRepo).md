# MonoRepo
I personally chose the `MonoRepo` for our projects that will be written in Firebase. Due to the reason that `Firebase` is technically a platform but it can also serve as your `Backend/Database` through `Firestore`. Another reason is that both sides will be written in `TypeScript` and will almost always be used/served in conjunction.

**TLDR;** This approach will contain both our `Frontend` in `Backend` projects in a `Repository` or directory. One Repository will contain at least two apps. Worry not because we have already designed a `CI-CD` pipeline to work with `MonoRepo`

# Structure
![image.png](/.attachments/image-5ffadc33-b51f-4a53-8c47-1aaa4b4e2c79.png)

In the folder structure above, the `/app` folder pertains to the `Angular` app while the `functions` pertains to the `Backend` or our `Firebase Functions`.

**Depending on project requirements, we might not need to create `Functions`. As database access is readily available from the `Angular` app using `AngularFire` (`Firestore`)**


---

Read more about `MonoRepo` here:
https://www.perforce.com/blog/vcs/what-monorepo#:~:text=A%20monorepo%20(mono%20repository)%20is,it%20easier%20to%20refactor%20code.

https://medium.com/better-programming/the-pros-and-cons-monorepos-explained-f86c998392e1