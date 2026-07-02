# Day 4 & 12: CloudTrail - Audit Logging & Threat Hunting

## What I Built
- Enabled CloudTrail trail: kiran-security-trail
- Connected to CloudWatch Logs for real-time querying
- Created metric filter for root account usage
- Created CloudWatch alarm that fires when root is used
- Confirmed alarm via email notification

## Threat Hunting Queries Written

### Query 1: Detect Root Account Usage

fields @timestamp, eventName, userIdentity.type, sourceIPAddress
| filter userIdentity.type = "Root"
| sort @timestamp desc
| limit 20

### Query 2: Detect S3 Policy Changes
fields @timestamp, eventName, userIdentity.type, sourceIPAddress
| filter eventSource = "s3.amazonaws.com"
| filter eventName in ["DeleteBucket", "PutBucketPolicy", "DeleteBucketPolicy", "PutBucketAcl"]
| sort @timestamp desc
| limit 20

### Query 3: Detect Security Group Changes
fields @timestamp, eventName, userIdentity.type, sourceIPAddress
| filter eventSource = "ec2.amazonaws.com"
| filter eventName in ["AuthorizeSecurityGroupIngress", "RevokeSecurityGroupIngress", "CreateSecurityGroup"]
| sort @timestamp desc
| limit 20

### Query 4: Detect IAM Changes
fields @timestamp, eventName, userIdentity.type, sourceIPAddress
| filter eventSource = "iam.amazonaws.com"
| filter eventName in ["CreateUser", "DeleteUser", "AttachUserPolicy", "UpdateLoginProfile", "CreateAccessKey"]
| sort @timestamp desc
| limit 20

## Real Findings from My Account
- Root used 13 times in one session — alarm fired correctly
- PutBucketPolicy by Root detected (S3 logging setup)
- UpdateLoginProfile by Root twice in 7 minutes — suspicious pattern
- Security group created by Root instead of IAM user

## Interview Talking Point
"I built a CloudTrail detection pipeline — metric filter → CloudWatch alarm → SNS email. When root was used, I received an alert within 5 minutes. I then hunted through logs using Logs Insights and found IAM and S3 changes made by root that should have been done by a scoped IAM user."
