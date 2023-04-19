Before the seeding can start, there are prerequisites that you might be dependent on the client such as subscriptions, organization, and etc. **Please make sure to obtain these items (mostly from the client or the engagement manager) beforehand so that you will not encounter any blockers when seeding**

---

## Azure Subscription
An Azure Subscription is required to create Azure Cloud Resources, such as an App Service (Web App) to which you deploy your applications or Databases such as SQL Server. Basically, any resource, free or not will require an Azure Subscription

## How to obtain access
Ask your client, project manager (SA), or engagement manager to grant you access by letting them invite your work email to their subscription. Make sure to let them know that you need at least the **contributor** (or owner) role to make things work. If you are setting it up on your own, don’t falter. Setting it up is very straightforward and no different than any other sign-up form.

To change access control for subscription, navigate to: Azure Portal > Subscriptions > My Subscription > Access Control (IAM). Once there you should see something like this

<IMG  src="https://lh3.googleusercontent.com/-kp8N2uGa9AiJBkDodManxp5gamsEadTWCKj1s1jHgbQ7YLcPL6q3MnAIkG06EUti1Sfb-usQytv3CuYIgBJD_voakYW2SlwAhaU1oUYCge1Hh8x6qOzfIIhiOioenPpF4VOmAca"/>


## What happens if I don’t have access
- You will not be able to create Azure Resources hence,  you cannot deploy your projects to the cloud
- You will not be able to set up your CI-CD/Release Pipelines and check if they work because there are no resources to check to begin with
- You will get blocked and might need to wait for a while for you to proceed to the next steps of seeding. So make sure you have access to this as soon as possible

## Azure DevOps
The AzureDevOps will contain the source code, sprints/board, and release pipelines. The role of the Project Seed will mostly revolve in this as the primary responsibility is to set these things up so they won’t become blockers when the core team gets on-boarded

## How to obtain access
Ask your client, project manager (SA), or engagement manager to grant you access by letting them invite your work email. It’s easier to create one on your own and it will also automatically give you full access rights. But most of the time, these are created by the clients so they will have full ownership

Make sure to
- Have a **Basic access level** otherwise, you won’t be able to access the Repos and Pipelines tab which are essential to this role
  - Grant basic access to users using this page https://dev.azure.com/<organization_name>/_settings/users

- Be a **Project Administrator** otherwise, you can’t manage sprints, backlog, work item states, and more
  - Make someone a Project Administrator through the Add administrator button located on this page https://dev.azure.com/<organization_name>/<project_name>/_settings/

<IMG  src="https://lh3.googleusercontent.com/Cp6OqQ72_Tjk_hFv0cXMeQW44V8giviq7uNS67nOmhhMsRO_YrqExyYMuc5tMzhH5y27J85hy2_LkBPdkvnFXkqwd0AbZ666u6etugr7mlLyQVsIu1C6dAUbiH28cpBlCd7haDZE"/>

## What happens if I don’t have access
 - You cannot do Project Seeding, AT ALL
   - The role revolves around setting up the repositories, build and release, sprint board, and more. These are all found in Azure DevOps