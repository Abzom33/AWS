## AWS Assingment 1 -  VPC & Networking

#### Objective : Create a custom VPC with one public and one private subnet, set up the correct routing for internet access, and deploy EC2 instances across them.


### Steps
Here are the steps I take in order to achieve this :


1. Create the VPC

I am going to create a Custom VPC with 2 subnets ; 1 public and 1 private

![alt text](image.png)

- Keep everything the same 
- Choose the IPv4 CIDR Range ; 10.0.0.0/16

2. Create the subnet
Whats makes a subnet public if it's routed to the Internet Gateway , which gives resources inside VPC internet access.
If it's not routed to IGW (Internet Gateway) then it's private subnet

Steps:
1. First click 'Create Subnet'
2. Then Attach custom VPC to the created subnet
3. Pick name of Subnet
4.  Choose an IPv4 subnet CIDR Range (**Note They must not overlap the other ranges in your VPC or subnets)
5. Choose AZ.
6. Repeat steps 1 - 6 



