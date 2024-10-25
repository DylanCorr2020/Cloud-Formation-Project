# CloudFormation Project

## Project Overview

This project uses AWS CloudFormation to create a secure infrastructure in a cloud environment. The setup includes a Virtual Private Cloud (VPC) with two public subnets and four private subnets, allowing communication between resources and the internet. Users can connect to the bastion host in **Public Subnet 1A** via SSH, then access EC2 instances in **Private Subnet 1A**. Security groups are configured for communication between the EC2 instances in **Private Subnet 1A** and **Private Subnet 2B**.

![Architecture Diagram](C:\Users\dylancorrGMIT\Desktop\VPC.draw.io)

## Prerequisites

Before deploying, ensure you have the following:

- [AWS Account](https://aws.amazon.com/)
- Admin user created in IAM
- [AWS CLI installed](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [VS Code or another code editor](https://code.visualstudio.com/download)

Run the following command to clone the repository down to your local machine

```bash
   git clone https://github.com/DylanCorr2020/Cloud-Formation-Project.git
```

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

```bash
 ssh -i bastion.pem ec2-user@<your public bastion ip address>
```

Then should show the Linux terminal

# Copying over the SSH key

Make sure you in the same folder as the SSH key where it was downloaded

Run the following command to copy over the SSH file from your local machine to the home directory

```bash
scp -i bastion.pem bastion.pem ec2-user@<your public bastion ip address>:~/
```

We are going to use this key file to authenticate into our EC2 server in the application private subnet1A

# Connect to EC2 in priavate Sunbnet1A

First copy Private ips of EC2 instances in both AAppPrivateSubnet1 and AppPrivateSubnet2B

Now we will SSH into our first EC2 in AppPrivateSubnet1

```bash
ssh -i bastion.pem ec2-user@<private ip address of EC2 >
```

Should know if your logged in if it diplays the ip address in the terminal this means you are connected to the the EC2 instance in privateSubnet1A

Then to ensure connection between the two instances by typing ping to the ip address of EC2 instance of in AppPrivateSubnet2B should give back a response

# Troubleshooting

After deploying your vpc stack run the following command

```bash
aws cloudformation describe-stack --stack-name vpc-stack
```

Stack Status: Ensure the stack status is "CREATE_IN_PROGRESS" or "UPDATE_IN_PROGRESS". If it's "FAILED" or "ROLLBACK_IN_PROGRESS", you'll need to investigate further.

Go to the CloudFormation Console and review the event history for your stack to see if there are any error messages.

Once you have fixed the error, you can either delete the stack and re-upload it or update the stack

```bash
   aws cloudformation delete-stack --stack-name vpc-stack
```

```bash
   aws cloudformation update-stack --stack-name vpc-stack --template-body file://vpc.yaml
```
