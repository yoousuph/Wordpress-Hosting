# WordPress on AWS EC2 with RDS (MySQL)

This project deploys a WordPress website hosted on an **Amazon EC2 instance** with its database hosted separately on **Amazon RDS (MySQL)**.  
It follows AWS best practices for scalability, maintainability, and security.

---

## 🧩 Architecture Overview

**Components:**
- **Amazon EC2:** Hosts the WordPress application (Apache/PHP)
- **Amazon RDS:** Managed MySQL database instance for WordPress
- **Amazon S3 (Optional):** For media storage (offloading uploads)
- **Amazon Security Groups:** Control inbound/outbound traffic for EC2 and RDS

**Flow:**

---

## 🚀 Setup Steps

### 1. Launch EC2 Instance

- **AMI:** Amazon Linux 2 or Ubuntu 22.04 LTS  
- **Instance Type:** t2.micro (Free Tier) or higher  
- **Security Group Rules:**
  - HTTP: 80 (Anywhere)
  - HTTPS: 443 (Optional)
  - SSH: 22 (Your IP only)
- **Key Pair:** Download and use for SSH access

After launch, SSH into the instance:

```bash
ssh -i "your-key.pem" ec2-user@<EC2-Public-IP>
```

### 2. Install Dependencies on EC2
