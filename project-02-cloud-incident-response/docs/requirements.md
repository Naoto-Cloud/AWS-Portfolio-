# Project Requirements

## Business Context
A Taiwan-based B2B SaaS company is expanding into Japan.
Japanese enterprise customers require reliable technical
support and clear communication during service incidents.

## Business Requirements
- Provide early detection of cloud infrastructure issues.
- Establish clear responsibilities between local BD,
  distributors, and HQ technical engineers.
- Improve customer communication during incidents.
- Keep infrastructure costs manageable.

## Technical Requirements
- Provision infrastructure using Terraform.
- Host a sample web application on Amazon EC2.
- Monitor CPU utilization with Amazon CloudWatch.
- Send automated alerts using Amazon SNS.
- Collect application and system logs.

## Incident Scenarios
1. High EC2 CPU utilization.
2. Web application unavailable.
3. Security group misconfiguration.

## Success Criteria
- Terraform configuration passes validation.
- CloudWatch alarms trigger correctly.
- SNS delivers test notifications.
- At least one simulated incident is documented.
- Test infrastructure can be safely destroyed.
