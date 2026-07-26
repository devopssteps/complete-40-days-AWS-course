 # **Terraform on AWS hands-on project** 

# Complete Project Architecture

```text
                              INTERNET
                                  |
                                  |
                         Internet Gateway
                                  |
                                  v
                    +-------------------------+
                    |       AWS VPC            |
                    |    10.0.0.0/16           |
                    |                          |
                    |   PUBLIC SUBNET          |
                    |   10.0.1.0/24            |
                    |                          |
                    |  +--------+  +--------+  |
                    |  | EC2-1  |  | EC2-2  |  |
                    |  | Public |  | Public |  |
                    |  +--------+  +--------+  |
                    |       |          |       |
                    |       +----------+       |
                    |              |            |
                    |      Public Route Table   |
                    |              |            |
                    |              v            |
                    |         0.0.0.0/0          |
                    |              |            |
                    |              v            |
                    |       Internet Gateway    |
                    |                          |
                    |--------------------------|
                    |                          |
                    |   PRIVATE SUBNET         |
                    |   10.0.2.0/24            |
                    |                          |
                    |       +--------+         |
                    |       | EC2-3  |         |
                    |       |Private |         |
                    |       +--------+         |
                    |           |              |
                    |     Private Route Table  |
                    |           |              |
                    |       NAT Gateway        |
                    |           |              |
                    +-----------|--------------+
                                |
                                v
                           Internet
```


---

# Final Infrastructure

| Resource               |   Quantity |
| ---------------------- | ---------: |
| VPC                    |          1 |
| Public Subnet          |          1 |
| Private Subnet         |          1 |
| Internet Gateway       |          1 |
| NAT Gateway            | 1 optional |
| Elastic IP             | 1 optional |
| Public Route Table     |          1 |
| Private Route Table    |          1 |
| Public Security Group  |          1 |
| Private Security Group |          1 |
| Public EC2             |          2 |
| Private EC2            |          1 |

---

# 📁 Step 1: Create Terraform Project

Create:

```bash
mkdir terraform-aws-infrastructure
cd terraform-aws-infrastructure
```

Create these files:

```text
terraform-aws-infrastructure/
│
├── provider.tf
├── variables.tf
├── vpc.tf
├── subnets.tf
├── internet-gateway.tf
├── nat-gateway.tf
├── route-tables.tf
├── security-groups.tf
├── ec2.tf
├── outputs.tf
└── terraform.tfvars
```


---

# 🔧 Step 2: Configure AWS Provider

Create `provider.tf`:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }

  required_version = ">= 1.6.0"
}

provider "aws" {
  region = var.aws_region
}
```

---

# 📌 Step 3: Create Variables

Create `variables.tf`:

```hcl
variable "aws_region" {
  description = "AWS Region"
  type        = string
  default     = "us-east-1"
}

variable "vpc_cidr" {
  description = "VPC CIDR"
  type        = string
  default     = "10.0.0.0/16"
}

variable "public_subnet_cidr" {
  description = "Public subnet CIDR"
  type        = string
  default     = "10.0.1.0/24"
}

variable "private_subnet_cidr" {
  description = "Private subnet CIDR"
  type        = string
  default     = "10.0.2.0/24"
}

variable "availability_zone" {
  description = "Availability Zone"
  type        = string
  default     = "us-east-1a"
}

variable "ami_id" {
  description = "Amazon Linux AMI ID"
  type        = string
}

variable "instance_type" {
  description = "EC2 Instance Type"
  type        = string
  default     = "t3.micro"
}

variable "key_name" {
  description = "Existing EC2 Key Pair name"
  type        = string
}
```

---

# 📌 Step 4: Create terraform.tfvars

Create:

```hcl
aws_region          = "us-east-1"
vpc_cidr            = "10.0.0.0/16"
public_subnet_cidr  = "10.0.1.0/24"
private_subnet_cidr = "10.0.2.0/24"

availability_zone = "us-east-1a"

ami_id = "YOUR_AMAZON_LINUX_AMI_ID"

instance_type = "t3.micro"

