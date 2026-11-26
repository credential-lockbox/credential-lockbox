# Security policy — Credential Lockbox

This project is a security pattern; flaws in it matter more than most bugs.

## Supported versions

Security fixes go into the latest release only: <https://github.com/credential-lockbox/credential-lockbox/releases/latest>. Older releases get no backports. This section (the table and the upgrade notes) is updated with each release.

| Version | Supported | Released as |
| --- | --- | --- |
| 0.4.0 (the latest release) | Yes | `v0.4.0`, from this repository |
| 0.3.2 | No (same scripts as 0.4.0) | `v0.3.2`, from this repository |
| 0.3.1 | No (same scripts as 0.4.0) | `v0.3.1`, from this repository |
| 0.3.0 | No (same scripts as 0.4.0) | `credential-lockbox-v0.3.0`, from `cmeans/muse-field-kit` |
| 0.2.1 | No | `encrypted-credential-handoff-v0.2.1`, from `cmeans/muse-field-kit` |
| 0.2.0 | No | `v0.2.0`, from `cmeans/muse-field-kit` |
| 0.1.0 | No | `v0.1.0`, from `cmeans/muse-field-kit` |

**What an upgrade involves:**

- **From 0.3.2.** Nothing changes for a setup with the script as the user's side: the scripts are byte-identical, and 0.4.0 changes only the instructions, adding the app as an optional user side ([`CHANGELOG.md`](CHANGELOG.md), 0.4.0). An app setup made under 0.3.2 as a mechanism change of its own can now follow [`SETUP.md`](SETUP.md)'s "The app as the user's side": check it against that section, record what it asks for, and keep the core's step 4 comparison in chat.
- **From 0.3.0 or 0.3.1.** No new key, recipient or re-staging. 0.3.0's, 0.3.1's, 0.3.2's and 0.4.0's scripts are byte-identical, so such an install has nothing to fix today. One still on a `cmeans/muse-field-kit` clone keeps working at its tag: field-kit's `main` no longer holds the scripts, so don't update that clone to `main`. Pointing its wrappers at a clone of this repository changes the helper's path, which [`SETUP.md`](SETUP.md) counts as a mechanism change: a written proposal, the user's approval and a fresh dummy round-trip. Make that change when a release changes a script, or earlier if you choose. Its installed skill can be reinstalled from this repository; that changes nothing that runs.
- **From 0.2.1.** No new key. All four scripts changed in 0.3.0, which also renamed the folder and the skill ([`CHANGELOG.md`](CHANGELOG.md), 0.3.0). So the user downloads their platform's script (`handoff.sh` or `handoff.ps1`) from the latest release, the agent's recorded sums change (a mechanism change), and the skill is reinstalled as `credential-lockbox`.
- **From 0.2.0.** Everything for 0.2.1, and first check each wrapper and the key folder against 0.2.1's new refusals (CHANGELOG, 0.2.1): `consume.py` refuses an `--env` target that isn't a credential variable's name (#78), and a key folder owned by another account (not this one or root), or that a group or others can write to (#86). Changing a wrapper or moving the key is a mechanism change too.
- **From 0.1.0.** Set up again: 0.2.0 replaced the cryptography (RSA through OpenSSL) with `age`.

## Reporting

- Report it privately at https://github.com/credential-lockbox/credential-lockbox/security/advisories/new (or: this repository's **Security and quality** tab, which may be under the "…" menu on a narrow window, then **Report a vulnerability**). You need to be signed in to GitHub. Only you and the repository's maintainers see the report, and it and any fix can be discussed there before disclosure.
- Please do **not** open a public issue for a security problem. If you can't use a private advisory, open a public issue with the [Security contact request](../../issues/new?template=security_contact.yml) form instead: it asks for no details, and the maintainer arranges a private channel.
- Reports about the *pattern* (a way the invariants fail even when the scripts are used as documented) are as welcome as reports about the scripts.
- Reports about the releases made in `cmeans/muse-field-kit` (0.3.0 and older) come here too.

## Scope notes

- The threat model and the ten invariants in [`README.md`](README.md) define what this pattern claims to defend against. A report that something in the “does not defend against” list is indeed not defended is a documentation discussion, not a vulnerability — but if the README's wording anywhere overstates the defended side, that overstatement is itself worth reporting.
- The identity under `test/` (`test-dummy-identity.txt`) is a published, throwaway test vector. It protects nothing; never use it for a real credential.
