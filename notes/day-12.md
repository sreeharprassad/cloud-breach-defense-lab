# Day 12 – Automated Detection & Alerting using CloudWatch & GuardDuty

## Objective
Implement automated detection and real-time alerting in AWS using CloudWatch and GuardDuty to identify and respond to suspicious activities without manual log analysis.

---

## Concepts Learned

### Why Automation is Important

Manual log analysis (Day 11) is not scalable.

In real-world environments:
- Thousands of events occur every minute
- Attackers act quickly
- Delayed detection leads to major impact

Automation enables:
- Real-time detection
- Faster response
- Reduced human effort

---

### Amazon CloudWatch

CloudWatch is used for:
- Monitoring logs and metrics
- Creating alerts (alarms)
- Triggering automated actions

Key components:
- Log Groups
- Metric Filters
- Alarms

---

### AWS GuardDuty

GuardDuty is a threat detection service that uses:
- Machine Learning
- Threat intelligence
- Behavior analysis

It detects:
- Credential compromise
- Unusual API activity
- Malicious IP communication
- Reconnaissance attempts

---

## Architecture Overview

CloudTrail → CloudWatch Logs → Metric Filters → Alarms → Notifications  
                         ↘ GuardDuty (Threat Detection)

---

## Practical Work

### 1. Enabled CloudTrail Log Integration with CloudWatch

Steps:
- Go to AWS Console → CloudTrail
- Select your trail
- Edit → Enable CloudWatch Logs
- Create or select a Log Group (e.g., `/aws/cloudtrail/logs`)
- Assign IAM role for CloudTrail logging

Result:
CloudTrail logs are now streamed to CloudWatch.

---

### 2. Created Metric Filters for Suspicious Activities

Navigated to:
CloudWatch → Log Groups → `/aws/cloudtrail/logs`

Created filters for:

#### a) Privilege Escalation Detection

Filter pattern:
{ ($.eventName = "AttachUserPolicy") || ($.eventName = "PutUserPolicy") }

---

#### b) Root Account Usage

Filter pattern:
{ $.userIdentity.type = "Root" }

---

#### c) Unauthorized API Calls

Filter pattern:
{ ($.errorCode = "UnauthorizedOperation") || ($.errorCode = "AccessDenied") }

---

### 3. Created CloudWatch Alarms

For each metric filter:

- Set threshold = 1
- Trigger immediately when activity occurs

Configured alarm actions:
- Send notification via SNS

---

### 4. Setup SNS Notifications

Steps:
- Created SNS Topic (e.g., `security-alerts`)
- Subscribed email for alerts
- Confirmed subscription

Result:
Receive real-time alerts for suspicious activities.

---

### 5. Enabled AWS GuardDuty

Steps:
- Navigate to GuardDuty
- Click "Enable GuardDuty"

No additional configuration required.

---

### 6. Simulated Attack Activity

Performed:
- IAM privilege escalation (AttachUserPolicy)
- Failed API calls
- Role assumption

---

### 7. Observed Detection

#### CloudWatch Alerts:
- Immediate alert triggered on suspicious API calls

#### GuardDuty Findings:
Examples:
- UnauthorizedAccess:IAMUser/ConsoleLogin
- Recon:IAMUser/NetworkPermissions
- PrivilegeEscalation:IAMUser/AnomalousBehavior

---

## Detection Strategy

### CloudWatch (Rule-Based Detection)

Detects:
- Known attack patterns
- Specific API calls
- Policy changes

---

### GuardDuty (Behavior-Based Detection)

Detects:
- Anomalies
- Suspicious patterns
- Known attack signatures

---

## Key Indicators of Compromise (IoCs)

- IAM policy changes
- Root account usage
- Unauthorized API attempts
- Unusual login behavior
- High-frequency API calls

---

## Security Observations

- CloudWatch provides precise, customizable detection
- GuardDuty provides intelligent threat detection
- Combined use significantly improves security visibility

---

## Remediation

- Investigate alerts immediately
- Disable compromised credentials
- Remove unauthorized IAM changes
- Rotate access keys
- Enforce MFA
- Apply least privilege

---

## Tools Used

- AWS CloudTrail
- CloudWatch
- SNS (Simple Notification Service)
- GuardDuty
- IAM
- S3
- Git & GitHub
- Markdown documentation

---

## Impact

Without automation:
- Attacks may go unnoticed
- Delayed incident response

With automation:
- Real-time threat detection
- Immediate alerts
- Faster mitigation

---

## Conclusion

This phase transforms cloud security from passive monitoring to active defense.

By integrating CloudWatch and GuardDuty:
- Suspicious activities are detected instantly
- Alerts enable rapid response
- Security posture is significantly improved

---

## Key Takeaway

Logging shows what happened.  
Monitoring detects it.  
Automation responds to it.

---

## Next Steps

Day 13 will focus on **Data Exfiltration Simulation (S3 & Snapshots)**, demonstrating how attackers steal sensitive data and how to detect it.