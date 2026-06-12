# AWS Cost Estimate — PeopleFlow Commercial (1000 users)

> Pricing as of 2026-05-29, based on AWS public pricing pages and AWS Pricing Calculator references.

## Assumptions used in this estimate

- ECS/Fargate usage modeled as: 2 tasks always on + burst of 2 extra tasks for 8h/day x 22 business days (to reflect 50 concurrent peak), Linux/x86.
- ALB modeled with 1 LCU average.
- CloudFront pricing modeled for South America edge delivery profile (relevant for LATAM audience).
- RDS backup storage assumed within free backup allocation (up to provisioned DB size).
- NAT data processing given by your input: 30 GB/month.

## us-east-1

| Service | Quantity | Unit price (USD) | Monthly total (USD) |
|---|---:|---:|---:|
| VPC NAT Gateway (hourly) | 730 hours | $0.045/hour | $32.85 |
| VPC NAT Gateway (data processing) | 30 GB | $0.045/GB | $1.35 |
| ECS Fargate vCPU | 906 vCPU-hours | $0.04048/vCPU-hour | $36.67 |
| ECS Fargate memory | 1,812 GB-hours | $0.004445/GB-hour | $8.05 |
| Application Load Balancer (hourly) | 730 hours | $0.0225/hour | $16.43 |
| ALB LCU | 730 LCU-hours | $0.008/LCU-hour | $5.84 |
| RDS PostgreSQL db.t4g.medium (Single-AZ) | 730 hours | $0.067/hour | $48.91 |
| RDS gp3 storage | 100 GB-month | $0.115/GB-month | $11.50 |
| S3 Standard storage | 100 GB-month | $0.023/GB-month | $2.30 |
| S3 PUT requests | 50K requests | $0.005/1K | $0.25 |
| S3 GET requests | 200K requests | $0.0004/1K | $0.08 |
| CloudFront data transfer out | 500 GB | $0.085/GB | $42.50 |
| CloudFront HTTPS requests | 5M requests | $0.01/10K | $5.00 |
| ECR storage | 5 GB-month | $0.10/GB-month | $0.50 |
| Secrets Manager | 10 secrets | $0.40/secret-month | $4.00 |
| CloudWatch Logs ingestion | 10 GB | $0.50/GB | $5.00 |
| Route 53 hosted zone | 1 zone | $0.50/zone-month | $0.50 |
| Route 53 DNS queries | 5M queries | $0.40/million | $2.00 |
| SES outbound email | 30K emails | $0.10/1K | $3.00 |

**Total: $226.73/month**

## sa-east-1

| Service | Quantity | Unit price (USD) | Monthly total (USD) |
|---|---:|---:|---:|
| VPC NAT Gateway (hourly) | 730 hours | $0.093/hour | $67.89 |
| VPC NAT Gateway (data processing) | 30 GB | $0.093/GB | $2.79 |
| ECS Fargate vCPU | 906 vCPU-hours | $0.08089/vCPU-hour | $73.29 |
| ECS Fargate memory | 1,812 GB-hours | $0.00889/GB-hour | $16.11 |
| Application Load Balancer (hourly) | 730 hours | $0.0288/hour | $21.02 |
| ALB LCU | 730 LCU-hours | $0.01024/LCU-hour | $7.48 |
| RDS PostgreSQL db.t4g.medium (Single-AZ) | 730 hours | $0.136/hour | $99.28 |
| RDS gp3 storage | 100 GB-month | $0.138/GB-month | $13.80 |
| S3 Standard storage | 100 GB-month | $0.0276/GB-month | $2.76 |
| S3 PUT requests | 50K requests | $0.0065/1K | $0.33 |
| S3 GET requests | 200K requests | $0.00052/1K | $0.10 |
| CloudFront data transfer out | 500 GB | $0.125/GB | $62.50 |
| CloudFront HTTPS requests | 5M requests | $0.022/10K | $11.00 |
| ECR storage | 5 GB-month | $0.10/GB-month | $0.50 |
| Secrets Manager | 10 secrets | $0.40/secret-month | $4.00 |
| CloudWatch Logs ingestion | 10 GB | $0.76/GB | $7.60 |
| Route 53 hosted zone | 1 zone | $0.50/zone-month | $0.50 |
| Route 53 DNS queries | 5M queries | $0.40/million | $2.00 |
| SES outbound email | 30K emails | $0.10/1K | $3.00 |

