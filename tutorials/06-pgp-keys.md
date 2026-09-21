# 6. PGP keys

**Goal:** add PGP keys so files can be encrypted for a partner and decrypted when received.

## Concepts

| Key type | Used for |
|----------|----------|
| **Public** | **Encrypting** files you send. Attach it to the partner as the **PGP Encryption Key**. |
| **Private** | **Decrypting** files you receive. Attach it as the **PGP Decryption Key**. Keep it secret. |

| Scope | Applies to |
|-------|-----------|
| **System** | Available system-wide |
| **Tenant** | One tenant only (reveals a Tenant field) |

## Add a key

1. Go to **PGP Keys → New**.
2. Enter a **Name**.
3. Select the **Type** (Public or Private) and **Scope**.
4. Paste the **PGP Key Content** (an ASCII-armored block).
5. For a passphrase-protected private key, enter the **Passphrase**.
6. Save.

> The built-in **Generate** button is a convenience for testing. For production exchanges with external partners, **generate keys with GPG or another OpenPGP-compliant tool** and paste them in.

If you do generate a Private key in the console, its matching public key is displayed **once**. Copy it before leaving the page.

Typical exchange:

1. **Your partner** sends you their **public** key. Add it as a Public key and set it as their **PGP Encryption Key**.
2. **You** send them your **public** key. Add your **private** key as a Private key and set it as their **PGP Decryption Key**.

## Attach keys to a partner

Edit the partner ([tutorial 3](03-onboard-a-trading-partner.md)) and pick the keys. The lists are filtered, so encryption shows only Public keys and decryption shows only Private keys. Jobs can also choose keys directly ([tutorial 7](07-partner-jobs.md)).

## Rotating keys

Coordinate with the partner so both sides switch to the new key at the same time. Otherwise transfers can fail.

## Next

[Automate transfers with partner jobs →](07-partner-jobs.md)
