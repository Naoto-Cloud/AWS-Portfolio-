# Project Requirements

## Project Background

Inspired by my previous experience in B2B SaaS business development and new market expansion, this project simulates the cloud infrastructure needs of a growing B2B SaaS company.

The company requires a secure, cost-conscious, and maintainable AWS environment to host a web application for business customers.

The initial architecture should be simple enough for a small technical team to operate, while allowing future improvements in scalability and availability.

This is a self-directed infrastructure engineering project, not a production system from my previous employment.

## Business Requirements

- The application is expected to support approximately 100–300 initial users. This is a planning assumption, not a validated capacity target.
- Business customers must be able to access the web application over the internet.
- The database must not be directly accessible from the public internet.
- Initial infrastructure costs should be kept low.
- Short periods of downtime are acceptable during the early stage.
- The infrastructure should support future growth.
- Infrastructure resources must be defined and managed using Terraform.
- The deployment region should be selected based on customer location, latency, cost, and data residency requirements.

## Technical Requirements

- Use Amazon VPC with separate public and private subnets.
- Deploy a Linux-based web server on Amazon EC2.
- Restrict network access using security groups.
- Use private subnets for the relational database.
- Apply IAM least-privilege principles.
- Use AWS Systems Manager Session Manager for administrative access where supported.
- Use Terraform to define the infrastructure.
- Document network traffic flows and routing decisions.
- Validate Terraform configuration before deployment.
- Document operational risks, limitations, and future scaling options.

## Project Scope and Limitations

This project prioritizes foundational cloud engineering skills over production-level high availability.

The initial architecture uses a single EC2 instance and does not include a load balancer or Auto Scaling.

A managed database is included in the target design but may be excluded from initial deployment to control costs.

AWS deployment and live infrastructure testing remain pending until an AWS account is available.
