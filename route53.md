# Route53
**Source:** [/server/aws/route53.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/route53.tf)

## Zone
- Single zone for Key Retrieval/Submission apps

## Record: Key Retrieval
- `A` record
- Alias to Key Retrieval CloudFront distribution
- Health checks on 443 for:
   - `/services/ping`
   - `/exposure-configuration/CA.json` (region based)
   - `/exposure-configuration/region.json` (region based)

## Record: Key Submission
- `A` Rrecord
- Alias to API Gateway for metrics
