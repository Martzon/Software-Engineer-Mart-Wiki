# Introduction
**Production** is the most critical environment to setup because it's expected to be used by actual end-users or customers. The good news is that, this is just like any other environment setup e.g. dev, staging, which at this point should already exist in your project, which make production setup relatively easier as you won't start from scratch

# Components
This section list down the different things that we need to setup, take into account when setting up production. **Note** that for every item in this section is most likely existing in `dev` or `staging`. It is very helpful for you to compare and check first so that you'll get an overview what you need to set up for `prod`

## Please read the individual wiki pages on how to set up each component

### Repository
The `prod` environment should directly map to the `master` branch of your code repository. If it does not exist yet, create it based from your `staging` branch.

If it's not updated, be sure to merge latest **stable** and **tested** changes from `staging` to `master`

### Gated Check-in and Branch Policies
Similar to other environments, `prod/master` should have it's own. **Note** that you can easily clone existing `Gated` builds and set it's trigger to `master`. You may see the detailed guide below

### Cloud Resources
Similar to how `dev` and `staging` are set up, whether you use App Service, SQL Database, Function Apps, all resources should also exist for your `production` environment. This time, the only difference will be their **Pricing Plans** because production needs better compute power

**Note** that the similar principle applies even if you do not use Azure. Basically, you need to duplicate every cloud resource that you use

### Custom Domains and SSLs
The prod environment will likely use a custom domain provided by the customer. The default domains in azure is `azurewebsites.net` which is not ideal for the customers to use.

This is configured on the Web App (App Service) settings. SSL Certificates can also be installed from there

### Third-party Integrations - API Keys and other Credentials
If you integrate with other software like a Payment Gateway, Email Service, and etc. High chances that these APIs use API Keys to authenticate, or other Credentials to do so. **Do not forget** to switch/use the production keys for these integrations. Most of the time you should put this in your **configuration files** so that you can easily change them

### Configuration
Any other configurable values that should change depending on the current environment should be prepared. Examples are Connection Strings, API Keys, HTTP Endpoints, and etc. **Note** that you can easily check your existing configuration files for `dev` or `staging` and see which values need to be configured for `prod`

### Licenses
If by any chance you used any APIs or Plugins that run in Free Mode or Free Trial. There is a chance that you need to buy Licenses for them. Note that at some cases, this will be settled by the client so make sure to inform your project lead or project manager.