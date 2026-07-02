# AWS Cloud Security Lab

Hands-on AWS security engineering lab documenting 16+ days of real cloud security work.

## What This Covers
- IAM users, roles, and least-privilege policies
- EC2 deployment and SSH access
- VPC architecture with public/private subnets
- CloudTrail audit logging and threat hunting
- CloudWatch alarms for security events
- AWS Config compliance rules
- VPC Flow Log analysis
- S3 security hardening
- Real incident investigation (IP: 35.203.211.153)

## Skills Demonstrated
- Cloud security monitoring
- Threat hunting using CloudTrail Logs Insights
- Network traffic analysis via VPC Flow Logs
- IAM policy writing and least privilege enforcement
- Security Group and NACL configuration

## Lab Environment
- Platform: AWS Free Tier
- Region: ap-south-1 (Mumbai)
- Account: Personal lab account

- ## Proof - Alarm Fired
![CloudWatch Alarm Email](alarm-fired.png)

Alarm triggered June 20, 2026 at 05:29 UTC. Root account used 16 times in a 5-minute window. Email received within 5 minutes of activity.