key_name = "YOUR-KEY-PAIR-NAME"
```

Replace:

```text
YOUR_AMAZON_LINUX_AMI_ID
```

with a valid Amazon Linux AMI ID for your region.

Replace:

```text
YOUR-KEY-PAIR-NAME
```

with your existing EC2 key pair name.

---

# 🌐 Step 5: Create VPC

Create `vpc.tf`:

```hcl
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name = "terraform-demo-vpc"
  }
}
```

Our VPC:

```text
VPC
10.0.0.0/16
```

---

# 🌐 Step 6: Create Public Subnet

Create `subnets.tf`:

```hcl
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = var.public_subnet_cidr
  availability_zone       = var.availability_zone
  map_public_ip_on_launch = true

  tags = {
    Name = "terraform-public-subnet"
  }
}
```

Public subnet:

```text
10.0.1.0/24
```

The important setting is:

```hcl
map_public_ip_on_launch = true
```

This automatically assigns public IP addresses to newly launched EC2 instances in this subnet.

---

# 🔒 Step 7: Create Private Subnet

Add to `subnets.tf`:

```hcl
resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.private_subnet_cidr
  availability_zone = var.availability_zone

  tags = {
    Name = "terraform-private-subnet"
  }
}
```

Private subnet:

```text
10.0.2.0/24
```

Notice:

```hcl
map_public_ip_on_launch = true
```

is not present.

Therefore, EC2 launched here does not automatically receive a public IPv4 address.

---

# 🌍 Step 8: Create Internet Gateway

Create `internet-gateway.tf`:

```hcl
resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "terraform-igw"
  }
}
```

Architecture:

```text
Public EC2
    |
Public Route Table
    |
Internet Gateway
    |
Internet
```

---

# 🛣️ Step 9: Create Public Route Table

Create `route-tables.tf`:

```hcl
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "terraform-public-route-table"
  }
}
```

Associate it with the Public Subnet:

```hcl
resource "aws_route_table_association" "public" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public.id
}
```

Traffic flow:

```text
EC2
 |
Public Subnet
 |
Public Route Table
 |
0.0.0.0/0
 |
IGW
 |
Internet
```

---

# 🛣️ Step 10: Create NAT Gateway

If you want your private EC2 to download updates or packages from the internet, you need a NAT Gateway.

Create `nat-gateway.tf`:

```hcl
resource "aws_eip" "nat" {
  domain = "vpc"

  tags = {
    Name = "terraform-nat-eip"
  }
}

resource "aws_nat_gateway" "main" {
  allocation_id = aws_eip.nat.id
  subnet_id     = aws_subnet.public.id

  depends_on = [
    aws_internet_gateway.main
  ]

  tags = {
    Name = "terraform-nat-gateway"
  }
}
```

Architecture:

```text
Private EC2
     |
Private Route Table
     |
NAT Gateway
     |
Public Subnet
     |
Internet Gateway
     |
Internet
```

The private EC2 can initiate outbound connections but does not receive unsolicited inbound connections from the internet through the NAT Gateway.

---

# 🛣️ Step 11: Create Private Route Table

Add to `route-tables.tf`:

```hcl
resource "aws_route_table" "private" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block     = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.main.id
  }

  tags = {
    Name = "terraform-private-route-table"
  }
}
```

Associate it:

```hcl
resource "aws_route_table_association" "private" {
  subnet_id      = aws_subnet.private.id
  route_table_id = aws_route_table.private.id
}
```

---

# 🔐 Step 12: Create Public Security Group

Create `security-groups.tf`:

```hcl
resource "aws_security_group" "public" {
  name        = "terraform-public-sg"
  description = "Security group for public EC2 instances"
  vpc_id      = aws_vpc.main.id

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["YOUR_PUBLIC_IP/32"]
  }

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "terraform-public-sg"
  }
}
```

Replace:

```text
YOUR_PUBLIC_IP/32
```

with your own public IP.

For example:

```text
203.0.113.10/32
```

Don't use `0.0.0.0/0` for SSH in a production environment.

---

# 🔒 Step 13: Create Private Security Group

Add:

```hcl
resource "aws_security_group" "private" {
  name        = "terraform-private-sg"
  description = "Security group for private EC2"
  vpc_id      = aws_vpc.main.id

  ingress {
    description     = "SSH from public instances"
    from_port       = 22
    to_port         = 22
    protocol        = "tcp"
    security_groups = [aws_security_group.public.id]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "terraform-private-sg"
  }
}
```

This is an important AWS security concept:

```text
Public EC2
    |
    | SSH
    v
