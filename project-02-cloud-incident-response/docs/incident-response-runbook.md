# Incident Response Runbook

## Business Scenario
A Japanese enterprise customer experiences an outage
in a SaaS application operated by a Taiwan-based company.

## Incident Detection
- Review CloudWatch alarms.
- Check EC2 instance health.
- Inspect application and system logs.

## Escalation Process
1. Customer contacts local BD or distributor.
2. Local BD coordinates customer communication.
3. HQ engineers investigate technical issues.
4. HQ provides updates to the local contact.
5. Local contact communicates with the customer.

## Technical Troubleshooting
- Check EC2 instance status.
- Review CPU and network metrics.
- Check Linux services and logs.
- Verify security group configuration.

## Recovery
- Apply corrective action.
- Confirm application availability.
- Monitor for recurring issues.

## Customer Communication
- Acknowledge the incident.
- Explain confirmed impact and current status.
- Provide regular progress updates.
- Share a post-incident summary.

## Proposed Response Targets
- Initial triage: within 15 minutes.
- First customer update: within 30 minutes.
- Progress updates: every 30 minutes.

These are proposed targets, not contractual SLAs.

## Project Status
Design completed. Deployment and testing pending.
