# Day 11 – Detection and Monitoring using CloudTrail & Logging

## Objective
Understand how to detect malicious activities in AWS by analyzing logs and monitoring events using AWS CloudTrail and related logging mechanisms.

---

## Concepts Learned

### Cloud Monitoring in AWS
Monitoring is essential for identifying suspicious activities, tracking user actions, and responding to security incidents in cloud environments.

---

### AWS CloudTrail
AWS CloudTrail records all API activity within an AWS account.

It captures:

- User actions (IAM, EC2, S3, etc.)
- API calls via CLI, SDK, or Console
- Identity details and timestamps

---

### Why Logging is Important

- Detect unauthorized access  
- Track attacker behavior  
- Support forensic investigations  
- Enable real-time alerting  

---

### Real-World Scenario

In real cloud attacks:

- Attackers use valid credentials  
- Perform privilege escalation  
- Exfiltrate data  

All these actions generate logs that can be detected if properly monitored.

---

## Practical Work

### 1. Enabled CloudTrail Logging

Verified CloudTrail was enabled for the AWS account.

Configured:

- Multi-region trail  
- Management events logging  

---

### 2. Generated Test Activity

Performed actions from previous days to simulate attacker behavior:

- IAM policy changes  
- Role assumption  
- S3 data access  

This ensures logs contain realistic attack data.

---

### 3. Viewed CloudTrail Event History

Navigated to:

AWS Console → CloudTrail → Event History

Filtered events such as:

- `AttachUserPolicy`  
- `PutUserPolicy`  
- `AssumeRole`  
- `CreateUser`  
- `GetObject`  

---

### 4. Analyzed Key Event Fields

Observed important log details:

- **Event Name** – Action performed  
- **User Identity** – Who performed the action  
- **Source IP Address** – Origin of request  
- **Event Time** – Timestamp  
- **Resources** – Target services  

---

### 5. Identified Suspicious Patterns

Detected behaviors such as:

- Sudden privilege escalation  
- Unusual IAM activity  
- High-frequency S3 access  
- Role assumptions from unexpected sources  

---

### 6. Log Storage (S3 Integration)

Configured CloudTrail to store logs in an S3 bucket for long-term retention and analysis.

---

## Identity Observation

Observed that:

- Even when attackers use valid credentials, their actions are logged  
- Temporary role assumptions appear with session details  
- Identity tracking is possible through CloudTrail logs  

---

## Security Observation

CloudTrail provides deep visibility into account activity, but:

- It does not automatically detect threats  
- Manual analysis or alerting systems are required  
- Without monitoring, attacks may go unnoticed  

Proper log analysis is critical for effective cloud security.

---

## Detection Strategy

Key indicators of compromise (IoCs):

- IAM policy modifications  
- Creation of new users or access keys  
- Role assumptions from unknown IPs  
- Large-scale S3 data access  
- Repeated failed or unusual API calls  

---

## Remediation

To improve detection and monitoring:

- Enable CloudTrail in all regions  
- Store logs securely in S3 with restricted access  
- Integrate with CloudWatch for alerts  
- Use AWS GuardDuty for automated threat detection  
- Regularly review logs and audit activity  
- Implement centralized logging strategy  

---

## Tools Used

- AWS Management Console  
- CloudTrail  
- S3 (for log storage)  
- IAM  
- Git  
- GitHub  
- Markdown documentation  

---

## Impact

Without proper monitoring:

- Attacks remain undetected  
- Data breaches go unnoticed  
- Incident response is delayed  

With effective logging:

- Faster detection  
- Better forensic analysis  
- Improved security posture  

---

## Conclusion

This phase demonstrates the importance of visibility in cloud security.

Even advanced attacks generate logs, and proper monitoring enables detection and response.

---

## Next Steps

Day 12 will focus on **automated detection and alerting using CloudWatch and GuardDuty**, enabling real-time response to suspicious activities.