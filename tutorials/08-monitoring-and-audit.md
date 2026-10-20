# 8. Monitoring and audit

**Goal:** keep an eye on server health, transfers and user activity.

## Dashboard

**Dashboard** shows activity, subscription status, file processing and active server nodes. Click any stat card to jump to that area. The recent files and activity lists cover all tenants and partners you can access.

## Banners

Banners at the top of the console flag things that need attention:

| Banner | Meaning |
|--------|---------|
| **Getting Started** | Setup items are still open, or something is wrong (for example storage is unreachable). See [tutorial 1](01-first-login-and-console-tour.md#3-work-through-getting-started). |
| **Update Available** | A newer release is out. Read its [release notes](../release-notes/README.md), then [upgrade](../README.md#-upgrading). It can be dismissed for the session. |
| **Subscription** | Your AWS Marketplace subscription couldn't be confirmed. See [Subscription status](#subscription-status). |

## Subscription status

The installation checks your AWS Marketplace subscription when it starts and once a day after that.

- If a check fails for a temporary reason, such as an AWS outage, everything keeps working and a warning banner shows for up to **5 days** while it retries.
- If the subscription is cancelled or can't be confirmed after that, the installation becomes **read-only**: you can still sign in, view and download data, but changes are blocked. A successful check restores normal operation.

If you see a subscription banner and believe your subscription is active, contact [support@xskaliber.com](mailto:support@xskaliber.com).

## Server monitoring

Go to **Servers**.

- Each **server node** is an SFTP server in your cluster. Nodes register automatically and report CPU, memory and active connections.
- Nodes send a heartbeat every **30 seconds**.
- A node with no heartbeat for **2 minutes** is marked **offline**.

If a node stays offline, check its ECS task in the AWS console and the stack's CloudWatch alarms. Set `AlarmNotificationEmail` on the stack to receive notifications.

## Partner files

**Partner Files** lists inbound (received from a partner) and outbound (sent to a partner) files. Use the direction filter, and click a file to see the processing steps (encryption, compression, virus scan) applied to it, along with retry counts and error messages.

## Activity log

**Activity Log** is the audit trail. It records logins, file uploads and downloads, and administrative changes to users, partners, keys and jobs, each with the acting user and a timestamp. Filter by **user**, **activity type** or **date range** when investigating an event.

## Suggested routine

| Frequency | Check |
|-----------|-------|
| Daily | Dashboard, and any **Failed** job executions |
| Weekly | Servers online, Activity Log for unusual logins, any **Update Available** banner |
| Quarterly | Users and ACLs still valid; deactivate leavers; rotate PGP keys |

## Next

[System settings →](09-system-settings.md)
