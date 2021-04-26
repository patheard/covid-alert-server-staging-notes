# CloudFront
**Source:** [/server/aws/cloudfront.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/cloudfront.tf)

- Defines `key_retrieval_distribution` and OAI using bucket `covid-shield-exposure-config-${var.environment}`
- Adds custom header for WAF rules
- Sets HTTPS and the certificate to use `aws_acm_certificate_validation.retrieval_covidshield`
- Sets WAF ACL `aws_wafv2_web_acl.key_retrieval_cdn`
- Defines cache behaviour (TTL, HTTP methods, paths):
```sh
# Cache
/exposure-configuration/*   # GET, HEAD

# Passthrough to aws_lb.covidshield_key_retrieval
/events/*                   # GET, HEAD
```