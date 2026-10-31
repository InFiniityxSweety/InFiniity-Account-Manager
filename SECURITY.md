# Security Policy

## Current status

InFiniity Account Manager is in private development. Minecraft AppID approval and real Microsoft/Premium end-to-end acceptance are pending. No production-ready Premium release or security audit is claimed. This repository distributes documentation only.

## Authentication and session safeguards

- Publisher-owned public Microsoft application; no embedded client secret or third-party launcher application ID.
- Official system-browser authorization, PKCE/S256, state validation, loopback callback validation and single-use callback handling.
- Xbox/XSTS and Minecraft Services token exchange, authenticated entitlement checks and Minecraft profile retrieval before saving a Microsoft profile.
- Windows DPAPI protection for persisted refresh and Minecraft access tokens, including backup copies. Profile metadata is not encrypted by this mechanism.
- Persisted refresh-token rotation, bounded retries for applicable temporary service failures, and reauthentication when authorization is revoked.
- Disconnected-session switching guards and rollback handling. Offline profiles cannot provide Microsoft/Minecraft authentication or bypass an online-mode server.

These safeguards are implementation details, not a guarantee against all attacks. Malware running as the same Windows user, a compromised operating system, browser or Minecraft process, and disclosure of process memory or private files remain outside the protection provided by local credential encryption.

## Reporting a suspected vulnerability

Do not publish tokens, passwords, account files, backups, identifying logs or an exploitable vulnerability in a public issue.

If this repository offers GitHub private vulnerability reporting, use **Security > Report a vulnerability**. Otherwise, use a private contact route explicitly published by the repository owner on their GitHub profile. If none is available, open an issue asking for a private reporting channel with only a general description, such as "security contact requested". Do not include exploit details or personal data until a private route is established.

A useful private report describes the affected development build, expected and actual behavior, and minimal reproduction steps using synthetic accounts or redacted examples. Never include live access tokens or refresh tokens. No response-time or bounty commitment is made.

## Public repository boundary

The intended tracked files are README.md, PRIVACY.md, SECURITY.md and .gitignore. Mod source, executables, JARs, full project archives, Minecraft files, local configuration, credentials and logs belong outside this repository. The allowlist in .gitignore helps prevent accidental staging; it does not replace reviewing every staged change and must never be bypassed to upload private files.
