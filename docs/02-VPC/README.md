# Day 6-7: VPC - Virtual Private Cloud

## Architecture Built


kiran-lab-vpc (10.0.0.0/16)
├── kiran-public-subnet (10.0.1.0/24) → Internet Gateway → internet
└── kiran-private-subnet (10.0.2.0/24) → no internet access


## Components Created
- VPC: kiran-lab-vpc (10.0.0.0/16)
- Public subnet: 10.0.1.0/24 (ap-south-1a)
- Private subnet: 10.0.2.0/24 (ap-south-1b)
- Internet Gateway: kiran-igw
- Route table: 0.0.0.0/0 → kiran-igw (public subnet only)

## Security Groups Configured
- Restricted SSH to single IP only (not 0.0.0.0/0)
- Created kiran-webserver-sg: HTTP/HTTPS public, SSH restricted
- Default outbound: all allowed

## NACL Configuration
- Added deny rule (rule 50) for IP 192.168.1.1/32
- Rule evaluated before allow-all rule 100
- Demonstrates stateless filtering at subnet level

## Security Finding
Putting databases in public subnets = critical misconfiguration.
Private subnet has no IGW route — database servers placed here are unreachable from internet.

## Interview Talking Point
"I built a VPC with public/private subnet separation, configured route tables with IGW for the public tier only, and demonstrated NACL rule ordering by blocking a specific IP before the allow-all rule."
