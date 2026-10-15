# MUX Signed Release Policy

This public repository distributes **binary releases and update metadata only**. The private source repository is the authority for source revision, tests and signing evidence.

## Release admission

A release is eligible for publication only when all of the following are true:

1. The exact private source commit and dependency lockfile are fixed and reviewed; production code, permissions and Firefox extension ID match the accepted manifest.
2. Source verification, reproducible XPI packaging, and disposable-profile Firefox native conformance pass.
3. Mozilla accepts unlisted signing; the resulting XPI's executable payload matches the reviewed unsigned candidate.
4. **Normal Firefox with signature checks enabled** successfully installs the signed XPI permanently and verifies account/container and encrypted Vault continuity after restart.
5. For a subsequent version, a real test installs the *previous* signed XPI, upgrades in place to the *new* signed XPI, and verifies preservation of the existing browser/registry/Vault state.
6. The exact immutable XPI is published and independently fetched from GitHub Releases over HTTPS; its SHA-256 matches the reviewed Mozilla response.
7. Only after that verification may the permanent `gh-pages/updates.json` endpoint begin advertising the version.
8. A final external check downloads the public update JSON and signed XPI and confirms the exact version, add-on ID, immutable XPI URL and SHA-256.

Passing tests in a local checkout does **not** prove a remote GitHub Actions workflow ran or that an XPI was signed by Mozilla.

## Public artifact naming

| Item | Convention |
| --- | --- |
| GitHub Release tag | `mux-v<VERSION>` |
| Signed binary | `mux-<FULL_PRIVATE_SOURCE_COMMIT>.xpi` |
| Public XPI URL | `https://github.com/bochkov-anton/mux-releases/releases/download/mux-v<VERSION>/mux-<FULL_PRIVATE_SOURCE_COMMIT>.xpi` |
| Update manifest | `https://bochkov-anton.github.io/mux-releases/updates.json` |
| Browser add-on identity | `mux@local.invalid` |

The private source commit is an identifier and release provenance reference, **not** a Git object copied to this repository. Public GitHub Release tags point to public distribution-repository commits.

A published release must not silently replace an existing tag/asset with different bytes. A partial or unknown remote operation requires inspection and human reconciliation, not automatic clobbering.

## Update and incident policy

The initial `updates.json` is valid JSON with an empty `updates` array. A real version is advertised only when a signed XPI has already been published and checked publicly.

Versions advance monotonically. Rollback of source code does not imply that a previously migrated Firefox IndexedDB database or encrypted Vault is reversible. During an incident, the maintainers can advertise **no new updates** without deleting existing releases or uninstalling extensions.

## Scope of public material

Permitted: non-sensitive release notes, the one signed XPI asset, public SHA-256/provenance descriptors, update metadata, documentation.

Forbidden: private source archives, review or CI evidence archives, build caches, credentials, API tokens, user data, Vault backups, profiles, cookies, TOTP secrets and unreviewed unsigned experimental binaries.

See [release integrity](docs/RELEASE_INTEGRITY.md) and [operations](docs/OPERATIONS.md).
