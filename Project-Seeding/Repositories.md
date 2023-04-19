## Repos
The first thing to set up is your source control (Git). It can be found under the **Repos** tab in Azure DevOps. There should be a default git repository created once a project is created and you may just rename it

## Step-by-step process
When you are in a project, click the **Project Settings** button found in the lowest left part of the screen

<IMG  src="https://lh3.googleusercontent.com/Kh11BWIcehpuIiQc0jYdur4TouctPijm9NOcBKORVB55HHRNZrxRCkW7W_7-ZJslehoPIAzSsOjBeoTBktRt4HSINYK1LMjXFLd-9j1qXN6VjQsn64rSqGHQbyn-LO4JRwqdxhqM" />

Find the **Repositories** tab, click it to list all your existing repositories. Most of the time you will need two repositories, one for the Frontend and one for the Backend. Create them if they are not yet existing. We will create a **Demo-Backend** and **Demo-Frontend** for this tutorial

<IMG  src="https://lh5.googleusercontent.com/vCepKj_e71SV5EW9m5TjefnjvrD3x8Mmysj08d-_Os0QuigwhY6tacrYVgZT9E3P6mzPt_M5YU_8CB3gcjEuQRwZQmr6MWprMHT8f4e60FdUyNq8Pzq9ujvHU6NLNedtPMbDSIYK" />

<IMG  src="https://lh5.googleusercontent.com/fwW4LvGPzruySyscu3LtzTZGy6GGzI4pvIhZ9S0wybdEKrN-KwF9Mo_YmYrYG3gN4TpjQfHu0RIg1mVSiW4E3tLK-zV5YybM_Mhe5hn52gsCm7nT8M6iREolW9WQQgIzWnainnEt" />

Once created, click the repository’s **Permissions** tab. Find/add the **Project Collection Build Service** under users and allow **Bypass policies when pushing** and **Contribute**. This will enable Azure DevOps to merge changes between branches

<IMG  src="https://lh6.googleusercontent.com/TYPITJYErWojBxew3FPH8MQaaVIuemlU9YspZQvx1Hv5ZoGi7cg4cqwknr4SGKwkj7x06aZBTqGE6K8G7K8H5fM5Cz_gU2186eZhct7CCJzqJqWQiSEkRNc75ehjFpHPouX5HYud" />

Download the Seed code/solution copy (zip) and prepare it for the next steps. **Please make sure ask if there are updated copies of the seed templates**

Backend: Please ask from your Project Lead, SE Head for Latest Copy
Frontend: Please ask from your Project Lead, SE Head for Latest Copy
---

For the Backend project, open it in Visual Studio and make sure you are able to Clean > Rebuild it without errors.

Once done, initiate a **Git bash** shell in the root directory (where the .sln file is found) of the solution. Go back to the **Demo-Backend** repository in Azure DevOps and you should be able to find a command to **Push an existing repository**

<IMG  src="https://lh3.googleusercontent.com/xWvtoH9iU7wfCbIaiOGmOpRtNjFGNLsuGBvczOTLs8BhAUEMp9eGZwd6VECWM4qEaYodqMAv6kBoVMGYgKhZQxoIgXDKiXycvzEDq0zY1ln_bd266CN0LN-MD0zeFzFyCV66Gb7X" />

Before executing those commands, execute these commands first:
1. git init
1. git add .
1. git commit -m “initial commit”

This will init a git repository, add all files from the zip, and commit them. Next, execute the command found in Azure DevOps to finally push/upload the seed code

You are likely to get an authentication error when you execute the commands provided by Azure DevOps. Hit the **Generate Credentials** button, and use the password generated to authenticate. Once done, refresh the page and you should be able to view your newly uploaded files

<IMG  src="https://lh3.googleusercontent.com/oZ_XsPxp8WVIsiLZFk6R3O5s3XumX34F92yqLgBppriDzYAcAZHZoaSm6KNgjeklyd7t7KhIpVoYTnA14QFGq2lnWx-7r1S6tY_eCAHTzbl9ZiERs5t6yfbXm2O09GbP2RPn_aeE" />

After you verify that the files are there, immediately navigate to the **Branches** page (found in the side nav) and create the **dev** branch based on **master**. Make the dev branch the “default” branch

<IMG  src="https://lh6.googleusercontent.com/MjBqAtXeugbH08FGW47Csd4ZBrvCSkW8WQkBSkmdmxoOiPwjqIElSjUIAaejyCOHJZ5cTNN0YICuNi_xuwfhjyLY2SSD0zGTIfMymXsKa6HnyUikfITt6zThKpVF5XEHy_6B-quI" />

Once done, repeat the steps for the **Frontend** project. Note that since it’s an Angular app, instead of Clean > Rebuild, you should run npm i followed by **npm run build-dev** after you have downloaded and extracted the Frontend-Seed zip template and proceed with the git commands

## Azure Pipelines - Gated, CI, and CD

Now that the repositories are set up, the next step is to build and deploy the projects.