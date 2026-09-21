# 1. First login and console tour

**Goal:** sign in for the first time, secure the initial account, and learn where everything lives.

## Before you start

- Your CloudFormation stack is in `CREATE_COMPLETE`.
- You have the **ApplicationURL** from the stack's **Outputs** tab.

## Steps

### 1. Sign in

1. Open the **ApplicationURL** in your browser.
2. Sign in with the initial administrator account created with your deployment:

   | Field | Value |
   |-------|-------|
   | **Username** | `admin` |
   | **Password** | `<changeme!>` |

> If the stack was launched without a certificate (`CertificateArn` empty), the site is served over plain HTTP. Use that only for evaluation, and add a certificate before real use.

### 2. Change the default password

1. Open your profile from the user menu (top right).
2. Enter your current password, then your new password, and save.

Do this immediately. It is the most important security step.

### 3. Tour the navigation

The side navigation for administrators contains:

| Menu | What it does |
|------|--------------|
| **Dashboard** | Stat cards, recent files and recent activity. Click a card to jump to that area. |
| **Partners** | Trading partners and their connection settings |
| **Partner ACLs** | IP allow-list rules per partner |
| **Partner Jobs** | Scheduled transfers and processing |
| **Partner Files** | Inbound and outbound files |
| **Activity Log** | Audit trail |
| **Tenants** | Organization boundaries |
| **Users** | Admins, web users and SFTP users |
| **Servers** | SFTP node health |
| **PGP Keys** | Encryption keys |
| **System Settings** | Global settings (system administrators only) |
| **SSO Integration** | Identity provider setup (system administrators only) |

### 4. Use in-page help

Every page has a **Help** drawer with tips for that screen. Open it whenever you're unsure what a field does.

## Next

[Tenants and users →](02-tenants-and-users.md)
