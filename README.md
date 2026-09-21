# Xskaliber EFT - Managed Enterprise File Transfer

<div align="center">

**The AWS Transfer Family alternative with complete enterprise features**

[Website & Pricing](https://www.xskaliber.com/eft/) • [Getting Started](#-getting-started) • [Report a Bug](#-reporting-bugs-and-issues) • [Support](#-support)

</div>

---

## 📌 About This Repository

This repository is the **public interface for Xskaliber EFT customers**. It is used for:

- **Help and getting-started documentation**
- **Capturing bugs, issues and feature requests** from customers

It does **not** contain product source code. Pricing, editions and detailed guidance are hosted at **[xskaliber.com/eft](https://www.xskaliber.com/eft/)**.

## 🎯 Overview

Xskaliber EFT is a production-ready, enterprise file transfer platform that provides AWS Transfer Family-comparable capabilities at a fraction of the cost, with complete infrastructure control.

| Feature | AWS Transfer Family | Xskaliber EFT |
|---------|---------------------|---------------|
| **Web UI** | ❌ None | ✅ Full admin & user portal |
| **Trading Partner Management** | ❌ Manual | ✅ Integrated workflow |
| **Data Pipeline** | ❌ Separate service | ✅ Built-in processing |
| **Monitoring** | Basic CloudWatch | ✅ Real-time cluster monitoring |
| **File Processing** | ❌ None | ✅ Encryption, compression, scanning |
| **Multi-tenant** | Limited | ✅ Complete isolation |

## ✨ Key Features

- **SFTP server**: SSH key and/or password auth, clustering behind a load balancer, per-partner IP whitelisting, optional 2FA
- **Web interface**: Trading partner portal, admin dashboard, RBAC with tenant isolation, job monitoring, audit log
- **Trading partner management**: Per-partner configuration, scheduled polling jobs, notifications, retention and archival policies
- **File processing**: PGP encryption/decryption, GZIP compression, ClamAV virus scanning, retrying job queue, optional AWS Lambda offload
- **Storage**: AWS S3, AWS EFS, MinIO (S3-compatible), or a hybrid per tenant/partner
- **Administration**: UI-managed configuration, license management, cluster health monitoring, PGP key management, AWS Secrets Manager integration
- **Compliance support**: Audit trails supporting SOC 2, HIPAA, GDPR and PCI DSS requirements

## 🎨 Screenshots

### Admin Dashboard
![Admin Dashboard](https://github.com/xskaliber/eft/blob/main/AdminDashboard.png)

### Server Monitoring
![Server Monitoring](https://github.com/xskaliber/eft/blob/main/SeverMonitoring.png)

### Activity Log
![Activity Log](https://github.com/xskaliber/eft/blob/main/ActivityLog.png)

### Web User Portal
![Web User Dashboard](https://github.com/xskaliber/eft/blob/main/WebUserDashboard.png)

## 🚀 Getting Started

1. **Get a license** - see editions, pricing and the free trial at **[xskaliber.com/eft](https://www.xskaliber.com/eft/)**, or email [sales@xskaliber.com](mailto:sales@xskaliber.com).
2. **Review the prerequisites**
   - Docker & Docker Compose (20.10+)
   - PostgreSQL 15+ (provided via Docker or a managed service)
   - 4GB RAM minimum (8GB recommended for production)
   - A valid Xskaliber EFT license key
   - AWS account (optional, for S3/EFS storage)
3. **Follow the installation and deployment guidance** at [xskaliber.com/eft](https://www.xskaliber.com/eft/) (Docker Compose, AWS ECS Fargate, storage backends, processing modes).
4. **Sign in** to the web UI and **change the default admin password immediately**.

### Deployment Options

- **Cloud**: AWS ECS Fargate or EKS, auto-scaling, RDS, multi-AZ high availability
- **On-premise**: Docker Compose on your own servers, VMware or bare metal

## 🐞 Reporting Bugs and Issues

Found a problem or have a feature request? Please [open an issue](https://github.com/xskaliber/eft/issues/new) in this repository.

Before opening one, search [existing issues](https://github.com/xskaliber/eft/issues) to see if it has already been reported. A good report includes:

- Xskaliber EFT version and deployment type (Docker Compose, ECS, on-premise)
- Storage backend and processing mode in use
- Steps to reproduce, expected behavior and actual behavior
- Relevant logs or screenshots (**remove passwords, keys, license keys and partner data first**)

See [bug_report.md](bug_report.md) for the full template.

> 🔒 **Security vulnerabilities**: do not post these publicly. Email [security@xskaliber.com](mailto:security@xskaliber.com).

## 💬 Support

- **Documentation and guidance**: [xskaliber.com/eft](https://www.xskaliber.com/eft/)
- **Bugs and feature requests**: [GitHub Issues](https://github.com/xskaliber/eft/issues)
- **Support**: [support@xskaliber.com](mailto:support@xskaliber.com) (response times depend on your edition)

## 📧 Contact

- **Sales**: sales@xskaliber.com
- **Support**: support@xskaliber.com
- **Security**: security@xskaliber.com

---

<div align="center">

© 2026 Xskaliber Software. All rights reserved.

</div>
