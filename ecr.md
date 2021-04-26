# ECR
**Source:** [/server/aws/s3.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/ecr.tf)

- Defines 3 repos:
```sh
covid-server/key-retrieval
covid-server/key-submission
covid-server/monolith
```
- Scans on push
- Keeps latest 30 images tagged with `^v.*$`

