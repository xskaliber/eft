# 7. Automate transfers with partner jobs

**Goal:** create a scheduled job that pulls or pushes files and optionally decrypts, encrypts, compresses or decompresses them.

## Job types

| Type | Does |
|------|------|
| **FTP Pull** | Downloads files from the partner's server into Xskaliber EFT |
| **FTP Push** | Uploads files from Xskaliber EFT to the partner's server |
| **File Processing** | Runs processing on files already in the system. It has no schedule or path fields. |

Pull and Push jobs need the partner to be configured with **Server Ownership = Partner** ([tutorial 3](03-onboard-a-trading-partner.md)).

## Example: pull and decrypt a daily file

1. Go to **Partner Jobs → New**.
2. Select the **Trading Partner**, then enter a **Job Name** and **Job Description**.
3. Set **Job Type** to **FTP Pull**.
4. Set the **Cron Schedule** (below), for example `0 6 * * *` for 06:00 UTC daily.
5. Fill in **File Name** (a name or wildcard pattern), **Source Path** on the partner's server, and **Destination Path**.
6. Tick **Use PGP Decryption** and choose the PGP Decryption Key. Set the **PGP File Extension** to match what the partner sends, for example `.pgp`.
7. If files arrive compressed, tick **Use Decompression** and pick the algorithm (**GZIP**, **BZIP2** or **ZIP**).
8. Choose what happens to originals with the **Lifecycle Strategy** (below).
9. Leave **Job Active** ticked and save.

## Cron schedule

Use a standard 5-field expression (`minute hour day month weekday`), evaluated in **UTC**.

| Expression | Runs |
|------------|------|
| `0 9 * * *` | Every day at 09:00 |
| `*/15 * * * *` | Every 15 minutes |
| `0 9 * * 1-5` | Weekdays at 09:00 |
| `0 0 1 * *` | First of the month, midnight |

Leave it blank to run the job **manually only**.

## Lifecycle strategy

Once encryption or compression is enabled, choose what happens to the original file:

| Option | Result |
|--------|--------|
| **Keep Both Files** | Original and processed copy are both kept |
| **Replace with Processed** | Original is removed |
| **Archive Original** | Original is moved to an archive location |

Use **Keep Both** or **Archive** if you need an audit trail.

## Check results and retry

1. Open the job and go to **Executions**.
2. Statuses are **Pending**, **In Progress**, **Success**, **Failed** and **Cancelled**.
3. For a **Failed** run, read the error message, fix the cause, then use **Retry** in the Actions column (up to the job's maximum retries).

To see each processing step applied to a file (decrypt, decompress, virus scan), open the file under **Partner Files**.

Common failure causes:

| Error mentions | Fix |
|----------------|-----|
| Host key mismatch | The partner's SFTP server presented a different host key than the one pinned on the partner. Confirm the change with the partner, then update or clear **Pinned SFTP Host Key** ([tutorial 3](03-onboard-a-trading-partner.md#partner-server-host-keys)). |
| Authentication | The partner's **Transfer User**, password or auth key is wrong or has changed |
| Decryption | The wrong **PGP Decryption Key** is selected, or its passphrase is wrong |

## Virus scanning

Files are scanned with ClamAV. Virus definitions update automatically every few hours, so the backend needs outbound HTTPS access to `database.clamav.net`. Stacks created from the standard template already have this.

## Next

[Monitoring and audit →](08-monitoring-and-audit.md)
