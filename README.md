# aws-private-ec2-bastion-architecture

## Project Overview

This project demonstrates how to deploy a **secure AWS infrastructure** where application servers run inside a **private subnet** and cannot be accessed directly from the internet.

Access to the private EC2 instance is only possible through a **Bastion Host** located in the public subnet. The private server also uses an **IAM Role** to access AWS services securely without storing credentials.

## Architecture

Access Flow:

Local Machine → Bastion Host → Private EC2 Instance → Amazon S3



---

## Technologies Used

- AWS VPC
- Amazon EC2
- IAM Roles
- Security Groups
- Nginx Web Server
- Amazon S3
- SSH

---

## Steps Implemented

### 1. Created VPC
CIDR Block:
10.0.0.0/16

![](/Screenshot%202026-03-07%20183535.png)


---

### 2. Created Subnets

Public Subnet
10.0.1.0/24

Private Subnet
10.0.2.0/24

![](/Screenshot%202026-03-07%20183917.png)



---

### 3. Launched Bastion Host

- Deployed EC2 in **Public Subnet**
- Enabled **Public IP**
- Allowed **SSH (Port 22)** from local machine

![](/Screenshot%202026-03-07%20185527.png)
---

### 4. Launched Private EC2 Instance

- Deployed EC2 in **Private Subnet**
- **No Public IP assigned**
- Allowed **SSH only from Bastion Host**

---

### 5. Connected to Private Server

Connect to Bastion Host:

![](/Screenshot%202026-03-07%20190133.png)

Then connect to Private EC2:

ssh -i key.pem ec2-user@<Private-EC2-IP>

![](/Screenshot%202026-03-07%20192357.png)

6. Installed Web Server
sudo yum update -y
sudo yum install nginx -y
sudo systemctl start nginx

![](/Screenshot%202026-03-07%20191446.png)


7. Implemented IAM Role

Created IAM Role with policy:

AmazonS3ReadOnlyAccess

![](/Screenshot%202026-03-07%20191812.png)

Attached the role to the Private EC2 instance.

![](/Screenshot%202026-03-07%20191852.png)


Security Features

Private EC2 instances have no public IP


IAM Roles used instead of access keys

Security Groups control traffic

Learning Outcomes

AWS VPC network architecture

Bastion Host implementation

Private EC2 security design

IAM Role based authentication

Secure infrastructure deployment

## Conclusion

This project demonstrates how to build a secure AWS infrastructure using best practices. The application server is deployed in a private subnet without a public IP, ensuring it is not directly accessible from the internet. Access to the private server is controlled through a Bastion Host, which improves security and limits exposure.