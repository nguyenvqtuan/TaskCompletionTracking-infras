# Task Completion Tracking Infrastructure

This repository contains the Terraform infrastructure code for the Task Completion Tracking project. It provisions AWS resources including an S3 bucket, an ECR repository, and IAM roles configured with GitHub OIDC for secure CI/CD integration.

## Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) (v1.5.7+)
- [AWS CLI](https://aws.amazon.com/cli/) configured with appropriate credentials.

## Resources Provisioned

- **AWS S3 Bucket**: `my-bucket` (with Versioning enabled and Private ACL).
- **AWS ECR Repository**: `my-ecr` for storing Docker images.
- **IAM Roles**: `github-role` configured to trust GitHub Actions via OIDC.

## Configuration Variables

| Name | Description | Type | Required |
|------|-------------|------|----------|
| `github_repo` | Configuration for OIDC trust. Format: `owner/repo` (e.g., `myuser/myproject`) | string | **Yes** |

## How to Run

1.  **Initialize Terraform**:
    Downloads necessary providers (AWS, TLS).
    ```bash
    terraform init
    ```

2.  **Plan the Infrastructure**:
    Preview changes before applying. You must provide the `github_repo` variable.
    ```bash
    terraform plan -var="github_repo=your-username/your-repo"
    ```

3.  **Apply Changes**:
    Provision the resources on AWS.
    ```bash
    terraform apply -var="github_repo=your-username/your-repo"
    ```

    **Example with specific values:**
    ```bash
    terraform apply -var="github_repo=octocat/hello-world"
    ```

    **Passing multiple variables:**
    ```bash
    terraform apply -var="github_repo=octocat/hello-world" -var="region=us-east-1"
    ```

### Using a `tfvars` file

Alternatively, create a `terraform.tfvars` file to store your configuration:

```hcl
# terraform.tfvars
github_repo = "your-username/your-repo"
```

Then simply run:
```bash
terraform apply
```
