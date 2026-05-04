# Day 13 – Data Exfiltration Simulation (S3 & EBS Snapshot Abuse)

## Objective
Simulate real-world data exfiltration techniques in AWS by abusing S3 access and EBS snapshots, and understand how such activities can be detected and mitigated.

---

## Concepts Learned

### What is Data Exfiltration?

Data exfiltration is the unauthorized transfer of sensitive data from a system to an external location controlled by an attacker.

In AWS environments, attackers commonly target:
- Amazon S3 buckets (documents, backups, logs)
- EBS snapshots (full disk data)
- Application storage containing credentials or configs

---

### Why Data Exfiltration Matters

The ultimate goal of most cloud attacks is **data theft**, not just access.

Potential impact:
- Exposure of sensitive data  
- Financial and reputational damage  
- Compliance violations  
- Loss of intellectual property  

---

## Attack Scenario

An attacker has:
- Valid IAM credentials  
- Elevated privileges (from previous privilege escalation)

Objectives:
1. Discover sensitive storage resources  
2. Extract valuable data  
3. Minimize detection during exfiltration  

---

## Practical Implementation

### 1. S3 Bucket Enumeration

List all S3 buckets:

```bash
aws s3 ls
```

---

### 2. Identify Target Bucket

Inspect contents of a bucket:

```bash
aws s3 ls s3://<bucket-name>
```
Look for:

- Backup files
- Logs
- Configuration files
- Sensitive documents

---

### 3. Download Specific Files

```bash
aws s3 cp s3://<bucket-name>/sensitive-file.txt .
```

---

### 4. Bulk Data Exfiltration

Download entire bucket:

```bash
aws s3 sync s3://<bucket-name> ./exfiltrated-data
```
**Observation**
This simulates large-scale data theft.

Indicators:

- High number of GetObject API calls
- Rapid increase in outbound data

---

### 5. Stealth Techniques (Attacker Perspective)

Attackers may:

Download data slowly over time
Target only high-value files
Use legitimate APIs to avoid suspicion

---

## Advanced Attack – EBS Snapshot Abuse

### 6. Enumerate Snapshots

```bash
aws ec2 describe-snapshots --owner-ids self
```
Snapshots may contain:

- OS data
- Application files
- Credentials
- Database backups

---

### 7. Create Volume from Snapshot 

```bash
aws ec2 create-volume \
--snapshot-id <snapshot-id> \
--availability-zone <zone>
```

---

### 8. Attach Volume to EC2

```bash 
aws ec2 attach-volume \
--volume-id <volume-id> \
--instance-id <instance-id> \
--device /dev/sdf
```

---

### 9. Extract Data from Volume

Steps:

- SSH into EC2 instance
- Mount the volume
- Browse file system
- Copy sensitive data

This simulates full disk-level data extraction.

---

## Detection Techniques

### Using CloudTrail

Monitor API calls such as:

- `GetObject`  
- `ListBuckets`  
- `DescribeSnapshots`  
- `CreateVolume`  
- `AttachVolume`  

---

### Using CloudWatch

Look for anomalies:

- Sudden spike in S3 access  
- High-frequency API calls  
- Unusual access times  
- Access from unknown IP addresses  

---

### Using GuardDuty

GuardDuty may detect:

- Anomalous data access behavior  
- Suspicious IAM activity  
- Unusual API usage patterns  

---

## Indicators of Compromise (IoCs)

- Large number of S3 `GetObject` requests  
- Bulk downloads in short duration  
- Access from unexpected locations  
- Snapshot access and volume creation  
- Unusual API usage patterns  

---

## Security Observations

- S3 is a primary target for data theft  
- EBS snapshots expose complete system data  
- Legitimate credentials make detection harder  
- Monitoring is critical for identifying exfiltration  

---

## Remediation Strategies

- Enable S3 access logging  
- Restrict bucket permissions using IAM  
- Apply least privilege principle  
- Encrypt sensitive data  
- Monitor activity using CloudTrail  
- Configure CloudWatch alerts  
- Enable GuardDuty for threat detection  
- Restrict snapshot access and sharing  

---

## Tools Used

- AWS CLI  
- Amazon S3  
- EC2 (EBS Snapshots)  
- CloudTrail  
- CloudWatch  
- GuardDuty  
- Git & GitHub  
- Markdown documentation  

---

## Impact

### Without Detection

- Data theft remains unnoticed  
- Long-term security breach  
- Exposure of sensitive information  

---

### With Detection

- Early identification of suspicious activity  
- Faster incident response  
- Reduced damage  

---

## Conclusion

This phase demonstrates how attackers move from access to impact by exfiltrating sensitive data from cloud environments.

Even with strong access control, lack of monitoring can result in undetected data breaches.

---

## Key Takeaway

Access is just the beginning.  
Data exfiltration is the real objective.  

---

## Next Steps

Day 14 will focus on:

**Defense Hardening & Prevention**

- Strengthening IAM policies  
- Securing S3 buckets  
- Implementing preventive controls  
- Improving overall cloud security posture  