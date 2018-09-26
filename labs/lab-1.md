# Lab 1 - Getting Started

**Purpose:** Setup a new AWS Account (if neccesary), and then become familiar with the service offerings.

## 1 - Create an AWS Account

If you do not yet have an AWS account, you will need to set one up in order to run any of these labs.  

Setting up an account can be accomplished at the following site:

https://aws.amazon.com/free/

To sign-up for AWS, you will need to have a private e-mail address and billing information.  For billing, don't worry.  AWS offers a free tier to learn their products and everything we will be using is covered by the free tier.  And, once your 12 months free are past, AWS does metered billing.  So unless you spin up an expensive resource, you won't be hit with sticker shock.

## 2 - Learn the AWS Console

Now that you have an AWS account setup, it's time to start learning what you can do with it.  You can log into the account at the following address (with the user ID and password you set up in step 1).  

https://console.aws.amazon.com

### 2.a - Regions

Once logging in, it is import that set your region.  AWS is a mult-region cloud provider with good cross-region support.  But almost every resource in AWS is region-bound.  Thus, you need to select which region you will be operating on.

From the dropdown in the top right of the screen, you should see (just to the left of 'Support') a dropdown with a region namme.  Pick this and choose the region you will be working on.

I will be doing all of my examples in US East (N. Virgina).  This region has an id of `us-east-1`.  If you choose to work from a different region, you will need to change the command line calls later on to target the correct region.

### 2.b - Service List

When initially logging in, you will see a list of the various services that AWS offers.  This list may be daunting at first, but we will spend some time moving through a set of services here.  

Once on the page for a each service, you can easily get back to the list of services from the `Services` dropdown on the main bar.

## 3 - Exploring Services

In this section of the lab, we will be looking through a handful of services that we will be using as this course goes along.  As we look at each service, AWS provides us with a good overview page (sometimes with very helpful videos and training links) to better understand the products.

### 3.a - EC2

Amazon EC2 (Amazon Elastic Cloud Compute) is a common first forray into AWS.  This is especially true in a lift-and-shift enterprise model.  

At its core, EC2 is a scalable virtual machine infrastructure that can run a number of server-based workloads.  Some workloads might be microservices.  Others may be large database instances.  But in all cases, you are declaring and paying for the compute, memory and storage for a virual machine that is running in the data center you have targetted.

As useful as EC2 is, we will not be using it in this course.  We will be targetting a full serverless stack.  (Serverless refers to a cloud architecture where all tasks run without the need to allocate or support servers, letting the cloud provider handle this for you.)  Thus, the allocation (and management of) application servers becomes a non-issue for us.

### 3.b - S3

Amazon S3 (Simple Storage Solution) is a distributed and highly-reliable key/value blob storage solution for AWS resources.  S3 is incredibly cheap.  And, it scales in terms of storage and performance to deal with exabytes of data.

There are many use cases for S3.  Amoung these use cases are:

* Static content storage for websites
* Interim storage for distributed processes
* Code artifact storage for AWS SAM model applicationsw
* Raw and processed storage for data lake back ends

We will be utilizing S3 to provide the storage of static files for the website we build,

### 3.c - Lambda

AWS Lambda was the first major deployment of a serverless Functions as a Service (FaaS) platform.  Effectively, Lambda allows you to run event-triggered code in a dynamically scalable environment without having to worry about provisioning and managing servers.  Effectively, you pay for resources ONLY when your functions are invoked.

We will be implemented the API backend for our website in Lambda.  The choice of language for our course will be Python 3.6.

### 3.d - API Gateway

Amazon API Gateway provides a sercure, scalable and managed way for other applications to interact with an API back end.  The APIs targetted by API gateway can be build and deployed in a number of manners.  They can be Lambda functions, Docker containers or services deployed to EC2.  

We will utilize API Gateway on top of our Lambda functions to allow the web site to access our APIs.

### 3.e - SQS

Amazon SQS (Simple Queue Service) is a tool to provide decoupled message-queue integration between two system.  Like Lambda, it runs as a serverless model.  Thus, resources are only payed for when messages are sent/received.

We will use SQS to allow asynch jobs to be run based on API calls in a reliable manner.

### 3.f - SNS

Amazon SNS (Simple Notification Service) is a pub-sub model of event notification.  It is closely related to SQS.  But, where as SQS is a point-to-point queue model, SNS is a pub/sub event model.

We will use SNS for setting up a text message alert system in our app.

### 3.g - Cognito

AWS Cognito is Amazon's user identity management service.  It is used to manage creating user ID and passwords in the system, as well as for federated permissions via Open ID Connect (OIDC).

As one of the last steps of our app, we will apply a log-in model to limit only authorized users to have access to our resources.

### 3.h - Cloud Formation

The last product we will use is Cloud Formation.  This is a product that allows deploying infrastructure as a template.  It is a major tool in a mature AWS Dev/Ops process.  

We will utilize Cloud Formation to deploy some components of our site.  Once we know how to deploy using the GUI and CLI, learning Cloud Formation should improve our overall delivery rate.

## Conclusion

At the conclusion of this lab, you should have learned how to do the following things:

* Create an AWS account
* Log into the AWS web console
* Navigate the services available in AWS
