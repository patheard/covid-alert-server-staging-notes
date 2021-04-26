# Metric Collection
**Sources:** 
- [/server/aws/mc-api-gateway.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/mc-api-gateway.tf)
- [/server/aws/mc-lambda.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/mc-lambda.tf)
- [/server/aws/mc-waf.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/mc-waf.tf)

## API Gateway
- Defines REST API Gateway to collect metrics
- Integration and stage created, which is mapped to custom URL
- Validates request payload against [/server/aws/models/metrics.json](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/models/metrics.json)
- Single POST create_method againt `var.service_name` which defaults to `save-metrics`
- Create method handled by Lambda function [/server/aws/lambda/create_metric.js](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/lambda/create_metric.js) which inserts record into DynamoDB table:
```js
const params = {
    TableName: process.env.TABLE_NAME,
    Item : {
        "uuid": {
            S: uuidv4(),
        },
        "expdate" : {
            N: ttl,
        },
        "raw": {
            S: event.body, // Assuming this is raw payload that matches metrics.json schema
        },
    },
};
```
- Creates CloudWatch log group `API-Gateway-Execution-Logs_${aws_api_gateway_rest_api.metrics.id}/${var.environment}`
- Sets logging level on method to `INFO`

## Lambda
- Defines `metrics` Lambda function
- Attached to private subnets `aws_subnet.covidshield_private.*`
- SG to allow 443 egress to S3 VPC endpoing (gateway)
- Role to allow CloudWatch logging and ENI creation in subnets

## WAF
- API Gateway stage ACLs:
```sh
# Block
AWSManagedRulesAmazonIpReputationList
AWSManagedRulesCommonRuleSet
AWSManagedRulesKnownBadInputsRuleSet
AWSManagedRulesLinuxRuleSet
AWSManagedRulesSQLiRuleSet
metrics_collection_rate_limit # 10,000 by IP
```