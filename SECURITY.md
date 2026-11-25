# Security policy — Credential Lockbox

This project is a security pattern; flaws in it matter more than most bugs.

## Supported versions

Security fixes go into the latest release only. Older releases get no backports, so upgrade to the latest: <https://github.com/credential-lockbox/credential-lockbox/releases/latest>.

| Version | Supported | Notes |
| --- | --- | --- |
| 0.3.x (the latest release) | Yes | `v0.3.1` and later, released from this repository. Their scripts are byte-identical to 0.3.0's, so a 0.3.0 install upgrades without setting up again. |
| 0.3.0 | No | Released as `credential-lockbox-v0.3.0` from `cmeans/muse-field-kit`, before the move. It keeps working there, but fixes go into this repository's releases. |
| 0.2.x | No | Released as `encrypted-credential-handoff-v0.2.1` and `v0.2.0`, from `cmeans/muse-field-kit`. Upgrade to the latest; 0.3.0 renamed the folder and the skill ([`CHANGELOG.md`](CHANGELOG.md)). |
| 0.1.x | No | 0.2.0 replaced its cryptography (RSA through OpenSSL) with `age`; a 0.1.x install sets up again. |

## Reporting

- Report it privately at https://github.com/credential-lockbox/credential-lockbox/security/advisories/new (or: this repository's **Security and quality** tab, which may be under the "…" menu on a narrow window, then **Report a vulnerability**). You need to be signed in to GitHub. Only you and the repository's maintainers see the report, and it and any fix can be discussed there before disclosure.
- Please do **not** open a public issue for a security problem. If you can't use a private advisory, open a public issue with the [Security contact request](../../issues/new?template=security_contact.yml) form instead: it asks for no details, and the maintainer arranges a private channel.
- Reports about the *pattern* (a way the invariants fail even when the scripts are used as documented) are as welcome as reports about the scripts.

## Scope notes

- The threat model and the ten invariants in [`README.md`](README.md) define what this pattern claims to defend against. A report that something in the “does not defend against” list is indeed not defended is a documentation discussion, not a vulnerability — but if the README's wording anywhere overstates the defended side, that overstatement is itself worth reporting.
- The identity under `test/` (`test-dummy-identity.txt`) is a published, throwaway test vector. It protects nothing; never use it for a real credential.
