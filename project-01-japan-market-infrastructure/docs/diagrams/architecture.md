
# Japan Market Infrastructure — Architecture

```mermaid
flowchart TB
    Internet["Internet"] --> IGW["Internet Gateway"]

    subgraph VPC["AWS VPC - 10.0.0.0/16"]
        IGW --> Public["Public Subnet - 10.0.1.0/24"]

        Public --> EC2["EC2 Web Server"]

        EC2 --> RDS["RDS MySQL - Single AZ"]

        subgraph Private["Private Database Subnets"]
            RDS
            SubnetB["Private Subnet B - 10.0.3.0/24"]
        end
    end
```

## Architecture Notes

- Region: ap-northeast-1 (Tokyo)
- EC2: Public subnet
- RDS: Private database subnets
- Database access: Restricted to the web security group
- Deployment status: Terraform validated, AWS deployment pending
