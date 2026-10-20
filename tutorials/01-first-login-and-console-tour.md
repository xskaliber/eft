# 1. First-run setup and console tour

**Goal:** claim your new installation, create the first administrator, and learn where everything lives.

## Before you start

- Your CloudFormation stack is in `CREATE_COMPLETE`.
- You can see the stack's **Outputs** tab. You'll use **SetupURL** and **SetupTokenLogs**.

There is **no default username or password**. Each installation is claimed once with a one-time setup token that only someone with access to your AWS account can read.

## Steps

### 1. Get the setup token

1. In the stack's **Outputs** tab, open the **SetupTokenLogs** link. It opens the backend's CloudWatch logs, filtered to the `FIRST-RUN SETUP` banner.
2. Copy the token from the banner.

> The token is valid for **24 hours**. If it expires before you finish, restart the backend service in ECS and a new token is printed. It can take a few minutes after the stack completes for the backend to start and print the banner.

### 2. Run the setup wizard

1. Open the **SetupURL** output (or the **ApplicationURL**; a new installation redirects to setup automatically).
2. **Verify**: paste the setup token.
3. **Administrator**: enter your first name, last name, email, username and password. Passwords need **at least 12 characters, with both letters and numbers**.
4. **Organization** (optional): set the **Application name** shown in the header and browser tab, and create your **first tenant**. You can do both later.
5. **Review** and finish.

You are signed in automatically. The token stops working and the setup page is closed for good.

> This first account is a **break-glass System Administrator**: it keeps password sign-in even if you later require [single sign-on](10-single-sign-on.md). Store its credentials somewhere safe and use a named account for day-to-day work.

> If the stack was launched without a certificate (`CertificateArn` empty), the site is served over plain HTTP. Use that only for evaluation, and add a certificate before real use.

### 3. Work through Getting Started

After setup you land on **Getting Started**, a checklist of what a new installation needs before partners can exchange files. Most items tick themselves off as the system detects them; use **Re-check** to refresh.

| Item | Done when |
|------|-----------|
| **Connect file storage** | The application can reach its S3 bucket. If not, the real error is shown. |
| **SFTP server online** | At least one SFTP server has reported in. This can take a few minutes on a new install. |
| **Use unique SFTP host keys** | The install has its own SSH host keys. New installs generate them automatically. |
| **Share SFTP connection details with partners** | You've noted the hostname, port and host key fingerprints to give partners. Set **SFTP Public Hostname** in [System Settings](09-system-settings.md) first if partners will use your own DNS name. |
| **Create your first tenant** / **Add a trading partner** | One exists ([tutorial 2](02-tenants-and-users.md), [tutorial 3](03-onboard-a-trading-partner.md)) |
| **Connect single sign-on** | *Optional.* An SSO integration is enabled, or you skip it ([tutorial 10](10-single-sign-on.md)) |
| **AWS Marketplace subscription verified** | The install has confirmed your subscription |
| **Review system settings** | You mark it done after reviewing [System Settings](09-system-settings.md) |

A **Getting Started** banner appears in the console until the list is done or you hide it. Problems such as unreachable storage always show, even when the banner is hidden. The checklist is available to System Administrators from the side navigation.

### 4. Tour the navigation

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
| **Getting Started** | Setup checklist (System Administrators only) |
| **System Settings** | Global settings (System Administrators only) |
| **SSO Integration** | Identity provider setup (System Administrators only) |
| **About** | Installed version, license terms and open-source components |

The running version is also shown in the console footer. When a newer release is available, an **Update available** banner and footer chip link to its [release notes](../release-notes/README.md).

### 5. Use in-page help

Every page has a **Help** drawer with tips for that screen. Open it whenever you're unsure what a field does.

## Changing your password

Open your **Profile** from the user menu (top right), enter your current password, then your new one.

If an administrator sets a password for you, it is **temporary**: you're asked to choose a new one the next time you sign in.

## Locked out?

- Another System Administrator can set a temporary password for you under **Users**.
- After **10 failed sign-in attempts in 15 minutes**, further attempts for that username are refused until the window passes.
- If no administrator can sign in, contact [support@xskaliber.com](mailto:support@xskaliber.com).

## Next

[Tenants and users →](02-tenants-and-users.md)
