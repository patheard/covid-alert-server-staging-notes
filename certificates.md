# Certificates
**Source:** [/server/aws/certificates.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/certificates.tf)

- Defines two certs:
   - `covidshield`: Key Retrieval/Submission ALBs, Metrics API Gateway
   - `retrieval_covidshield`: CloudFront in us-east-1
- Creates DNS validation records for both