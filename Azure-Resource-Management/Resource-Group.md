## Resource Group
A resource group is a container that holds related resources for an Azure solution. The resource group can include all the resources for the solution, or only those resources that you want to manage as a group. You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization. Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.

The resource group stores metadata about the resources. Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored. For compliance reasons, you may need to ensure that your data is stored in a particular region.

## Creating a Resource Group
1. Go to portal.azure.com
1. Select Create New Resource and look for or type in Resource Group
1. For the **Basics** tab:
   1. Choose the subscription under which the resource group will be created
   1. Make sure to follow the naming convention when naming the resource group
   1. Make sure to put in the proper region (Southeast Asia)
1. Proceed and Azure Portal will now begin to create the Resource Group
