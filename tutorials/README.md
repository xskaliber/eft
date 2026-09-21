# Xskaliber EFT Tutorials

Step-by-step guides for setting up and using Xskaliber EFT after your [AWS Marketplace deployment](../README.md#-getting-started) is running.

## Suggested order

| # | Tutorial | Who it's for | Time |
|---|----------|--------------|------|
| 1 | [First login and console tour](01-first-login-and-console-tour.md) | Administrators | 10 min |
| 2 | [Tenants and users](02-tenants-and-users.md) | Administrators | 15 min |
| 3 | [Onboard a trading partner](03-onboard-a-trading-partner.md) | Administrators | 15 min |
| 4 | [Restrict access with IP ACLs](04-ip-access-control.md) | Administrators | 5 min |
| 5 | [SFTP users and SSH keys](05-sftp-users-and-ssh-keys.md) | Administrators, partners | 10 min |
| 6 | [PGP keys](06-pgp-keys.md) | Administrators | 10 min |
| 7 | [Automate transfers with partner jobs](07-partner-jobs.md) | Administrators | 20 min |
| 8 | [Monitoring and audit](08-monitoring-and-audit.md) | Administrators | 10 min |
| 9 | [System settings](09-system-settings.md) | System administrators | 15 min |
| 10 | [Single sign-on (SSO)](10-single-sign-on.md) | System administrators | 15 min |
| 11 | [Using the web portal](11-web-user-portal.md) | Web users | 5 min |

## Key concepts

| Term | Meaning |
|------|---------|
| **Tenant** | A top-level organization boundary. Partners, users and files are scoped to a tenant for data isolation. |
| **Trading partner** | An external organization you exchange files with over SFTP. |
| **ACL** | An IP allow-list rule for a partner. |
| **Partner job** | An automated, scheduled transfer or processing task. |
| **Persona** | A user's role: Administrator, System Administrator, Web User, or SFTP User. |

Each page in the console also has a **Help** drawer (the `?` icon) with context-sensitive guidance.

Something unclear or broken? [Open an issue](https://github.com/xskaliber/eft/issues/new).
