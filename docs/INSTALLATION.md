# Installing MUX in Firefox

**The first production release has not been published yet.** Do not install an unsigned experimental build as a substitute.

## Requirements

- Firefox Desktop **128 or newer**.
- A normal Firefox profile capable of installing Mozilla-signed add-ons.
- A verified signed XPI from the [official MUX Releases page](https://github.com/bochkov-anton/mux-releases/releases).

Firefox Android and cross-device session synchronization are not guaranteed by the desktop release.

## Install a signed release

When an official release appears:

1. Open its GitHub Release page and review the stated Firefox requirements and release notes.
2. Download the exact `mux-<full-private-source-commit>.xpi` asset from that release. Never download an asset from a third-party mirror or a mutable `latest.xpi` URL.
3. In Firefox, open `about:addons`, select the gear menu, choose **Install Add-on From File…**, and select the downloaded XPI.
4. Allow Firefox to authenticate the Mozilla signature **with its default signature enforcement enabled**. If Firefox reports an unsigned or incompatible extension, stop; do not disable signature checks or migrate user data to make installation succeed.
5. Confirm that MUX appears under Extensions and that its sidebar opens. Create a synthetic test account/context before importing any important metadata.
6. If updating from an existing supported MUX version, back up registry metadata and any opted-in encrypted Vault first. A source downgrade is not proof that local database schema migrations can be reversed.

The published SHA-256 digest provides byte integrity. **Only Firefox/Mozilla signature enforcement authenticates the add-on signature**, not a locally generated checksum.

## Automatic updates

The extension's permanent update channel is:

`https://bochkov-anton.github.io/mux-releases/updates.json`

Initially, the URL advertises **zero** releases. After the owner's Pages configuration is enabled, a successful HTTP 200 for a no-updates manifest is normal. Firefox will only be offered versions that passed the signed-release gates and whose XPI URL/hash match the approved release.

The update feed cannot change the extension's Gecko ID or retroactively configure builds installed without this URL.

## Devices, browser sessions and passwords

MUX can isolate accounts into Firefox Containers and store local account metadata. Users may choose to keep credentials/TOTP in a locally encrypted Vault and manually export an encrypted archive.

**It does not copy an authenticated website session to another device.** Importing a registry or Vault backup does not log you into OpenAI, Google or other websites. Firefox cookies and contextual identities belong to the local browser profile and must not be assumed portable.

If a profile reports corruption or unexpected missing contexts after migration, keep the backup and contact the maintainer without posting private data in a public issue.

## Установка — кратко

Пока **нет опубликованного Mozilla-signed XPI**. После первого релиза откройте [Releases](https://github.com/bochkov-anton/mux-releases/releases), скачайте подписанный файл и установите его через `about:addons` → меню с шестерёнкой → **Install Add-on From File**. Не отключайте проверку подписи Firefox. Архив Vault и метаданные можно переносить вручную, но действующий вход на сайты и cookies не переносятся.

See [Release integrity](RELEASE_INTEGRITY.md) and [FAQ](FAQ.md).
