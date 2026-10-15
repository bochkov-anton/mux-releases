# Public Distribution Repository Operations

This guide is for the owner of the **public** `bochkov-anton/mux-releases` repository. It intentionally contains no private MUX source or secret values.

## Repository branches

`main` is the documentation branch: `README.md`, `SECURITY.md`, `RELEASE_POLICY.md`, `CONTRIBUTING.md`, `docs/` and simple Git metadata only. There must be no application code, build logs, private source archives, unsigned binaries or user data.

`gh-pages` is a **separate orphan branch** that initially contains **exactly**:

```text
.nojekyll
index.html
updates.json
```

The initial `updates.json` is the canonical empty update feed. Do not add `README.md`, source files, CI workflows, secrets, coverage reports, archives, binaries or dependencies to `gh-pages`.

## Enable GitHub Pages (owner action)

After both branches exist on GitHub:

1. Open `bochkov-anton/mux-releases` → **Settings** → **Pages**.
2. Under **Build and deployment**, select **Deploy from a branch**.
3. Choose branch **`gh-pages`** and folder **`/(root)`**. Click **Save**.
4. Wait for the real Pages deployment status to succeed and open:
   `https://bochkov-anton.github.io/mux-releases/`
5. Confirm that `https://bochkov-anton.github.io/mux-releases/updates.json` returns **HTTP 200** with the exact no-updates JSON, not GitHub's HTML 404 page.
6. Ensure this Pages site is dedicated **only to MUX release update metadata**; replacing branch content should not overwrite a personal website.

Do not select **GitHub Actions** as the Pages deployment source for this contract: the reviewed private CI uses a GitHub App token to update **only** `gh-pages/updates.json` in this public repository. GitHub's normal Pages branch build then serves the new bytes.

## Public GitHub App (owner action)

Configure a separate GitHub App installed **only on this public repository**, not on the private source. It requires repository **Contents: read/write** (release creation and the single update JSON file) and **Pages: read** (configuration validation), plus the standard Metadata read permission.

The private source CI protects `MUX_PUBLIC_APP_ID` and `MUX_PUBLIC_APP_PRIVATE_KEY` inside distinct reviewer-gated environments `mux-production-release` and `mux-production-feed`. It requests a separate short-lived token for each stage, explicitly restricted to repository `mux-releases`.

Neither a source-repository `GITHUB_TOKEN` with write authority nor a broad persistent personal access token should be used to publish public distribution files. Repository protection must account for the GitHub App's authorized Contents API update of `gh-pages`.

## Release flow

The private source workflow is deliberately manual and defaults to review-only. Once the exact signed XPI passes source, AMO and real Firefox checks, a reviewer may approve publishing the immutable XPI into a public GitHub Release.

The second protected environment checks that the same exact asset is **already publicly downloadable**, validates its SHA-256 and only then uses a GitHub Contents API `PUT` to update `gh-pages/updates.json` with a previous Git blob SHA. The final smoke check fetches both public URLs without authentication.

The public repository should not contain release tooling source or the CI evidence itself.

## Incident response and rollback boundaries

If an update is unsafe, approved maintainers can publish a canonical empty update manifest and verify that GitHub Pages serves it. They must not automatically delete past signed release assets, install a lower Firefox version, modify a user's Vault or assume a local database downgrade is possible.

A partially created GitHub Release draft, failed GitHub App API request or pending Pages build is an **uncertain external effect**, requiring inspection before a repeat. Never force-push the public `gh-pages` branch or replace a published XPI with different bytes just to make a workflow pass.

## Post-enable acceptance checklist

The repository is ready for the *next* release stage when:

- Public `main` shows only reviewed documentation, not private source.
- Public `gh-pages` tree has only the three initial files.
- GitHub Pages serves the empty manifest as HTTP 200 at the permanent URL.
- An installed, public-repo-only GitHub App exists with the minimum permissions.
- Protected approval is configured separately for source AMO signing, signed XPI publication and public feed update.
- Private GitHub CI is green on the intended immutable source revision.

**This checklist is not proof that Mozilla has signed a production XPI.** See [Release policy](../RELEASE_POLICY.md).
