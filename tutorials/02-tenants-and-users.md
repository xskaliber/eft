# 2. Tenants and users

**Goal:** create a tenant and add the different kinds of users.

## Concepts

A **tenant** is a top-level organization boundary. Trading partners, users and files are scoped to a tenant, which keeps data isolated.

Users have one or more **personas**:

| Persona | Access |
|---------|--------|
| **System Administrator** | Everything, including System Settings and SSO |
| **Administrator** | Manages partners, jobs, users and keys |
| **Web User** | Signs in to the web portal to view and download files |
| **SFTP User** | Connects with an SFTP client |

Administrator and System Administrator are **exclusive**: selecting one clears any other persona and any tenant or partner assignment. **Web User** and **SFTP User** can be combined.

## Create a tenant

1. Go to **Tenants → New**.
2. Fill in:
   - **Display Name**: shown across the console; can be changed later.
   - **System Code**: a short, unique identifier, typically uppercase letters and numbers.
3. Save.

> Treat the **System Code** as permanent. Changing it later can break references elsewhere.

## Create a user

1. Go to **Users → New**.
2. Enter **Username**, **Email Address**, **First Name** and **Last Name**.
3. Choose a persona:
   - For an administrator, tick **Administrator** (or **System Administrator**).
   - For a partner's staff, tick **Web User** and/or **SFTP User**.
4. For Web or SFTP users, select the **Tenant** first, then the **Trading Partner**. The partner list only shows partners under that tenant.
5. Review the **Home Directory**. It auto-fills as `users/{username}`.
6. For SFTP users, set the **SFTP Shell**. Keep `/bin/false` (the default) for SFTP-only access.
7. Save.

Setting a tenant or partner on a user limits the data and files they can see to that organization.

> Only System Administrators can edit Administrator or System Administrator accounts.

## Deactivating a user

Edit the user and untick **Active**. Their history is kept.

## Next

[Onboard a trading partner →](03-onboard-a-trading-partner.md)
