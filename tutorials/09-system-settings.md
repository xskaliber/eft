# 9. System settings

**Goal:** review and adjust global platform settings such as email, security policy and processing limits.

**Requires:** System Administrator. Settings apply globally across **all tenants**.

## Where to find them

Go to **System Settings**. Settings are grouped into tabs:

| Tab | Covers |
|-----|--------|
| **Storage Configuration** | Storage type and provider, bucket, region, endpoint, user directory prefix |
| **SFTP Configuration** | Port, max connections, idle and connection timeouts, compression, log level, SSH host keys |
| **SMTP/Email Configuration** | Mail server used for notifications such as job completion emails |
| **Security Configuration** | Token lifetime, password length, login lockout |
| **File Processing Configuration** | Processing mode, file size limit, timeout, concurrency |
| **Application Configuration** | Application name, environment, debug and maintenance modes |

Each row shows the setting, its current value, its type, and badges:

- **Encrypted** or **Sensitive**: the value is masked in the list and stored encrypted.
- **Restart**: the change takes effect only after the service is restarted.

> Many storage, database and secret values on a Marketplace deployment are provisioned by the CloudFormation stack. Leave those unchanged unless support advises otherwise, and adjust the settings below instead.

## Change a setting

1. Open the relevant tab and click the **Edit** (pencil) icon on the row.
2. Enter the new value. Some settings are dropdowns or on/off switches, and numeric settings enforce a valid range.
3. Enter a **Change Reason**. It is required and is recorded in the history.
4. Save.

Settings marked **Restart** show a warning in the dialog. Apply them during a maintenance window.

## View change history

Click the **History** icon on a row to see previous values, who changed them, when, and why. Use it to audit or work out what changed before a problem started.

## Common tasks

### Set up email notifications

Job completion emails and other notifications need a mail server. In **SMTP/Email Configuration**, set:

| Setting | Notes |
|---------|-------|
| **SMTP Host** | Your mail server hostname (empty by default) |
| **SMTP Port** | `587` by default |
| **SMTP Username** / **SMTP Password** | Password is stored encrypted |
| **From Address** | Sender shown on notifications, for example `noreply@yourcompany.com` |
| **Use TLS** | Keep on unless your server requires otherwise |

Then create a [partner job](07-partner-jobs.md) with **Send Completion Email** to test it. If you use Amazon SES, use its SMTP endpoint and SMTP credentials.

### Tighten login security

In **Security Configuration**:

| Setting | Default | Range |
|---------|---------|-------|
| **Min Password Length** | 8 | 6-128 |
| **Max Login Attempts** | 5 | 3-10 |
| **Lockout Duration** (minutes) | 30 | 5-1440 |
| **JWT Expiration** (hours) | 24 | 1-720 |

Consider a longer minimum password length, and a shorter token lifetime for stricter session control. For staff, prefer [SSO](10-single-sign-on.md).

### Tune SFTP

In **SFTP Configuration**:

| Setting | Default | Range |
|---------|---------|-------|
| **Max Connections** | 100 | 1-10000 |
| **Idle Timeout** (seconds) | 300 | 60-3600 |
| **Connection Timeout** (seconds) | 300 | 30-3600 |
| **Log Level** | INFO | DEBUG, INFO, WARN, ERROR |

Use `DEBUG` temporarily while troubleshooting a partner connection, then return it to `INFO`.

### Manage SSH host keys

Under **SFTP Configuration** you can view, copy and download the server's **RSA, ECDSA and ED25519 host keys**, see their fingerprints, and click **Generate New** to replace one. Restart the SFTP service afterwards for a change to apply.

> **Regenerating a host key changes the server's fingerprint.** Partners will see a host-key mismatch warning on their next connection. Notify them first, and share the new fingerprint through a trusted channel.

### Tune file processing

In **File Processing Configuration**:

| Setting | Default | Range |
|---------|---------|-------|
| **Processing Mode** | `backend` | `backend` or `lambda` |
| **Max File Size** (MB) | 100 | 1-10000 |
| **Processing Timeout** (minutes) | 30 | 1-1440 |
| **Concurrent Jobs** | 10 | 1-100 |

`lambda` mode requires the Lambda file-processing add-on to have been enabled on your CloudFormation stack (`EnableLambdaFileProcessing`).

### Maintenance and environment

In **Application Configuration**, set **Environment** to `production` for live use. **Maintenance Mode** and **Debug Mode** are on/off switches. Leave **Debug Mode** off in production.

## Good practice

- Always give a specific **Change Reason**, since it becomes your audit record.
- Change one setting at a time and verify before moving on.
- Check the **History** before reverting a change, so you restore the right value.

## Next

[Single sign-on →](10-single-sign-on.md)
