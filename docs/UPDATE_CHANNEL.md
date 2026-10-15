# Firefox Update Channel

## Stable identity

| Property | Value |
| --- | --- |
| Add-on Gecko ID | `mux@local.invalid` |
| Permanent update URL | `https://bochkov-anton.github.io/mux-releases/updates.json` |
| Public Pages repository | `bochkov-anton/mux-releases` |
| Pages source | `gh-pages`, root `/` |
| Signed binary location | Version-tagged GitHub Releases assets in the same public repository |
| Source code location | A separate **private** repository, never mirrored here |

This update URL is compiled into the Firefox extension **before the first supported signed installation**. The repository owner must enable Pages from the reviewed `gh-pages` branch before any production release; a bare Git branch is not proof that a public HTTPS feed exists.

## Safe initial manifest

Before the first signed release, `updates.json` intentionally contains:

```json
{
  "addons": {
    "mux@local.invalid": {
      "updates": []
    }
  }
}
```

This is a **valid no-updates state**, not a missing release or a signed package. Do not advertise an unsigned XPI as a test.

## Version publication

When the first Mozilla-signed and browser-verified XPI has been published at an immutable GitHub Release URL, the private release pipeline can replace only `gh-pages/updates.json` with a Firefox update entry for the approved version.

Its update entry includes a strictly monotonic `version`, the exact `update_link` to the signed XPI, `update_hash` in the form `sha256:<64 lowercase hex characters>`, and reviewed Firefox minimum-version metadata.

Only these signatures, version and source-bound hashes are admitted. The feed never stores credentials, TOTP seeds, cookies or browser profiles.

The update is submitted through the GitHub Contents API using the previously verified **Git blob SHA** as an optimistic concurrency condition. A different live version, unexpected file, SHA mismatch or concurrent mutation blocks publication. GitHub Pages may take time to serve a new commit; final production success requires a subsequent unauthenticated public read of both the manifest and signed XPI bytes.

## Emergency pause

During an incident, the authorized maintainer can restore the exact **empty updates manifest** through the separately protected public-feed workflow. A pause means Firefox is not offered *new* versions. Existing installed add-ons are not uninstalled, XPI assets are not silently deleted, and no local IndexedDB/Vault downgrade is attempted.

See [Release policy](../RELEASE_POLICY.md) and [Operations](OPERATIONS.md).
