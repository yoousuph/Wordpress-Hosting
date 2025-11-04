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
