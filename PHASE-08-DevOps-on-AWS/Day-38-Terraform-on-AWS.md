# Terraform on AWS 

By the end of this tutorial, we will be able to:

* Understand Infrastructure as Code (IaC)
* Install Terraform
* Configure AWS CLI
* Write Terraform configuration files
* Deploy AWS resources
* Update infrastructure
* Destroy infrastructure
* Use variables, outputs, modules, and remote state
* Follow Terraform best practices

---

# Prerequisites

* AWS Account
* IAM User with Programmatic Access
* AWS CLI
* Terraform (latest version)
* Visual Studio Code
* Git
* Basic Linux commands

---

# Architecture

```
Developer
     │
     │ terraform apply
     ▼
Terraform
     │
     ▼
AWS API
     │
     ├── VPC
     ├── Internet Gateway
     ├── Route Table
     ├── Public Subnet
     ├── Security Group
     ├── EC2 Instance
     └── Elastic IP
```

---

# Section 1 – What is Terraform?

Explain:

* Infrastructure as Code
* Declarative vs Imperative
* Terraform workflow

```
Write Code

↓

terraform init

↓

terraform plan

↓

terraform apply

↓

AWS Infrastructure
```

---

# Section 2 – Install Terraform

### Windows

Download Terraform

Extract

Add to PATH

Verify

```bash
terraform version
```

Expected output

```
Terraform v1.x.x
```

---

# Section 3 – Install AWS CLI

```bash
aws configure
```

Provide:

```
Access Key

Secret Key

Region

Output=json
```

Verify

```bash
aws sts get-caller-identity
```

---

# Section 4 – Create Project

```
terraform-demo/

│

├── provider.tf

├── main.tf

├── variables.tf

├── outputs.tf

└── terraform.tfvars
```

---

# provider.tf

```hcl
terraform {
  required_version = ">= 1.8"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = var.aws_region
}
```

---

# variables.tf

```hcl
variable "aws_region" {
  default = "us-east-1"
}

variable "instance_type" {
  default = "t3.micro"
}
```

---

# main.tf

```hcl
resource "aws_instance" "web" {

  ami           = "ami-xxxxxxxx"

  instance_type = var.instance_type

  tags = {
    Name = "Terraform-EC2"
  }

}
```

Explain how to find the latest Amazon Linux 2023 AMI using the AWS Console or a data source so students don't hard-code an outdated AMI.

---

# outputs.tf

```hcl
output "public_ip" {

  value = aws_instance.web.public_ip

}
```

---

# Section 5 – Initialize Terraform

```bash
terraform init
```

Explain:

* Downloads providers
* Creates `.terraform`
* Creates `.terraform.lock.hcl`

---

# Section 6 – Validate

```bash
terraform validate
```

Purpose

Checks syntax.

---

# Section 7 – Format

```bash
terraform fmt
```

Formats code automatically.

---

# Section 8 – Plan

```bash
terraform plan
```

Explain

Nothing is created.

Terraform only shows

```
+ create

~ modify

- destroy
```

---

# Section 9 – Apply

```bash
terraform apply
```

Type

```
yes
```

Terraform creates

* EC2

Verify

AWS Console

EC2

Running

---

# Section 10 – Show State

```bash
terraform show
```

---

# Section 11 – State File

Explain

```
terraform.tfstate
```

Contains

* Resource IDs
* IP addresses
* Metadata

---

# Section 12 – Change Infrastructure

Change

```
t3.micro

↓

t3.small
```

Run

```bash
terraform plan
```

Students observe

```
~ update
```

Apply

```bash
terraform apply
```

---

# Section 13 – Outputs

```bash
terraform output
```

Example

```
54.182.25.100
```

---

# Section 14 – Variables

```
terraform.tfvars
```

```hcl
aws_region="us-east-1"

instance_type="t3.micro"
```

---

# Section 15 – Destroy

```bash
terraform destroy
```

Everything created by Terraform is deleted.

---

# Section 16 – Build a Real Infrastructure

Deploy:

```
VPC

↓

Subnet

↓

Internet Gateway

↓

Route Table

↓

Security Group

↓

EC2

↓

Elastic IP
```

Students learn dependencies.

---

# Section 17 – Remote State

Explain why storing `terraform.tfstate` locally is risky.

Create:

* S3 bucket
* DynamoDB table

Store state remotely.

---

# Section 18 – Modules

Create

```
modules/

vpc/

ec2/

security-group/
```

Call

```hcl
module "ec2" {

 source="./modules/ec2"

}
```

---

# Section 19 – Workspaces

```bash
terraform workspace list

terraform workspace new dev

terraform workspace new prod

terraform workspace select prod
```

---

# Section 20 – Best Practices

* Never edit `terraform.tfstate` manually.
* Use a remote backend (S3 + DynamoDB or the current AWS-recommended locking mechanism).
* Store secrets in a secure secret manager rather than hard-coding them.
* Use modules to keep code reusable.
* Use variables instead of fixed values.
* Keep code in Git.
* Review `terraform plan` before every `apply`.

---

# Common Commands

```bash
terraform init
terraform validate
terraform fmt
terraform plan
terraform apply
terraform show
terraform output
terraform state list
terraform taint RESOURCE
terraform untaint RESOURCE
terraform import RESOURCE ID
terraform refresh
terraform destroy
terraform workspace list
terraform workspace new
terraform workspace select
```

> **Note:** Some commands such as `terraform refresh` and `terraform taint` have changed over time and are no longer the preferred workflow in recent Terraform versions. Mention this to your audience and introduce their modern alternatives where appropriate.

---
