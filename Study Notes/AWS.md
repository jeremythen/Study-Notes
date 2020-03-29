- [Info](#info)
  - [Buckets](#buckets)
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
- [IAM (Identity Access Management)](#iam-identity-access-management)
- [S3 (Simple Storage Service)](#s3-simple-storage-service)
  - [S3 data consistency](#s3-data-consistency)
  - [S3 Guarantees](#s3-guarantees)
  - [S3 Features](#s3-features)
  - [S3 Storage Classes](#s3-storage-classes)
  - [S3 Charges](#s3-charges)
  - [S3 Lab](#s3-lab)
- [CloudFront](#cloudfront)
  - [Create a CloudFront distribution](#create-a-cloudfront-distribution)
- [EC2 (Amazon Elastic Compute Cloud)](#ec2-amazon-elastic-compute-cloud)
  - [EC2 Pricing Models](#ec2-pricing-models)
  - [EC2 Instance Types](#ec2-instance-types)
    - [EBS](#ebs)
  - [Create a web server](#create-a-web-server)
  - [Load balancing](#load-balancing)
  - [EC2 Bootstrap script](#ec2-bootstrap-script)
  - [EC2 image](#ec2-image)
  - [Create Auto Scaling Groups to make a fault tolerant web](#create-auto-scaling-groups-to-make-a-fault-tolerant-web)
- [AWS Command Line - LAB](#aws-command-line---lab)
- [Roles](#roles)
- [Database and RDS](#database-and-rds)
- [Exam notes](#exam-notes)
  - [S3](#s3)
  - [CloudFront](#cloudfront-1)
  - [EC2](#ec2-1)
  - [Roles](#roles-1)
  - [Load balancers](#load-balancers)
  - [DynamoDB](#dynamodb)

# Info

## Buckets

* jeremythenbucket

# Check

* Supperintelligence book

# Terms

* Edge Locations
* VPC (Virtual Private Cloud)
* Route53 (Amazon's DNS service)
* Content Delivery
* OLTP vs OLAP
* Data Warehousing

# Notes

* AWS has regions around the world and more are being added.
* Use the regions near you.
* Some regions may not have some services.
* For the first AWS certification, make sure to have a deep understanding of VPC.
* To get new user's credentials, click on the user, Security Credentials, make the current credential inactive and Create Access Key.
* The private key is the key to open the public key.

* You can add scripts to an instance when you are creating it, this way when it launches you can install things and etc. Called bootstrap scripts.

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

# IAM (Identity Access Management)

Here you can create users, give privileges, control authentication, etc.

* MFA (Multi Factor Authentication, with Google Authenticator)

# S3 (Simple Storage Service)

S3 is a place to put your files, like images, videos, audios, files that are not going to change.
Files can be from 0 to 5 TB.

Files are stored in Buckets, with unique names.

Example:

service-region-
https://s3-eu-west-1.amazonaws.com/bucketname

If the file was successfully uploaded, a 200 HTTP code will be returned.

S3 is Object based, which means just files.

They have:

* Key, value, version Id, metadata, subresources.

The key is the object name and the value is the actual data.

## S3 data consistency

* Read after Write
  * Able to read the file right away
* Eventual Consistency for overwrite PUTS and DELETES
  * Changes (update/delete) take some time to propagate

## S3 Guarantees

* Built for 99.99% availability for the S3 platform.
* 99.999999999% durability (11 x 9s)

## S3 Features

* Tiered Storage Available
* Lifecycle Management
* Versioning
* Encryption
* Secure your data using Access Control Lists and Bucket Policies
* Access Control is on a file level
* Bucket Policies is on a bucket level

## S3 Storage Classes

* S3 Standard
* S3 - IA (Infrequently Access)
* S3 One Zone - IA
* S3 - Intelligent Tiering
  * Intelligently moves files to the more cost efective S3 class.
* S3 Glacier
  * Cheaper. Retrieval from minutes to hours
* S3 Glacier Deep Archive
  * Cheaper. Retrieval from 12 hours.

## S3 Charges

* Storage
* Requests
* Storage Management Pricing
* Data Transfer Pricing
* Transfer Acceleration
* Cross Region Replication Pricing

## S3 Lab

When you select S3, the region changes to GLOBAL.

To make any uploads to a Bucket public, put this in the Permissions > Bucket Policy option.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::BUCKET_NAME/*"
            ]
        }
    ]
}

```

# CloudFront

It's Amazon's CDN (Content Delivery Network)

Can be used to deliver your entire website, including dynamic, static, streaming content. 

## Create a CloudFront distribution

* Under Networking & Content Delivery, select CloudFront > Create Destribution

# EC2 (Amazon Elastic Compute Cloud)

Its just a virtual server in the cloud.

## EC2 Pricing Models

* On Demand
  * Allows you to pay a fixed rate by hour/second. No commitment.
* Reserved
  * Cheaper. With 1 to 3 year contract term.
* Spot
  * Allows you to bid price.
* Dedicated Hosts
  * Physical EC2 server dedicated for your use.
  
## EC2 Instance Types

There are families of EC2 instances specialized in different use cases.
Like I3 for High Speed Storage, T3 Lowest Cost, General Purpose, etc.

### EBS

Allows you to create storage volumes and attach them to Amazon EC2 instances. Is a 'virtual disk in the cloud'.

* SSD
  * GP2 (General Purpose SSD)
  * IO1 (Provisioned IOPS SSD). Fastest.
* Magnetic (HDD)
  * ST1 (Throughput Optimized HDD)
  * SC1 (Cold HDD).

## Create a web server

1) Login to your EC2 instance
2) Update yum (which is a package manager) with:
> yum update -y
3) Install apache server 'yum install httpd'
4) go to /var/www/html

## Load balancing

There are 3 types of AWS load balancers:

1) Application Load Balancer
2) Network Load Balancer (ultra-high performance)
3) Classic Load Balancer

To create an Application Load Balancer

4) Go to EC2
5) Load Balancing, Load Balancer
6) Application Load Balancer > Create

When you create a new instance and want to register it to a load balancer, go to Load Balancing > Target Groups and add that instance to the load balancer you created previously.

## EC2 Bootstrap script

While creating an EC2 instance, you can put a bootstrap script in Advanced Details like:

```bash
#!/bin/bash
yum install httpd php php-mysql -y
cd /var/www/html
wget https://wordpress.org/wordpress-5.1.1.tar.gz
tar -xzf wordpress-5.1.1.tar.gz
cp -r wordpress/* /var/www/html/
rm -rf wordpress
rm -rf wordpress-5.1.1.tar.gz
chmod -R 755 wp-content
chown -R apache:apache wp-content
service httpd start
chkconfig httpd on
```

## EC2 image

You an select an instance, Actions > Image > Create Image.
This works like a snapshot of the same instance that can act as a node.

## Create Auto Scaling Groups to make a fault tolerant web

Don't forget to terminate it after working with it.


# AWS Command Line - LAB

* To login in PuTTY, or command line

> login as: ec2-user
> ssh ec2-user@3.80.211.105 -i MyPrivateKey.pem

* To confure aws from the console

> aws configure

* To create a s3 bucket. 'mb' stands for 'make bucket'

> aws s3 mb s3://jeremythenbucket

* See all bucket list

> aws s3 ls

* Upload a file to S3 from console. 'cp' stands for 'copy'

> aws s3 cp hello.txt s3://jeremythenbucket/hello.txt

* To see the .aws directory, to see config and credentials

> cd ~
> cd .aws
> ls

* To override the Access Key ID and Secret Access Key

> aws configure
> AWS Access Key ID: putwhateverwrong
> AWS Secret Access Key: putwhateverwrong

* Remove the .aws directory. This way your EC2 instance doesn't try to use the credentials in there and uses your role instead.

> rm -rf .aws

* Elevate your user

> sudu su


# Roles

1) Go to IAM
2) Roles
3) Create Roles
4) Select the service (like EC2)
5) Filter and select the Amazon permision, like AmazonS3FullAccess
6) Role name, description
7) Create Role
8) Go to EC2
9) Select your instance
10) Actions
11) Instance Settings > Attach/Replace a AIM Role
12) Apply

# Database and RDS

RDS (SQL/OLTP)

* SQL
* MySQL
* PostgreSQL
* Oracle
* Autora
* MariaDB

DynamoDB (No SQL)
Red Shift OLAP

Redshift is Amazon's Data Warehouse solution. Used for Business Intelligence or Data Warehousing.

ElasticCache caches the most common queries. To speed up performance of existing databases. It supports Memcached and Redis.





---

# Exam notes

SNS is a way of sending you an email to notify you.

User Access types:

* Programmatic access (using the Command Line)
* AWS Management Console access
* Amazon SDK access

Policies are specified in JSON.

IAM settings are Global, you don't specify a region, all user creation, etc., are created globally.

The root account is your email, has full administrator access. You should create users for others.

A group is a place to store your users and inherit all permissions specified in that group. Policies consists of JSON.

## S3

* Object-based, upload files
* Files from 0 Bytes to 5TB
* Unlimited storage
* Files stored in Buckets
* S3 is a universal namespace, name must be globally unique
* 200 HTTP code when files uploads fine
* Files saved as Key Value pair
* IAM Policies to Users and Groups
* You can use to host STATI websites
* S3 Scales automatically

## CloudFront

* Edge Location is the location where content will be cached, near the client.
* Origin, the original service where the file was uploaded.
* Distribution, name of CDN which consists of a collection of Edge Locations.
* Web Distribution and RTMP (used for media streaming)
* Edge Locations are not READ only.
* Objects are cached for the time to live (TTL)
* You can clear cached objects (will get charged)


## EC2

* Linux - SSH (port 22)
* Microsoft = Remote Desktop Protocol (port 3389)
* HTTPS (port 443)
* HTTP (port 80)
* Design for failure, have one EC2 instance in each availability zone

## Roles

* Roles are much more secure than using access key id's and secret access keys and are easier to use.
* You can apply roles to EC2 instances at any time and the changes are visible immediately.
* Roles are universal. You don't need to specify region, similar to users.

## Load balancers

There are 3 types of AWS load balancers:

1) Application Load Balancer (make intelligent decisions)
2) Network Load Balancer (ultra-high performance)
3) Classic Load Balancer

Have EC2 instances in different availability zones in case one failes.

Use bootstrap scripts.

## DynamoDB

Amazon's NO/SQL database


---