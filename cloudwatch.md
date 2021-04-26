# CloudWatch
**Source:** [/server/aws/cloudwatch.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/cloudwatch.tf)

- Creates CloudWatch log group
- Defines warn and critical metric alarms:
```sh
# ECS metrics
(retrieval|submission)_cpu_utilization_high
(retrieval|submission)_memory_utilization_high

# Unauthorized
unauthorized_new_one_time_code_requests_(warn|critical)
unauthorized_one_time_code_claim_requests_(warn|critical)
unauthorized_upload_requests_(warn|critical)

# Code errors
five_hundred_response_(warn|critical)
error_logged_(warn|critical)
fatal_logged_(warn|critical)

# Action alarms
key_clear_called                        # diagnosis_keys truncated
ddos_detected_(retrieval|submission)    # detected at ALB
ddos_detected_cdn                       # detected by retrieval CDN
ddos_detected_route53

# Health checks
route53_retrieval_health_check
route53_retrieval_health_check_ca_json
route53_retrieval_health_check_region_json
route53_submission_health_check

# API Gateway
metrics_api_gateway_errors_above_threshold
metrics_api_gateway_min_invocations_threshold
metrics_api_gateway_max_invocations_threshold
metrics_api_gateway_max_latency_threshold

# Lambda
save_metrics_average_duration
```