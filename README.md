# CloudFormation Project

## Project Overview

This project uses AWS CloudFormation to create a secure infrastructure in a cloud environment. The setup includes a Virtual Private Cloud (VPC) with two public subnets and four private subnets, allowing communication between resources and the internet. Users can connect to the bastion host in **Public Subnet 1A** via SSH, then access EC2 instances in **Private Subnet 1A**. Security groups are configured for communication between the EC2 instances in **Private Subnet 1A** and **Private Subnet 2B**.

![Architecture Diagram](path_to_architecture_image)

## Prerequisites

Before deploying, ensure you have the following:

- [AWS Account](https://aws.amazon.com/)
- Admin user created in IAM
- [AWS CLI installed](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [VS Code or another code editor](https://code.visualstudio.com/download)

## Deploying the Stack to AWS

1. Open a terminal in the directory where your repository is located.
2. Run the following command to create the stack:

   ```bash
   aws cloudformation create-stack --stack-name vpc-stack --template-body file://vpc.yaml
   ```

# Connectiong to the Bastion Host

First download the SSH key for key for Bastion Host

Copy over the the public id address of bastion host in the aws console

Then go the terminal make sure you are in the same directory where the SSH file was downloaded

ssh -i bastion.pem ec2-user@_your public bastion ip address _

Then should show the Linux terminal

# Copying over the SSH key

Make sure you in the same folder as the SSH key where it was downloaded

Run the following command to copy over the SSH file from your local machine to the home directory

scp -i bastion.pem bastion.pem ec2-user@_your public bastion ip address _:~/

We are going to use this key file to authenticate into our Ec2 server in the application private subnet1A

# Connect to EC2 in priavate Sunbnet1A

First copy Private ips of Ec2 instances in both AAppPrivateSubnet1 and AppPrivateSubnet2B

Now we will SSH into our first EC2 in AppPrivateSubnet1

ssh -i bastion.pem ec2-user@_ private ip address of EC2 _

should know if your logged in if it diplays the ip address in the terminal this means you are connected to the the Ec2 instance in privateSubnet1A

Then to ensure connection between the two instances by typing ping to the ip address of EC2 instance of in AppPrivateSubnet2B should give back a response

# Troubleshooting
