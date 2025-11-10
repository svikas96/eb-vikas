# AWS 3-Tier Architecture


This repository demonstrates a simple 3-tier architecture deployed to AWS using Terraform.


Tiers:
- **Presentation (frontend)**: static site served from S3 + CloudFront or a small Nginx container behind ALB.
- **Application (app)**: Auto Scaling group of EC2 instances (or ECS/Fargate) behind an ALB.
- **Data (db)**: Amazon RDS (Postgres) in private subnets.


## What's included
- Terraform configuration to create VPC, subnets, ALB, ASG, RDS, S3, and security groups.
- A minimal Node.js app (app/) to run on the application tier.
- A simple static frontend (frontend/) to demonstrate separation of concerns.
- GitHub Actions workflow to run `terraform fmt`, `terraform init/plan` and (optionally) `terraform apply`.


## Quick start
1. Install Terraform and AWS CLI.
2. Configure AWS credentials locally (or use GitHub Secrets for CI/CD).
3. `cd terraform` then:
- `terraform init`
- `terraform plan -out=tfplan`
- `terraform apply tfplan`


## GitHub Actions
- The included workflow will run `terraform fmt` and `terraform plan` on PRs.
- For `terraform apply` from the workflow you must add `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `TF_STATE_S3_BUCKET`/`TF_STATE_S3_KEY` and `TF_STATE_DYNAMODB_TABLE` secrets.


## Security & changes
- Security groups are intentionally minimal for the demo — restrict them for production.
- Use an encrypted S3 bucket + DynamoDB locking for remote state in team environments.
