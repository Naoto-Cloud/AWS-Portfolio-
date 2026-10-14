# Project 01 — AWS Network Architecture

## Architecture Diagram

```mermaid
flowchart TB
    Internet((Internet))

    subgraph AWS["AWS Region: Tokyo (ap-northeast-1)"]
        subgraph VPC["VPC: 10.0.0.0/16"]
            IGW["Internet Gateway"]
            RT["Public Route Table"]

            subgraph AZA["Availability Zone A"]
                Public["Public Subnet: 10.0.1.0/24"]
                PrivateA["Private Subnet A: 10.0.2.0/24"]
            end

            subgraph AZB["Availability Zone B"]
                PrivateB["Private Subnet B: 10.0.3.0/24"]
            end

            DBGroup["DB Subnet Group"]
        end
    end

    Internet --- IGW
    RT --> IGW
    Public --> RT
    PrivateA -.-> DBGroup
    PrivateB -.-> DBGroup
```

## Architecture Overview

This project defines a foundational AWS network using Terraform.

- **VPC:** Provides an isolated virtual network.
- **Public Subnet:** Uses a route table with a default route to the Internet Gateway.
- **Private Subnets:** Located in two Availability Zones and have no direct route to the Internet Gateway.
- **DB Subnet Group:** Groups the two private subnets for potential future RDS deployment.

## Current Implementation Status

The Terraform configuration has passed local formatting and validation checks.

The infrastructure has not yet been deployed to AWS.

EC2 instances, RDS databases, and NAT Gateways are not currently included.
