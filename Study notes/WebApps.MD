<!-- This is a comment that will not appear in the rendered output -->

This file contains study notes for Azure Cloud App Service. It covers various topics, from plan types to deployment slots.(in the making)

# Getting Started with Azure App Service
## What is Azure App Service?

Azure App Service is a platform as a service (PaaS) for building and hosting:

- Web apps  
- Mobile back ends  
- RESTful APIs  


It allows you to use your language of choice without managing the underlying infrastructure, as Azure provides most of what you need to run your preferred stack.

---> Azure App Service is a fully managed web application hosting platform.

Azure App Service supports:  
- .NET  
- Java (Java SE, Tomcat, and JBoss EAP)  
- Node.js  
- Python  
- PHP  
- Custom containers  

Depending on your needs, you can choose scaling or auto-scaling options, select between a Windows or Linux OS, and enable automated deployments.


## Creating a Web App

The Azure portal provides a wizard to create a web app. This wizard requires the following fields (We will see with the CLI later):
| **Feature**  | **Description** |
|----------|-------------|
| Subscription    | A valid and active Azure subscription.      |
| Resource group    | A valid resource group.      |
| Name    | The name of the web app. This name becomes part of the app's URL, so it must be unique among all Azure App Service web apps.         |
| Publish    | You can deploy your application to App Service as code or as a ready-to-run Docker Container     |
| Runtime stack    | For every Application, a runtime should be specified  |
| Operating system    | Wondows or Linux     |
| Region | Region from which your application is served|
| Pricing Plans    | App Service plans and pricing      |




## Azure App Service plans

**An app always runs in an App Service plan.** 
An App Service plan defines a set of compute resources for a web app to run --> --> --> **An App Service plan is a set of virtual server resources that run App Service apps.**

A plan's size (sometimes referred to as **pricing tier**) determines the performance characteristics of the virtual servers that run the apps assigned to the plan, and the App Service features to which those apps have access.

**- Every App Service web app must be assigned to a single App Service plan, while One or more apps can be configured to run on the same computing resources (or in the same App Service plan).**

### How does it work ?
When an App Service plan is created in a certain region (ex : West Europe), a **set of compute resources is created for that plan in that region**.
--> --> Then All Apps in an App Service Plan run these compute resources as defined by the App Service plan chosen.


Each App Service plan defines:
- Operating System (Windows or Linux)
- Region (West US, etc.)
- Number of VM instances
- Size of VM instances (Small, Medium, Large)
- Pricing tier (Free, Shared, Basic, Standard Premium, PremiumV2, PremiumV3, Isolated, IsolatedV2)
 


### Pricing tiers : 






- **Shared Compute : Free and Shared**
    - Runs an app on the same Azure VM as other App Service apps, including apps of other customers,
    - These tiers allocate CPU quotas to each app that runs on the shared resources, and the resources can't scale out.

- **Dedicated compute : Basic, Standard, Premium, PremiumV2, and PremiumV3**
    - Run apps on dedicated Azure VMs,
    - Only apps in the same App Service plans share the same compute resources. The higher the tier, 
    - The more VM instances are available to you for scale-out.


- **Isolated : Isolated and IsolatedV2**
    - Run dedicated Azure VMs on dedicated Azure Virtual Networks (kind of create an isolated VM as if even the hardware is isolated).
    - It provides network isolation on top of compute isolation to your apps. 
    - It provides the maximum scale-out capabilities.


### Scalling :

- In the **Free** and **Shared** tiers, an app receives CPU minutes on a shared VM instance and **can't scale out**.

- In other tiers : 

    - An app runs on all the VM instances configured in the App Service plan.
    - If multiple apps are in the same App Service plan, they all share the same VM instances.
    - If you have multiple deployment slots for an app, all deployment slots also run on the same VM instances.
    - If you enable diagnostic logs, perform backups, or run WebJobs, they also use CPU cycles and memory on these VM instances.

--> the App Service plan is the scale unit of the App Service apps

**Ex :** If the plan is configured to run five VM instances, then all apps in the plan run on all five instances. If the plan is configured for autoscaling, then all apps in the plan are scaled out together based on the autoscale settings.


## Deploy to App Service
App Service supports both automated and manual deployment.

### Automated deployment
Process used to push out new features and bug fixes in a fast and repetitive pattern with minimal effect on end users.

Automated deployment (or continuous deployment) is supported by the following options : 
- Azure DevOps Services,
- GitHub,
- Bitbucket.

