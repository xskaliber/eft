# 10. Single sign-on (SSO)

**Goal:** let your staff sign in to the console through your identity provider (IdP).

**Requires:** System Administrator.

## Scope

SSO authenticates **Administrator and System Administrator** accounts only. Tenants and their web/SFTP users continue to be managed inside the tool and are not affected.

## Before you start

Create an OpenID Connect (OIDC) application in your IdP and note its **Client ID**, **Client Secret** and **Issuer URL**. Register the **Redirect URL** shown on the Xskaliber EFT form as an allowed redirect in the IdP.

## Steps

1. Go to **SSO Integration → Add**.
2. Enter:

   | Field | Value |
   |-------|-------|
   | **Display Name** | Label for the integration |
   | **Issuer URL** | Your IdP's issuer |
   | **Client ID** / **Client Secret** | From the IdP application |
   | **Redirect URL** | Copy this into the IdP's allowed redirects |
   | **Scopes** | Scopes to request |

3. Optional group-based access:
   - **Group Claim Name**: the claim carrying group membership
   - **Admin Group Value** and **System Admin Group Value**: the group names that map to each role
   - **Default Role for New Accounts**: `admin` or `sysadmin`
4. Optional: tick **Automatically create an account on first sign-in** (just-in-time provisioning).
5. Tick **Enabled** and save.

## Things to know

- **Only one integration can be enabled at a time.** Enabling one disables any other.
- Once an admin account is linked to SSO, **password sign-in is disabled for it.**
- **Keep a break-glass account outside SSO** in case the IdP is unavailable.
- With a group claim, removing someone from the group deactivates their account on their **next sign-in attempt**, not instantly. It does not end a session already in progress. Adding them back reactivates it.

## Next

[Using the web portal →](11-web-user-portal.md)
