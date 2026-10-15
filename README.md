## AWS Assingment 1 -  VPC & Networking

#### Objective : Create a custom VPC with one public and one private subnet, set up the correct routing for internet access, and deploy EC2 instances across them.


### Steps
Here are the steps I take in order to achieve this :


1. Create the VPC

I am going to create a Custom VPC with 2 subnets ; 1 public and 1 private

<img width="1593" height="575" alt="image" src="https://github.com/user-attachments/assets/aa0f55cb-6180-4bca-ace7-43486235ec70" />


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

<img width="1105" height="723" alt="image" src="https://github.com/user-attachments/assets/eb463793-7f39-412b-a1a8-7ecc418d0fc0" />

3. I created a Security Group

Public EC2 SG: allow SSH/HTTP only from your IP
<img width="1599" height="349" alt="image" src="https://github.com/user-attachments/assets/1e8d4a3a-422b-4420-934a-394923387131" />

Private EC2 SG: allow only internal access

<img width="1596" height="579" alt="image" src="https://github.com/user-attachments/assets/9d29c4eb-9245-456d-8cba-a7150c4b58b5" />



5. Created an EC2 instance 

I created an EC2 instance and attached into Public Subnet and VPC .

Steps:
1. Click Launch Type
2. Give a name
3. Leave AMI and Instance type default 
4. Edit Network Settings 
5. Attach Network --> Custom VOC
6. Subnet --> Public Subnet
7. Finsih

<img width="1588" height="703" alt="image" src="https://github.com/user-attachments/assets/92faa77e-b4fe-4526-afe7-5f58854ab53c" />


5. Created Internet Gateway

This is going to allows our resources in my VPC to access the Internet.

1. Click `Create Internet Gateway `
2. Attach to my VPC

<img width="1596" height="343" alt="image" src="https://github.com/user-attachments/assets/09c5a5af-8865-4be1-9f9f-966caecc41dc" />


6. Update route table

This is to ensure that traffic from our VPC is able to go the IGW , thus access the Internet or other resources.

1. Click 'Create Route Table
2. Give it a name and attach it to our VPC.

<img width="1599" height="675" alt="image" src="https://github.com/user-attachments/assets/3be87165-9e29-47e3-8e9a-f4f8988056df" />


Now we are going edit the route table for our Public Subnet to IGW.

<img width="1252" height="194" alt="image" src="https://github.com/user-attachments/assets/05cbcc6f-1a23-49ff-87ee-4f36c900b8e0" />


After we need to explicity associate ` Public Subnet` to this route table as by default Subnet uses the main route table that was created along with custom VPC. This is ensure that our `Public Subnet` uses this route table that we made.

<img width="1342" height="276" alt="image" src="https://github.com/user-attachments/assets/2d9b61b8-4d3b-46cb-95c6-8e9b492ea377" />


7. Result
## Now our public subnet access Internet Via IGW 

<img width="1597" height="712" alt="image" src="https://github.com/user-attachments/assets/b189a850-e1cc-49bd-8f2c-77ff5ba51f53" />


## Private Subent


1. To allow our resources inside the private instances access the Internet . We need to first create a an EC2 instance inside the subnet.

   <img width="1324" height="41" alt="image" src="https://github.com/user-attachments/assets/9c8a5dab-7a62-4bb2-8ebe-3d1debeae1d0" />

2. We need to create a NAT Gateway and route it our private subnet.

<img width="1599" height="473" alt="image" src="https://github.com/user-attachments/assets/8ca6f969-c309-440c-bf6c-3bd29f0e919b" />


3. Final Result :

The public subnet has now become a bastion host . This means in order to access my private EC2 instance , I need to ssh from my bastion host into the private ec2 instance. As you
can see they both instances have internet due to routing the public subnet to IGW and private subnet to NAT Gateway.



## Video : 

https://github.com/user-attachments/assets/d9d3f88f-fc9a-4e27-8abd-e58957cd3910


















## Challenges 

When attempting this assignment here are the errors I came across and how I resolved them .

1. My EC2 instance will not connect

<img width="1597" height="712" alt="image" src="https://github.com/user-attachments/assets/b189a850-e1cc-49bd-8f2c-77ff5ba51f53" />

Solution : 

When I tried to this EC2 instance , I used the AWS EC2 Instance Connect which does not match my SG rules , therfore It blocked access. 
The only it would work was if I connected from my own machine via SSH.

The result :

<img width="810" height="426" alt="image" src="https://github.com/user-attachments/assets/cd2bbbb8-85c7-4806-baa2-3b3eb6698e89" />


