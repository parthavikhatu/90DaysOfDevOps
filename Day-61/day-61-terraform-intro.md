# Day 61 – Introduction to Terraform and Your First AWS Infrastructure

## Objective

Today I started learning **Terraform**, one of the most popular Infrastructure as Code (IaC) tools. I installed Terraform, connected it to AWS using the AWS CLI, created an S3 bucket and an EC2 instance, explored the Terraform state file, modified infrastructure, and finally destroyed all resources using Terraform commands.

---

# Task 1 – Infrastructure as Code (IaC)

## What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is the process of creating and managing cloud infrastructure using code instead of manually creating resources through the AWS Console.

Instead of clicking buttons every time, we write configuration files that Terraform reads and uses to automatically create resources like EC2 instances, S3 buckets, VPCs, databases, and more.

This makes infrastructure faster, repeatable, and less prone to human error.

---

## Why is IaC important in DevOps?

IaC is important because:

- It automates infrastructure creation.
- It eliminates manual configuration errors.
- Infrastructure can be recreated anytime.
- Infrastructure changes can be version controlled using Git.
- Teams can collaborate using the same code.
- It enables faster and more reliable deployments.

---

## Problems solved by IaC compared to manual AWS Console creation

Manual AWS Console:

- Time-consuming
- Human errors are common
- Difficult to recreate environments
- No version control
- Hard to maintain consistency

Using Terraform:

- Fast automation
- Same infrastructure every time
- Easy rollback using Git
- Infrastructure becomes reusable
- Easy collaboration among teams

---

## Terraform vs CloudFormation vs Ansible vs Pulumi

| Tool | Purpose | Language |
|------|----------|----------|
| Terraform | Infrastructure provisioning | HCL |
| AWS CloudFormation | AWS infrastructure provisioning | JSON / YAML |
| Ansible | Configuration management and automation | YAML |
| Pulumi | Infrastructure provisioning | Python, Java, Go, TypeScript, C# |

---

## What does Declarative mean?

Terraform is declarative because we describe **what infrastructure we want**, not **how to create it**.

Example:

"I need one EC2 instance."

Terraform automatically determines the steps required to create it.

---

## What does Cloud-Agnostic mean?

Terraform supports multiple cloud providers.

The same Terraform tool can manage:

- AWS
- Azure
- Google Cloud
- Oracle Cloud
- VMware
- Kubernetes
- GitHub
- Docker

This is why Terraform is called **cloud-agnostic**.

---

# Task 2 – Install Terraform and Configure AWS

## Installed Terraform

```bash
terraform -version
```

Output:

```text
Terraform v1.x.x
```

---

## Configured AWS CLI

```bash
aws configure
```

Entered:

- AWS Access Key
- Secret Access Key
- Region
- Output Format

Verified AWS connection:

```bash
aws sts get-caller-identity
```

Output:

- AWS Account ID
- IAM User ARN

---

# Task 3 – Create an S3 Bucket

## main.tf

```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "mybucket" {
  bucket = "parthavi-terraform-2026-demo"
}
```

---

## Terraform Commands

Initialize Terraform

```bash
terraform init
```

Preview Changes

```bash
terraform plan
```

Create Resources

```bash
terraform apply
```

---

## Screenshot

> Add Screenshot of `terraform apply`

---

## Verify

Verified the bucket in the AWS S3 Console.

---

## What did terraform init download?

`terraform init` downloaded:

- AWS Provider Plugin
- Required dependencies
- Provider lock file
- Created the `.terraform` directory

---

## What does the .terraform directory contain?

It contains:

- Downloaded provider plugins
- Provider binaries
- Dependency information
- Internal Terraform files

---

# Task 4 – Create an EC2 Instance

Added the following resource:

```terraform
resource "aws_instance" "web" {

  ami           = "ami-0f5ee92e2d63afc18"

  instance_type = "t2.micro"

  tags = {
    Name = "TerraWeek-Day1"
  }

}
```

Executed:

```bash
terraform plan
terraform apply
```

Verified the EC2 instance in the AWS Console.

---

## Screenshot

