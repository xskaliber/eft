# 5. SFTP users and SSH keys

**Goal:** create an SFTP user that connects with an SSH key.

## Steps

1. Go to **Users → New**.
2. Enter the user's name, username and email.
3. Tick **SFTP User** (add **Web User** as well if they also need the portal).
4. Select the **Tenant**, then the **Trading Partner**.
5. Keep **SFTP Shell** as `/bin/false` for SFTP-only access. Choose `/bin/bash` or `/bin/sh` only if the user needs interactive shell access.
6. Under **SSH Public Key**, either:
   - **Paste** an existing public key from the user, or
   - Click **Generate Key Pair**.
7. Save.

> **If you generate a key pair, the private key is shown only once.** Copy it and send it to the user through a secure channel right away. It cannot be retrieved afterwards, and generating a new pair replaces the old key.

Asking the partner to send you their **public** key is the safest approach, because the private key then never leaves their hands.

## Connect

Give the user the **SftpEndpoint** from your CloudFormation stack's **Outputs** tab:

```bash
sftp -i ~/.ssh/partner_key username@<SftpEndpoint>
```

Files they upload appear under **Partner Files** as inbound, and can be picked up by [partner jobs](07-partner-jobs.md).

## Troubleshooting

| Symptom | Check |
|---------|-------|
| `Permission denied (publickey)` | The public key saved on the user matches the private key being used, and the user is **Active** |
| Connection times out | The partner's IP is allowed by `SftpAllowedCidr` on the stack and by any [ACL rules](04-ip-access-control.md) |
| Connects but lands in the wrong folder | Review the user's **Home Directory** |

## Next

[PGP keys →](06-pgp-keys.md)
