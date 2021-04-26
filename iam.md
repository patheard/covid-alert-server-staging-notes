# IAM
**Source:** [/server/aws/iam.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/iam.tf)

## Key Retrieval
- Defines `covidshield_key_retrieval` role which allows:
   - ECR task execution (via [`AmazonECSTaskExecutionRolePolicy`](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_execution_IAM_role.html))
   - Secrets Manager access to:
```
key_submission_env_key_claim_token
key_retrieval_env_hmac_key
key_retrieval_env_ecdsa_key
server_database_url
key_submission_metrics_password
```

## Key Retrieval
Same as above, with Secrets Manager access to:
```
key_submission_env_key_claim_token
server_database_url
```

## Codedeploy
- Role to update ECS deployments via [`AWSCodeDeployRoleForECS`](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/codedeploy_IAM_role.html)

## Validate Deployment Lambda
- Role to [validate deployment](https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorial-ecs-deployment-with-hooks.html) using a Lambda function:
   - `codedeploy:PutLifecycleEventHookExecutionStatus`
   - [`AWSLambdaBasicExecutionRole`](https://gist.github.com/bernadinm/6f68bfdd015b3f3e0a17b2f00c9ea3f8#file-all_aws_managed_policies-json-L1447-L1473)