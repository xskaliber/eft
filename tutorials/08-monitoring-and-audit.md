# 8. Monitoring and audit

**Goal:** keep an eye on server health, transfers and user activity.

## Dashboard

**Dashboard** shows activity, subscription status, file processing and active server nodes. Click any stat card to jump to that area. The recent files and activity lists cover all tenants and partners you can access.

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
| Weekly | Servers online, Activity Log for unusual logins |
| Quarterly | Users and ACLs still valid; deactivate leavers; rotate PGP keys |

## Next

[System settings →](09-system-settings.md)
