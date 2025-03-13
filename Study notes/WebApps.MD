# Azure App Service Study Notes (in the making)
<!-- This is a comment that will not appear in the rendered output -->

This file contains study notes for Azure Cloud App Service. It covers various topics, from plan types to deployment slots.

## Getting Started with Azure App Service
### What is Azure App Service?

Azure App Service is a platform as a service (PaaS) for building and hosting:

- Web apps  
- Mobile back ends  
- RESTful APIs  

It allows you to use your language of choice without managing the underlying infrastructure, as Azure provides most of what you need to run your preferred stack.
|
|
--> Azure App Service is a fully managed web application hosting platform.

Azure App Service supports:  
- .NET  
- Java (Java SE, Tomcat, and JBoss EAP)  
- Node.js  
- Python  
- PHP  
- Custom containers  

Depending on your needs, you can choose scaling or auto-scaling options, select between a Windows or Linux OS, and enable automated deployments.

1. Creating a Web App

| **Feature**  | **Description** |
|----------|-------------|
| Subscription    | A valid and active Azure subscription.      |
| Resource group    | A valid resource group.      |
| Name    | The name of the web app. This name becomes part of the app's URL, so it must be unique among all Azure App Service web apps.         |
| Publish    | You can deploy your application to App Service as code or as a ready-to-run Docker Container     |
| Runtime stack    | For every Application, a runtime should be specified  |
| Operating system    | Wondows or Linux     |
| Region from which your application is served| Region       |
| Pricing Plans    | App Service plans and pricing      |

### Examine Azure App Service plans
### Deploy to App Service
### Explore authentication and authorization in App Service

### Discover App Service networking features

## Web App Settings Configuration

## Scaling and Azure App Service

## Deployment Slots