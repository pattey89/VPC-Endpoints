<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** PATRICK ADDAI  
**Email:** patrickaddai1689@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a networking service provided by AWS and gives the ability to isolate the public internet, set up secure connection between our resources and control traffi flows/security.

### How I used Amazon VPC in this project

I used Amazon VPC today to set up VPC Endpoint, specifically an S3 Gateway. This provide my VPC with direct, private access to another AWS service.

### One thing I didn't expect in this project was...

One thing I didn't expect was to see my own S3 bucket getting blocked once I saved my bucket's new policy to block all access/traffic except from my endpoint.

### This project took me...

2 hours 2o mins including practice time!

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step I am going to create a VPC from scratch!
Launch an EC2 instance, which I'll connect to using EC2 Instance Connect later and then Set up an S3 bucket so that I can set up and endpoint architecture and test that setup in the last step of this project.


### Step 2 - Connect to EC2 instance

In this step I am connecting directly using the EC2 Instance connect. Connecting to instance will help us with accessing S3 and running commands later in this project.

### Step 3 - Set up access keys

In this step, I will set up an access key so that my EC2 instance will have access to AWS environment. We can think of access key almost like log in details for EC2 instances/applications (non humans) to interact with AWS services.

### Step 4 - Interact with S3 bucket

In this step, I am appluing my access key credentials to our EC2 instance and then I am using AWS CLI and my EC2 isntance to access Amazon S3. 

---

## Architecture set up

I started my project by launching three key resources - a VPC, EC2 isntance and S3 bucket.

I also set up an S3 bucket with two files inside.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured was the AWS access key ID, secret access key that matching that key ID, the default region type and the default output format.

An Access Keys are credentials that an EC2 instance/other server/application would need to get access to my AWS environment e.g. creating resources, reading what's inside my AWS account etc.

Secret access keys are like password in the context of access key/credentials for my EC2 isntance to get access to my AWS services/environment.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use IAM admin roles instead! This means the necesary permission will be attached to an IAM role, then the role will be associated with the relaevant resources. 

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls. This command is used to list all buckets in AWS account.



The terminal responded with a list of my account S3 bucket. This indicated that the access keys was set up correctly and can give my EC2 instance access to my AWS account and environment.clear


![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command 'aws s3 ls s3://nextwork-vpc-endpoints-myname' which returned list of all of the objects inside that S3 bucket.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command 'sudo touch /tmp/nextwork.txt'. This command creates empty file named nextwork.txt and saves it locally in the EC2 instance.

The second command I ran was 'aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-endpoints-myname'. This command will will copy the file I created i.e. nextwork.txt and upload that to my S3 bucket!

The third command I ran was 'aws s3 ls s3://nextwork-vpc-endpoints-myname' which validated that a new file was created and uploaded into my S3 bucket!

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, we are setting up a VPC endpoint so that communication between our VPC and other services (especially S3) is direct and secure.

### Step 6 - Bucket policies

In this step, I am testing my endpoint connection by blocking off all traffic to my S3 bucket except for traffic coming from my endpoint.

### Step 7 - Update route tables

In this step I am testing my endpoint connection between my bucket and EC2 instance.

### Step 8 - Validate endpoint conection

In this step I am going to validate my VPC Endpoint set up one more time. I am also going to use endpoint polices to restrict my EC2 instances access to my AWS environment.

---

## Setting up a Gateway

I set up an S3 Gateway, which is a type of endpoint specifically designed for Amazon S3 Gateway work by updating the route table of associated subnets so that S3 bound traffic goes through the Gateway instead of the internet

### What are endpoints?

An endpoint in AWS is a service that allows private connections between your VPC and other AWS services without needing the traffic to go over the internet.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it

My bucket policy will deny traffic from ALL sources - except for traffic coming from my VPC endpoint.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because my bucket policy is denying all traffice that doesn't come from my endpoint i.e. the policy denies traffic from the AWS Management Console.

I also had to update my route table because my route table by default didn't provide a route for traffic in my public subnet to the VPC endpoint.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I visited the Endpoint page of my VPC console and  I modified the route table from there to associate my VPC's public subnet.

After updating my public subnet's route table, my EC2 instance could connect with my S3 bucket! Access was no longer deny.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a type of policy designed for specifying the range of resources and actions permitted by an endpoint.

I updated my endpoint's policy by changing the effect from 'Allow' to 'Deny'.  I could see the effect of this right away, because my EC2 was again deny access to S3 when I tried to run another AWS S3 command.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-endpoints_3e1e79a3)

---

---
