# Day 01 – Project Setup & Cloud Fundamentals

## Objective
Set up the project repository and understand the fundamental concepts of cloud computing and cloud security before starting hands-on security labs.

---

## Concepts Learned

### Cloud Computing
Cloud computing is the delivery of computing services such as servers, storage, networking, and databases over the internet instead of running them on local machines or physical infrastructure.

### Cloud Security
Cloud security focuses on protecting cloud-based infrastructure, applications, and data from unauthorized access, attacks, and misconfigurations.

### Shared Responsibility Model
Cloud security operates under a shared responsibility model. The cloud provider is responsible for securing the infrastructure, while the customer is responsible for securing their data, identities, configurations, and applications.

### Cloud Misconfiguration
Cloud misconfiguration occurs when cloud resources are improperly configured, potentially exposing sensitive data or services to attackers. Many real-world cloud breaches happen due to misconfigurations.

---

## Practical Work

### 1. Created Project Repository
Created a repository on GitHub to document and manage the Cloud Breach-to-Defense Lab project.

Actions performed:
- Created repository
- Added README file
- Selected MIT License
- Added project description

### 2. Set Up Local Project Structure
Cloned the repository locally and created folders for documentation.

Current project structure:

cloud-breach-defense-lab  
├── README.md  
├── LICENSE  
└── notes  
    └── day-01.md

### 3. Explored AWS Cloud Environment
Logged into the AWS Management Console and explored core services that will be used later for simulating security scenarios.

Key services explored:
- IAM (Identity and Access Management)
- EC2 (Virtual servers)
- S3 (Object storage)
- CloudTrail (Activity logging)

This exploration helped understand where important security configurations are managed.

---

## Security Insights

During exploration, it became clear that many cloud services allow powerful configurations. If misconfigured, these services may expose sensitive resources.

Common cloud risks include:
- Publicly accessible storage buckets
- Overly permissive access policies
- Exposed credentials
- Lack of logging and monitoring

These misconfigurations will be intentionally simulated in later stages of this lab to understand how attackers exploit them and how defenders detect and fix them.

---

## Tools Used

- Git
- GitHub
- AWS Management Console
- Markdown documentation

---

## Next Steps

Day 02 will focus on Identity and Access Management (IAM) in AWS, including creating users, roles, and policies and understanding how misconfigured permissions can lead to security risks.