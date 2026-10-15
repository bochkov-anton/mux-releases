# MUX — Firefox Releases

**Status: preparing the first signed release. No production XPI has been published yet.**

This is the **public distribution repository** for MUX, a Firefox Desktop extension for managing separate browser account contexts, local account metadata, and an optional encrypted credential and TOTP vault.

The source repository, its Git history, build infrastructure, and signing evidence remain **private**. This repository is intentionally not a source-code mirror.

## Getting MUX

The first official download will appear under [GitHub Releases](https://github.com/bochkov-anton/mux-releases/releases) **only after Mozilla unlisted signing and real Firefox verification succeed**. Until a signed release appears, there is nothing here that should be installed as a production add-on. Do not use a random unsigned XPI or disable Firefox's signature enforcement.

When a verified release is available, use the [installation guide](docs/INSTALLATION.md) and verify its signed status in Firefox.

### Firefox update channel

The permanent Firefox update endpoint is:

**https://bochkov-anton.github.io/mux-releases/updates.json**

Its initial state intentionally contains **no advertised updates**. An empty update list means "no release is being offered", **not** an installation error. After this repository's owner enables GitHub Pages from the `gh-pages` branch, the endpoint will be publicly reachable. Signed XPI binaries are hosted as immutable GitHub Release assets; Pages hosts only lightweight update metadata.

## What MUX does — and does not do

MUX manages isolated Firefox account contexts and locally stored account metadata. Its optional Vault can keep user-entered credentials and TOTP seeds encrypted **locally**, and it supports user-mediated encrypted backups.

MUX **does not synchronize website login sessions or cookies between devices**. Moving registry data or an encrypted Vault archive between devices does not restore the other device's authenticated browser sessions. Each Firefox profile maintains its own browser contexts.

Current primary target: **Firefox Desktop, version 128 or newer**. Android functionality and compatibility are not implied by desktop releases.

## Release integrity

Published releases must use:

- An immutable tag `mux-v<VERSION>` with exactly one Mozilla-signed `mux-<40-character-source-commit>.xpi` asset.
- A SHA-256 digest matching the independently reviewed signed archive.
- A successful installation in **normal Firefox with signature checks enabled**, followed by restart and local account/Vault continuity tests.
- An update manifest pointing **only** to the exact matching signed asset. No automatic downgrade and no `latest.xpi` redirect.

Read the [release policy](RELEASE_POLICY.md), [integrity and trust guide](docs/RELEASE_INTEGRITY.md), and [update channel contract](docs/UPDATE_CHANNEL.md).

## Documentation

| Topic | Document |
| --- | --- |
| Installing and verifying a signed release | [Installation](docs/INSTALLATION.md) |
| Update feed, versioning and delivery | [Update channel](docs/UPDATE_CHANNEL.md) |
| Signed XPI verification and provenance limits | [Release integrity](docs/RELEASE_INTEGRITY.md) |
| GitHub Pages enablement and incident response | [Repository operations](docs/OPERATIONS.md) |
| Privacy, session isolation and device transfers | [FAQ](docs/FAQ.md) |
| Reporting a security issue safely | [Security policy](SECURITY.md) |
| Public issue and documentation contributions | [Contributing](CONTRIBUTING.md) |

## Кратко по-русски

**Это публичный репозиторий релизов MUX, а не исходного кода.** Первая версия для обычного Firefox пока не опубликована: сначала необходимы подпись Mozilla и проверка установки. После выпуска XPI появится в разделе [Releases](https://github.com/bochkov-anton/mux-releases/releases).

Синхронизация учётных записей и зашифрованных архивов **не означает перенос действующих авторизованных сессий или cookies**. На другом устройстве вход на сайты выполняется отдельно. Приватные данные, пароли и TOTP не размещаются в этом репозитории.

**Never post passwords, Vault archives, TOTP seeds, cookies, recovery codes or private browser profiles in public issues.**
