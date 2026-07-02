# Day 1-2: IAM - Identity and Access Management

## What I Built
- Created IAM user `kiran-admin` with AdministratorAccess
- Created custom policy `kiran-s3-readonly` with least privilege JSON
- Attached policy to user

## Key Security Findings
- Root account should never be used for daily tasks
- Least privilege: only s3:GetObject and s3:ListBucket on one specific bucket
- IAM roles use temporary credentials — safer than long-term access keys

## Policy Written
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["s3:GetObject", "s3:ListBucket"],
    "Resource": [
      "arn:aws:s3:::kiran-lab-bucket-0516",
      "arn:aws:s3:::kiran-lab-bucket-0516/*"
    ]
  }]
}
```

## Interview Talking Point
"I wrote a least-privilege IAM policy restricting EC2 access to read-only on a single S3 bucket, then verified the role couldn't perform delete operations — access denied confirmed enforcement."
