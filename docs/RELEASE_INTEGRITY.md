# Signed XPI Integrity and Provenance

This public repository does **not** host the private build/source tree. It hosts only the final Mozilla-signed executable XPI and non-sensitive release metadata after review.

## Independent release checks

The official workflow requires separate evidence for:

1. The exact private source commit and frozen dependency lockfile.
2. Reproducible unsigned build with approved Firefox permissions and archive inventory.
3. Real Firefox native conformance on disposable synthetic profiles.
4. Mozilla unlisted signing of the reviewed payload and source archive.
5. Normal Firefox installation **with signature enforcement** and restart, with account/container/Vault continuity verified.
6. For upgrades, a different signed XPI of a higher version and a genuine in-place upgrade test preserving local encrypted Vault and browser bindings.
7. Source-bound comparison against the actual public XPI bytes and its declared SHA-256.
8. Separate authenticated approval of the stable Pages update feed, followed by **public CDN re-verification**.

A checksum validates bytes against a reviewed digest but is **not a substitute for Firefox's authenticated signedState**. A successful upload or GitHub Actions job alone is not proof that the signed file is publicly available.

## Verifying a downloaded file yourself

In a published release, compare the XPI against the published SHA-256. Replace `<file>.xpi` and `<expected-sha256>` with values from the real release notes; no real version is currently advertised here.

Linux/macOS:

```sh
shasum -a 256 <file>.xpi
# or: sha256sum <file>.xpi
```

Windows PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 .\<file>.xpi
```

Check the full 64-hex-character digest, not just a short prefix, and install only if Firefox accepts the package's Mozilla signature.

## Immutable release names

Signed assets are named `mux-<FULL_PRIVATE_SOURCE_COMMIT>.xpi`, attached under tag `mux-v<VERSION>`. The Git tag belongs to the **public distribution Git repository**, while the hash in the filename identifies the separately reviewed **private source commit**. The private Git objects and signing certificates are not mirrored to this repo.

Never treat a URL ending in `latest.xpi` or a reconstructed unsigned package as the official artifact.

## Privacy

Public release notes can disclose version, source commit hash, archive SHA-256, supported Firefox versions and high-level changes. They must **not** disclose private signing credentials, raw AMO JWTs, users' profiles, account labels, encrypted Vault backups, TOTP seeds, browser cookies, identity credentials or CI evidence containing any such data.

For sensitive reports, use [SECURITY.md](../SECURITY.md) rather than public issues.
