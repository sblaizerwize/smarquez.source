---
title: How-To Guide
type: docs
weight: 1
---

# Deploying using Octopus in Betelgeuse 
Last updated: 06/11/2020

---
## Introduction  
This guide explains you how to manually deploy to the AWS Cloud any of the following Betelgeuse projects using Octopus deploy:

*   Orion.Client
*   Orion.Bellatrix
*   Orion.Rigel
*   Orion.Saiph

{{< hint info >}}
**Note:**  
These projects are automatically deployed to the development and testing environments. Both environments share the same projects and versions. For the laboratory environment, some of these packages are deployed manually. 
{{< /hint >}}

The deployment process of Betelgeuse projects is detailed in the [Architecture Guide]({{< relref "/docs/architecture" >}}). Briefly, the process consists of four stages that run automatically after a developer makes a pull request in GitLab:

1. **Prebuild**. Determines image version.
2. **Build and Test**. Builds, analyzes static code, and publishes the .NET core application and its dependencies to a folder for deployment. 
3. **Push**. Builds, tags, and pushes a dockerized image of the .NET core application to the container registry of GitLab and to the AWS Elastic Container Registry (ECR). It also packs the powershell deployment script into a NuGet package and pushes it to the Octopus built-in repository.
4. **Deploy**. Creates a release with the specified version in the **Prebuild** step and deploys it to a deployment environment. 

This guide describes how you can run the **Deployment** stage manually. 

---
## Log In to Octopus

1. Go to **Octopus Deploy** site. 
2. Log in to Octopus.
    * If you are a admin user:
        - In the Log in page, click on the **Google** button to sign in using admin SSO. 
        - Identify yourself using your admin credentials. 
    * If you are a dev user:
        - Identify yourself using your dev credentials. 

Once you login, you are redirected to the **Octopus dashboard** that displays all the Betelgeuse projects and their release versions on their respective deployment environments. 

___
## Deploy Betelgeuse Projects Manually

This section describes how you can deploy Betelgeuse projects manually using Octopus GUI. As an example, the following steps illustrate the process for deploying the bellatrix microservice manually. 

### Select a Project
1. In the Octopus dashboard screen, select the **Orion.Bellatrix** project under the **Default Project Group** column.  \
The application shows an overview of the project and its versions deployed in each of the deployment environments.

### Create a Release
1. Click on the **CREATE RELEASE** button, located on the top left corner of the screen under the project’s name.\
Octopus loads the latest version release included in the Octopus Built-in registry pushed from GitLab. It also includes all the packages integrated in this release. 
2. Select the version and packages for the release you want to deploy. 
3. Click on the **SAVE** button located at the top right corner of the section. 
4. On the left panel, click on **Overview**.\
Octopus displays the latest release that you created in step 1. 

### Deploy the Release
1. Click on the **DEPLOY…** button under the environment where you want to deploy the release.\
Octopus redirects you to a new screen that shows you step-by-step the progress of the task. 
2. Click on the **TASK LOG** tab to check the deployment logs.
3. Filter the deployment logs with the following parameters:
    - Expand = All
    - Log level = Verbose
    - Log fail = All
{{< hint danger >}}
**Important:**  
Deployment logs can help you to monitor and debug the deployment process.
{{< /hint >}}
4. In the top menu, go to Dashboard to verify that the deployment process is ready for the deployment environment you selected. 

