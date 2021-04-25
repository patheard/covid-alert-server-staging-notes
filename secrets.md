# Secrets
**Source:** [/server/aws/secrets.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/secrets.tf)

Following managed with Secrets Manager, along with versions:

## Database
```sh
server_database_url
```

## Key Retrieval
```sh
key_retrieval_env_hmac_key
key_retrieval_env_ecdsa_key
```

## Key Submission
```sh
key_submission_env_key_claim_token
key_submission_metrics_password
```