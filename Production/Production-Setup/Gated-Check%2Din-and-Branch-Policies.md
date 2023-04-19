As stated before, these two are already existing because of `dev` and `staging`. It's fairly easy to duplicate the existing ones for your `prod/master`


## Gated Check-in
Are found under the `Pipelines` menu and `Pipelines` menu item with the name preceded by "Gated". There are two types of Gated builds
1. Created using a `yml` file
2. Created using Azure DevOps UI (old version)

### Cloning
If it was created using a `yml` file, you cannot directly clone it using Azure DevOps UI. You may follow this steps to clone

For `yml` created Gated Builds:
1. Navigated to the Gated CI/Pipeline
2. Click Edit
3. Copy the `yml` definition to clipboard
4. Created a new Pipeline with the same `yml` definition

See example `yml` below:
![image.png](/.attachments/image-f5913bd8-e7cc-45b9-b9a9-ff1d046c513f.png)


## Branch Policies
1. Navigate to `Repos > Branches`, then say hover on `dev` and click on `Branch Policies`

![image.png](/.attachments/image-c4f3f1c9-1bc7-4026-8f53-9da237cdbf29.png)

2. On a new tab, open the branch policies for `master` which is not yet configured, copy all configuration found in `dev` or `staging` to `master`. See below what to change/configure

![image.png](/.attachments/image-56567cc9-c4ed-4bc7-9bce-296523c81aac.png)

![image.png](/.attachments/image-d4ef8e24-6103-4afb-99cf-ed35c83a34fa.png)


3. Gated Check-in below should be pointed to the newly created/cloned above