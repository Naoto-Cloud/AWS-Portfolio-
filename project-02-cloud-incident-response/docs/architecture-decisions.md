# Architecture Decisions

## Compute: Amazon EC2
A Linux-based EC2 instance hosts a sample SaaS application.

## Infrastructure as Code: Terraform
Terraform provides reproducible infrastructure deployment.

## Monitoring: Amazon CloudWatch
CloudWatch collects EC2 metrics and application logs.
The CloudWatch Agent is used for additional log collection.

## Notifications: Amazon SNS
SNS sends incident alerts to designated support contacts.

## Incident Ownership
- Local BD: Customer communication and coordination.
- Distributor: Optional first point of contact.
- HQ Engineering: Technical investigation and recovery.

## Security
- Apply least-privilege IAM permissions.
- Restrict inbound access using security groups.
- Never store credentials in GitHub.

## Cost Management
Use minimal AWS resources for testing.
Destroy test resources after validation.

## Future Improvements
- HTTP health monitoring.
- Automated incident ticket creation.
- Centralized incident dashboards.
