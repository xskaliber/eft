# 3. Onboard a trading partner

**Goal:** register a partner and understand the settings that matter.

## Concepts

A **trading partner** is an external organization you exchange files with over SFTP. Each partner has its own connection settings, ACLs, PGP keys, jobs and users.

## Steps

1. Go to **Partners → New**.
2. Select the **Tenant** and enter a **Display Name**.
3. Choose **Server Ownership**:

   | Choice | Use when | Extra fields |
   |--------|----------|--------------|
   | **US** | Xskaliber EFT hosts the SFTP server the partner connects to | None |
   | **Partner** | The partner hosts their own SFTP/FTP/FTPS server that you pull from or push to | Transfer Protocol, Host, Port, User, Password or Auth Key |

4. If you chose **Partner**, fill in the connection details:
   - **Transfer Protocol**: `SFTP`, `FTP` or `FTPS`
   - **Transfer Host** and **Port**
   - **Transfer User**
   - Authenticate with either a **Transfer Password** **or** an **Auth Key** (SSH key material). Leave the one you don't use blank.
   - For SFTP, optionally paste the partner server's **Pinned SFTP Host Key** (for example `ssh-ed25519 AAAA...`). See [Partner server host keys](#partner-server-host-keys) below.
5. Optionally choose a **PGP Encryption Key** (public keys only, used for files you send) and a **PGP Decryption Key** (private keys only, used for files they send you). These can be added later. See [PGP keys](06-pgp-keys.md).
6. Leave **Active** ticked and save.

## Finish onboarding

Open the partner from the **Partners** list. The detail page has tabs:

| Tab | Use it to |
|-----|-----------|
| **Jobs** | See automated transfers ([tutorial 7](07-partner-jobs.md)) |
| **ACLs** | Restrict source IPs ([tutorial 4](04-ip-access-control.md)) |
| **Files** | See recent inbound and outbound files |
| **Users** | See accounts tied to this partner ([tutorial 5](05-sftp-users-and-ssh-keys.md)) |

## Partner server host keys

When Xskaliber EFT connects to a partner's SFTP server, it checks the server's host key, so files can't be redirected to an impostor.

- **Leave it blank** and the key is recorded automatically on the first connection (trust on first use).
- **Paste it in** if the partner gives it to you up front. This is the more secure option.
- If the server later presents a **different key, the transfer is refused** and the job fails with a host key error.
- If the partner legitimately rotates their host key, confirm the change with them, then edit the partner and **clear** the field (or paste the new key). Changing the host or port also clears it.

## Stored credentials

Transfer passwords and auth keys are never shown again after you save them. When editing a partner, leave those fields blank to keep the stored values.

## Pausing a partner

Edit the partner and untick **Active**. New transfers and job runs are blocked, while historical data is kept.

## Next

[Restrict access with IP ACLs →](04-ip-access-control.md)
