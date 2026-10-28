
# B2B SaaS Cloud Infrastructure — AWS & Terraform

## Project Overview

Inspired by my previous experience in B2B SaaS business development and market expansion, this independent project explores how to design and implement cloud infrastructure for a growing SaaS company.

The objective is to build a secure, cost-conscious, and maintainable AWS infrastructure using Terraform, with a focus on networking, access control, Linux operations, and infrastructure troubleshooting.

Rather than deploying resources without a clear purpose, this project begins with business requirements and translates them into technical architecture and infrastructure-as-code configurations.

**Project status:** The core AWS networking, IAM resources, security groups, and EC2 instance have been provisioned using Terraform. Terraform configuration validation passes.

AWS Systems Manager Session Manager connectivity was successfully verified without exposing SSH port 22. Nginx was manually installed and started on the EC2 instance, and an HTTP 200 OK response was confirmed locally using `curl -I http://localhost`.

The EC2 instance is currently stopped to control costs. The latest Terraform plan proposes replacing the instance due to a public IP assignment discrepancy observed after stopping it. No replacement has been applied, and this discrepancy remains under review.

The RDS configuration is retained separately in `rds.tf.example` and has not been deployed. External HTTP connectivity, database integration, and workload testing have not yet been completed.


## Business Requirements

The hypothetical business scenario involves a B2B SaaS company expanding into the European market.

The infrastructure should:

- Support an initial customer base of approximately 100–300 users.
- Provide a publicly accessible web application.
- Isolate the database from direct internet access.
- Balance cost efficiency, security, and maintainability.
- Support future scalability and operational improvements.

The estimated user count is a planning assumption, not a validated capacity benchmark.

## Architecture

**AWS Region:** Europe (Frankfurt) — `eu-central-1`

### Networking

- Custom VPC (`10.0.0.0/16`)
- One public subnet (`10.0.1.0/24`) for the web server
- Two private subnets (`10.0.2.0/24` and `10.0.3.0/24`) across separate Availability Zones
- Internet Gateway
- Public route table with an internet route
- Public subnet association

The private subnets are intended for database resources and do not have direct internet access through the public route table.

### Compute

- Amazon EC2 (`t3.micro`)
- Amazon Linux 2023 AMI selection
- IAM instance profile for AWS Systems Manager
- IMDSv2 required
- Public subnet placement for the initial web server

The initial architecture uses a single EC2 instance to minimize complexity and cost.

This design is not highly available and would require additional components for production-grade resilience.

### Database

- Amazon RDS for MySQL
- Private DB subnet group
- Single-AZ deployment configuration
- Encrypted storage
- AWS-managed master password
- Public accessibility disabled

The RDS instance configuration is retained in `rds.tf.example` as an optional example and is excluded from the active Terraform deployment to avoid unnecessary costs.

The DB subnet group and database security group have been provisioned, but no RDS database instance has been deployed or tested.

### Security

- Separate security groups for web and database resources
- HTTP inbound access on port 80 for the web server
- MySQL access on port 3306 restricted to the web security group
- No direct public database access
- IAM role with Systems Manager permissions
- IMDSv2 enforced on EC2

HTTP access is included for initial connectivity testing. HTTPS and further security hardening are planned improvements.

## Design Decisions

The initial architecture prioritizes simplicity, cost control, and practical learning over high availability.

**EC2:** Selected to provide direct experience with Linux server administration, networking, and infrastructure troubleshooting.

**RDS:** Selected to reduce database administration overhead while providing a managed relational database service.

**Public/private subnet separation:** Designed to expose only the web tier while keeping database resources isolated from direct internet access.

**Terraform:** Selected to define infrastructure declaratively, support repeatable deployments, and maintain infrastructure configuration under version control.

**Frankfurt Region:** Selected as a hypothetical deployment location for a SaaS company serving European customers.

Actual region selection would depend on customer location, latency, regulatory requirements, service availability, and costs.

See [Architecture Decisions](docs/architecture-decisions.md), [Architecture](docs/architecture.md), and [Business Requirements](docs/requirements.md).

## Implementation and Validation

### Completed

- Defined the AWS infrastructure using Terraform.
- Applied Terraform formatting.
- Passed Terraform static configuration validation.
- Provisioned initial AWS infrastructure resources.
- Launched an EC2 instance in the Frankfurt Region.
- Configured an EC2 IAM instance profile with AWS Systems Manager permissions.
- Configured Git exclusions for Terraform state files, local provider files, and installation artifacts.

### Not Yet Completed

