# Security Policy

## Current status

The Premium main mod remains development build 1.0.4-dev.2. The original AppID application was declined without a stated reason. A real owner-performed dev.1 attempt failed at Minecraft Services login_with_xbox with HTTP 403 / Invalid app registration. No revised approval, completed Premium acceptance, production-ready release or independent security audit is claimed. This repository distributes documentation only.

## Authentication and session safeguards

- Publisher-owned public Microsoft application; no embedded client secret or third-party launcher application ID.
- Official system-browser authorization, PKCE/S256, state validation, loopback callback validation and single-use callback handling.
- Implemented Xbox/XSTS and Minecraft Services exchange, recognized Java-entitlement checks and authenticated profile validation before saving or activating a Microsoft profile; real post-login acceptance is blocked by service access.
- Windows DPAPI protection for persisted refresh and Minecraft access tokens, including backup copies. Profile metadata is not encrypted by this mechanism.
- Issuer-bound refresh tokens, rotation checkpoints, process coordination and bounded retries; ambiguous refresh POSTs are not blindly replayed. Classified permanent application or reauthentication errors pause automatic attempts in the running client.
- Disconnected-session guards, off-thread preparation, internal one-use activation permits and client-thread commit/rollback handling. Unverified snapshots and direct apply calls cannot activate a session through the mod's normal integration paths. Successful full Premium commit/rollback is still unverified.
- Premium-only entry points with no offline fallback. Legacy offline records and source are preserved separately from activation; a future addon is neither implemented nor approved.

These safeguards are implementation details, not a guarantee against all attacks. Malware running as the same Windows user, a compromised operating system, browser or Minecraft process, and disclosure of process memory or private files remain outside the protection provided by local credential encryption.

## Reporting a suspected vulnerability

Do not publish tokens, passwords, account files, backups, identifying logs or an exploitable vulnerability in a public issue.

If this repository offers GitHub private vulnerability reporting, use **Security > Report a vulnerability**. Otherwise, use a private contact route explicitly published by the repository owner on their GitHub profile. If none is available, open an issue asking for a private reporting channel with only a general description, such as "security contact requested". Do not include exploit details or personal data until a private route is established.

A useful private report describes the affected development build, expected and actual behavior, and minimal reproduction steps using synthetic accounts or redacted examples. Never include live access tokens or refresh tokens. No response-time or bounty commitment is made.

## Public repository boundary

The intended tracked files are README.md, PRIVACY.md, SECURITY.md and .gitignore. Mod source, executables, JARs, full project archives, Minecraft files, local configuration, credentials and logs belong outside this repository. The allowlist in .gitignore helps prevent accidental staging; it does not replace reviewing every staged change and must never be bypassed to upload private files.
