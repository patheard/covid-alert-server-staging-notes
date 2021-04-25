# RDS
**Source:** [/server/aws/rds.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/rds.tf)

## Cluster
- Aurora cluster with instances provisioned in the 3 `aws_subnet.covidshield_private.*` subnets
- Maintenance window `07:00-09:00`
- 1 day retention on backups
- Delete protection
- Encrypted with default service key

## Security Group
- `aws_security_group.covidshield_database`
