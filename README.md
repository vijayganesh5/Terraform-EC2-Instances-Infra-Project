# 🌍 Launch Linux EC2 Instances in Two Regions using Terraform

## 🧠 Overview

In this task, you’ll use **Terraform** to **automate the creation of two Linux EC2 instances** — each in a **different AWS region** — using a **single Terraform configuration file**.

Terraform helps you manage your infrastructure as code, so you don’t have to manually launch instances in the AWS console.

---

## ⚙️ Tech Stack

* ☁️ **AWS EC2** – Virtual machines in the cloud
* 🏗️ **Terraform** – Infrastructure as Code (IaC) tool
* 💻 **AWS CLI** – To authenticate and configure credentials

---

## 🧩 Prerequisites

Before you start, make sure you have:

1. 🪟 **AWS EC2 Ubuntu instance** (to perform the task)

2. 🧑‍💻 **Terraform** installed →

   ```bash
   sudo apt update
   sudo apt install -y unzip
   wget https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip
   unzip terraform_1.6.6_linux_amd64.zip
   sudo mv terraform /usr/local/bin/
   terraform -version
   ```

3. 🔑 **AWS CLI** configured →

   ```bash
   aws configure
   ```

   Provide:

   * AWS Access Key ID
   * AWS Secret Access Key
   * Default region (e.g., ap-south-1)
   * Output format: json

4. 🧾 **IAM user** with EC2 permissions

---

## 🏗️ Steps to Perform the Task

### 1️⃣ Create a Terraform Working Directory

```bash
mkdir terraform-multi-region-ec2
cd terraform-multi-region-ec2
```

### 2️⃣ Create the Terraform Configuration File

Create a file named `main.tf`

```hcl
provider "aws" {
  region = "ap-south-1"
}

provider "aws" {
  alias  = "us"
  region = "us-east-1"
}

resource "aws_instance" "india_ec2" {
  ami           = "ami-0dee22c13ea7a9a67"
  instance_type = "t2.micro"
  tags = {
    Name = "India-EC2"
  }
}

resource "aws_instance" "us_ec2" {
  provider      = aws.us
  ami           = "ami-0866a3c8686eaeeba"
  instance_type = "t2.micro"
  tags = {
    Name = "US-EC2"
  }
}
```

---

### 3️⃣ Initialize Terraform

```bash
terraform init
```

---

### 4️⃣ Validate the Configuration

```bash
terraform validate
```

---

### 5️⃣ Plan the Deployment

```bash
terraform plan
```

This shows what Terraform will create.

---

### 6️⃣ Apply the Configuration

```bash
terraform apply -auto-approve
```

Terraform will launch two EC2 instances — one in **ap-south-1** and another in **us-east-1**.

---

### 7️⃣ Verify in AWS Console

✅ Go to the **EC2 dashboard** → Select **Mumbai (ap-south-1)** and **N. Virginia (us-east-1)** regions → You’ll see one EC2 instance in each region.

---

## 🧹 Cleanup – Destroy the Resources

Once testing is done, delete everything to avoid charges:

```bash
terraform destroy -auto-approve
```

---

## 🚀 Expected Output

* Two EC2 instances successfully launched — one in **India (ap-south-1)** and one in **US (us-east-1)**.
* Instances visible in their respective regional dashboards.

---

## 💡 Key Learning

✅ Learn how to:

* Use **multiple providers** in Terraform
* Deploy resources in **different AWS regions** using one config file
* Manage AWS infrastructure efficiently through **Infrastructure as Code**

---

## 🎉 Output Link with Screenshots:
- https://docs.google.com/document/d/13XJ7WoDAvJjtE6tgVGaMZm-ob9fVF77v_iaJ8qguEnU/edit?usp=drive_link

---


