# Day 06 – Cloud Enumeration and Permission Discovery

## Objective
Understand how attackers explore a cloud environment after gaining access and learn how to identify permissions and accessible resources.

---

## Concepts Learned

### Enumeration in Cloud
Enumeration is the process of gathering information about a system after gaining initial access.

In cloud environments, attackers do not exploit systems immediately. Instead, they first try to understand:

- What resources exist
- What permissions they have
- What actions they can perform

---

### Identity-Based Reconnaissance
In cloud environments, everything is controlled by identity (IAM users/roles).

Attackers focus on:
- Who am I?
- What can I access?
- What permissions do I have?

---

### Permission Discovery
Permissions define what actions an identity can perform.

If an attacker gains access to an account, they will check:
- Allowed actions (read, write, admin)
- Accessible services (S3, EC2, IAM)

This helps determine the **blast radius**.

---

### Why Enumeration is Important
Enumeration helps attackers:
- Find sensitive data
- Identify misconfigurations
- Discover privilege escalation paths

Without enumeration, attackers are operating blindly.

---

## Practical Work

### 1. Identified Current Identity
Used AWS console to understand which IAM user is currently active.

Observed:
- Username
- Attached policies
- Access level

---

### 2. Reviewed IAM Permissions
Navigated to IAM dashboard and inspected:

- User permissions
- Attached policies
- Group memberships

Goal:
Understand what actions this identity can perform.

---

### 3. Explored Accessible Services
Checked which AWS services are accessible:

- S3 (storage)
- EC2 (compute)
- IAM (identity management)

Observed what actions were allowed without restriction.

---

### 4. Analyzed Potential Risks
Based on permissions, identified:

- If sensitive data can be accessed
- If new resources can be created
- If privilege escalation is possible

---

## Security Observation

If an attacker gains access to an IAM user, they can map the entire cloud environment using enumeration techniques.

Even without exploiting vulnerabilities, misconfigured permissions can allow attackers to:

- Access sensitive data
- Modify infrastructure
- Escalate privileges

This shows that **identity security is critical in cloud environments**.

---

## Tools Used

- AWS Management Console
- IAM Dashboard
- Git
- GitHub
- Markdown documentation

---

## Next Steps

Day 07 will focus on **credential abuse**, where we simulate how attackers misuse valid credentials to perform unauthorized actions.