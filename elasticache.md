# ElastiCache
**Source:** [/server/aws/elasticache.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/elasticache.tf)

- ElastiCache Redis, cluster-mode disabled ([`default.redis5.0`](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/ParameterGroups.Redis.html)) with 3 cache clusters (1 primary, 2 replica)
- Attached to private subnets `aws_subnet.covidshield_private.*` in three AZs
- Port 6379