Private EC2
```

The Private Security Group allows SSH from the **Public Security Group**, rather than allowing SSH from the entire internet.

---

# 💻 Step 14: Create Public EC2 #1

Create `ec2.tf`:

```hcl
resource "aws_instance" "public_1" {
  ami                         = var.ami_id
  instance_type               = var.instance_type
  subnet_id                   = aws_subnet.public.id
  key_name                    = var.key_name
  associate_public_ip_address = true

  vpc_security_group_ids = [
    aws_security_group.public.id
  ]

  user_data = <<-EOF
              #!/bin/bash
              dnf update -y
              dnf install -y httpd
              systemctl enable httpd
              systemctl start httpd

              echo "<h1>Public EC2 Server 1</h1>" > /var/www/html/index.html
              echo "<p>Deployed using Terraform</p>" >> /var/www/html/index.html
              EOF

  tags = {
    Name = "terraform-public-ec2-1"
  }
}
```

---

# 💻 Step 15: Create Public EC2 #2

Add:

```hcl
resource "aws_instance" "public_2" {
  ami                         = var.ami_id
  instance_type               = var.instance_type
  subnet_id                   = aws_subnet.public.id
  key_name                    = var.key_name
  associate_public_ip_address = true

  vpc_security_group_ids = [
    aws_security_group.public.id
  ]

  user_data = <<-EOF
              #!/bin/bash
              dnf update -y
              dnf install -y httpd
              systemctl enable httpd
              systemctl start httpd

              echo "<h1>Public EC2 Server 2</h1>" > /var/www/html/index.html
              echo "<p>Deployed using Terraform</p>" >> /var/www/html/index.html
              EOF

  tags = {
    Name = "terraform-public-ec2-2"
  }
}
```

---

# 🔒 Step 16: Create Private EC2

Add:

```hcl
resource "aws_instance" "private" {
  ami                         = var.ami_id
  instance_type               = var.instance_type
  subnet_id                   = aws_subnet.private.id
  key_name                    = var.key_name
  associate_public_ip_address = false

  vpc_security_group_ids = [
    aws_security_group.private.id
  ]

  user_data = <<-EOF
              #!/bin/bash
              dnf update -y
              dnf install -y httpd
              systemctl enable httpd
              systemctl start httpd

              echo "<h1>Private EC2 Server</h1>" > /var/www/html/index.html
              EOF

  tags = {
    Name = "terraform-private-ec2"
  }
}
```

---

# 📤 Step 17: Create Terraform Outputs

Create `outputs.tf`:

```hcl
output "vpc_id" {
  value = aws_vpc.main.id
}

output "public_subnet_id" {
  value = aws_subnet.public.id
}

output "private_subnet_id" {
  value = aws_subnet.private.id
}

output "public_ec2_1_public_ip" {
  value = aws_instance.public_1.public_ip
}

output "public_ec2_2_public_ip" {
  value = aws_instance.public_2.public_ip
}

output "private_ec2_private_ip" {
  value = aws_instance.private.private_ip
}

output "nat_gateway_public_ip" {
  value = aws_eip.nat.public_ip
}
```

---

# 🚀 Step 18: Initialize Terraform

Run:

```bash
terraform init
```

You should see Terraform downloading the AWS provider.

---

# 🔍 Step 19: Validate

Run:

```bash
terraform validate
```

Expected:

```text
Success! The configuration is valid.
```

---

# 🧹 Step 20: Format

Run:

```bash
terraform fmt
```

---

# 📋 Step 21: Create Execution Plan

Run:

```bash
terraform plan
```

Terraform will show:

```text
Plan: XX to add, 0 to change, 0 to destroy
```

This is a great point to explain:

> `terraform plan` does not create infrastructure. It only shows what Terraform intends to do.

---

# 🚀 Step 22: Deploy Everything

Run:

```bash
terraform apply
```

Confirm:

```text
yes
```

Terraform will create:

```text
VPC
 |
 +-- Internet Gateway
 |
 +-- Public Subnet
 |     |
 |     +-- Public EC2 #1
 |     |
 |     +-- Public EC2 #2
 |
 +-- Private Subnet
 |     |
 |     +-- Private EC2
 |
 +-- Public Route Table
 |
 +-- Private Route Table
 |
 +-- NAT Gateway
 |
 +-- Public Security Group
 |
 +-- Private Security Group
