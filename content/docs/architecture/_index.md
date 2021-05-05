---
title: Architecture Guide
type: docs
weight: 1
---

# **Architecture Guide Betelgeuse**
Last updated: 23/11/2020

---
## Purpose
The purpose of this guide is to describe the software architecture of the Betelgeuse application and its interaction with third-party applications.

## Audience
This document is useful to the developers and stakeholders of Orion who are implementing or updating new features for the Betelgeuse application. 

---
## Introduction

Betelgeuse is a serverless application hosted in the AWS cloud. Unlike the monolithic architecture of the previous Betelgeuse system, Betelgeuse is implemented as a [containerized .NET application](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/) following a microservice-based architectural style. This style decomposes the monolithic approach into three main components, each associated with a microservice: bellatrix, rigel, and saiph.  Each microservice undertakes a single business responsibility from the old Betelgeuse system as follows:

*   **Bellatrix Microservice**: Handles transactions of individuals such as create/update clients and group leaders. It also manages brands, regions, routes, and groups.
*   **Rigel Microservice**: Handles transactions related to credits and payments. 
*   **Saiph Microservice**: Handles the communication of Betelgeuse with third-party systems and processes transaction reports. 

Although microservices run independently and, therefore, are built separately, they continuously interact among themselves. The microservices are built as container images orchestrated by the [AWS Elastic Container Service](https://aws.amazon.com/ecs/) (ECS). [AWS Fargate](https://aws.amazon.com/fargate/) provisions the infrastructure of the ECS clusters. Each microservice has its own database decoupled from the other microservices. Data is migrated from the previous Betelgeuse system and stored in serverless [Aurora MySQL](https://aws.amazon.com/rds/aurora/mysql-features/) relational databases. Moreover, communication among the microservices is asynchronous and based on integration events. It follows the principles of [request-response messaging for publish-subscribe channels](https://aws.amazon.com/blogs/compute/implementing-enterprise-integration-patterns-with-aws-messaging-services-publish-subscribe-channels/), using both [Amazon SNS](https://aws.amazon.com/sns/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc) topics and [Amazon SQS](https://aws.amazon.com/sqs/) queues.

Betelgeuse is deployed on the cloud using the [Octopus Deploy](https://octopus.com/docs/getting-started) tools. GitLab CI/CD tools ensure continuous integration and continuous delivery of the application by implementing automated pipelines. In addition, Betelgeuse uses [Terraform](https://www.terraform.io/) templates to implement Infrastructure as Code on AWS. 

Finally, the Betelgeuse client application is stored in a bucket of [Amazon S3](https://aws.amazon.com/s3/) and served as a Single Page Application (SPA) using [AWS Cloudfront](https://aws.amazon.com/cloudfront/). The components of the client application are built using the [Angular Framework](https://angular.io/docs). 

The Betelgeuse application comprises the following modules:

* Betelgeuse Identity and Authorization Module
* Betelgeuse Web Frontend
* Betelgeuse Backend
* Betelgeuse Security
* Betelgeuse Monitoring

**Figure 1** provides a high-level description of the Betelgeuse application.

![Arquitectura]({{< resource url="/architecture/architecture-highlevel.png" >}})
***Figure 1. Betelgeuse Architecture***\
&nbsp;

The architectural style of Betelgeuse follows the good practices of [Clean Architecture](https://docs.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures). This style is suitable for complex business logics that involve several areas. The advantages of the Betelgeuse architecture are the following:

- **It follows the Dependency Inversion Principle (DIP).** This principle states that high-level modules should not depend on low-level modules. The interplay between both modules must be thorugh abstractions. Therefore, high-level modules of the Betelgeuse such as data, infrastructure, dependencies, and user interface are decoupled from low-level modules (business rules). This principle focuses the Betelgeuse architecture on the business logic of Orion.
- **It complies with a Domain Driven Design (DDD)**. DDD is a software development approach that links the implementation of the application to the core business concepts of the client. This approach enables to map the old monolithic architecture of Betelgeuse consisting of use cases into domains. Each domain then correlates to a microservice in the new model of Betelgeuse. 
- **It is scalable**. Microservices can scale up as Orion business logic does. Each microservice can assume a single business responsibility. 

---
## Betelgeuse Identity and Authorization Module

This section describes the business logic of Betelgeuse for an end user to access and navigate the application according to their role in Orion. 

[Amazon Cognito](https://aws.amazon.com/cognito/) is the AWS service that enables authentication and authorization of Betelgeuse end users. Cognito [user pools](https://docs.aws.amazon.com/cognito/latest/developerguide/getting-started-with-cognito-user-pools.html) verify the identity of users so that they can directly sign in and sign up to the application. A user pool enables Betelgeuse to create and maintain an end-user directory that includes information such as profile, company, zone, and office. 

Betelgeuse, includes two methods to authenticate an end user: 

*   Directly registering the new user’s profile in the AWS Cognito console. 
*   Using a third-party SAML 2.0 identity provider, such as Azure Active Directory, for integrating Office 365 single sign-on (SSO), as **Figure 2** shows. 


![Identity]({{< resource url="/architecture/identity.png" >}})
***Figure 2. Authentication Flow of Betelgeuse Users using Office 365***\
&nbsp;

The user authentication flow using a third-party identity provider is the following: 

1. The user enters the domain of the Betelgeuse application.
2. The application redirects the user to the Amazon Cognito hosted UI to authenticate using Office 365 SSO.
3. Amazon Cognito redirects the user to the Microsoft login site to enter their Office 365 credentials. 
4. If the user authenticates successfully, Azure Active Directory provides four claims related to the user profile: role, office, zone, and company to Amazon Cognito using the SAML 2.0 standard, an industry standard for federated authentication.

{{< hint info >}}
**Note:**  
Originally, Orion’s user information was kept on a local Windows server. Eventually, the user directory was uploaded to the Azure Active Directory in the cloud using the Azure AD connect service. 
{{< /hint >}}

5. Next, Cognito issues a JSON Web Token (JWT) to the Betelgeuse application using the [OAuth 2.0 implicit grant flow](https://aws.amazon.com/blogs/mobile/understanding-amazon-cognito-user-pool-oauth-2-0-grants/), which enables Cognito to directly return a JWT to Betelgeuse after the user successfully authenticates. The OAuth 2.0 standard is used to control user authorization.  
6. The [Amplify framework](https://aws.amazon.com/amplify/) decodes and verifies the JWT. If valid, it grants the user access to the application. 

{{< hint danger >}}
**Important:**  
The Betelgeuse application uses the SDKs and libraries provided by the AWS Amplify framework to integrate AWS services. Amplify also handles the Betelgeuse sign in and sign up flow by implementing direct calls to the methods of the [Auth class](https://docs.amplify.aws/lib/auth/getting-started/q/platform/js) using the SDK of Angular CLI. 
{{< /hint >}}

---
## Betelgeuse Frontend

This section describes the elements, along with their properties and relationships, that support the client and static content of Betelgeuse. An end user interacts with these elements after successfully identifying and accessing the application.  
 
The Betelgeuse application uses the [Angular JavaScript framework](https://angular.io/) to build a Single-Page web Application (SPA). Amazon CloudFront serves the client and static content of the application, stored in an S3 Bucket. Betelgeuse Frontend communicates to the backend microservices rigel, bellatrix, and saiph using a REST API Interface. 

A CloudFront distribution is a reliable and secure way to serve content more efficiently because it enables Betelgeuse to cache the most frequently requested content. Each CloudFront distribution uses an[ SSL certificate](https://aws.amazon.com/certificate-manager/#:~:text=AWS%20Certificate%20Manager%20(ACM)%20Private,lifecycle%20of%20your%20private%20certificates.) to identify the Betelgeuse site and secure its private network communications. Moreover, each deployment environment: development, laboratory, testing, and production has its own CloudFront distribution.

Frontend DNS (Domain Name System) requests are routed to the CloudFront distribution using the Amazon Route 53 service by means of an alternate DNS domain. The CloudFront distribution points to the origin S3 Bucket that hosts the client application. The S3 Bucket is configured for website hosting with policies to grant external access. For more details, check the section [**Routing Traffic to CloudFront Distributions**](#cloudfront).

---
## Betelgeuse Backend

This section describes the following topics:

* The architecture of the microservices as containerized images along with their infrastructure provisioning
* The routing of incoming traffic from the Frontend
* The structure of the Virtual Private Cloud (VPC) and subnets
* The request-response messaging among microservices
* The deployment of the Betelgeuse application

---
### Containerized-Based Microservices
Betelgeuse uses a microservice-based architecture. Each microservice is a containerized application that has its own database. Betelgeuse includes three main microservices: bellatrix, rigel, and saiph. These microservices exist in all the deployment environments of the application: development, laboratory, testing, and production. 

![AWS-ECS-FARGATE]({{< resource url="/architecture/aws-ecs-fargate.png" >}})

***Figure 3. Interplay between the ECS Cluster and AWS Fargate for Building the Microservices.***\
&nbsp;

As **Figure 3** shows, each deployment environment is built on an [AWS ECS](https://aws.amazon.com/ecs/) (Elastic Container Service) cluster and launched using [AWS Fargate](https://aws.amazon.com/fargate/). Amazon ECS is an orchestration service that handles your containers using services. Services define tasks based on a [task definition](https://docs.aws.amazon.com/AmazonECS/latest/userguide/task_definitions.html), which works as a blueprint that describes how to provision your containers. Tasks are one-time executions of your containers. For example, the development environment includes an ECS cluster with three ECS services: 

*   orion-dev-bellatrix
*   orion-dev-rigel
*   orion-dev-saiph

Each service can contain a single or multiple tasks representing a container image of a specific microservice. You can scale up to any number of tasks for maintaining your application’s availability if a task failure occurs.

As mentioned above, the ECS service builds a container image of a microservice using a task definition. A task definition is required to run Docker images in ECS. The task definition defines some parameters such as the origin Docker image, CPU, and memory for each task, launch type, and ports. Betelgeuse uses [AWS ECR](https://aws.amazon.com/ecr/) (Elastic Container Registry) to store the Docker images implemented and built in GitLab by the developers. The ECS service consumes the Docker images from the AWS ECR and builds the container image of the microservices using the task definition. For more details, consult the [**Deployment section**](#deployment). To ensure compatibility and usage of the latest image version, GitLab uses semantic versioning ([semver](https://semver.org/)) of images.

[AWS Fargate](https://aws.amazon.com/fargate/) enables you to run your containers without requiring the whole capacity of EC2 instances. Fargate handles the infrastructure required for each ECS cluster. [Fargate launch type](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/launch_types.html) provisions your tasks with the required number of CPU cores and gigabytes of memory defined in the task definition. 

---
### Traffic Distribution
Betelgeuse’s domain name is **orion.com.mx**. This domain includes the following subdomains:

*   dev.orion.com.mx
*   lab.orion.com.mx
*   test.orion.com.mx
*   api-dev.orion.com.mx
*   api-lab.orion.com.mx
*   api-test.orion.com.mx

[Amazon Route 53](https://aws.amazon.com/route53/) is responsible for routing traffic to **orion.com.mx** and its corresponding subdomains by means of a public hosted zone. A hosted zone contains records that define how the internet traffic is routed for Betelgeuse DNS queries. Amazon Route 53 handles DNS queries and routes traffic to a specific destination of the Betelgeuse application. 

The Amazon Route 53 service main responsibilities include:

*   Mapping domain names to CloudFront distributions, Application Load Balancers and S3 Buckets. 
*   Routing traffic for a domain and its subdomains using records. 
*   Determining how to respond to DNS queries using a routing policy. 
*   Determining the format of the value that returns in response to a DNS query.

The following sections describe in detail how Amazon Route 53 maps domain names to CloudFront distributions and Application Load Balancers.

---
#### Routing Traffic to CloudFront Distributions {#cloudfront}

To describe how Amazon Route 53 distributes traffic to a CloudFront distribution, the following steps use the dev.orion.com.mx subdomain as an example. 

1. The frontend sends a **dev.orion.com.mx** DNS query.
2. The Amazon Route 53 service routes traffic for this subdomain to the alternate domain name CNAME associated with the CloudFront distribution. 

{{< hint info >}}
**Note:**  
The DNS query name must exactly match the CloudFront alternate domain name. For example, if the alias record name is dev.orion.com.mx the alternate domain of the CloudFront distribution must be named likewise.
{{< /hint >}}

3. The CloudFront distribution points to the S3 bucket endpoint and serves the client and static content stored in the bucket.  

{{< hint info >}}
**Note:**  
The CloudFront distribution uses an SSL certificate to secure all communications among the AWS resources of the internal network. An SSL certificate is created per domain name using the [Amazon ACM service](https://console.aws.amazon.com/ec2/home?region=us-east-1#SecurityGroups:).
{{< /hint >}}

---
#### Routing Traffic to Application Load Balancers

Betelgeuse microservices are placed behind an HTTP/HTTPS load balancer secured by an SSL certificate. The load balancer routes traffic to the microservices based upon inbound rules defined on specific ports. Furthermore, the application load balancers have a security group, which acts as a virtual firewall to control inbound and outbound traffic. 

To describe how Amazon Route 53 distributes traffic to an application load balancer, the following steps use the **api-lab.orion.com.mx** subdomain as an example. 

1. The frontend sends a **api-lab.orion.com.mx/bellatrix** DNS query.
2. Amazon Route 53 routes all incoming traffic from this DNS name to the application load balancer (ALB) of the laboratory environment. 
3. The ALB redirects traffic to a microservice target group based on the route name (**/bellatrix/**, **/rigel/**, or **/saiph/**). 

{{< hint danger >}}
**Important:**  
The ALB is configured to listen to ports: 80, 443, 8080, 8443, 8810, and 8811. ALB listeners check for connection requests that use the HTTP or HTTPs protocols on these ports. Each listener includes rules to route incoming traffic to a specific target group.
{{< /hint >}}

4. The target group contains a target of type IP. In this case, the target is the private IP address assigned to the task of the bellatrix microservice. This IP address is dynamic and changes every time the task or the service is restored. 

{{< hint info >}}
**Note:**  
All incoming traffic from ports that use the HTTP protocol is redirected to ports using the HTTPs protocol. This configuration ensures that all incoming requests have an SSL certificate to secure the connection.
{{< /hint >}}

For security purposes, each deployment environment has its own Virtual Private Network (VPC) that complies with the network architecture of Orion. A VPC contains three availability zones. Each availability zone includes a private and an isolated subnet for a total of six subnets. Private subnets host container images of the microservices. On the other hand, isolated subnets host databases. Besides, the ALB has an associated SSL certificate to secure communications and encrypt sent data. The Betelgeuse application has an additional security layer, the user must connect to Orion’s VPN to access the microservices resources.

{{< hint info >}}
**Note:**  
Only the development environment has both the microservice ECS tasks and databases configured on private subnets. Isolated subnets are not used. 
{{< /hint >}}

---
## Asynchronous Communication

Communication among the microservices that integrate the Betelgeuse application is based on events using both [Amazon Simple Notification Service (SNS)](https://aws.amazon.com/sns/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc) topics and [Amazon Simple Queue (SQS)](https://aws.amazon.com/sqs/) service. This strategy ensures a decoupled and asynchronous interaction among the different microservices that follows the principle of request-response messaging for publish-subscribe channels. In this scheme, an event bus collects all the events produced by a microservice. Then, it distributes them among the subscribed queues of other microservices, as **Figure 4** shows. 

As an example, the following steps describe in detail the communication scheme of the bellatrix microservice with the rigel and saiph microservices.  

1. The bellatrix microservice produces a new event.
2. The Amazon SNS service, that listens to events from the list of topics of all the microservices, performs two actions: 
    * It fans this event out to the list of registered topics of the rigel and saiph microservices. 
    * It processes all event logs parallelly and stores them in an S3 bucket for further reference and inspection. To accomplish that, 
        1. A Lambda function pushes the events to [Amazon Kinesis Data Firehose](https://aws.amazon.com/kinesis/data-firehose/?kinesis-blogs.sort-by=item.additionalFields.createdDate&kinesis-blogs.sort-order=desc). 
        2. The Kinesis Data Firehose service captures and delivers the streaming data (events) into an S3 bucket.  
If required, a second Lambda function can perform an identity transformation of the events in the stream. 
3. The Amazon SQS service subscribed to the topic collects the new event. 
4. The Amazon SQS service appends the event to the queue of the rigel and saiph microservices, respectively. 
5. The rigel and saiph microservices process the event. 
Parallelly, the event is collected by a [Death Letter Queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html) (DLQ) to ensure that the event is processed. A DLQ can handle duplicated events. If required, all DLQ logs can be processed by a Lambda function and stored in an S3 bucket. 

![COMMUNICATION]({{< resource url="/architecture/communication.png" >}})
***Figure 4. Asynchronous and Decoupled Communication among Betelgeuse Microservices.***\
&nbsp;

___
## Deployment {#deployment}

Betelgeuse uses the Octopus tools for deploying the containerized images of the microservices in the cloud. Each deployment environment (development, testing, laboratory, and production) includes five containerized images. Octopus executes a PowerShell script that tells the AWS CLI which processes and resources to implement, as well as which specific version of the images stored in the AWS ECR to use. **Figure 5** describes the deployment process of the Betelgeuse application. 

![DEPLOYMENT]({{< resource url="/architecture/deployment-octopus.png" >}})
***Figure 5. Deployment Process of Betelgeuse Environments using Octopus***\
&nbsp;

To understand the deployment process of containerized images, the following steps describe how Octopus deploys the bellatrix image into the development environment. 

1. A developer makes a pull request to the **Orion.Betelgeuse.Bellatrix** repository.
2. GitLab CI/CD implements automatically the following stages:
    * **Prebuild**
        - Determines image version using semantic versioning specification v.1.0.0 ([SemVer](https://semver.org/)). 
    * **Build and Test**
        - Executes unit tests to the .NET project and all its dependencies. 
        - Builds, analyzes static code, and publishes the .NET core application and its dependencies to a folder for deployment. 
    * **Push**
        - Builds, tags, and pushes a dockerized image of the .NET core application to the container registry of GitLab (CI_REGISTRY_IMAGE).
        - Builds, tags, and pushes a dockerized image of the .NET core application to the AWS Elastic Container Registry (ECR).
        - Packs the powershell deployment script into a NuGet package and pushes it to the Octopus built-in repository. 
    * **Deploy** 
        - Creates a release with the specified version in the **Prebuild** step and deploys it to the development environment. 
3. Octopus runs the PowerShell script, which contains custom deployment actions to be performed by the AWS CLI. \
Octopus tells AWS ECR to deploy the bellatrix image that matches the specified version number of the created release.

{{< hint danger >}}
**Important:**  
Octopus enables custom powershell scripts to have access to the AWS CLI. This requires a previous authentication step to provide AWS credentials to Octopus.
{{< /hint >}}

---
## Betelgeuse Security

The Betelgeuse application complies with the following security checkpoints:

___
### General Security Checkpoints

*   Users must connect to the Orion VPN to access the application.
*   Users must have Office 365 credentials or have a username and password provided by the IT department to enter the application.  
The IT department can create, organize, and update users directly on the AWS console of Cognito based on a role and permission matrix. 
*   Users have restricted permissions to particular Betelgeuse functionalities based on their role and the permission matrix. 

{{< hint info >}}
**Note:**  
The permission matrix applies to each endpoint of every microservice (bellatrix, rigel, and saiph) and to particular functionalities (windows) of the application’s frontend.
{{< /hint >}}

___
### Architectural-Level Security Checkpoints

*   S3 buckets that store the client application have configured access policies. 
*   Cloudfront distributions that serve the client application have a SSL certificate.
*   Application Load Balancers that distribute frontend DNS queries to the microservices have a SSL certificate. 
*   Each deployment environment has its own VPC including three private and three isolated subnets. Private subnets host the microservices whereas isolated subnets host the databases. 
*   Developers can connect to the isolated Amazon Aurora RDS databases from their local machine using an Amazon EC2 instance as a [bastion host](https://aws.amazon.com/premiumsupport/knowledge-center/rds-connect-ec2-bastion-host/). This approach enables them to securely administer and give maintenance to the databases.
*   Infrastructure as code of Betelgeuse uses Terraform templates. [AWS Systems Manager Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html) manages secrets such as passwords, API keys, and other sensitive information (in a string format) that is consumed by the Terraform templates.
*   All requests from the frontend to the backend using the REST API interface require a bearer token.
*   All incoming traffic to the microservices is redirected by the Application Load Balancers to port 443 that uses the HTTPs protocol.  

___
## Betelgeuse Monitoring 

The [AWS CloudWatch](https://aws.amazon.com/cloudwatch/) service monitors the AWS infrastructure of Betelgeuse. This service enables you to select metrics to audit AWS resources such as EC2 instances, logs, SNS messages, SQS queues, CloudFront distributions, Application Load Balancers, and so on. Additionally, **Grafana** is integrated in the technological stack of Betelgeuse as an open source analytics and monitoring solution to check the AWS infrastructure.