- External HTTP connectivity testing from the internet.
- RDS provisioning and database connectivity testing.
- Database network isolation testing with a running database.
- Deployment and verification of automated Nginx installation using EC2 User Data.
- CloudWatch monitoring and incident response exercises.
- Infrastructure performance and capacity testing.
- HTTPS configuration, load balancing, and Auto Scaling.

### Terraform Troubleshooting

During infrastructure development, Terraform proposed replacing the EC2 instance because of an updated Amazon Linux 2023 AMI and differences in public IP assignment.

I pinned the AMI to prevent unexpected changes caused by automatically selecting the latest image.

After stopping the EC2 instance through the AWS Console to control costs, Terraform detected a change in its public IP assignment state.

The latest `terraform plan` proposes replacing the EC2 instance because `associate_public_ip_address` is reported as `false` in the refreshed state while the Terraform configuration specifies `true`.

I reviewed the plan and deliberately avoided applying the replacement to preserve the existing instance and its manually configured Nginx installation.

This discrepancy remains unresolved and will be reviewed before any future Terraform apply.

### Validation Limitations

Terraform configuration validation passes, but this does not guarantee successful deployment or application functionality.

The EC2 instance was successfully provisioned, and AWS Systems Manager Session Manager connectivity was verified without exposing SSH port 22.

Nginx was manually installed and started on Amazon Linux 2023. A local HTTP response of `200 OK` was confirmed using `curl -I http://localhost`.

External HTTP connectivity has not yet been verified, and the web server has not been tested after restarting the stopped instance.

No RDS database instance has been deployed, and the infrastructure has not been tested against the assumed workload of 100–300 users.

The EC2 instance is currently stopped to limit ongoing costs.

## Cost Considerations

Cost control is a key design requirement.

The initial deployment uses a small EC2 instance (`t3.micro`) to keep costs manageable. The instance is stopped when not in use, although EBS storage and other provisioned resources may still incur charges.

Amazon RDS is excluded from the active deployment. Its configuration is retained in `rds.tf.example` for future testing, subject to a separate cost review.

However, actual AWS charges depend on resource usage, storage, networking, pricing, and account-specific credits or offers.

**Important:** The active Terraform configuration does not provision an RDS instance. However, EC2, EBS storage, public IPv4 addresses, and other AWS resources may incur charges depending on usage and configuration.

Running `terraform apply` may create billable infrastructure. Deployment should only proceed after reviewing the execution plan and estimated costs.

## Next Steps

1. Investigate and resolve the EC2 replacement proposed by Terraform before applying further infrastructure changes.
2. Test the existing EC2 User Data script on a newly provisioned instance after reviewing the replacement plan and costs.
3. Verify external HTTP connectivity and troubleshoot networking or security group issues if necessary.
4. Evaluate RDS deployment costs before provisioning a database.
5. Test database connectivity and network isolation.
6. Add Amazon CloudWatch monitoring and incident response exercises.
7. Implement HTTPS and evaluate additional security hardening.
8. Explore load balancing and Auto Scaling when justified by availability and workload requirements.


## Technologies

- **Cloud:** Amazon Web Services (AWS)
- **Infrastructure as Code:** Terraform
- **Operating System:** Amazon Linux 2023
- **Networking:** VPC, Subnets, Route Tables, Internet Gateway, Security Groups
- **Compute:** Amazon EC2
- **Database:** Amazon RDS for MySQL (configuration only)
- **Identity and Access Management:** AWS IAM
- **Operations:** AWS Systems Manager
- **Version Control:** Git

## Author

An independent cloud engineering portfolio project combining international B2B SaaS business experience with AWS infrastructure design, Terraform configuration, Linux operations, and cloud troubleshooting.

The project demonstrates my transition from business-facing technology roles toward hands-on cloud infrastructure engineering.


## Implementation and Verification

The following components have been successfully deployed and tested:

- AWS VPC with public and private subnets
- EC2 instance running Amazon Linux 2023
- IAM role configured for AWS Systems Manager
- Successful EC2 access via SSM Session Manager without opening SSH port 22
- Nginx installed and started on EC2
- HTTP 200 OK response verified locally using `curl -I http://localhost`

### Current Limitations

- External HTTP access has not yet been verified.
- RDS has not been deployed to avoid unnecessary costs.
- An EC2 User Data script (`user-data.sh`) has been added to automate Nginx installation and startup.
- The User Data configuration passes `terraform validate` but has not yet been deployed or tested on a newly launched EC2 instance.
- The existing EC2 instance remains stopped, and the proposed Terraform replacement has not been applied.
- Load balancing and auto scaling are planned future improvements.
