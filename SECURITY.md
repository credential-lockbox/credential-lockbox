# Security policy — Credential Lockbox

This project is a security pattern; flaws in it matter more than most bugs.

## Supported versions

Security fixes go into the latest release only: <https://github.com/credential-lockbox/credential-lockbox/releases/latest>. Older releases get no backports. This table is updated with each release.

| Version | Supported | Released as |
| --- | --- | --- |
| 0.3.2 (the latest release) | Yes | `v0.3.2`, from this repository |
| 0.3.1 | No (same scripts as 0.3.2) | `v0.3.1`, from this repository |
| 0.3.0 | No (same scripts as 0.3.2) | `credential-lockbox-v0.3.0`, from `cmeans/muse-field-kit` |
| 0.2.x | No | `encrypted-credential-handoff-v0.2.1` and `v0.2.0`, from `cmeans/muse-field-kit` |
| 0.1.x | No | `v0.1.0`, from `cmeans/muse-field-kit` |

**What an upgrade involves:**

- **From 0.3.0 or 0.3.1.** No new key, recipient or re-staging. 0.3.0's, 0.3.1's and 0.3.2's scripts are byte-identical, so a 0.3.0 or 0.3.1 install has nothing to fix today and keeps working where it is. Pointing an install's wrappers at a clone of this repository changes the helper's path, which [`SETUP.md`](SETUP.md) counts as a mechanism change: a written proposal, the user's approval and a fresh dummy round-trip. Make that change when a release changes a script, or earlier if you choose.
- **From 0.2.x.** No new key. 0.3.0 renamed the folder and the skill ([`CHANGELOG.md`](CHANGELOG.md), 0.3.0), and `handoff.sh` and `consume.py` changed since 0.2.1. So the user downloads the latest release's script, the agent's recorded sums change (a mechanism change), and the skill is reinstalled as `credential-lockbox`.
- **From 0.1.x.** Set up again: 0.2.0 replaced the cryptography (RSA through OpenSSL) with `age`.

## Reporting

- Report it privately at https://github.com/credential-lockbox/credential-lockbox/security/advisories/new (or: this repository's **Security and quality** tab, which may be under the "…" menu on a narrow window, then **Report a vulnerability**). You need to be signed in to GitHub. Only you and the repository's maintainers see the report, and it and any fix can be discussed there before disclosure.
- Please do **not** open a public issue for a security problem. If you can't use a private advisory, open a public issue with the [Security contact request](../../issues/new?template=security_contact.yml) form instead: it asks for no details, and the maintainer arranges a private channel.
- Reports about the *pattern* (a way the invariants fail even when the scripts are used as documented) are as welcome as reports about the scripts.
- Reports about the releases made in `cmeans/muse-field-kit` (0.3.0 and older) come here too.

## Scope notes

- The threat model and the ten invariants in [`README.md`](README.md) define what this pattern claims to defend against. A report that something in the “does not defend against” list is indeed not defended is a documentation discussion, not a vulnerability — but if the README's wording anywhere overstates the defended side, that overstatement is itself worth reporting.
- The identity under `test/` (`test-dummy-identity.txt`) is a published, throwaway test vector. It protects nothing; never use it for a real credential.
