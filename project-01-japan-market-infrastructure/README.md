# Japan Market Infrastructure — AWS & Terraform

## Project Overview

This project models the infrastructure requirements of a Taiwanese B2B SaaS company expanding into the Japanese market.

The objective is to design a secure, cost-conscious AWS environment for an initial customer base of approximately 100–300 users.

Infrastructure is defined using Terraform to support consistency, repeatability, and future expansion.

## Business Requirements

- Support a small-scale SaaS application entering the Japanese market.
- Make the web application publicly accessible.
- Keep the database isolated from direct internet access.
- Minimize initial infrastructure costs.
- Allow for future scalability as the business grows.

## Architecture

**AWS Region:** Asia Pacific (Tokyo) — ap-northeast-1

**Networking**
- Custom VPC (10.0.0.0/16)
- One public subnet
- Two private subnets across separate Availability Zones
- Internet Gateway and public route table

**Compute**
- Amazon EC2 running Amazon Linux 2023
- IAM role for AWS Systems Manager

**Database**
- Amazon RDS for MySQL
- Private database subnets
- Single-AZ deployment configuration
- Storage encryption enabled

**Security**
- Separate security groups for web and database resources
- Database inbound access restricted to the web security group
- No public database endpoint
- IMDSv2 required for EC2
- RDS master password managed by AWS Secrets Manager

## Architecture Decisions
[View Architecture Diagram](docs/diagrams/architecture.md)

**Why EC2?**

EC2 provides a straightforward starting point for hosting a small SaaS application while maintaining control over the server environment.

**Why RDS?**

RDS reduces the operational overhead associated with database installation, maintenance, and backups.

**Why public and private subnets?**

Separating publicly accessible compute resources from private database resources reduces unnecessary network exposure.

**Why Single-AZ?**

The initial project prioritizes cost efficiency over high availability. A production system with stricter uptime requirements would benefit from additional redundancy.

## Security Considerations

This configuration demonstrates network segmentation, restricted database access, IAM-based instance management, and encrypted database storage.

Further production hardening would include HTTPS, tighter outbound rules, secure application-level credential retrieval, monitoring, and enhanced backup and recovery policies.

## Validation Status

- Terraform formatting: completed
- Terraform static validation: passed
- AWS deployment: pending
- Live infrastructure testing: not completed

The infrastructure has not been deployed because AWS account registration remains unresolved.

Terraform validation confirms configuration consistency but does not verify deployment success or runtime functionality.

## Future Improvements

- Deploy and test the infrastructure in AWS.
- Configure HTTPS and TLS termination.
- Add monitoring with Amazon CloudWatch.
- Introduce load balancing and Auto Scaling when traffic justifies the additional cost.
- Add CI checks for Terraform formatting, validation, and security scanning.
- Evaluate Multi-AZ database deployment for stronger availability requirements.

## Technologies

AWS | Terraform | Linux | Infrastructure as Code | VPC | EC2 | RDS | IAM | Security Groups

## Author

Cloud infrastructure portfolio project demonstrating AWS architecture design, Terraform configuration, and security-focused infrastructure planning.
