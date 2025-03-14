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

<br><br>

### Pricing tiers : 


- **Shared Compute : Free and Shared**
    - Runs an app on the same Azure VM as other App Service apps, including apps of other customers,
    - These tiers allocate CPU quotas to each app that runs on the shared resources, and the resources can't scale out.
<br><br>

- **Dedicated compute : Basic, Standard, Premium, PremiumV2, and PremiumV3**
    - Run apps on dedicated Azure VMs,
    - Only apps in the same App Service plans share the same compute resources. The higher the tier, 
    - The more VM instances are available to you for scale-out.
    
In the Free and Shared tiers, an app receives CPU minutes on a shared VM instance and can't scale out.
<br><br>

- **Isolated : Isolated and IsolatedV2**
    - Run dedicated Azure VMs on dedicated Azure Virtual Networks (kind of create an isolated VM as if even the hardware is isolated).
    - It provides network isolation on top of compute isolation to your apps. 
    - It provides the maximum scale-out capabilities.


### Scalling :










## Deploy to App Service
## Explore authentication and authorization in App Service

## Discover App Service networking features

# Web App Settings Configuration

# Scaling and Azure App Service

# Deployment Slots

# App Services Environement