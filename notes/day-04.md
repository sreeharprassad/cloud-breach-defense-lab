# Day 04 – Cloud Storage Security and S3 Misconfiguration

## Objective
Understand how cloud storage works in AWS and learn how misconfigured storage services can lead to data exposure.

---

## Concepts Learned

### Cloud Storage
Cloud storage allows organizations to store files and data on remote servers managed by a cloud provider instead of storing them locally. These storage systems are scalable and accessible through the internet.

### Amazon S3
Amazon Simple Storage Service (S3) is an object storage service used to store files such as images, logs, backups, and application data.

Data in S3 is stored inside containers called **buckets**.

### Buckets
A bucket is a logical container used to store objects (files) in S3. Each bucket has its own permissions and access configurations.

### Public Access
S3 buckets can be configured to allow public access. If public access is enabled without proper control, files stored inside the bucket may become accessible to anyone on the internet.

### Data Exposure Risk
One of the most common cloud security incidents occurs when S3 buckets are accidentally exposed to the public internet due to misconfiguration.

Attackers often scan cloud environments looking for publicly accessible storage.

---

## Practical Work

### Accessed the S3 Service
Logged into the AWS Management Console and navigated to the S3 service.

### Created a Bucket
Created a new S3 bucket for testing purposes.

Configuration used:
- Bucket Name: `cloud-lab-storage-demo`
- Region: Default region
- Default configuration settings

### Uploaded a Test File
Uploaded a sample file to understand how objects are stored and managed inside the bucket.

### Explored Permission Settings
Reviewed different access control settings including:
- Block Public Access
- Bucket Policies
- Access Control Lists (ACL)

These settings determine who can access files stored in the bucket.

---

## Security Observation

Improperly configured S3 buckets can expose sensitive data such as:
- Backup files
- Application logs
- Internal documents
- Databases

If public access is allowed, attackers may be able to download files directly from the internet.

---

## Remediation

To prevent data exposure:

- Enable **Block Public Access** for buckets
- Avoid allowing public read permissions
- Use **IAM roles and policies** to control access
- Regularly audit bucket permissions
- Monitor access using logging services

Following these practices helps reduce the risk of accidental data leaks.

---

## Tools Used

- AWS Management Console
- Amazon S3
- Git
- GitHub
- Markdown documentation

---

## Next Steps

Day 05 will focus on **cloud credentials and API keys**, and how leaked credentials can allow attackers to gain unauthorized access to cloud environments.