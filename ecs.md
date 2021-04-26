# ECS
**Source:** [/server/aws/ecs.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/ecs.tf)

- Defines ECS cluster with Key Retrieval and Key Submission tasks/services.
- Image deploy managed by Codedeploy

## Tasks
- Fargate
- Images from ECR:
```sh
covid-server/key-retrieval
covid-server/key-submission
```
- Task definitions in:
   - [/server/aws/task-definitions/covidshield_key_retrieval.json](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/task-definitions/covidshield_key_retrieval.json)
   - [/server/aws/task-definitions/covidshield_key_submission.json](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/task-definitions/covidshield_key_submission.json)

## Services
- Deployed to private subnets with no public IP `aws_subnet.covidshield_private.*`
- Load balancer is entry point:
```sh
aws_lb_target_group.covidshield_key_retrieval   # port 8001
aws_lb_target_group.covidshield_key_submission  # port 8000
```

