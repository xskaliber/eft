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
![Admin Dashboard](https://github.com/xskaliber/eft/blob/main/images/AdminDashboard.png)

### Server Monitoring
![Server Monitoring](https://github.com/xskaliber/eft/blob/main/images/SeverMonitoring.png)

### Activity Log
![Activity Log](https://github.com/xskaliber/eft/blob/main/images/ActivityLog.png)

### Web User Portal
![Web User Dashboard](https://github.com/xskaliber/eft/blob/main/images/WebUserDashboard.png)

## 🚀 Getting Started

Xskaliber EFT is sold through **AWS Marketplace** as a container product with **CloudFormation delivery**. It deploys into **your own AWS account**, so your data never leaves your environment. See editions and pricing at **[xskaliber.com/eft](https://www.xskaliber.com/eft/)**.

### 1. Subscribe on AWS Marketplace

Find **Xskaliber EFT** in AWS Marketplace and subscribe. Marketplace grants your account pull access to the container images and meters usage automatically, so no separate license key is needed.

### 2. Prerequisites

- An AWS account and region (the container images are hosted in `us-east-1` Marketplace ECR)
- Permissions to create CloudFormation stacks, IAM roles, VPC, ECS, Aurora, S3, ALB/NLB and Secrets Manager resources
- *(Recommended for production)* An issued **ACM certificate** in the target region for HTTPS, plus a Route 53 hosted zone if you want a DNS alias

### 3. Launch the CloudFormation stack

Choose **Launch CloudFormation template** from your Marketplace subscription and fill in the parameters:

| Parameter | Purpose |
|-----------|---------|
| `DeploymentName` | Short identifier (3-32 lowercase letters, digits, hyphens) used to prefix resources. Choose it once; don't rename it later. |
| `DeploymentSize` | `small`, `medium` or `large` (sizes the database, backend, frontend and SFTP nodes) |
| `CertificateArn` | ACM certificate for HTTPS. If empty the UI is served over plain HTTP, which is for **evaluation only**. |
| `AlbAllowedCidr` / `SftpAllowedCidr` | Restrict who can reach the web UI and SFTP endpoint (defaults to `0.0.0.0/0`) |
| `CreateNewVpc` | Create a new VPC (default), or set to `false` and supply `ExistingVpcId` and the public/private subnet IDs |
| `EnableMultiAzRds` | Multi-AZ database for high availability |
| `EnableLambdaFileProcessing` | Optional serverless file-processing add-on |
| `HostedZoneId` / `DomainName` | Optional Route 53 alias record |
| `AlarmNotificationEmail` | Optional CloudWatch alarm notifications |

Leave the container image and product code parameters at their defaults unless support tells you otherwise.

The stack provisions the VPC, Aurora Serverless v2 (PostgreSQL), S3 storage, generated secrets, and ECS services for the backend, frontend and SFTP server, behind an Application Load Balancer (web/API) and a dedicated Network Load Balancer (SFTP).

### 4. Access your installation

When the stack reaches `CREATE_COMPLETE`, open its **Outputs** tab:

- **ApplicationURL**: the web UI
- **SftpEndpoint**: the hostname for partner SFTP connections

Sign in to the web UI as the initial administrator and **change the default admin password immediately**. If you did not set a domain, point a DNS name at the endpoints before onboarding partners.

### Upgrading

Update the stack from the AWS console with the new image tags for the new release (`BackendImageTag`, `FrontendImageTag`, `SftpImageTag`). Release notes are announced on the Marketplace listing.

### Removing a deployment

Delete the stack in CloudFormation. Your S3 data bucket and a final database snapshot are retained by default so nothing is deleted silently. Remove them manually once you no longer need them.

### Deployment sizing

| Size | Database (Aurora ACU) | Backend | SFTP node |
|------|----------------------|---------|-----------|
| small | 0.5-4 | 0.5 vCPU / 1 GB | t3.small |
| medium | 1-8 | 1 vCPU / 2 GB | t3.medium |
| large | 2-16 | 2 vCPU / 4 GB | t3.large |

## 🐞 Reporting Bugs and Issues

Found a problem or have a feature request? Please [open an issue](https://github.com/xskaliber/eft/issues/new) in this repository.

Before opening one, search [existing issues](https://github.com/xskaliber/eft/issues) to see if it has already been reported. A good report includes:

- Xskaliber EFT version (image tags) and AWS region
- Deployment size and whether the Lambda file-processing add-on is enabled
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
