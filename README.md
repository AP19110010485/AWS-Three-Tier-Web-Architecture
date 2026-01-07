# AWS Three-Tier Web Architecture Project

## Architecture Overview
![AWS Architecture - DrawIO](https://github.com/pandacloud1/AWS_Project1/assets/134182273/3e46931f-0802-48a7-b044-22cd2afde467)

# AWS Three-Tier Web Architecture Project

## Description

This project demonstrates a hands-on implementation of a three-tier web architecture on AWS. All networking, security, application, and database components are manually created and configured to achieve high availability, scalability, and fault tolerance using AWS best practices.

---

## Architecture Overview

A public-facing Application Load Balancer routes client traffic to EC2 instances in the web tier. The web tier runs Nginx servers that host a React.js frontend and forward API requests to an internal-facing Application Load Balancer. The internal load balancer routes traffic to a Node.js-based application tier, which interacts with an Amazon Aurora MySQL Multi-AZ database. Load balancing, health checks, and auto scaling are implemented at each tier to ensure availability.

---

## Algorithm

### AWS PROJECT

---

# Creating 3 Tier Architecture & Integrating Other AWS Resources

## Step 1: Download Code from GitHub in Your Local System

* Clone or download the project repository to your local machine

## Step 2: Create Two S3 Buckets

* Create one S3 bucket for storing web-server and app-server code
* Upload the application code from your local system
* Create another S3 bucket for storing VPC Flow Logs

## Step 3: Create IAM Role with Policies

* Attach AmazonS3ReadOnlyAccess policy
* Attach AmazonSSMManagedInstanceCore policy

## Step 4: Create VPC, Subnets, IGW, NAT Gateway, and Route Tables

* Create a VPC
* Create public and private subnets
* Enable auto-assign public IP for web-tier public subnets
* Create and attach an Internet Gateway
* Create a NAT Gateway for private subnets
* Configure route tables
* Enable VPC Flow Logs and send logs to the S3 bucket

## Step 5: Create Security Groups

* External-Load-Balancer-SG: Allow HTTP (80) from 0.0.0.0/0
* Web-Tier-SG: Allow HTTP from External-Load-Balancer-SG
* Internal-Load-Balancer-SG: Allow HTTP from Web-Tier-SG
* App-Tier-SG: Allow port 4000 from Internal-Load-Balancer-SG
* DB-Tier-SG: Allow MySQL (3306) from App-Tier-SG

## Step 6: Create DB Subnet Group and RDS

* Create a DB subnet group
* Create an Amazon Aurora MySQL database with Multi-AZ enabled
* Place the database in the DB subnet group

## Step 7: Configure Application Tier

* Launch a test application server
* Install required packages and test database connectivity
* Create an AMI from the instance
* Create a launch template using the AMI
* Create a target group
* Create an internal Application Load Balancer
* Create an Auto Scaling Group
* Update nginx.conf with Internal ALB DNS and upload it to S3

## Step 8: Configure Web Tier

* Launch a test web server
* Install Nginx and Node.js (React)
* Test connectivity with the application tier
* Create an AMI from the instance
* Create a launch template using the AMI
* Create a target group
* Create a public Application Load Balancer
* Create an Auto Scaling Group

## Step 9: Add External ALB DNS Record in Route 53

* Create or update Route 53 records pointing to the external ALB

## Step 10: Create CloudWatch Alarms and SNS

* Configure CloudWatch alarms for monitoring
* Set up SNS notifications for alerts

## Step 11: Create CloudTrail

* Enable CloudTrail for auditing and API activity logging

## Step 12: Delete the Entire Infrastructure

* Delete CloudFront distributions (if any)
* Delete CloudWatch alarms
* Remove Route 53 records
* Delete load balancers, target groups, auto scaling groups, and launch templates
* Delete security groups
* Delete NAT Gateway (wait approximately 5 minutes)
* Release Elastic IP addresses
* Delete the VPC
* Delete RDS instances and DB subnet group

---

## Outcome

This project demonstrates the ability to design, deploy, monitor, and clean up a secure, scalable, and highly available three-tier web architecture on AWS, suitable for real-world production environments and cloud engineering portfolios.

---