```

---

# 🔎 Step 23: Verify Infrastructure

Run:

```bash
terraform output
```

You should get:

```text
vpc_id
public_subnet_id
private_subnet_id
public_ec2_1_public_ip
public_ec2_2_public_ip
private_ec2_private_ip
nat_gateway_public_ip
```

---

# 🌐 Step 24: Test Public EC2

Get the public IP:

```bash
terraform output public_ec2_1_public_ip
```

Open:

```text
http://PUBLIC-IP
```

You should see:

```text
Public EC2 Server 1
Deployed using Terraform
```

Test the second:

```text
http://PUBLIC-IP-2
```

You should see:

```text
Public EC2 Server 2
Deployed using Terraform
```

---

# 🔒 Step 25: Connect to Public EC2

From your laptop:

```bash
ssh -i mykey.pem ec2-user@PUBLIC-IP
```

Now you are inside Public EC2.

---

# 🔐 Step 26: Connect to Private EC2

Because Private EC2 has no public IP, you cannot directly connect from the internet.

The recommended demo method is:

```text
Your Laptop
     |
     | SSH
     v
Public EC2
     |
     | SSH
     v
Private EC2
```

For example:

```bash
ssh ec2-user@PRIVATE-IP
```

However, the private EC2 needs the SSH private key to authenticate. For a classroom demo, you can use SSH agent forwarding or another secure approach rather than copying your private key onto the public server.

A cleaner approach is:

```bash
ssh -A -i mykey.pem ec2-user@PUBLIC-IP
```

Then from the public EC2:

```bash
ssh ec2-user@PRIVATE-IP
```

Your exact SSH command depends on your key setup and OS.

---

# 🌍 Step 27: Test Private EC2 Internet Access

Inside Private EC2:

```bash
curl https://www.google.com
```

Or:

```bash
sudo dnf update -y
```

The traffic should flow:

```text
Private EC2
     |
Private Route Table
     |
NAT Gateway
     |
Public Subnet
     |
Internet Gateway
     |
Internet
```

This demonstrates an important AWS networking concept:

> Private EC2 can access the internet **outbound** through NAT Gateway but does not have a public IP and is not directly reachable from the public internet.

---

# 🧪 Step 28: Verify AWS Console

Now open the AWS Console and show students:

### VPC

```text
VPC
10.0.0.0/16
```

### Subnets

```text
Public
10.0.1.0/24

Private
10.0.2.0/24
```

### Internet Gateway

```text
terraform-igw
```

### Route Tables

Public:

```text
0.0.0.0/0 → Internet Gateway
```

Private:

```text
0.0.0.0/0 → NAT Gateway
```

### Security Groups

Public:

```text
SSH → Your IP
HTTP → 0.0.0.0/0
```

Private:

```text
SSH → Public Security Group
```

### EC2

```text
Public EC2 #1
Public IP: YES

Public EC2 #2
Public IP: YES

Private EC2
Public IP: NO
Private IP: YES
```

This is a very good point to explain the difference between **public subnet** and **private subnet**.

---

# 🧠 Important Concept: What Makes a Subnet Public?

A subnet is considered public when its route table has a route to an Internet Gateway:

```text
0.0.0.0/0
      |
      v
Internet Gateway
```

A private subnet does not have a direct route to the Internet Gateway.

Instead:

```text
Private Subnet
      |
      v
NAT Gateway
      |
      v
Internet Gateway
      |
      v
Internet
```

---

# 🧹 Step 29: Destroy the Infrastructure

When your demo is finished:

```bash
terraform destroy
```

Confirm:

```text
yes
```

Terraform will delete the infrastructure it created.

This is one of the biggest benefits of Infrastructure as Code:

```text
terraform apply
        ↓
Create Infrastructure

terraform destroy
        ↓
Delete Infrastructure
```

---

# 🎓 Your Complete Hands-On Class Flow

For your YouTube video or AWS course, I recommend teaching the demo in this order:

### Part 1 — Architecture

```text
VPC
 ├── Public Subnet
 │    ├── EC2-1
 │    └── EC2-2
 │
 └── Private Subnet
      └── EC2-3
```

### Part 2 — Terraform

```text
Provider
   ↓
VPC
   ↓
Subnets
   ↓
Internet Gateway
   ↓
Route Tables
   ↓
NAT Gateway
   ↓
Security Groups
   ↓
EC2
   ↓
Outputs
```

### Part 3 — Commands

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

### Part 4 — Verify

```text
AWS Console
   ↓
VPC
   ↓
Subnets
   ↓
Route Tables
   ↓
Security Groups
   ↓
EC2
```

### Part 5 — Test

```text
Laptop
   ↓
Public EC2
   ↓
Private EC2
```

### Part 6 — Cleanup

```bash
terraform destroy
```

---
