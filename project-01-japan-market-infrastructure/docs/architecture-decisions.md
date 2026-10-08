# Architecture Decisions

## Decision 1: Compute — Amazon EC2

I chose Amazon EC2 because the company is still small and a simple, cost-conscious infrastructure was one of the main requirements for the initial Japan launch.

A single EC2 instance keeps the initial architecture simple, while allowing the infrastructure to evolve later by adding components such as a load balancer and Auto Scaling as traffic grows.

## Decision 2: Database — Amazon RDS

I chose Amazon RDS because the application needs to store structured relational data such as customer accounts, company information, subscriptions, and application settings.

Amazon S3 is object storage and is better suited for files such as documents, images, backups, and logs, rather than the relational application data required for this project.

## Decision 3: Network Design — Public and Private Subnets

I separated the infrastructure into public and private subnets to improve security and control access to the database.

The web application needs to be accessible from the internet, while the database should not be directly exposed to the public internet. Therefore, the EC2 instance will initially run in a public subnet, while Amazon RDS will run in a private subnet.

## Decision 4: Security Groups

Access to Amazon RDS will be restricted to only the necessary database traffic from the application EC2 instance.

This reduces unnecessary network access to the database and improves the overall security of the infrastructure.

## Decision 5: VPC CIDR Design

I chose a /16 CIDR block for the VPC to leave sufficient address space for future expansion as the Japan business grows.

I chose /24 CIDR blocks for the subnets because they provide sufficient IP address capacity for the initial infrastructure while leaving room within the VPC for additional subnets in the future.

