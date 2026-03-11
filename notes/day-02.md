# Day 02 – Identity and Access Management (IAM)

## Objective
Understand how identity and access control work in cloud environments and learn how permissions are managed using IAM in AWS.

---

## Concepts Learned

### Identity in Cloud
In cloud environments, identities represent entities that interact with cloud resources. These identities can be users, roles, or services that need permission to perform actions.

Managing identities securely is important because compromised identities can lead to unauthorized access to cloud resources.

### IAM (Identity and Access Management)
IAM is a service in AWS used to control access to cloud resources. It allows administrators to create users, assign permissions, and manage access policies.

IAM helps enforce the principle of least privilege by granting only the permissions required to perform specific tasks.

### IAM Users
An IAM user represents a person or application that needs access to AWS resources. Each user has unique credentials and permissions.

IAM users should be used for daily access instead of the root account.

### IAM Policies
Policies are JSON-based permission documents that define what actions an identity is allowed or denied to perform.

Policies control which services, resources, and actions a user or role can access.

### Principle of Least Privilege
The principle of least privilege means giving identities only the permissions necessary to perform their tasks.

This reduces the risk of damage if an identity is compromised.

### Blast Radius
Blast radius refers to the potential damage that can occur if an identity or system is compromised.

Reducing permissions helps limit the blast radius in case of an attack.

---

## Practical Work

### 1. Accessed AWS Console
Logged into the AWS Management Console using the root user account.

### 2. Navigated to IAM Service
Opened the IAM service to manage identities and access permissions.

### 3. Created an IAM User
Created a new IAM user for administrative access instead of using the root account.

Steps performed:
- Opened IAM service
- Selected "Users"
- Clicked "Create user"
- Entered username: `lab-admin`
- Enabled console access

### 4. Assigned Permissions
Attached the `AdministratorAccess` policy to the IAM user to allow full access to AWS services for lab experimentation.

### 5. Generated Login Credentials
AWS generated credentials for the IAM user including:
- Username
- Password
- Console login link

These credentials can now be used to log into AWS instead of the root account.

---

## Security Insights

Using the root account for daily tasks is dangerous because it has unrestricted access to all AWS resources.

Creating IAM users allows better control over permissions and helps track actions performed by specific identities.

Improperly configured IAM permissions can lead to security risks such as privilege escalation or unauthorized resource access.

---

## Tools Used

- AWS Management Console
- IAM Service
- Git
- GitHub
- Markdown documentation

---

## Next Steps

Day 03 will focus on cloud networking fundamentals and launching an EC2 instance with a security group configuration to understand public exposure risks.