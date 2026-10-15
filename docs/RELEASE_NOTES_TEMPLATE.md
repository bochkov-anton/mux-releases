# MUX <VERSION> — Release notes template

**Template only — NOT an actual signed release or a download link.** Release maintainers must fill the fields from reviewed private source and public signed artifacts.

| Field | Required reviewed value |
| --- | --- |
| Release tag | `mux-v<VERSION>` |
| Private source commit | Exact 40-character Git SHA |
| Mozilla-signed binary | `mux-<FULL_SOURCE_SHA>.xpi` |
| Signed binary size | Exact byte count |
| Signed binary SHA-256 | Full 64-character lowercase digest |
| Firefox support | Minimum supported Firefox version |
| Install/restart evidence | Real signature-enforced Firefox smoke result |
| Upgrade evidence (if applicable) | Exact previous-to-current signed-XPI/Vault report |
| Update feed | `https://bochkov-anton.github.io/mux-releases/updates.json` |

## What's changed

Write user-facing functionality and bug fixes only after verification.

## Browser and data compatibility

Describe any compatibility floor, local registry/Vault schema change and required backup step. Never promise authenticated cookie/session migration between devices.

## Security and privacy

Document meaningful security changes without disclosing passwords, credentials, private user data or active secrets.

## Verification

Link the public binary and publish its SHA-256. State clearly whether the normal-Firefox signed-install and optional signed-upgrade checks passed. Do not claim a signature or successful installation based on an unsigned local test fixture.

## Known limitations

Record explicitly anything unsupported in this release: Android, third-party site authentication portability, experimental features or irreversible local migrations.
