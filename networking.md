# Networking
**Source:** [/server/aws/networking.tf](https://github.com/cds-snc/covid-alert-server-staging-terraform/blob/master/server/aws/networking.tf)

## VPC
```sh
00001010.00000000 | 00000000.00000000 # 10.0.0.0/16
```
## Subnets
Three private, three public across 3 availability zones.
### Private
```sh
00001010.00000000.00000001 | 00000000 # 10.0.1.0/24
00001010.00000000.00000010 | 00000000 # 10.0.2.0/24
00001010.00000000.00000011 | 00000000 # 10.0.3.0/24
```

### Public
```sh
00001010.00000000.00000100 | 00000000 # 10.0.4.0/24
00001010.00000000.00000101 | 00000000 # 10.0.5.0/24
00001010.00000000.00000110 | 00000000 # 10.0.6.0/24
```

## Internet Gateway
- Route table association in 3 public subnets
- Default `0.0.0.0/0` association

## Security Groups
- Default blocking all ingress/egress (removes the default AWS SG which allows all ingress from network interfaces with same SG and all egress).

### Key Retrieval/Submission Apps
- Ingress from ALB
- Egress to PrivateLink, S3, Database, Redis

### Privatelink
- Ingress on 443 for Key Retrieval/Submission Apps

### Load balancer
- Public ingress from 443/8443
- Egress to private subnets on 8000/8001

### Database
- Ingress on 3306

### Redis
- Ingress on 6379

## Network ACLs
1. Deny ingress 22/3389
2. Allow `ALL` ingress/egress

