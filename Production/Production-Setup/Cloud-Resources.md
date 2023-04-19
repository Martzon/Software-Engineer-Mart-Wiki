This guide is specific to `Azure`, but the general concept should apply to other cloud providers like `AWS` or `Google`

Because `dev` and `staging` is already set up, you will only need to mimic what those environments have. The typical setup would be `AppServices`, a `Database` e.g. `SQL`, `ApplicationInsights`, `Function Apps` and etc.

The **general rule** is to create all resources based on `staging` or `dev` in your `production` `Resource Group`

---
# Resource Creation

**IMPORTANT**: before creating these resources, ensure that you have permission from your Project Manager (from PH or SA) or Client(s) as these Production-grade resources cost money $$$

## ResourceGroups
**Ensure** you create a **separate** resource group for prod resources. **Do not** mix these resources to existing resource groups

## Regions
**Ensure** that you pick the closest region where your client is, or where most of their customers will be based. If you are not sure, consult with your PM or Client

## Monitoring (Application Insights)
When creating `AppServices` or `FunctionApps`, take note of the **Monitoring** Tab. Each resource should have respective `ApplicationInsights` resource

## AppServices (WebApp)
For each `AppService` created for production, ensure that:
 - **App Service Plan Pricing Tier** is at least `Standard 1 (S1)` - this allows you to install SSL Certificates, Custom Domain in the future, and of course this plan has relatively better specs or compute power to accommodate production load
 - **Each** API project should have respective `S1 App Service Plan`
 - **Note** that for AppServices that **only hosts a Frontend** e.g. Angular, you may include them in the same S1 App Service Plan of their respective API project
 - Ensure to configure **Monitoring** by creating an `ApplicationInsights` resource before finalizing

Please see guide images below for the important settings to note
![image.png](/.attachments/image-61ccda0e-79a0-46f4-9597-a8616748378c.png)

## FunctionApps
For each `AppService` created for production, ensure that:
 - You are in `Consumption Plan` unless otherwise not recommended by the Architect - this allows your Function Apps to Auto-scale based on load. For busier environments there's also a `Premium Plan` but often not needed. Make sure to consult your PM, Architect, or Client(s) for this
 - Ensure to configure **Monitoring** by creating an `ApplicationInsights` resource before finalizing

Please see guide images below for the important settings to note
![image.png](/.attachments/image-665a7fa3-753c-4c12-a019-0402da1ec60a.png)

## SQL Database
The pricing plan of an SQL Database should be **DTU-based** and should start in `Standard 1 (S1) Tier`
![image.png](/.attachments/image-3b4fae80-8327-4567-a396-ce48a3b56e1d.png)

For other settings, please see below
![image.png](/.attachments/image-ceaa41d0-cea1-439c-a743-e7653665d248.png)