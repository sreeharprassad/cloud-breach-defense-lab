# Day 03 – Cloud Networking Fundamentals and EC2 Deployment

## Objective
Understand the basics of cloud networking in AWS and deploy a virtual server to observe how network configurations can affect system exposure.

---

## Concepts Learned

### Virtual Private Cloud (VPC)
A Virtual Private Cloud (VPC) is a logically isolated network within AWS where cloud resources are deployed. It allows administrators to define IP address ranges, routing rules, and network security configurations.

### Public vs Private Resources
Cloud resources can be configured to be publicly accessible or restricted to internal networks. Public resources have internet connectivity, while private resources are accessible only within the internal cloud network.

### Security Groups
Security groups act as virtual firewalls for AWS resources such as EC2 instances. They control inbound and outbound traffic by allowing or denying specific network ports and IP ranges.

### Attack Surface
The attack surface refers to the total number of potential entry points an attacker can use to access a system. Exposing services such as SSH or web servers to the public internet increases the attack surface.

---

## Practical Work

### 1. Accessed the EC2 Service
Logged into the AWS Management Console and navigated to the EC2 dashboard to manage virtual machines.

### 2. Launched an EC2 Instance
Created a new virtual machine with the following configuration:

- Operating System: Amazon Linux
- Instance Type: t2.micro
- Network: Default VPC
- Auto-assign Public IP: Enabled

### 3. Created a Security Group
Configured a security group to control network access to the instance.

Inbound rule configured:

- Protocol: SSH
- Port: 22
- Source: 0.0.0.0/0

This rule allows SSH connections from any IP address on the internet.

### 4. Generated an SSH Key Pair
Created and downloaded a key pair that can be used to securely connect to the EC2 instance.

### 5. Observed Public Exposure
After launching the instance, AWS assigned a public IP address. This means the server is reachable from the internet depending on the security group configuration.

---

## Security Insights

Allowing SSH access from `0.0.0.0/0` exposes the server to the entire internet. This configuration is common in misconfigured environments and can allow attackers to attempt brute-force login attacks.

Reducing exposure by restricting access to specific IP addresses can significantly lower the risk.

Understanding how networking configurations affect exposure is an important part of securing cloud environments.

---

## Tools Used

- AWS Management Console
- EC2 Service
- Security Groups
- Git
- GitHub
- Markdown documentation

---

## Next Steps

Day 04 will focus on cloud storage security and exploring how misconfigured storage services such as S3 buckets can expose sensitive data.