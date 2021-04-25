# Load Balancer
**Source:** [/server/aws/lb.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/lb.tf)

## Key Retrieval
- LB on public subnets: `aws_subnet.covidshield_public.*`
- Access logs: `cbs-satellite-account-bucket${data.aws_caller_identity.current.account_id}`, prefix `/elb_logs_v2`
- SG: `aws_security_group.covidshield_load_balancer`

### Target groups
- HTTP:8001, target type `ip`
- Health check on `/services/ping`
- Targets are bound defined by codedeploy.tf and ecs.tf
```sh
covidshield_key_retrieval   # codedeploy.tf blue
covidshield_key_retrieval_2 # codedeploy.tf green
```

### Listeners
- HTTPS, forward:
```sh
covidshield_key_retrieval       # port 443
covidshield_key_retrieval_test  # port 8443
```

## Key Retrieval
Same same except target groups connect on port 8000.
