# AWS Cloud Infrastructure Portfolio

Hands-on cloud infrastructure projects using AWS, Terraform, and Infrastructure as Code (IaC).

## About This Repository

I'm transitioning into cloud infrastructure engineering, building practical projects to apply my knowledge of AWS architecture, networking, security, and infrastructure automation.

I hold the AWS Certified Solutions Architect – Associate and HashiCorp Terraform Associate certifications.

My focus is on understanding not only how infrastructure works, but also why particular architectural decisions make sense in terms of security, reliability, operational efficiency, and cost.

## Projects

### Project 01 — Japan Market Infrastructure

**Technologies:** AWS, Terraform, VPC Networking

A Terraform-based AWS network infrastructure project designed for a hypothetical Japan-based business environment.

The current configuration includes:

- A custom VPC in the Tokyo AWS Region (`ap-northeast-1`)
- One public subnet and two private subnets
- Private subnets across two Availability Zones
- An Internet Gateway and public route table
- A DB subnet group for potential future database deployment

**Current status:**

- Terraform configuration written
- `terraform fmt` and `terraform validate` completed
- Source code committed and pushed to GitHub
- AWS deployment and live verification pending

[View Project 01](project-01-japan-market-infrastructure/)

## Technical Focus

- AWS networking and infrastructure design
- Infrastructure as Code with Terraform
- Security and network isolation
- High availability and architectural trade-offs
- Git and version control
- Technical documentation and design decisions

## My Approach

I believe good infrastructure design starts with understanding business requirements.

When evaluating technical solutions, I consider:

- **Security:** How can access and exposure be minimized?
- **Reliability:** How should the infrastructure handle failures?
- **Cost:** What is appropriate for the project's scale and budget?
- **Operations:** How can infrastructure be maintained and reproduced efficiently?

My goal is to develop the practical skills needed to contribute to cloud infrastructure and engineering teams.

## Certifications

- AWS Certified Solutions Architect – Associate
- AWS Certified Cloud Practitioner
- HashiCorp Certified: Terraform Associate

## Next Steps

- Document the network architecture with a diagram
- Review security and networking design decisions
- Deploy and verify the infrastructure in AWS when account access is available
- Expand the portfolio with additional infrastructure projects
