# Terraform — Quick Notes

## What is Terraform?

- Terraform is an infrastructure-as-code (IaC) tool by HashiCorp for provisioning and managing cloud and on-prem resources using declarative configuration files.
- Uses a declarative language called HCL (HashiCorp Configuration Language).

## Core Concepts

- Provider: plugin that manages resources for a specific platform (e.g., `aws`, `azurerm`, `google`).
- Resource: a single infrastructure object (e.g., `aws_instance`, `azurerm_storage_account`).
- Data source: read-only info from provider (e.g., lookup existing VPCs).
- Module: reusable collection of Terraform files (can be local or remote).
- State: JSON file storing the current mapping between configuration and real resources (`terraform.tfstate`).
- Plan: preview of changes (`terraform plan`).
- Apply: enact changes (`terraform apply`).

## Basic Workflow

1. Write configuration (`.tf` files).
2. Initialize provider plugins: `terraform init`.
3. Preview changes: `terraform plan`.
4. Apply changes: `terraform apply`.
5. Inspect state: `terraform show` / `terraform state list`.

## Useful Commands

- `terraform init` — initialize working directory and download providers.
- `terraform validate` — checks syntax and internal consistency.
- `terraform fmt` — format files to canonical HCL style.
- `terraform plan -out=tfplan` — generate a plan and save to file.
- `terraform apply tfplan` — apply a saved plan.
- `terraform destroy` — remove all managed resources.

## State Management

- By default, state is stored locally in `terraform.tfstate`. For team usage, use remote state backends (S3, Azure Blob, GCS) with locking (DynamoDB, CosmosDB, etc.).
- Protect state: it can contain secrets and resource IDs — store securely and limit access.

## Modules & Reuse

- Create modules for repeated patterns (network, compute, storage).
- Use versioned remote modules from the registry or Git repos.
- Keep modules small, well-documented, and parameterized via `variables`.

## Variables & Outputs

- `variable` blocks define inputs; provide defaults or pass via `-var` / `tfvars` / environment variables.
- `output` blocks expose values (e.g., IPs, URLs) after apply.

## Security & Best Practices

- Avoid committing secrets in `.tf` files or state; use secret managers or environment variables.
- Pin provider and module versions to avoid unexpected changes.
- Use remote state with locking for team collaboration.
- Run `terraform fmt` and `terraform validate` in CI before applying.
- Review `terraform plan` before `apply` — use saved plan files for controlled apply.

## Example (AWS EC2)

```hcl
provider "aws" {
	region = "us-east-1"
}

resource "aws_instance" "web" {
	ami           = "ami-0c55b159cbfafe1f0"
	instance_type = "t3.micro"
}
```
