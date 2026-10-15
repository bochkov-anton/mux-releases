# MUX Release FAQ

### Is there a production release I can install now?

Not yet. The public repository is prepared for distribution, but a real Mozilla-signed XPI must first pass independent normal-Firefox and Vault conformance checks. The empty `updates.json` means no version is currently advertised.

### Why is the source code not in this repository?

The main project source, signing workflow, dependency locks and test artifacts are stored in a separate private repository. This repository deliberately exposes only public documentation, signed binaries after review and update metadata. It is **not** a Git mirror of the private project.

### Does MUX copy website sessions and cookies between computers?

No. Firefox browser contexts and third-party authentication cookies are local to the browser profile. Importing an account registry or encrypted Vault backup on a different device does not make websites consider that device already signed in.

### Can credentials or TOTP seeds be transferred?

MUX's optional local encrypted Vault supports user-mediated encrypted backups. Passwords/TOTP are not kept in the ordinary registry export and never belong in this public distribution repository. A user must explicitly export/import a protected archive and unlock it locally.

### What does a Mozilla-signed XPI guarantee?

It confirms that Firefox accepts the package as signed by Mozilla. A SHA-256 digest helps verify the exact downloaded bytes. Neither mechanism by itself guarantees that every feature is bug-free; each release also requires source-bound tests and a real Firefox installation/restart check.

### Why is the update feed empty?

Until a signed release is published, there is no version to advertise. A small valid empty manifest prevents Firefox from being offered an unsigned or speculative build.

### What happens if a bad release is discovered?

The maintainer can temporarily advertise no new updates while investigating. Already installed extensions remain installed, and local browser databases are not automatically rolled back.

### Can I use the Firefox Android edition?

This distribution is desktop-first. Android behavior and account-container capabilities require separate review and are not implied by a desktop XPI.

### How do I report bugs?

For non-sensitive compatibility and documentation issues, open a public issue without private user data. Security vulnerabilities should follow [the security policy](../SECURITY.md), not a public issue.
