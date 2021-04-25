# KMS
**Source:** [/server/aws/kms.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/kms.tf)

- Two keys for CloudWatch, which only differ for the key's policy principal:
```sh
cw          # "Principal": { "Service": "logs.ca-central-1.amazonaws.com" }
cw_us_east  # "Principal": { "Service": "logs.us-east-1.amazonaws.com" }
```
