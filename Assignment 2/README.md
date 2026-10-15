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





1b.  Here is the VPC :