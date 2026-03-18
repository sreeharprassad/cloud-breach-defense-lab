# Day 05 – Cloud Credentials and Access Key Security

## Objective
Understand how cloud credentials work in AWS and learn how exposed credentials can lead to unauthorized access and cloud breaches.

---

## Concepts Learned

### Cloud Credentials
Cloud credentials are used to authenticate and authorize access to cloud resources. In AWS, these are mainly:

- Access Key ID
- Secret Access Key

These credentials allow programmatic access to AWS services.

---

### IAM Access Keys
IAM users can generate access keys to interact with AWS services via CLI, SDKs, or scripts.

Anyone who has these keys can access AWS resources based on the permissions assigned to that user.

---

### Credential Exposure Risk
If access keys are leaked (for example, uploaded to GitHub or exposed in code), attackers can use them to:

- Access cloud resources
- Download sensitive data
- Launch new services (which may incur cost)
- Modify or delete infrastructure

This is one of the most common real-world cloud security issues.

---

### Principle of Least Privilege
Credentials should only have the minimum permissions required to perform their task.

Over-permissioned credentials increase the **blast radius** if compromised.

---

### EC2 Metadata Service (Concept)
When an EC2 instance has an IAM role attached, it can retrieve temporary credentials from the metadata service.

If an attacker gains access to the instance, they may extract these credentials and use them externally.

---

## Practical Work

### 1. Explored IAM Credentials
Navigated to the IAM service and reviewed how credentials are managed for users.

### 2. Created Access Keys (Study Purpose)
Observed how access keys are generated for an IAM user and understood their structure.

(Note: Keys were not exposed publicly and were handled securely.)

### 3. Understood Credential Usage
Learned how access keys are used in:
- AWS CLI
- Applications
- Automation scripts

### 4. Studied Credential Risks
Analyzed how credential leaks can occur:
- Hardcoded in source code
- Uploaded to public repositories
- Shared insecurely

---

## Security Observation

Exposed credentials can allow attackers to fully access cloud resources depending on the permissions assigned.

Unlike passwords, access keys often do not require additional verification, making them highly sensitive.

Many real-world breaches occur because developers accidentally upload credentials to public repositories.

---

## Remediation

To protect cloud credentials:

- Never store credentials in source code
- Use environment variables or secure storage
- Rotate access keys regularly
- Disable unused credentials
- Use IAM roles instead of long-term access keys
- Apply least privilege permissions

---

## Tools Used

- AWS Management Console
- IAM (Identity and Access Management)
- Git
- GitHub
- Markdown documentation

---

## Next Steps

Day 06 will focus on **attack simulation**, where we start thinking like an attacker and perform enumeration of cloud permissions.