**Total: $395.94/month**

## Top 3 Cost Drivers

1. **Compute + DB base capacity** (ECS Fargate + RDS instance): largest fixed monthly floor.
2. **CloudFront data transfer out** (500 GB): network egress is a major variable driver.
3. **NAT Gateway hourly charge** (especially in sa-east-1): high fixed networking tax even at modest throughput.

In both regions, these three categories contribute >60% of total monthly spend.

## Optimizations

- **Compute Savings Plans (1 year, no upfront, Fargate ~17%)**  
  Estimated savings on Fargate component:  
  - us-east-1: ~$7.60/month saved (from ~$44.72)  
  - sa-east-1: ~$15.20/month saved (from ~$89.40)

- **RDS Reserved Instance (1 year)**  
  Typical planning estimate for db.t4g.medium is ~30% off instance-hours (storage unchanged):  
  - us-east-1: ~$14.67/month saved (from ~$48.91 compute)  
  - sa-east-1: ~$29.78/month saved (from ~$99.28 compute)

- **Single-AZ vs Multi-AZ tradeoff**  
  - Single-AZ: cheaper, but lower resilience for DB failover events.  
  - Multi-AZ: materially higher cost (roughly double DB compute and replicated storage), but production-grade availability.

- **Gateway VPC Endpoint for S3**  
  - Removes NAT data-processing cost for S3-bound private subnet traffic.  
  - Estimated direct savings from your 30 GB NAT data assumption:  
    - us-east-1: up to ~$1.35/month  
    - sa-east-1: up to ~$2.79/month  
  - Note: Gateway Endpoint itself has no hourly charge.

## Production Hardened Range

- Baseline (this estimate, Single-AZ + 1 NAT): **$226.73 (us-east-1)** / **$395.94 (sa-east-1)**
- Hardened (Multi-AZ RDS + 2 NAT): **~$321.34 (us-east-1)** / **~$527.03 (sa-east-1)**

## Per-User Economics

- us-east-1: $226.73 / 1000 users = **$0.23/user/month**
- sa-east-1: $395.94 / 1000 users = **$0.40/user/month**

## Disclaimers

- This is an estimate from AWS public price points; final bill depends on real traffic profile, AZ mix, and exact request/LCU behavior.
- CloudFront egress price varies by viewer geography; this model uses South America-oriented delivery.
- Fargate burst usage is modeled (business-hour peak). If autoscaling runs longer, compute cost increases linearly.
- ALB LCU is workload-sensitive (new connections, active connections, processed bytes, rule evals); 1 LCU average is conservative for this scale.
- For board/client presentation, validate final line items in AWS Pricing Calculator with your exact architecture JSON before sign-off.

## AWS official pricing sources

- AWS Pricing landing: https://aws.amazon.com/pricing/
- AWS Pricing Calculator: https://calculator.aws/
- AWS Fargate pricing: https://aws.amazon.com/fargate/pricing/
- Amazon RDS pricing: https://aws.amazon.com/rds/postgresql/pricing/
- Amazon VPC pricing (NAT Gateway): https://aws.amazon.com/vpc/pricing/
- Application Load Balancer pricing: https://aws.amazon.com/elasticloadbalancing/pricing/
- Amazon S3 pricing: https://aws.amazon.com/s3/pricing/
- Amazon CloudFront pricing: https://aws.amazon.com/cloudfront/pricing/
- Amazon ECR pricing: https://aws.amazon.com/ecr/pricing/
- AWS Secrets Manager pricing: https://aws.amazon.com/secrets-manager/pricing/
- Amazon CloudWatch pricing: https://aws.amazon.com/cloudwatch/pricing/
- Amazon Route 53 pricing: https://aws.amazon.com/route53/pricing/
- Amazon SES pricing: https://aws.amazon.com/ses/pricing/
