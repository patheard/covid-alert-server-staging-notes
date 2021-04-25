# Kinesis
**Source:** [/server/aws/kinesis.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/kinesis.tf)

- Defines two Kinesis Firehose delivery streams (and roles/policy) for WAF logs:
```sh
firehose_waf_logs
firehose_waf_logs_us_east
```
