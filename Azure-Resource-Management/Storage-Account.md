By default, creating a function app already creates a corresponding storage account that will host all of the files for the said app. However, when in need of storing blobs or other files that the function app has to access/process, it is best to create a separate storage account that solely handles these files, so that the function app files are separate from the files for processing. This reduces the risks of losing both when one of the storage accounts fail. Here are the instructions for creating a stand alone storage account:

## Creating a Storage Account Resource

1. Go to portal.azure.com
1. Select Create New Resource and look for or type in Storage Account
1. For the Basics tab:
   1. Make sure to follow the naming convention when naming the resource
   1. Choose the proper resource group
   1. Make sure to put in the proper region (Southeast Asia)
1. Proceed and Azure Portal will now begin to create the Storage Account Resource
