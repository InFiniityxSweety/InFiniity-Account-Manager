# Security Policy

## Current status

InFiniity Account Manager is an independent, unofficial project maintained by InFiniityxSweety. It is not approved by or associated with Mojang or Microsoft.

The Premium main mod is development build 1.0.4-dev.3. This build adds the independence notice in the existing account-information area, checked in isolated clients; authentication and account-management behavior are unchanged from dev.2. The original AppID application was declined without a stated reason. A real owner-performed dev.1 attempt failed at Minecraft Services login_with_xbox with HTTP 403 / Invalid app registration. No revised approval, completed Premium acceptance, production-ready release or independent security audit is claimed. This repository distributes documentation only.

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

Do not post vulnerabilities, exploit details, sensitive evidence, identifying logs, account files or backups in public issues.

**GitHub Private Vulnerability Reporting is enabled, verified on November 4, 2026.** For security vulnerabilities, use [Report a vulnerability](https://github.com/InFiniityxSweety/InFiniity-Account-Manager/security/advisories/new), available under **Security and quality > Advisories > Report a vulnerability**. GitHub sign-in is required. The enabled API status and the actual reporting link on the public Advisories page were checked; no test report was submitted.

General questions, bug reports and feature requests belong in [GitHub Issues](https://github.com/InFiniityxSweety/InFiniity-Account-Manager/issues). Issues are public: do not include vulnerabilities, exploit details, personal information or sensitive evidence. Private vulnerability reporting is for security vulnerabilities, not general support, private messaging or privacy requests.

A useful private report describes the affected development build, expected and actual behavior, and minimal reproduction steps using synthetic accounts or redacted examples. Never send passwords, authentication codes, access or refresh tokens, or complete account files, even through a private route. No response-time, support or bounty commitment is made.

## Public repository boundary

The intended tracked files are README.md, PRIVACY.md, SECURITY.md and .gitignore. Mod source, executables, JARs, full project archives, Minecraft files, local configuration, credentials and logs belong outside this repository. The allowlist in .gitignore helps prevent accidental staging; it does not replace reviewing every staged change and must never be bypassed to upload private files.
