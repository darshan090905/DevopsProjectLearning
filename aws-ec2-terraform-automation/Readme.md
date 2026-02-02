# AWS EC2 Infrastructure Automation with Terraform

This project automates the deployment of a secure Ubuntu web server on AWS using Terraform. It includes remote state management, automated software provisioning, and dynamic security group configurations.

---

## 🏗️ Architecture

The infrastructure is defined as code (IaC) to ensure consistency across deployments:

- **Compute**: AWS EC2 Instance (t3.micro)
- **OS**: Ubuntu Jammy 22.04 LTS (Dynamically fetched via Data Source)
- **Security**: Custom Security Group with SSH and HTTP ingress rules
- **State Management**: Remote S3 backend for state storage and locking
- **Provisioning**: Automated setup using remote-exec and local-exec

---

## 📂 Project Structure

| File/Folder   | Purpose |
|---------------|----------|
| backend.tf    | Configures S3 bucket (terraformstate32456) for state storage |
| Instance.tf   | Defines EC2 instance and provisioning |
| InstID.tf     | Fetches latest Ubuntu AMI using data source |
| Keypair.tf    | Uploads SSH public key to AWS |
| SecGrp.tf     | Manages security group rules (22, 80) |
| provider.tf   | Configures AWS provider and region |
| dovekey       | Private SSH key for instance access |

---

## 🚀 Getting Started

### Prerequisites

1. AWS CLI configured using `aws configure`
2. S3 bucket `terraformstate32456` created in `us-east-1`
3. `web.sh` script present in project root directory

---

### Deployment Steps

#### 1. Initialize Terraform

```bash
terraform init
```

#### 2. Plan Infrastructure

```bash
terraform plan
```

#### 3. Apply Configuration

```bash
terraform apply -auto-approve
```

---

## 🛠️ Technical Details

### Automated Provisioning

The following steps run automatically after EC2 creation:

1. Copies `web.sh` to `/tmp` directory
2. Grants execute permission and runs script using sudo
3. Saves private IP to `private_ips.txt`

---

### Security Groups

#### Ingress Rules

- TCP 22 (SSH) → 0.0.0.0/0
- TCP 80 (HTTP) → 0.0.0.0/0

#### Egress Rules

- Allows all outbound IPv4 and IPv6 traffic

---

## 📊 Outputs

After successful deployment, Terraform displays:

- `WebPublicIP`  → Public IP of web server
- `WebPrivateIP` → Private IP of instance
- `instance_id`  → EC2 instance ID

---

## 📌 Notes

- Do not commit private keys to GitHub
- Use `.gitignore` for sensitive files
- Always review `terraform plan` before apply

---


