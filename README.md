# Xskaliber EFT - Managed Enterprise File Transfer

<div align="center">

[![Docker](https://img.shields.io/badge/Docker-Hub-2496ED?logo=docker)](https://hub.docker.com/r/yourorg/meft)
[![AWS Compatible](https://img.shields.io/badge/AWS-Compatible-FF9900?logo=amazon-aws)](https://aws.amazon.com)
[![License](https://img.shields.io/badge/license-Commercial-blue.svg)](LICENSE)

**The AWS Transfer Family alternative with complete enterprise features**

[Features](#-key-features) • [Quick Start](#-quick-start) • [Pricing](#-pricing) • [Documentation](#-documentation) • [Support](#-support)

</div>

---

## 🎯 Overview

Xskaliber EFT is a **production-ready, enterprise file transfer platform** designed to provide AWS Transfer Family-comparable capabilities at a fraction of the cost. Perfect for enterprises requiring secure B2B file transfers with complete infrastructure control.

### Why Choose Xskaliber EFT?

| Feature | AWS Transfer Family | Xskaliber EFT |
|---------|---------------------|------|
| **Monthly Cost (100 users)** | ~$2,160 + data transfer | ~$842-942 (67% savings) |
| **Web UI** | ❌ None | ✅ Full admin & user portal |
| **Trading Partner Management** | ❌ Manual | ✅ Integrated workflow |
| **Data Pipeline** | ❌ Separate service | ✅ Built-in processing |
| **Monitoring** | Basic CloudWatch | ✅ Real-time cluster monitoring |
| **File Processing** | ❌ None | ✅ Encryption, compression, scanning |
| **Multi-tenant** | Limited | ✅ Complete isolation |
| **Setup Time** | Hours | ✅ 15 minutes |

## ✨ Key Features

### 🔐 Enterprise-Grade SFTP Server
- **Multi-protocol support**: SFTP with SSH key and/or password authentication
- **High availability**: Cluster-ready with load balancer support
- **Auto-scaling**: Deploy behind AWS Network Load Balancer for elastic scaling
- **Session monitoring**: Real-time tracking of active connections across cluster
- **IP whitelisting**: Per-partner access control lists (ACLs)
- **Multi-factor authentication**: Optional 2FA support

### 🌐 Modern Web Interface
- **Trading Partner Portal**: Self-service file upload/download interface
- **Admin Dashboard**: Complete control center with real-time metrics
- **User Management**: Role-based access control (RBAC) with tenant isolation
- **Job Monitoring**: Real-time visibility into file processing pipelines
- **Activity Audit**: Comprehensive logging of all user actions for compliance
- **Mobile Responsive**: Access from any device

### 💼 Trading Partner Management
- **Partner Configuration**: Define partners with custom settings per relationship
- **Scheduled Jobs**: Automated file polling and processing workflows
- **Metadata Tracking**: Full lineage tracking for compliance requirements
- **Notification System**: Email alerts for file arrivals, processing status, errors
- **Dynamic Lifecycle**: Configurable file retention and archival policies
- **Batch Operations**: Process multiple files with single configuration

### 📦 Advanced File Processing
- **PGP Encryption/Decryption**: Industry-standard asymmetric encryption
- **Compression**: GZIP compression with configurable levels
- **Virus Scanning**: ClamAV integration with automatic quarantine
- **Job Queue**: PostgreSQL-backed queue with automatic retry logic
- **Lambda Integration**: Optionally offload processing to AWS Lambda for infinite scale
- **Error Handling**: Intelligent retry with exponential backoff

### ☁️ Cloud-Native Storage
- **AWS S3 Integration**: Direct integration with S3 for object storage
- **AWS EFS Support**: Shared filesystem across SFTP cluster nodes
- **MinIO Compatibility**: Use MinIO for S3-compatible on-premise storage
- **Hybrid Storage**: Mix storage types per tenant or partner
- **Automatic Provisioning**: Storage backends configured via environment variables

### 🎛️ System Administration
- **Database-Backed Configuration**: Manage settings via UI without restarts
- **License Management**: Flexible licensing for your deployment size
- **Server Cluster Monitoring**: Real-time health metrics for all nodes
- **PGP Key Management**: Centralized key storage and rotation
- **Secure Secrets**: Integration with AWS Secrets Manager
- **Audit Compliance**: Complete audit trails for SOC 2, HIPAA, GDPR

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Network Load Balancer                     │
│                    (Port 22 - SFTP Traffic)                  │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┬────────────────┐
        │            │            │                │
    ┌───▼───┐   ┌───▼───┐   ┌───▼───┐      ┌────▼────┐
    │ SFTP  │   │ SFTP  │   │ SFTP  │ ...  │  SFTP   │
    │ Node 1│   │ Node 2│   │ Node 3│      │  Node N │
    └───┬───┘   └───┬───┘   └───┬───┘      └────┬────┘
        └────────────┼────────────┴──────────────┘
                     │
        ┌────────────▼────────────────────────────────┐
        │     Shared Storage (S3, EFS, MinIO)         │
        └─────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│              Application Load Balancer (HTTPS)               │
│                    (Web UI & API Traffic)                    │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┬────────────────┐
        │            │            │                │
    ┌───▼───┐   ┌───▼───┐   ┌───▼───┐      ┌────▼────┐
    │Backend│   │Backend│   │Backend│ ...  │ Backend │
    │ API 1 │   │ API 2 │   │ API 3 │      │  API N  │
    └───┬───┘   └───┬───┘   └───┬───┘      └────┬────┘
        │            │            │                │
        └────────────┼────────────┴────────────────┘
                     │
        ┌────────────▼────────────────────────────────┐
        │      PostgreSQL RDS (Multi-AZ)          │
        └──────────────────────────────────────────────┘
```

### Deployment Options

**Cloud Deployment (Recommended)**
- AWS ECS Fargate or EKS
- Auto-scaling based on load
- Managed database (RDS)
- High availability across multiple AZs

**On-Premise Deployment**
- Docker Compose on your servers
- VMware or bare metal
- Use existing infrastructure
- Complete data sovereignty


## 📋 Prerequisites

- Docker & Docker Compose (20.10+)
- PostgreSQL 15+ (provided via Docker or managed service)
- 4GB RAM minimum (8GB recommended for production)
- Valid MEFT license key
- AWS Account (optional - for S3/EFS storage)

## 🚀 Quick Start

### 1. Request Your License

**[Contact us for a license key →](mailto:sales@xskaliber.com)**

Available editions:
- **Starter**: Up to 10 trading partners - $299/month
- **Professional**: Up to 100 users - $999/month  
- **Enterprise**: Unlimited users - Custom pricing
- **Trial**: 30-day free trial available

### 2. Download MEFT

```bash
# Create deployment directory
mkdir meft-deployment
cd meft-deployment

# Download docker-compose configuration
curl -o docker-compose.yml https://releases.yourcompany.com/meft/latest/docker-compose.yml

# Download environment template
curl -o .env https://releases.yourcompany.com/meft/latest/.env.example
```

### 3. Configure Environment

Edit `.env` file with your settings:

```bash
# Database Configuration
DB_CONNECTION_URL=postgres://postgres:yourpassword@db:5432/meft?sslmode=disable

# Storage Configuration
STORAGE_TYPE=s3  # Options: local, s3, efs
S3_BUCKET=your-meft-bucket
S3_REGION=us-east-1

# Application URLs
NEXTAUTH_URL=https://yourdomain.com
BACKEND_URL=http://backend:8080
```

### 4. Start MEFT

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Verify all services are running
docker-compose ps
```

### 5. Access Your Installation

- **Web UI**: http://localhost:3000 (or your configured domain)
- **SFTP**: Port 22 (sftp username@yourdomain.com)

**Default admin credentials:**
- Email: `admin@example.com`
- Password: `admin123`

⚠️ **Change default password immediately after first login**

## ⚙️ Configuration

### Storage Backends

#### AWS S3 (Production Recommended)
```bash
STORAGE_TYPE=s3
S3_BUCKET=your-meft-bucket
S3_REGION=us-east-1
S3_ACCESS_KEY=<your access key>
S3_SECRET_KEY=<your secrets key>
```

#### AWS EFS (Multi-Node SFTP)
```bash
STORAGE_TYPE=efs
USER_DATA_MOUNT_POINT=/mnt/efs/sftp-users
# EFS mounted via Docker volumes
```

#### MinIO (On-Premise S3-Compatible)
```bash
STORAGE_TYPE=s3
S3_ENDPOINT=http://minio:9000
S3_BUCKET=meft-storage
S3_ACCESS_KEY=minioadmin
S3_SECRET_KEY=minioadmin
S3_USE_SSL=false
```

### Database Configuration

**Development:**
```bash
DB_CONNECTION_URL=postgres://postgres:postgres@db:5432/meft?sslmode=disable
```

**Production (AWS RDS):**
```bash
DB_CONNECTION_URL=postgres://admin:SecurePass123@meft-prod.abc123.us-east-1.rds.amazonaws.com:5432/meft?sslmode=require
```

### Processing Mode

**Direct Processing** (simpler, included in backend):
```bash
PROCESSING_MODE=direct
```

**Lambda Processing** (scalable, optional add-on):
```bash
PROCESSING_MODE=lambda
LAMBDA_ENCRYPTION_ARN=arn:aws:lambda:...
LAMBDA_DECRYPTION_ARN=arn:aws:lambda:...
```

## 🚢 Deployment to AWS

### Option 1: ECS Fargate (Recommended)

We provide Terraform templates for one-click AWS deployment:

```bash
# Download deployment package
curl -LO https://releases.yourcompany.com/meft/latest/aws-deployment.tar.gz
tar -xzf aws-deployment.tar.gz
cd aws-deployment

# Configure
cp terraform.tfvars.example terraform.tfvars
# Edit terraform.tfvars with your settings

# Deploy
terraform init
terraform plan
terraform apply
```

**What gets deployed:**
- VPC with public/private subnets
- Network Load Balancer (SFTP)
- Application Load Balancer (Web/API)
- ECS Fargate cluster with auto-scaling
- RDS PostgreSQL Multi-AZ
- EFS for shared storage
- CloudWatch monitoring

**Estimated monthly cost:** $500-800 for small deployments

### Option 2: Docker Compose on EC2

For simpler deployments:

```bash
# Launch EC2 instance (t3.large or larger)
# Install Docker and Docker Compose

# Download and configure
wget https://releases.yourcompany.com/meft/latest/docker-compose.yml
wget https://releases.yourcompany.com/meft/latest/.env.example
cp .env.example .env
# Edit .env

# Start
docker-compose up -d

# Setup HTTPS (optional)
sudo certbot --nginx -d yourdomain.com
```

## 🎨 Screenshots

### Admin Dashboard
![Admin Dashboard](https://releases.yourcompany.com/meft/screenshots/dashboard.png)

### Trading Partner Management
![Partner Management](https://releases.yourcompany.com/meft/screenshots/partners.png)

### File Processing Jobs
![Job Monitoring](https://releases.yourcompany.com/meft/screenshots/jobs.png)

### User Portal
![User Files](https://releases.yourcompany.com/meft/screenshots/user-portal.png)

## 📚 Documentation

- **[Installation Guide](https://docs.yourcompany.com/meft/installation)** - Detailed setup instructions
- **[Configuration Reference](https://docs.yourcompany.com/meft/configuration)** - All configuration options
- **[AWS Deployment Guide](https://docs.yourcompany.com/meft/aws-deployment)** - ECS/EKS setup
- **[Storage Configuration](https://docs.yourcompany.com/meft/storage)** - S3, EFS, MinIO setup
- **[Admin Guide](https://docs.yourcompany.com/meft/admin)** - Managing users and partners
- **[API Reference](https://docs.yourcompany.com/meft/api)** - REST API documentation
- **[Troubleshooting](https://docs.yourcompany.com/meft/troubleshooting)** - Common issues

## 🏢 Use Cases

### Enterprise B2B File Transfer
Replace expensive EDI/MFT solutions:
- **Healthcare**: HIPAA-compliant patient data exchange
- **Finance**: PCI-compliant transaction file processing  
- **Retail**: Automated inventory and order file transfers
- **Manufacturing**: Supply chain integration with partners
- **Logistics**: Real-time shipment data exchange

### Secure Partner Onboarding
- Create partner accounts with isolated directories
- Generate and distribute SFTP credentials securely
- Configure automated file processing pipelines
- Monitor file arrivals and processing status in real-time
- Send notifications on success/failure

### Automated Data Pipelines
- Poll partner SFTP servers on schedules
- Decrypt incoming encrypted files automatically
- Decompress archives
- Scan for viruses before processing
- Transform and route to downstream systems
- Archive with configurable retention policies

## 🔒 Security & Compliance

MEFT includes enterprise-grade security features:

✅ **Transport Encryption**: TLS 1.3 for HTTPS, SSH for SFTP  
✅ **Data Encryption**: PGP/GPG encryption for files at rest  
✅ **Key Management**: AWS Secrets Manager integration  
✅ **Authentication**: Multi-factor support, SSH keys + passwords  
✅ **Authorization**: Role-based access control (RBAC)  
✅ **Audit Logging**: Complete user activity tracking  
✅ **IP Whitelisting**: Per-partner ACL support  
✅ **Virus Scanning**: Real-time malware detection  

**Compliance Support:**
- **GDPR**: Data access logs, deletion capabilities
- **HIPAA**: Encryption, audit trails, access controls
- **SOC 2**: Logging, monitoring, access management  
- **PCI DSS**: Encrypted storage, access controls, monitoring

## 📊 Scalability & Performance

### Horizontal Scaling

- **SFTP**: 1000+ concurrent connections per node
- **API**: < 100ms average response time
- **Processing**: Scales with Lambda or backend capacity
- **Database**: 10,000+ queries/second with RDS

### Performance Metrics

Tested with real-world workloads:
- 500 concurrent SFTP users
- 10,000 files/hour throughput
- 99.9% uptime SLA
- < 2 second file processing start time

## 💰 Pricing

### Starter Edition
**$299/month** or **$2,990/year** (save 17%)
- Up to 10 users
- 100GB storage included
- Community support
- All core features
- Perfect for small teams

### Professional Edition  
**$999/month** or **$9,990/year** (save 17%)
- Up to 100 users
- 1TB storage included
- Email support (24hr response)
- All features + Lambda processing
- Multi-tenant support
- Perfect for growing businesses

### Enterprise Edition
**Custom pricing**
- Unlimited users
- Unlimited Trading Partners
- 24/7 phone + email support
- 99.9% uptime SLA
- Dedicated account manager
- Custom integrations
- On-premise deployment options
- White-label available

### 30-Day Free Trial
Try MEFT risk-free with full Enterprise features:
- No credit card required
- Full feature access
- Up to 10 users
- Community support

**[Start Your Free Trial →](https://yourcompany.com/trial)**

## 💰 Cost Comparison

### vs. AWS Transfer Family

| Users | AWS Transfer Family | MEFT Professional | Annual Savings |
|-------|---------------------|-------------------|----------------|
| 10 | $438/mo | $299/mo | $1,668/year |
| 50 | $1,080/mo | $999/mo | $972/year |
| 100 | $2,160/mo | $999/mo | **$13,932/year** |
| 500 | $10,800/mo | Custom | **$100,000+/year** |

*AWS pricing assumes 24/7 server + data transfer. MEFT uses your infrastructure.*

### Total Cost of Ownership (100 users)

**AWS Transfer Family:**
- SFTP Service: $1,800/month
- Data Transfer: $512/month (10TB)
- Storage (S3): $230/month
- **No Web UI** (would need custom development)
- **Total: $2,542/month = $30,504/year**

**MEFT Professional:**
- License: $999/month
- AWS Infrastructure: ~$500/month (ECS + RDS + S3)
- **Includes Web UI**
- **Total: $1,499/month = $17,988/year**

**Savings: $12,516/year (41% less)**

## 💬 Support

### Community Support (All Editions)
- **Documentation**: [docs.yourcompany.com/meft](https://docs.yourcompany.com/meft)
- **Knowledge Base**: [kb.yourcompany.com](https://kb.yourcompany.com)
- **GitHub Issues**: Bug reports and feature requests
- **Community Forum**: [community.yourcompany.com](https://community.yourcompany.com)

### Professional Support (Pro & Enterprise)
- **Email Support**: support@yourcompany.com
- **Response Time**: 24 hours (Pro), 4 hours (Enterprise)
- **Video Calls**: Available for Enterprise customers
- **Slack Channel**: Direct access to engineering team

### Emergency Support (Enterprise Only)
- **24/7 Phone Support**: +1-XXX-XXX-XXXX
- **Response Time**: 1 hour for critical issues
- **Dedicated Engineer**: Assigned to your account

## 🎯 Getting Started

1. **[Request a License Key](mailto:sales@xskaliber.com)** or **[Start Free Trial](https://yourcompany.com/trial)**
2. **Download**: Get the deployment package
3. **Configure**: Edit .env file with your settings
4. **Deploy**: Run docker-compose up -d
5. **Access**: Login to web UI and start using MEFT

## 🔗 Links

- **Website**: [yourcompany.com/meft](https://yourcompany.com/meft)
- **Documentation**: [docs.yourcompany.com/meft](https://docs.yourcompany.com/meft)
- **Docker Hub**: [hub.docker.com/r/yourorg/meft](https://hub.docker.com/r/yourorg/meft)
- **Demo**: [demo.yourcompany.com](https://demo.yourcompany.com)


## 📧 Contact

- **Sales**: sales@xskaliber.com
- **Support**: support@xskaliber.com  
- **Security**: security@xskaliber.com

---

<div align="center">

**Ready to replace AWS Transfer Family?**

[Get Started Free](https://yourcompany.com/trial) • [Request Demo](https://yourcompany.com/demo) • [Contact Sales](mailto:sales@yourcompany.com)

---

© 2026 Xskaliber Software. All rights reserved.

</div>
