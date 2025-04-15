# SQL Server to AWS RDS Migration Lab

This project simulates a real-world migration of a local SQL Server Express database to AWS RDS using AWS services and best practices.

## Key Technologies
- AWS CloudFormation (Infrastructure as Code)
- AWS Client VPN with Easy-RSA Certificates
- Amazon RDS SQL Server Deployment
- AWS Database Migration Service (DMS)
- Local SQL Server Express Setup

## Project Goals
- Deploy isolated private networking for RDS using VPC/Subnets
- Secure VPN access to the RDS instance
- Configure SQL Server Express locally with sample data
- Migrate data to RDS using AWS DMS
- Troubleshoot networking and connectivity issues

## Documentation
Full detailed guide available here:
[docs/migration-guide.md](docs/migration-guide.md)

---

## Note:
Sensitive variables (passwords, endpoints) have been redacted for security.
