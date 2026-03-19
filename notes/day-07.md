# Day 07 – Credential Abuse and Identity Misuse

## Objective
Understand how attackers misuse valid cloud credentials to perform unauthorized actions and explore the risks associated with compromised identities.

---

## Concepts Learned

### Credential Abuse
Credential abuse occurs when an attacker gains access to valid credentials (such as IAM user credentials or access keys) and uses them to interact with cloud resources.

Unlike traditional attacks, no vulnerability exploitation is required. The attacker simply uses legitimate access.

---

### Identity Misuse
In cloud environments, identities control access to resources. If an identity is compromised, attackers can act as a legitimate user.

This makes detection difficult because actions appear normal in logs.

---

### Why Credential Abuse is Dangerous
Credential-based attacks are powerful because:

- They bypass traditional security defenses
- They use legitimate authentication
- They often go undetected for long periods
- They depend on misconfigured or over-permissive identities

---

### Real-World Risk
Many cloud breaches occur because:

- Credentials are leaked in public repositories
- Access keys are exposed in applications
- Permissions are overly broad

---

## Practical Work

### 1. Simulated Credential Usage
Used an IAM user with assigned permissions to interact with AWS services.

Observed how actions performed using valid credentials appear legitimate.

---

### 2. Accessed Cloud Resources
Using the IAM user:

- Accessed S3 buckets
- Viewed EC2 instances
- Explored IAM configurations

This simulates how an attacker would explore resources after gaining credentials.

---

### 3. Performed Allowed Actions
Tested what actions could be performed based on permissions:

- Viewing resources
- Listing data
- Checking configurations

This helped understand how permissions define the impact of credential compromise.

---

### 4. Evaluated Blast Radius
Analyzed how much damage could be done using the current permissions.

Identified that higher permissions increase the risk and potential impact.

---

## Security Observation

If an attacker obtains valid credentials, they can operate inside the cloud environment without triggering immediate suspicion.

Because actions are performed using legitimate access, it becomes difficult to distinguish between normal and malicious behavior.

Over-permissive IAM policies significantly increase the risk of large-scale damage.

---

## Remediation

To reduce the risk of credential abuse:

- Avoid using long-term access keys when possible
- Use IAM roles instead of static credentials
- Apply least privilege permissions
- Rotate credentials regularly
- Monitor identity activity using logging tools
- Enable multi-factor authentication (MFA)

---

## Tools Used

- AWS Management Console
- IAM (Identity and Access Management)
- Git
- GitHub
- Markdown documentation

---

## Next Steps

Day 08 will focus on **role misuse and trust relationships**, exploring how attackers can assume roles and gain additional permissions.