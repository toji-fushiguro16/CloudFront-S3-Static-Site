# Private S3 Static Website with CloudFront

Terraform deploys a static website to a private Amazon S3 bucket and serves it globally through CloudFront. Origin Access Control (OAC) signs CloudFront requests so the bucket can stay private.

## Architecture

```text
Browser --HTTPS--> CloudFront --signed S3 request--> Private bucket
```

## Deploy

Prerequisites: Terraform 1.6+, AWS CLI, and an AWS identity allowed to create S3 and CloudFront resources.

```bash
aws configure
terraform init
terraform plan
terraform apply
```

Terraform prints `site_url` after deployment. CloudFront distributions can take several minutes to become available.

## Clean up

```bash
terraform destroy
```

The S3 bucket is configured for Terraform to empty it during destroy. Review the plan before applying or destroying resources.

## Security and cost

The bucket blocks public access; only the CloudFront distribution can read objects. CloudFront and S3 usage may incur charges, especially on repeated requests. Destroy the stack after the demo. The distribution uses the default CloudFront certificate and domain.
