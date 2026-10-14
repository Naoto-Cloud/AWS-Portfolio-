# B2B SaaS Cloud Infrastructure — AWS & Terraform

## Project Overview

Inspired by my previous experience in B2B SaaS business development and market expansion, this independent project explores how to design cloud infrastructure for a growing SaaS company.

The objective is to create a secure, cost-conscious, and maintainable AWS infrastructure using Terraform, with a focus on networking, access control, and operational readiness.

**Project status:** Terraform configuration completed and validated locally. AWS deployment and runtime testing are pending.

## Business Requirements

- Support an initial customer base of approximately 100–300 users.
- Provide a publicly accessible web application.
- Isolate the database from direct internet access.
- Balance cost efficiency, security, and maintainability.
- Support future scalability and operational improvements.

## Architecture

**AWS Region:** Europe (Frankfurt) — `eu-central-1`

**Networking**
- Custom VPC (`10.0.0.0/16`)
- One public subnet for the web server
- Two private subnets across separate Availability Zones
- Internet Gateway, public route table, and subnet association

**Compute**
- Amazon EC2 with Amazon Linux 2023 AMI selection
- IAM instance profile for AWS Systems Manager
- IMDSv2 required

**Database**
- Amazon RDS for MySQL
- Private DB subnet group
- Single-AZ configuration
- Encrypted storage and AWS-managed master password

**Security**
- Separate security groups for web and database
- HTTP inbound access to the web security group
- MySQL access restricted to the web security group
- No public database access
- IAM role with Systems Manager permissions

## Design Decisions

The initial architecture prioritizes simplicity and cost control over high availability.

EC2 provides direct control over the Linux server environment. RDS reduces database administration overhead. Public/private subnet separation limits direct exposure of database resources.

Frankfurt is selected as a hypothetical deployment region for a SaaS company serving European customers. Actual region selection would depend on customer location, latency, regulatory requirements, and costs.

See [Architecture Decisions](docs/architecture-decisions.md) and [Business Requirements](docs/requirements.md).

## Validation and Limitations

- Terraform formatting: completed
- Terraform static validation: passed
- AWS deployment: not yet performed
- Application installation and runtime testing: not yet performed
- Infrastructure cost and performance: not yet verified

The infrastructure has not been deployed because AWS account access remains unresolved.

Terraform validation checks configuration consistency but does not confirm that AWS resources can be provisioned successfully.

The current configuration includes EC2 and RDS resources. Applying the full configuration would provision chargeable resources; cost review is required before deployment.

## Next Steps

- Resolve AWS account access and review deployment costs.
- Install and configure a Linux web server.
- Test HTTP connectivity and database network isolation.
- Add monitoring and troubleshooting scenarios.
- Implement HTTPS and evaluate further production hardening.
- Introduce load balancing and Auto Scaling when justified.

## Technologies

AWS · Terraform · Linux · VPC · EC2 · RDS · IAM · Security Groups · Infrastructure as Code

## Author

Independent cloud engineering portfolio project combining B2B SaaS business requirements with infrastructure design and Terraform-based configuration.
