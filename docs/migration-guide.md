# AWS CloudFormation + Client VPN + SQL Server RDS + DMS Migration Lab

## Overview

This guide documents the full, replicable process of migrating a local SQL Server Express database to AWS RDS using CloudFormation, AWS Client VPN, and AWS DMS.

---

## Phase 1: CloudFormation VPC + RDS Setup

- Deploy VPC with public/private subnets
- NAT Gateway for outbound internet access
- RDS SQL Server instance in private subnet
- Security Groups to allow VPN client access on port 1433

Deploy:
```bash
aws cloudformation deploy   --template-file ./cf-vpc-rds.yml   --stack-name vpc-rds-lab   --capabilities CAPABILITY_NAMED_IAM
```

---

## Phase 2: AWS Client VPN Setup

- Generate TLS certificates using Easy-RSA
- Import server and client certs to AWS ACM
- Create AWS Client VPN Endpoint
- Associate with private subnets
- Authorize access to RDS subnet CIDR
- Enable split-tunnel for better client performance

---

## Phase 3: Local SQL Server Express Setup

- Install SQL Server Express locally
- Enable SQL Authentication
- Create test user (SQL Auth)
- Restore AdventureWorks sample database
- Configure firewall to allow TCP 1433 inbound

---

## Phase 4: AWS Database Migration Service (DMS)

- Create DMS replication instance in private subnet
- Define source endpoint (local SQL Server over VPN)
- Define target endpoint (RDS SQL Server)
- Configure migration task
- Validate data replication into RDS

---

## Key Learnings & Troubleshooting Notes

- AWS RDS SQL Server Express requires DBName to be blank during creation.
- VPN configuration requires enabling split-tunnel to prevent client internet dropouts.
- TCP 1433 firewall and SQL Server settings must allow remote SQL Authentication.
- Use `nc -vz` or `Test-NetConnection` to verify port 1433 connectivity before DMS.

---

## Resources Used
- AWS CloudFormation
- AWS ACM
- AWS Client VPN
- AWS DMS
- SQL Server Express
- AdventureWorks Sample Database

---

## Next Steps
- Automate DMS migration with CloudFormation or Terraform.
- Explore multi-region or cross-account migration scenarios.
- Implement logging and monitoring enhancements.