# Metrics
**Source:** [/server/aws/metrics.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/metrics.tf)

## Filters 
Metric log filters for the following:
- UnclaimedOneTimeCodeTotal
- ClaimedOneTimeCodeTotal
- DiagnosisKeyTotal

**Note:** 
- 8 filter aggregators are required for each because of the app metric log structure 
- 1 filter per metric array position, which performs the following: `$.updates[${count.index}].sum`

## Alarms
- Warn and critical alarms for each filter
- Use the [warn/critical SNS topics](sns.md).