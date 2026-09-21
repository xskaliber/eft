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

## Pausing a partner

Edit the partner and untick **Active**. New transfers and job runs are blocked, while historical data is kept.

## Next

[Restrict access with IP ACLs →](04-ip-access-control.md)
