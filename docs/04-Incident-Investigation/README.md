# Day 14: Real Incident Investigation

## Scenario
Alert received: suspicious IP 35.203.211.153 seen in environment.
Task: Investigate using VPC Flow Logs and CloudTrail.

## Investigation Steps

### Step 1: VPC Flow Log Analysis
Searched kiran-vpc-flow-logs for IP 35.203.211.153

**Finding:**

35.203.211.153 → 172.31.15.241 port 12580 TCP 1 packet REJECT

- Single probe packet to random port 12580
- Action: REJECTED by Security Group
- No repeated attempts

### Step 2: CloudTrail Correlation
Searched CloudTrail Event History by Source IP: 35.203.211.153

**Finding:** 0 API calls from this IP
- No authentication attempts
- No AWS console access
- No service calls

## Verdict
**Internet scanner. No breach.**
Security Group blocked the connection before it reached the instance.
No CloudTrail activity confirms the IP never authenticated to AWS.

## Recommended Action
No immediate action required. IP blocked at network layer.
Optional: Add IP to NACL deny list if repeated scanning observed.

## What This Demonstrates
- Correlation across two data sources (network + API logs)
- Differentiating a scan from an actual compromise
- Understanding that REJECT in flow logs = Security Group working correctly

- 