> Add Screenshot of EC2 Instance

---

## How does Terraform know the S3 bucket already exists?

Terraform keeps track of every resource it creates inside the **terraform.tfstate** file.

When `terraform plan` runs, Terraform compares:

- Current State (terraform.tfstate)
- Desired State (main.tf)

Since the S3 bucket already existed in the state file, Terraform only created the EC2 instance.

---

# Task 5 – Terraform State File

Terraform stores information about every managed resource inside:

```text
terraform.tfstate
```

---

## Commands Used

### Show Current Infrastructure

```bash
terraform show
```

Shows all managed resources in a readable format.

---

### List Managed Resources

```bash
terraform state list
```

Example:

```text
aws_s3_bucket.mybucket
aws_instance.web
```

---

### Show S3 Bucket Details

```bash
terraform state show aws_s3_bucket.mybucket
```

Displays detailed information about the S3 bucket.

---

### Show EC2 Details

```bash
terraform state show aws_instance.web
```

Displays detailed information about the EC2 instance.

---

## What information does the state file store?

The state file stores:

- Resource IDs
- Resource Names
- ARNs
- Tags
- Region
- Dependencies
- Current configuration
- Resource attributes
- Metadata

Terraform uses this information to manage infrastructure efficiently.

---

## Why should we never edit the state file manually?

Manual editing may:

- Corrupt the state
- Cause resource mismatches
- Lead to infrastructure errors
- Break future Terraform operations

---

## Why should the state file not be committed to Git?

The state file may contain:

- Resource IDs
- Internal metadata
- Sensitive information
- Infrastructure details

It is better to store it securely in a **remote backend** such as an S3 bucket with state locking.

---

# Task 6 – Modify Infrastructure

Changed EC2 tag:

Before:

```text
TerraWeek-Day1
```

After:

```text
TerraWeek-Modified
```

Executed:

```bash
terraform plan
```

Terraform showed:

```text
~ update in-place
```

Applied the changes:

```bash
terraform apply
```

Verified the updated tag in the AWS Console.

---

## Terraform Plan Symbols

| Symbol | Meaning |
|---------|----------|
| + | Create Resource |
| ~ | Modify Existing Resource |
| - | Destroy Resource |

---

## Was it recreated?

No.

Only the tag changed, so Terraform performed an **in-place update**.

---

# Destroy Infrastructure

Executed:

```bash
terraform destroy
```

Terraform deleted:

- EC2 Instance
- S3 Bucket

Verified both resources were removed from the AWS Console.

---

# Terraform Commands Summary

| Command | Description |
|----------|-------------|
| terraform init | Initializes Terraform and downloads providers |
| terraform fmt | Formats Terraform files |
| terraform validate | Validates Terraform syntax |
| terraform plan | Shows execution plan |
| terraform apply | Creates or updates infrastructure |
| terraform show | Displays current infrastructure |
| terraform state list | Lists managed resources |
| terraform state show | Displays details of a resource |
| terraform destroy | Deletes infrastructure |

---

# Files Created

```
terraform-basics/
│
├── main.tf
├── terraform.tfstate
├── .terraform/
├── .terraform.lock.hcl
└── .gitignore
```

---

# .gitignore

```text
.terraform/
*.tfstate
*.tfstate.backup
```

---

# Key Learnings

- Learned the basics of Infrastructure as Code (IaC).
- Installed and configured Terraform with AWS.
- Created an S3 bucket using Terraform.
- Created an EC2 instance using Terraform.
- Understood the Terraform workflow (`init`, `plan`, `apply`, and `destroy`).
- Explored the `terraform.tfstate` file and learned why it is important.
- Learned how Terraform detects infrastructure changes using the state file.
- Understood the meaning of Terraform plan symbols (`+`, `~`, `-`).
- Destroyed infrastructure safely using Terraform.

---

# Conclusion

Today I completed my first Terraform project by provisioning AWS resources using code instead of the AWS Console. I learned the complete Terraform workflow, understood the importance of the state file, and experienced how Infrastructure as Code makes cloud resource management faster, repeatable, and reliable.
