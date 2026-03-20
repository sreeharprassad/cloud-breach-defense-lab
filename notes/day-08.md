# Day 08 – Role Misuse and Trust Relationship Exploitation

## Objective
Understand how attackers exploit IAM roles and misconfigured trust relationships to gain unauthorized access and perform actions beyond their original permissions.

---

## Concepts Learned

### IAM Roles
IAM roles are temporary identities that can be assumed by users, services, or external accounts to gain specific permissions.

Unlike IAM users, roles rely on trust relationships and provide short-lived credentials.

---

### Trust Relationships
A trust relationship defines **who is allowed to assume a role** using the "Principal" element in the trust policy.

---

### Role Misuse
Role misuse occurs when trust policies are overly permissive or incorrectly configured, allowing unintended entities to assume the role.

Common issues include:

- `"Principal": "*"` (public access)
- Allowing unknown AWS accounts
- Missing conditional restrictions (MFA, IP, etc.)

---

### Why Role Misuse is Dangerous

- Enables indirect privilege escalation
- Provides temporary credentials that appear legitimate
- Bypasses IAM permission boundaries
- Difficult to detect due to short-lived sessions

---

## Practical Work

### 1. Created Misconfigured IAM Role

Configured a role with an insecure trust policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

### 2. Attached Permissions to Role

Assigned permissions such as:

- S3 read access  
- EC2 describe access  

---

### 3. Simulated Role Assumption

Used AWS CLI to assume the role:

```bash
aws sts assume-role \
--role-arn <role-arn> \
--role-session-name attacker-session
```

---

### 4. Used Temporary Credentials

After assuming the role, temporary credentials were obtained:

- Access Key ID  
- Secret Access Key  
- Session Token  

These credentials were configured in the AWS CLI and used to:

- List S3 buckets  
- Describe EC2 instances  

---

### 5. Identity Observation

Observed that:

- Actions were executed under the **assumed role identity**  
- The original IAM user was not directly visible  
- Temporary sessions masked the source identity  

---

## Security Observation

Misconfigured trust relationships allow attackers to assume roles without needing explicit IAM permissions.

This enables:

- Unauthorized access to resources  
- Lateral movement within the environment  
- Use of temporary credentials that appear legitimate in logs  

Such activity can blend with normal operations, making detection challenging.

---

## Remediation

To secure IAM roles and prevent misuse:

- Avoid using `"Principal": "*"` in trust policies  
- Restrict access to specific trusted entities only  
- Use condition-based controls (MFA, IP restrictions)  
- Apply least privilege to role permissions  
- Enable and monitor AWS CloudTrail logs  
- Regularly audit IAM roles and trust relationships  

---

## Tools Used

- AWS Management Console  
- IAM (Identity and Access Management)  
- AWS CLI  
- STS (Security Token Service)  
- Git  
- GitHub  
- Markdown documentation  

---

## Next Steps

Day 09 will focus on **privilege escalation techniques**, where attackers abuse IAM permissions to gain administrative-level access and take full control of cloud resources.