<!--
  Template for a new release page. Copy to vX.Y.Z.md, fill it in, and delete
  any section that has nothing in it (except "Before you upgrade": write
  "Nothing." there so readers know they checked).

  Publishing a release:
  1. Add vX.Y.Z.md from this template.
  2. Add a row to the top of the table in release-notes/README.md.
  3. Update the "latest release" link in the main README.md.
  4. Update manifest.json: "latest", "released_at", "severity"
     ("security" or "routine") and "release_notes_url", set to
     https://github.com/xskaliber/eft/blob/main/release-notes/vX.Y.Z.md
     Running installs read this file to show the Update Available banner,
     so change it last, once the Marketplace version is live.

  Do NOT create a GitHub Release or a version tag in this repo. GitHub
  attaches "Source code (zip/tar.gz)" downloads to every release and they
  can't be removed. This file is the release note; the manifest links to it.

  Audience: customers' administrators. Describe what they see and do in the
  console or CloudFormation. Don't mention source files, internal service
  names, migrations or environment variables.
-->

# Xskaliber EFT X.Y.Z

**Released:** YYYY-MM-DD
**Type:** Routine release | Security release. All customers should upgrade.
**Upgrading from:** X.Y.Z

One or two sentences on the theme of the release.

## Before you upgrade

| # | Change | What to do |
|---|--------|------------|
| 1 | | |

Upgrade with **Update stack → Replace existing template**, using the X.Y.Z deployment template from your Marketplace subscription. See [Upgrading](../README.md#-upgrading).

## After you upgrade

1.

## New

-

## Security

-

## Fixes

-

## Removed

-

## Known issues

None at release.

---

Questions about this release: [support@xskaliber.com](mailto:support@xskaliber.com). Found a problem? [Open an issue](https://github.com/xskaliber/eft/issues/new).
