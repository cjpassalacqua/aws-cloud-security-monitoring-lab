#AWS Cloud Security Monitoring Lab

This project demonstrates a foundational AWS security monitoring environment designed to simulate real-world cloud security operations.
It includes identity hardening, centralized logging, CLI-based management, and preparation for threat detection and compliance scanning using AWS native tools.

---

#Objectives

* Establish secure AWS administration using IAM, MFA, and least privilege.
* Configure centralized, auditable logging with CloudTrail + S3.
* Prepare AWS-native threat detection tools (GuardDuty, Security Hub).
* Use AWS CLI to automate setup and validate configuration.
* Document architecture and controls to mirror actual cloud security workflows.

---

#Services Used

* IAM – MFA, admin user, secure root governance
* CloudTrail – API activity logging across the account
* S3 – Encrypted bucket for log storage
* AWS CLI – Terminal-based configuration and automation
* GuardDuty
* Security Hub
* IAM Access Analyzer

---

#Architecture Diagram

```
User (IAM Admin)
      │
      ├── AWS Console (MFA)
      │
      └── AWS CLI ───────────────┐
                                 │
                                 ▼
                         AWS CloudTrail
                                 │
                                 ▼
                        S3 Log Storage Bucket
                                 │
        ┌────────────────────────┴────────────────────────┐
        │                                                 │
        ▼                                                 ▼
  GuardDuty (Threat Detection)*                 Security Hub (Compliance)*
                                                     ▼
                                           IAM Access Analyzer*
```
![AWS Cloud Security Architecture](<paste-the-raw-image-URL-here>)

Services to be enabled after AWS account activation completes.

---

#Key Features

* Strong identity security through IAM admin user + enforced MFA.
* Root account locked down and converted to emergency-only use.
* CloudTrail trail created via AWS CLI with a secure bucket policy.
* Logs stored privately with bucket-owner-only permissions.
* CLI verified with `aws sts get-caller-identity`.
* Environment structured to support SOC-style monitoring once GuardDuty/Security Hub are activated.

---

#Commands Used (CLI)

#Configure CLI:

```bash
aws configure
aws sts get-caller-identity
```

#Create S3 bucket:

```bash
aws s3api create-bucket --bucket security-logs-<timestamp>
```

#Add CloudTrail bucket policy:

```bash
aws s3api put-bucket-policy --bucket BUCKETNAME --policy file://policy.json
```

#Create and start CloudTrail:

```bash
aws cloudtrail create-trail --name my-security-trail --s3-bucket-name BUCKETNAME
aws cloudtrail start-logging --name my-security-trail
```

#Confirm CloudTrail:

```bash
aws cloudtrail get-trail-status --name my-security-trail
```

---

#Skills Demonstrated

* AWS Identity & Access Management
* Multi-factor authentication
* CloudTrail configuration & validation
* Secure S3 storage policies
* Command-line cloud automation
* Cloud security architecture documentation
* Threat detection readiness
* Realistic entry-level cloud security workflows

---

#Next Steps (Planned Enhancements)

* Enable and configure GuardDuty
* Enable Security Hub controls (CIS AWS Foundations)
* Enable IAM Access Analyzer
* Add automated remediation checks
* Add CloudWatch metric alarms
* Add attack simulations (IAM brute force, unusual API calls)

---

#About This Project

This is part of my cloud security portfolio as I transition into Cloud Security Support and AWS security roles.
The project mirrors how security teams set up foundational visibility, identity hardening, and threat detection pipelines in a new AWS environment.

