# 9. System settings

**Goal:** review and adjust global platform settings such as SFTP limits, host keys and processing limits.

**Requires:** System Administrator. Settings apply globally across **all tenants**.

## Where to find them

Go to **System Settings**. Settings are grouped into tabs:

| Tab | Covers |
|-----|--------|
| **Storage Configuration** | Storage provider, bucket, region and user directory prefix |
| **SFTP Configuration** | Public hostname, port, max connections, timeouts, compression, log level, SSH host keys |
| **SMTP/Email Configuration** | Mail server details. Email notifications aren't available yet, so these values aren't used. |
| **Security Configuration** | Security-related values (see [Sign-in security](#sign-in-security)) |
| **File Processing Configuration** | File size limit, timeout, concurrency |
| **Application Configuration** | Application name and description, environment, debug and maintenance modes |
| **Updates** | Whether the installation checks for new releases, and the result of the last check (see [Update checks](#update-checks)) |

Each row shows the setting, its current value, its type, and badges:

- **Managed by deployment**: the value comes from your CloudFormation stack and is re-applied every time the service starts. It has no edit button. To change it, update the stack.
- **Read-only**: the value is recorded by the system, such as the result of the last update check. It is shown for reference and has no edit button.
- **Encrypted** or **Sensitive**: the value is masked in the list and stored encrypted.
- **Restart**: the change takes effect only after the service is restarted.

On a Marketplace deployment the storage bucket and region, the environment, and the file size and processing timeout limits are managed by the deployment.

## Change a setting

1. Open the relevant tab and click the **Edit** (pencil) icon on the row.
2. Enter the new value. Some settings are dropdowns or on/off switches, and numeric settings enforce a valid range.
3. Enter a **Change Reason**. It is required and is recorded in the history.
4. Save.

Settings marked **Restart** show a warning in the dialog. Apply them during a maintenance window.

## View change history

Click the **History** icon on a row to see previous values, who changed them, when, and why. Use it to audit or work out what changed before a problem started.

## Common tasks

### Set the SFTP public hostname

**SFTP Public Hostname** (SFTP Configuration) is the name partners connect to. It is shown on **Getting Started** when you share connection details. On AWS it fills in automatically with the SFTP load balancer's hostname. If you've pointed your own DNS name (for example `sftp.yourcompany.com`) at the **SftpEndpoint**, change it to that name.

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

Each installation generates its own unique host keys automatically.

> **Regenerating a host key changes the server's fingerprint.** Partners will see a host-key mismatch warning on their next connection. Notify them first, and share the new fingerprint through a trusted channel.

### Tune file processing

In **File Processing Configuration**:

| Setting | Default | Range |
|---------|---------|-------|
| **Max File Size** (MB) | 100 | 1-10000 |
| **Processing Timeout** (minutes) | 30 | 1-1440 |
| **Concurrent Jobs** | 10 | 1-100 |

File processing (encryption, compression and virus scanning) runs inside the application's backend service. On a Marketplace deployment, **Max File Size** and **Processing Timeout** are managed by the deployment.

### Maintenance and environment

In **Application Configuration**, **Maintenance Mode** and **Debug Mode** are on/off switches. Leave **Debug Mode** off in production. **Environment** is managed by the deployment and is `production` on Marketplace installs.

## Sign-in security

These protections are built in and always on. The values under **Security Configuration** don't change them yet.

| Protection | Behavior |
|------------|----------|
| Password strength | At least **12 characters**, with both letters and numbers |
| Temporary passwords | A password set by an administrator must be changed by the user at their next web sign-in |
| Failed sign-ins | After **10 failed attempts in 15 minutes**, further attempts for that username are refused until the window passes |
| Sessions | Sign-in sessions last up to **24 hours**. Deactivating a user, changing their personas or resetting their password takes effect immediately. |

For staff accounts, prefer [single sign-on](10-single-sign-on.md) so your identity provider's policies (MFA, password rules) apply.

## Update checks

Once a day the installation checks whether a newer Xskaliber EFT release is available, by reading a small public version file from this repository. Nothing about your installation is sent. When a newer release is out, the console shows an **Update Available** banner (see [Upgrading](../README.md#-upgrading)).

The **Updates** tab has one setting:

| Setting | Default | What it does |
|---------|---------|--------------|
| **Check for Updates** | On | Turn it off if your network blocks outbound internet access or your policy doesn't allow software to check for updates. The change takes effect without a restart. |

The other rows on the tab are **Read-only** and show the result of the most recent check:

| Row | Shows |
|-----|-------|
| **Last Checked At** | When the last check ran |
| **Latest Known Version** | The newest release the check found |
| **Latest Release Severity** | `routine`, or `security` for a release that fixes a security issue |
| **Latest Release Notes URL** | The release notes for that version |
| **Last Check Error** | Why the last check failed. Empty when it succeeded. |

If outbound internet access is blocked, the check fails quietly, **Last Check Error** says why, and nothing else is affected. Either allow the version file through your firewall (see [Network access](../README.md#network-access)) or turn **Check for Updates** off. With checks off you won't see the banner, so watch the [release notes](../release-notes/README.md) for new versions instead.

## Good practice

- Always give a specific **Change Reason**, since it becomes your audit record.
- Change one setting at a time and verify before moving on.
- Check the **History** before reverting a change, so you restore the right value.

## Next

[Single sign-on →](10-single-sign-on.md)
