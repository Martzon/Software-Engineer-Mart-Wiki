**Note:** This not entirely for Staging or Prod only. It could be any other new instance whatever you may want to call it. This is basically the procedure on how to deploy the source code to firebase


---

## Manual items that need to be created:
1. Firebase App through Firebase Console (https://console.firebase.google.com)


## Things to be created manually in Firebase
1. Hosting/Site - The place where the angular app gets uploaded. In the side nav, under Build -> Hosting, create the site by following the Wizard / Get Started Button
2. Firestore - Side nav, under Build -> Firestore, create it, select the database's region
3. Locate the values to be put in the `environment` file. Side Nav -> Gear Icon -> Project Settings -> Scroll Down and look for CDN
![image.png](/.attachments/image-69844c7c-140e-4ec4-9738-053db811a010.png)
4. Enable User/Password and Social (google) Authentication; Build -> Authentication -> Toggle Switches


## Things to do in Azure DevOps
1. You will just most likely need to clone all Gated, CI, and CDs; having to replace all "staging" strings and repository calls with the new environment e.g. "prod"
2. The `Promote to Staging` step/stage in the CD, make sure to update the merge commands from `staging` to `prod` and vice versa
2. Of course, the new branch `master`
3. Create the new Variables for the new Environment. Under Pipelines -> Library, there should be a `Firebase` Variable Group with variables like `DevToken`, `StagingToken`, obtain the new values and save it as `ProdToken` and so on. Generate the token using `Firebase CLI`: `firebase login:ci`
 