### Manual deployment
App service support Manual deployment through the following options : 
- Git (a Git URL can be added as a remote repo),
- Cli (with the "webapp up" feature), 
- Zip deploy (with curl or a similar HTTP),
- FTP/S (Old fashion, butcould be needed for some cases).

### Continuous deployment for containers : 
Azure App service allow deployment from the Azure Container Registry or other container registries. 

Automating this process can be done following theses steps : 
- Build and tag the image,
- Push the tagged image,
- Update the deployment slot with the new image tag.
<!--
/////also (cf later) (cf Sidecar containers later )/////
-->

## Explore authentication and authorization in App Service
You can sign in users and access data by writing minimal or no code in your web app, RESTful API, mobile back end, or Azure Functions.

| Provider            | Sign-in endpoint         | How-To guidance                   |
|---------------------|--------------------------|------------------------------------|
| Microsoft Entra     | /.auth/login/aad         | [App Service Microsoft Entra platform login](https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-aad?tabs=workforce-configuration) |
| Facebook            | /.auth/login/facebook    | [App Service Facebook login](https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-facebook)         |
| Google              | /.auth/login/google      | [App Service Google login](https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-google)        |
| X                   | /.auth/login/x           | [App Service X login](https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-twitter)                |
| Any OpenID Connect  | /.auth/login/"providerName" | [App Service OpenID Connect login](https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-openid-connect)   |
| GitHub              | /.auth/login/github      | [App Service GitHub login](https://learn.microsoft.com/en-us/azure/app-service/configure-authentication-provider-github)           |

### Authorization behavior
- **Allow unauthenticated requests.** This option defers authorization of unauthenticated traffic to your application code

- **Require authentication.** This option rejects any unauthenticated traffic to your application. This rejection can be a redirect action to one of the configured identity providers.

## Discover App Service networking features

There are two main deployment types for Azure App Service:

- **The multitenant public service** hosts App Service plans in the Free, Shared, Basic, Standard, Premium, PremiumV2, and PremiumV3 pricing SKUs.
- **The single-tenant App Service Environment (ASE)** hosts Isolated SKU App Service plans directly in your Azure virtual network.

### Multitenant networking features
**Because there are many different customers in the same App Service scale unit,** Instead of connecting the networks, you need features to handle the various aspects of application communication for Inbound and Outbound

| **Inbound features**            | **Outbound features**         |
|---------------------|--------------------------|
| App-assigned address     | Hybrid Connections         |
| Access restrictions     | Gateway-required virtual network integration         |
| Service endpoints     | Virtual network integration         |
| Private endpoints     |         |


# App Settings & connection strings


## 1. App Settings:

- We call app settings the **variables passed as environment variables to the application code.**
- These are **key-value pairs** that can be used to configure your application. They are typically used for application-specific settings such as feature flags, environment variables, or any other configuration data that your application needs to function (as in the template bellow).

    ```json
    {
        "name": "<key-1>",
        "value": "<value-1>",
        "slotSetting": false
    },
    {
        "name": "<key-2>",
        "value": "<value-2>",
        "slotSetting": false
    },
    ```

- App settings are accessible to applications as environment variables. The can be retrieved using the environment variable access methods provided by the programming language used.
- **For ASP.NET and ASP.NET Core developers** setting app settings in App Service is like setting them in `appSettings` in **Web.config** or **appsettings.json**, but the values in App Service override the ones in Web.config or appsettings.json.

## 2. Connection Strings

- These are specifically used to store information required to **connect to external resources** like databases, storage accounts, or other services.
- setting connection strings in App Service are like setting them in `connectionStrings` in **"Web.config"**, but the values you set in App Service override the ones in Web.config. **For other language stacks, it's better to use app settings instead**

    ```json
    {
        "name": "name-1",
        "value": "conn-string-1",
        "type": "SQLServer",
        "slotSetting": false
    },
    {
        "name": "name-2",
        "value": "conn-string-2",
        "type": "PostgreSQL",
        "slotSetting": false
    },
    ```

- Connection strings are also accessible as environment variables, but they are specifically intended for connection-related information, ensuring that sensitive data like credentials are stored securely.

!! Both app settings and connection strings can be managed through the Azure Portal, and changes to them can be made without needing to redeploy the application. This makes it easy to update configurations or connection details as needed.




# Scaling and Azure App Service

# Deployment Slots

# App Services Environement