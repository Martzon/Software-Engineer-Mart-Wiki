## Creating a Function App Resource
1. Go to portal.azure.com
1. Select Create New Resource and look for or type in Function App
1. For the **Basics** tab:
   1. Make sure to follow the naming convention when naming the resource
   1. Put in .Net Core as the runtime stack
   1. Put in the appropriate .Net Core version - If you are working with .Net Core 2.x and there are no options for version 2.x, don’t worry as it can be changed later
   1. Make sure to put in the proper region (Southeast Asia)
1. For the **Hosting** tab:
   1. Select the proper storage account that the function app will use and/or reference
   1. Select Windows OS
   1. Select Consumption as Plan type
1. Under **Monitoring** tab, you may either select a preexisting Application Insights resource or create a new one
1. Proceed and Azure Portal will now begin to create the Function App Resource (If you are working with .Net Core 2.x continue to follow the steps below)
1. Once Azure has created the function app, navigate to it.
1. In the Overview screen, find and select **Function App Settings**, a new tab should pop up
1. In the **Function App Settings** tab, change the runtime version from **~3** to **~2** and save

## Setting up CI-CD of Function Apps in DevOps
### One-Pipeline-Deploys-All Setup
**Note**: Preferably, this should only be used on Dev environments. Moreover, this entry assumes the project already have pipelines that are set up

### CI setup
1. In Azure DevOps, navigate to the project pipeline (CI) and then go to the **Tasks** tab and select the **Publish** step
1. In **Path to Projects**, add the relative link(s) to the function app(s) to add. In the image shown below, an **Audit Trail** Function app was being added so the relative link to the **.csproj** file was added.<br/>
<IMG  src="https://lh4.googleusercontent.com/xtMBvBg5Bs3EB5abX8rwgDwRIVU9CgY1mExcPZN6rC1aSAIxDE4C3kKCkxIg-O_-BCIykhRKYb2vJ-B_yfBvHjaDlmMfFyXPja7nUvJYNobh2dkr5gq9usHTGc-Y_xThZqNIW1Ge"  width="602"  height="247" style="margin-left:0px;margin-top:0px"/>
1. Save the changes and queue a build - this is to generate a new **Artifact**. Wait for the build to finish

### CD setup

1. Navigate to **Pipelines** at the DevOps sidebar, select **Release** and then select the CD of the repository
1. Click **Edit** at the upper-right and navigate to the **Tasks** tab
1. Click the plus sign to the right of **Run on agent**
1. Add an **Azure App Service Deploy** task <br/>
<IMG  src="https://lh4.googleusercontent.com/dxm7QGUXB1BVjvEIV26i-hSrV8BQ6tOhbRg-JPVfD-csbtpP5l2SYIYRvuFlYPnjl4Z7wSQs8A34uaW50BTlIxbYKFDTlUhKXNm9fYncS_2U9ZaP0nnbIquRQSc8aRUNhOs3H2Db"  width="713"  height="280" style="margin-left:0px;margin-top:0px"/>
1. Fill up the required fields:
   1. Select the proper Azure Subscription
   1. For **App Service type**: select **Function App on Windows** (or Linux depending on what OS you chose when you created the Function App in Azure Portal
   1. For **Package or folder**: click **Browse**. A small window should pop up. Expand all items and find the .zip file of the appropriate function app - If you cannot find the **.zip** file either the artifact is not yet updated or the CI of the repository was set up wrong
1. Save the settings and create a release
1. If the release was successful, verify that your function app is properly deployed by going to Azure Portal and navigating to the appropriate function app(s)
1. At the Function App resource, click **Functions** at the left sidebar. You should see the names of the method calls inside the function app there

## One Service, One Pipeline Setup (Path filters)
### CI setup
1. In Azure DevOps, navigate to **Pipelines** > **Pipelines** and then select **New Pipeline**
1. A numbered list should show, select **Use the classic editor**
1. In the next page, select Azure Repos Git as the source. Select your appropriate Backend repository, then select the proper default branch (staging when making a staging CI, master when making a master CI)
1. In the next page, select the **ASP.NET Core** template
1. In the proceeding page click on the **Pipeline** box. Rename the CI properly (i.e. follow the naming convention and name it based on the function app it will build).
1. Adjust **Agent Specification** into the appropriate agent in your DevOps
1. Next, we need to configure the tasks involved in the CI: No changes are needed for the Restore task
1. For the Build task, change the **Path to project(s)** line into the proper path of the function app, similar to what is shown below: <br/>
<IMG  src="https://lh3.googleusercontent.com/VELKMLtoJ_n3tOrcc8XcSfZUs65i5pr9jA1esSZPttvyAsAHWEKfB1Cz_c8DFjg5K5q9r0Jd4WBYsBDOBwEltYtmmucUyPnpV-J9B-4c_FsPRSzNP1JguidSRdy7yBkGetRkE4-j"  width="602"  height="247" style="margin-left:0px;margin-top:0px"/>
1. At the Publish task, un-tick the **Public web projects** checkbox. Next, click the chain icon beside **Path to project(s)** and then click **Unlink**. Lastly, input under "Path to project(s)" the same thing that you put on Step 9.
1. To set up path filters
