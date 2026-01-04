# AWS-Portfolio-
## Overview
This repository is my learning portfolio for AWS Solutions Architect.
I will document small hands-on projects and architecture designs step by step.

## Current status
- AWS Cloud Practitioner: Passed
- Studying AWS Solutions Architect (Associate)

## Goal
To understand AWS architecture and explain design decisions clearly.

## How I think as a Solution Architect

When comparing AWS services such as EC2, Lambda, and managed databases,
I enjoy thinking from a business perspective rather than focusing only on technology.

I consider factors like:
- Business impact
- Security responsibility
- Operational efficiency
- Cost effectiveness

I believe there is no single "best" service.
The best solution always depends on the business requirements and constraints.


### AWS Storage & Load Balancing: Key Differences

Today, I deepened my understanding of the differences between EBS, Instance Store, and ELB.

| Feature | **EBS (Elastic Block Store)** | **Instance Store** | **ELB (Elastic Load Balancing)** |
| :--- | :--- | :--- | :--- |
| **Type** | Network-attached Storage | Physically-attached Storage | Load Balancer |
| **Persistence** | Data persists after instance termination | Data is lost if instance is terminated (Ephemeral) | N/A (Distributes traffic) |
| **Main Use Case** | Databases, Boot volumes | High-speed cache, Temporary data | High availability, Scalability |
| **Key Takeaway** | Think of it as a "Network USB Drive". | Think of it as a "Built-in SSD". | Think of it as a "Traffic Cop". |

**My Notes:**
* **EBS:** Can be detached and reattached to other instances. Reliable for long-term storage.
* **Instance Store:** Incredible I/O speed, but very risky for important data.
* **ELB:** Essential for distributing incoming traffic across multiple EC2 instances to ensure security and availability.
