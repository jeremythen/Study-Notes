- [Check](#check)
- [Terms](#terms)
- [Notes](#notes)
- [Services](#services)
  - [Networking & Content Deliver](#networking--content-deliver)
  - [Compute](#compute)
  - [Storage](#storage)
  - [Databased](#databased)
  - [Migration](#migration)
  - [Analytics](#analytics)
  - [Security and Identity](#security-and-identity)
  - [Management Tools](#management-tools)
  - [Appplication Services](#appplication-services)
  - [Developer Tools](#developer-tools)
  - [Mobile Services](#mobile-services)
  - [Business Productivity](#business-productivity)
  - [Desktop and App Streaming](#desktop-and-app-streaming)
  - [Artificial Intelligence](#artificial-intelligence)
  - [Messaging](#messaging)
- [Practitioner](#practitioner)
  - [Region](#region)
  - [Availability Zone (AZ)](#availability-zone-az)
  - [Edge Location](#edge-location)
  - [Choosing the right AWS Region](#choosing-the-right-aws-region)
  - [Type of AWS accounts](#type-of-aws-accounts)
- [EC2](#ec2)
  - [Creating A Billing Alarm](#creating-a-billing-alarm)
    - [Exam notes](#exam-notes)


# Check

* Supperintelligence book

# Terms

* Edge Locations
* VPC (Virtual Private Cloud)
* Route53 (Amazon's DNS service)
* Content Delivery

# Notes

* AWS has regions around the world and more are being added.
* Use the regions near you.
* Some regions may not have some services.
* For the first AWS certification, make sure to have a deep understanding of VPC.


# Services

## Networking & Content Deliver

* VPC
* Route53
* Cloud Front
* Direct Connect (connect to AWS via direct internet line)

## Compute

* EC2 (Elastic Conpute Cloud, a virtual machine in the cloud)
* EC2 Container Service (containers like docker, allows to run apps in EC2 with containers, etc)
* Elastic Beanstalk
* Lambda (no OS, just upload your code and call it, use it)
* Lightsail (out of the box cloud, easy to customize)

## Storage

* S3, Simple Storage Service (Virtual disc in the cloud to store files, objects, audio, videos, etc)
* Glacier (to archive/store files slowly)
* EFS (Elastic File Service). Can install databases here.
* Storage Gateway (connecting S3 to other systems, etc)
  
## Databased

* RDS (Relational Database Service, like Oracle, MeriaDB, Postgre, etc)
* DynamoDB (non relational database, really scalable)
* Redshift (it's like Elasticsearch)
* Elasticache (To cache data in your cloud)

## Migration

* Snowball (to upload data to AWS)
* DMS (Database Migration Service), to migrate a database from on premise to AWS, or AWS to any other area.
* SMS, Server Migration Service (migrates/replicates virtual machines to AWS)
  
  ## Analytics

  * Athena (run SQL queries on files, csv, json)
  * EMR (Big Data processing)
  * Cloud Search (fully managed from AWS)
  * Elastic Search
  * Kinesis (analysing real-time data, for finalcial, customers, social media feeds, etc)
  * Data Pipeline (moving data from one part to another, from S3 to DynamoDB and viceversa)
  * Quick Sight (Business analytic tool)

## Security and Identity

* IAM (setting up users, setting privileges, etc)
* Inspector (inspects the virtual machines to check what is going on)
* Certificate Manager
* Directory Service
* WAF, Web Application Firewall (like SQL injection, etc)
* Artifacts

## Management Tools

* Cloud Watch (monitor performance, etc)
* Cloud Formation (documents/describe your AWS environment)
* Cloud Trail (audit changes to the AWS environment, changes, etc)
* Opsworks
* Config Manager (auditing environment, sending alerts)
* Service Catalog (allows as an enterprise what service you allow to use or not)
* Trusted Advisor (tips on how to do custom automatation, etc.)

## Appplication Services

* Step Functions (shows what is going on in your apps)
* SWF
* API Gateway (constrol the API flow, etc)
* AppStream
* Elastic Transcoder (changing videos format)

## Developer Tools

* CodeCommit (like GitHub)
* CodeBuild (to compile the code)
* CodeDeploy (deploy the code to the EC2 instances)
* CodePipeline (tracks versions of code)

## Mobile Services

* Mobile Hub (design features for you mobile apps, push notification, analytics, etc)
* Cognito (have users sign up/sign to your apps)
* Device Farm (Quality of you app, testing you app)
* Mobile Analytics (analyzes your user's data)
* Pinpoint (understand  how your users uses your app)
  
## Business Productivity

* WorkDocs (storing your important documents in the cloud)
* WorkMail (sending and receiving emails)
* iOT (having many devices out there and keeping track of them)
  
## Desktop and App Streaming

* WorkSpaces (having your operating system on the cloud)
* AppStream 2.0 (stream desktop application)

## Artificial Intelligence

* alexa
* lex
* Polly (turns text into voice, .mp3, etc)
* Machine Learning (analyze data, predict, etc)
* Rekognition (recognizes a picture and tells you what things there are)

## Messaging

* SNS (notifying you, by email, text, etc)
* SQS (a queue system)
* SES

---

# Practitioner

## Region

A Region is a physical location in the world which consists of 2 or more availability zone close to each other.

## Availability Zone (AZ)

An availability zone is basically a data center, where there are a lot of servers.

## Edge Location
  * Are endpoints for AWS which are used for caching content.

## Choosing the right AWS Region

* Data Sovereinty Laws
* Latency to end users
* AWS Services (particular regions may have particular services)


## Type of AWS accounts

* Basic
* Developern (starts a 29 a month)
* Business (starts at 100 a month)
* Enterprise (starts at 15,000 a month. Gets a TAM, or Tecnical Account Manager assigned)

# EC2

* On Compute, click EC2
* On the left menu, click Key Pair
* Give the key a name and create it.
* Add it to PuTTY

## Creating A Billing Alarm

* 1) CloudWatch
* 2) Billing
* 3) Create Alarm
* Set up options
* Next
* Create SNS (Simple Notification Service)
* Create new topic
* Put your email
* Create Topic
* Next
* Add alarm name and description
* Next
* Create Alarm
* Check email and subscribe

### Exam notes

SNS is a way of sending you an email to notify you.
