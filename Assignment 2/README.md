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
