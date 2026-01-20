# AWS Infrastructure with Terraform & Terragrunt

This repository contains AWS infrastructure code using Terraform modules managed by Terragrunt.

## Structure

```
├── terragrunt.hcl              # Root Terragrunt config (provider, backend)
├── modules/                    # Reusable Terraform modules
│   └── vpc/                    # VPC module
├── environments/               # Environment-specific configs
│   ├── dev/                    # Development environment
│   │   ├── account.hcl
│   │   ├── region.hcl
│   │   ├── env.hcl
│   │   └── us-east-1/
│   │       └── vpc/
│   └── prod/                   # Production environment
│       ├── account.hcl
│       ├── region.hcl
│       ├── env.hcl
│       └── us-east-1/
│           └── vpc/
```

## Prerequisites

- Terraform >= 1.7.0
- Terragrunt >= 0.55.0
- AWS CLI configured with appropriate credentials
- S3 bucket for state storage
- DynamoDB table for state locking

## Usage

```bash
# Navigate to environment/region/module
cd environments/dev/us-east-1/vpc

# Initialize and plan
terragrunt init
terragrunt plan

# Apply changes
terragrunt apply

# Apply all modules in an environment
cd environments/dev
terragrunt run-all apply
```

## Configuration

1. Update `account.hcl` with your AWS account ID
2. Create S3 bucket: `<account_name>-terraform-state`
3. Create DynamoDB table: `terraform-locks`
