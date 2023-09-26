# terraform-state-s3-backend

Setup S3 and DynamoDB state backend for Terraform

## How to use

Make sure you have `aws-cli` and `terraform` set up.

```
terraform init
AWS_PROFILE=project AWS_REGION=us-east-1 terraform apply -var bucket_name=project-tfstate -var table_name=project-tfstate-lock
```

These commands will create bucket name which will store Terraform state and
DynamoDB table that will store state locks to prevent parallel writes.
