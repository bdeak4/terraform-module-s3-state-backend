# terraform-state-s3-backend

Setup S3 and DynamoDB backend for Terraform state

## How to use (standalone)

Make sure you have `aws-cli` and `terraform` set up.

```
terraform init
AWS_PROFILE=project AWS_REGION=us-east-1 terraform apply -var bucket_name=project-tfstate -var table_name=project-tfstate-lock
```

These commands will create encrypted private S3 bucket which will store
Terraform state and DynamoDB table that will store state locks to prevent
parallel writes.

## How to use (as terraform module)

```tf
terraform {
  required_version = ">= 1.0.0, < 2.0.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region  = "us-east-1"
  profile = "project"
}

module "tfstate_backend" {
  source = "github.com/bdeak4/terraform-state-s3-backend"

  bucket_name = "project-tfstate"
  table_name  = "project-tfstate-lock"
}
```