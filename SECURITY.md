# Security Policy

## Supported release status

There is **no publicly certified production XPI yet**. Only a release that has been signed by Mozilla, validated in normal Firefox, and linked from this repository's official Releases section should be considered a supported distribution artifact.

Security updates will be offered through the fixed HTTPS update manifest once the first supported release is published. The update feed will not advertise an unsigned or unreviewed archive.

## Reporting vulnerabilities

Please report suspected security issues **privately**, without publishing exploit details or sensitive test data in a public issue.

If the repository's **Private vulnerability reporting** option is enabled, open the repository's **Security → Report a vulnerability** form. Otherwise, contact the repository maintainer through a private GitHub channel and request a secure reporting path before supplying details. Do not assume a public GitHub issue is confidential.

For a useful, privacy-preserving report, include the affected MUX release version, Firefox version and operating system, steps using disposable synthetic data, the expected behavior and the observed behavior. Do not attach real login credentials, TOTP seeds, browser session cookies, private profile directories or encrypted Vault archives.

## Boundaries and expectations

- Browser account containers, encrypted Vault data and registry records stay in the user's Firefox profile unless the user explicitly exports a backup.
- Transferring a backup does not transfer authenticated third-party site sessions.
- Mozilla's real Firefox add-on signature check is authoritative for installability; a local checksum alone is not proof of signing.
- Signed XPI assets must be bound to a fixed Git source revision and checked against their published SHA-256.
- Production publication and changes to `gh-pages/updates.json` require separate, explicitly approved workflows.
- A pause of the update feed stops **new version advertisements**; it does not remove already installed extensions or undo local data migrations.

## Coordinated handling

After receiving a security report, the maintainer may temporarily pause update advertisements, investigate the affected version, publish an independently verified signed replacement and issue release notes. The public repository must not be used to store private investigation materials or user data.
