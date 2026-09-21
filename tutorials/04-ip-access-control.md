# 4. Restrict access with IP ACLs

**Goal:** limit a partner's SFTP access to known IP addresses.

## How ACLs work

Each ACL is an **allow-list** entry that permits connections from an address or range as that partner.

- A partner with **no ACL rules is not IP-restricted**.
- Add at least one rule to start restricting access.
- Only **IPv4** addresses and CIDR ranges are supported (no IPv6, no hostnames).

## Steps

1. Go to **Partner ACLs → New** (or use the **ACLs** tab on the partner's page).
2. Select the **Trading Partner**.
3. Enter the **IP/Netmask**:
   - A single address: `203.0.113.5`
   - A range in CIDR notation: `203.0.113.0/24`
4. Save. Repeat for each address or range.

Also review the `SftpAllowedCidr` and `AlbAllowedCidr` parameters on your CloudFormation stack. They control network-level access to the SFTP endpoint and web UI for everyone.

## Good to know

- Changes take effect on the partner's **next connection**. Existing sessions are not disconnected.
- Ask the partner for their **outbound public IPs** (often a NAT gateway) before adding rules, and add all of them to avoid locking them out.

## Next

[SFTP users and SSH keys →](05-sftp-users-and-ssh-keys.md)
