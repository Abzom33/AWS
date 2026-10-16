## Assignment 2 - Application Load Balancer

A common DevOps pattern: multiple EC2 instances behind an ALB. This teaches load balancing, health checks, and proper security group isolation.

## Objective

Deploy two EC2 instances behind an ALB. The ALB must handle all incoming traffic. EC2 instances should not be accessible directly from the internet.

## Build Steps

1. Create two EC2 instances

- This is where we going to lauch our web servers to test to see if ALB works.
- We are going Launch two EC2 instances in the same VPC
- Ensure that the 2 EC2 instances are instances

1a. Here is the EC2 Instances :

Both Instances are in the same VPC  


<img width="1353" height="325" alt="image" src="https://github.com/user-attachments/assets/2b5bdc93-8160-4de8-9fd1-8f515b0d8933" />







1b.  Here is the VPC :


<img width="1361" height="360" alt="image" src="https://github.com/user-attachments/assets/938f19be-1be5-4853-aabf-b306153252da" />


1c . Here is the subnets

<img width="1413" height="176" alt="image" src="https://github.com/user-attachments/assets/5decf871-b015-4b0c-b0bb-3cdaa48b81bf" />





1c . Installing a simple web server for EC2 instance

```
!#/bin/bash
yum upgrade -y
yum update -y 
yum install httpd -y

systemctl enable httpd 
systemctl start httpd

echo "<h1>Welcome name to Server 1</h1>"> /var/www/html/index.html

```

2. Creating Application Load Balancer

This going to sit in front of our EC2 instances and direct traffic to the EC2 instances , perform health checks and auto scale.


2a . Creating Application Load Balancer (ALB)

You are presented with two options when creating ALB:


    1. Internet facing - This allows you to route request from the internet to your resource inside a VPC
    2. Internal   - This allows you to route request internally within your VPC . Doesn't route outside access.

    Based on this I am going use Internet facing as I need to my ALB to accept routes from the Internet since I am making web server which need Internet access .

    To do this you need make your subnet public by attaching an IGW to the VPC and routing it to your subnets .


2b. Creating Target Group

Target Group = set of destination that the ALB will route to.

In this case it is the EC2 instances :

<img width="776" height="533" alt="image" src="https://github.com/user-attachments/assets/3f7b6de8-c3e1-489c-bf51-ba52c85f29df" />


This is the destination of a Target Group :

<img width="1316" height="353" alt="image" src="https://github.com/user-attachments/assets/7c56ae61-a03b-4c65-a81c-3bfcd6a29bcc" />


Here is the result :

<img width="1390" height="675" alt="image" src="https://github.com/user-attachments/assets/a0b4a7b5-bef0-4441-aeaf-36e77bf30d77" />


    
2c . Creating Security Groups for the ALB

Security Groups act as a firewall for the ALB , allow/deny traffic based on rules

- ALB SG: allow HTTP from anywhere

<img width="1596" height="490" alt="image" src="https://github.com/user-attachments/assets/303d236a-a350-47dd-b567-5f3afaa32f74" />



- EC2 SG: allow HTTP only from the ALB SG.
- This is to make it private so th EC2 instance won't be available to the public

  <img width="1328" height="194" alt="image" src="https://github.com/user-attachments/assets/978a73b8-1324-4188-90f7-9e1482f5dc21" />



2D. Full ALB

<img width="1334" height="271" alt="image" src="https://github.com/user-attachments/assets/cfb2b292-abb6-4822-b0c1-02a4e27681af" />




3. Final Result




https://github.com/user-attachments/assets/4938907d-682c-47bc-9cf6-c0d542b06b14




3a . Health Checks

<img width="1592" height="692" alt="image" src="https://github.com/user-attachments/assets/c050dca1-b362-4ca7-9943-c3371eecf8db" />



