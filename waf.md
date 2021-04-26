# WAF
**Source:** [/server/aws/waf.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/waf.tf)

Defines:
- Allowed IPs/CIDRs for key claims
- Key submission ACLs:
```sh
# Block
AWSManagedRulesAmazonIpReputationList
AWSManagedRulesCommonRuleSet
AWSManagedRulesKnownBadInputsRuleSet
AWSManagedRulesLinuxRuleSet
AWSManagedRulesSQLiRuleSet
KeySubmissionClaimKeyURIRateLimit01-05 on `/claim-key` # Why 5?

# Allow
Valid key submission URL patterns
```
- Key retrieval ALB allow based on [`CloudFrontCustomHeader`](https://aws.amazon.com/blogs/security/how-to-enhance-amazon-cloudfront-origin-security-with-aws-waf-and-aws-secrets-manager/) existing with correct value
- Key retrieval CDN rate limiting (us-east-1)
- Attach WAF logging to Kinesis Firehose delivery stream

