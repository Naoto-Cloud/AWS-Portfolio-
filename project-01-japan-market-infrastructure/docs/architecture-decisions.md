# Architecture Decisions

## Decision 1: Compute — Amazon EC2

I selected Amazon EC2 to provide a flexible Linux-based compute environment for a growing B2B SaaS company.

A single EC2 instance is sufficient for the initial learning architecture, keeping the system simple and operationally manageable.

EC2 also provides hands-on opportunities to configure Linux services, inspect system logs, manage processes, and troubleshoot HTTP connectivity.

**Trade-off:** A single instance introduces a single point of failure. Future improvements could include an Application Load Balancer and Auto Scaling Group.

## Decision 2: Database — Amazon RDS for MySQL

Amazon RDS for MySQL was selected as the target relational database service because the hypothetical SaaS application requires structured data, such as customer accounts, subscriptions, and application settings.

RDS reduces some database administration overhead compared with running MySQL directly on EC2.

**Trade-off:** A managed database introduces additional cost. Initial deployment may omit RDS while retaining its Terraform configuration as an optional component.

## Decision 3: Networking — Public and Private Subnets

The architecture separates public-facing resources from database resources.

The EC2 web server is initially placed in a public subnet, while the database is assigned to private subnets across two Availability Zones.

A public route table provides a default route to an Internet Gateway. The database is not assigned public internet access.

**Trade-off:** A production architecture could place application servers in private subnets behind a public Application Load Balancer, improving network isolation at additional cost.

## Decision 4: Security — Security Groups and IAM

Security groups restrict inbound traffic to required ports and approved sources.

HTTP traffic is allowed to the web server on TCP port 80 for the initial demonstration. Database access is limited to TCP port 3306 from the web server security group.

An IAM role provides the EC2 instance with permissions required for AWS Systems Manager.

**Trade-off:** HTTP does not encrypt traffic. HTTPS with a valid certificate and a suitable TLS termination point is required before handling sensitive production traffic.

## Decision 5: IP Addressing — VPC and Subnet CIDR

The VPC uses 10.0.0.0/16, with separate /24 subnets for public and private resources.

This layout provides a straightforward network structure for learning subnetting, routing, and network segmentation.

**Trade-off:** The /16 VPC is larger than the initial environment requires. In a real organization, address allocation should account for existing networks and potential connectivity conflicts.

## Decision 6: Infrastructure as Code — Terraform

Terraform was selected to define AWS infrastructure declaratively and maintain the configuration in Git.

This supports repeatability, change review, and future expansion.

The configuration will be checked using terraform fmt and terraform validate before deployment.

**Trade-off:** Terraform introduces state management responsibilities. A future production-oriented version would use a protected remote state backend and controlled deployment workflows.

## Decision 7: AWS Region Selection

The initial target region is eu-central-1 (Frankfurt), based on a hypothetical primary customer base in continental Europe.

This choice illustrates how customer location, latency, data residency, service availability, and cost influence region selection.

**Trade-off:** A single-region architecture cannot tolerate a complete regional outage. Multi-region deployment is outside the scope of the initial project.

## Decision 8: Operations and Troubleshooting

The project will include Linux service management, HTTP connectivity checks, network diagnostics, and log inspection.

These operational tasks are intended to demonstrate not only infrastructure provisioning but also the ability to investigate service failures.

**Trade-off:** The initial environment does not provide full production-grade monitoring, automated recovery, or comprehensive incident management. These capabilities will be explored further in Project 02.
