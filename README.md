# Xskaliber EFT - Managed Enterprise File Transfer

<div align="center">

**The AWS Transfer Family alternative with complete enterprise features**

[Website & Pricing](https://www.xskaliber.com/eft/) • [Getting Started](#-getting-started) • [Tutorials](tutorials/README.md) • [Report a Bug](#-reporting-bugs-and-issues) • [Support](#-support)

</div>

---

## 📌 About This Repository

This repository is the **public interface for Xskaliber EFT customers**. It is used for:

- **Help and getting-started documentation**, including step-by-step [tutorials](tutorials/README.md)
- **[Release notes](release-notes/README.md)** for each published version
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

- **SFTP server**: SSH key and/or password auth, clustering behind a load balancer, per-partner IP allow-lists
- **Web interface**: Trading partner portal, admin dashboard, RBAC with tenant isolation, job monitoring, audit log
- **Trading partner management**: Per-partner configuration, scheduled pull/push jobs over SFTP, FTP and FTPS, archival policies
- **File processing**: PGP encryption/decryption, GZIP/BZIP2/ZIP compression, ClamAV virus scanning with automatic definition updates, retrying job queue
- **Storage**: AWS S3 (provisioned by the stack)
- **Administration**: Guided first-run setup and Getting Started checklist, UI-managed configuration, cluster health monitoring, PGP key management, AWS Secrets Manager integration, in-app update notifications
- **Security**: No default passwords, per-install SFTP host keys, host-key pinning for partner servers, per-partner IP allow-lists, OIDC single sign-on
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

Xskaliber EFT is sold through **AWS Marketplace** as a container product for Amazon ECS, launched with a CloudFormation template. It deploys into **your own AWS account**, so your data never leaves your environment. Pricing is a fixed monthly fee billed by AWS. See editions and pricing at **[xskaliber.com/eft](https://www.xskaliber.com/eft/)**.

### 1. Subscribe on AWS Marketplace

Find **Xskaliber EFT** in AWS Marketplace and subscribe. Marketplace grants your account pull access to the container images, and the running installation confirms your subscription automatically, so no separate license key is needed.

### 2. Prerequisites

- An AWS account and region (the container images are hosted in `us-east-1` Marketplace ECR)
- Permissions to create CloudFormation stacks, IAM roles, VPC, ECS, Aurora, S3, ALB/NLB and Secrets Manager resources
- *(Recommended for production)* An issued **ACM certificate** in the target region for HTTPS, plus a Route 53 hosted zone if you want a DNS alias
- Outbound HTTPS access from the stack's private subnets (see [Network access](#network-access)). A new VPC created by the stack already has this.

### 3. Launch the CloudFormation stack

From your Marketplace subscription, choose **Continue to Launch** and open the version's **deployment template** (Launch Stack link). Fill in the parameters:

| Parameter | Purpose |
|-----------|---------|
| `DeploymentName` | Short identifier (3-32 lowercase letters, digits, hyphens) used to prefix resources. Choose it once; don't rename it later. |
| `DeploymentSize` | `small`, `medium` or `large` (sizes the database, backend, frontend and SFTP nodes) |
| `CertificateArn` | ACM certificate for HTTPS. If empty the UI is served over plain HTTP, which is for **evaluation only**. |
| `AlbAllowedCidr` / `SftpAllowedCidr` | Restrict who can reach the web UI and SFTP endpoint (defaults to `0.0.0.0/0`) |
| `CreateNewVpc` | Create a new VPC (default), or set to `false` and supply `ExistingVpcId` and the public/private subnet IDs |
| `EnableMultiAzRds` | Multi-AZ database for high availability |
| `DatabaseDeletionProtection` | Protects the database from accidental deletion (default `true`) |
| `HostedZoneId` / `DomainName` | Optional Route 53 alias record |
| `AlarmNotificationEmail` | Optional CloudWatch alarm notifications |

Leave `TemplateBucketUrl` and the container image parameters at their defaults unless support tells you otherwise. They are pre-set for the version you are launching.

The stack provisions the VPC, Aurora Serverless v2 (PostgreSQL), S3 storage, generated secrets, and ECS services for the backend, frontend and SFTP server, behind an Application Load Balancer (web UI) and a dedicated Network Load Balancer (SFTP). All application secrets are generated for you.

### 4. Run first-time setup

When the stack reaches `CREATE_COMPLETE`, open its **Outputs** tab:

| Output | Use |
|--------|-----|
| **ApplicationURL** | The web UI |
| **SetupURL** | The first-run setup wizard |
| **SetupTokenLogs** | Link to the backend logs containing the one-time setup token |
| **SftpEndpoint** | The hostname for partner SFTP connections |

There is **no default administrator password**. Open **SetupTokenLogs** to copy the one-time setup token, then open **SetupURL** and create your first administrator. The [first tutorial](tutorials/01-first-login-and-console-tour.md) walks through it, and the in-app **Getting Started** checklist takes you through the rest.

If you did not set a domain, point a DNS name at the endpoints before onboarding partners.

### Network access

The installation makes these outbound HTTPS (443) connections. A stack that creates its own VPC allows them through a NAT gateway. If you deploy into an existing VPC or filter egress through a proxy or firewall, allow:

| Destination | Purpose |
|-------------|---------|
| AWS service endpoints in your region, and AWS Marketplace in `us-east-1` | Container images, storage, secrets, logs and subscription checks |
| `database.clamav.net` | Virus definition updates, several times a day |
| `raw.githubusercontent.com` | Daily check for new Xskaliber EFT releases ([manifest.json](manifest.json) in this repository). Optional; nothing breaks if blocked, and it can be turned off under **System Settings → Updates**. |
| Your trading partners' servers | Partner jobs that pull from or push to partner SFTP/FTP/FTPS servers |

## 🔄 Upgrading

When a new release is available, administrators see an **Update Available** banner in the console. Read the [release notes](release-notes/README.md) for that version first: they list anything you need to do before or after upgrading.

1. In AWS Marketplace, open your subscription and copy the **deployment template** URL for the new version.
2. In CloudFormation, select your stack and choose **Update stack → Replace existing template**, then paste that URL.
3. On the parameters page, keep your existing values **except** `TemplateBucketUrl`, `BackendImageTag`, `FrontendImageTag` and `SftpImageTag`. CloudFormation offers your previous values for these; replace them with the new template's defaults, which point at the new version.
4. Submit the update. ECS replaces the containers one service at a time, and database changes are applied automatically when the new backend starts.

The version you are running is shown in the console footer and on the **About** page.

## 🧹 Removing a deployment

Delete the stack in CloudFormation. Your S3 data bucket and a final database snapshot are retained by default so nothing is deleted silently. Remove them manually once you no longer need them. If `DatabaseDeletionProtection` is on, turn it off with a stack update before deleting. If a first launch failed and the stack is stuck, turn off deletion protection on the Aurora cluster in the RDS console, then delete the stack.

## 📏 Deployment sizing

| Size | Database (Aurora ACU) | Backend | SFTP node (max nodes) |
|------|----------------------|---------|-----------------------|
| small | 0.5-4 | 0.5 vCPU / 2 GB | t3.small (2) |
| medium | 1-8 | 1 vCPU / 2 GB | t3.medium (4) |
| large | 2-16 | 2 vCPU / 4 GB | t3.large (6) |

The backend includes the ClamAV virus scanner, which keeps about 1 GB of virus definitions in memory.

## 📝 Release notes

Release notes for every published version are in **[release-notes/](release-notes/README.md)**. The latest release is **[1.0.3](release-notes/v1.0.3.md)**.

## 📖 Tutorials

Once your stack is running, follow the step-by-step **[tutorials](tutorials/README.md)**:

1. [First-run setup and console tour](tutorials/01-first-login-and-console-tour.md)
2. [Tenants and users](tutorials/02-tenants-and-users.md)
3. [Onboard a trading partner](tutorials/03-onboard-a-trading-partner.md)
4. [Restrict access with IP ACLs](tutorials/04-ip-access-control.md)
5. [SFTP users and SSH keys](tutorials/05-sftp-users-and-ssh-keys.md)
6. [PGP keys](tutorials/06-pgp-keys.md)
7. [Automate transfers with partner jobs](tutorials/07-partner-jobs.md)
8. [Monitoring and audit](tutorials/08-monitoring-and-audit.md)
9. [System settings](tutorials/09-system-settings.md)
10. [Single sign-on (SSO)](tutorials/10-single-sign-on.md)
11. [Using the web portal](tutorials/11-web-user-portal.md)

## 🐞 Reporting Bugs and Issues

Found a problem or have a feature request? Please [open an issue](https://github.com/xskaliber/eft/issues/new) in this repository.

Before opening one, search [existing issues](https://github.com/xskaliber/eft/issues) to see if it has already been reported. A good report includes:

- Xskaliber EFT version (shown in the console footer and on the **About** page) and AWS region
- Deployment size, and whether you deployed into a new or existing VPC
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
