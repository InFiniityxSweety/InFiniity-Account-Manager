# Privacy Notice

Last updated: November 4, 2026.

InFiniity Account Manager is an independent, unofficial project maintained by InFiniityxSweety. It is not approved by or associated with Mojang or Microsoft.

This notice describes the private Premium main mod, development build 1.0.4-dev.3. The original AppID application was declined without a stated reason; a real attempt on dev.1 failed at Minecraft Services with Invalid app registration. No revised approval or completed Premium acceptance is claimed. This repository provides documentation only and operates no account service.

## Information used by the mod

For Microsoft-authenticated profiles, the mod processes the Minecraft player name, profile UUID, profile/skin information, account type, favorites, Microsoft refresh token, Minecraft Services access token, token expiry and the public application ID that issued the authorization. Short-lived Microsoft, Xbox and XSTS tokens and OAuth state/PKCE values are used during authentication. Microsoft passwords are entered only on Microsoft's sign-in pages and are not requested, received or stored by the mod.

Existing offline records from earlier combined versions retain their chosen name, derived offline UUID, profile type and favorites. The Premium main mod preserves them in the shared storage but does not display, create, activate or manage them. The earlier offline source is retained separately; a possible future addon is not implemented or enabled. Offline records carry no Microsoft refresh credentials and do not prove Minecraft ownership.

## Storage and protection

Saved data is held in the current Windows user's local InFiniity Account Manager data directory. Refresh and Minecraft access tokens are encrypted using Windows DPAPI, including their copies in the mod's backup files. Profile metadata such as player names, UUIDs, account type and favorites remains readable in the local account file. The application identifier is public and is not a secret.

Atomic writes, backups, recovery and process locks reduce the risk of accidental data loss. DPAPI is tied to the Windows user and is not protection against malicious software running with that user's access. Sensitive data must be available in process memory when used. Local operating-system, browser and game caches are governed by their own behavior.

## Network communication

When the user adds, renews or uses a Microsoft profile, the client communicates directly with Microsoft's identity platform, Xbox Live/XSTS and Minecraft Services. The local HTTP callback receives the browser's authorization response on a loopback interface; token exchanges use HTTPS. Profile and skin display can use Minecraft's profile and texture services. Joining a multiplayer server also communicates the selected player identity as part of Minecraft's normal connection process.

The mod has no maintainer-operated authentication backend, account synchronization, advertising or analytics service. It does not send saved accounts or tokens to the maintainer. Microsoft, Mojang, hosting providers, browser software and multiplayer server operators process their own traffic under their respective policies. Users should review Microsoft's [privacy statement](https://privacy.microsoft.com/privacystatement).

## Retention and user control

Saved profiles remain available until the user removes them or deletes the local data. Users can remove saved Microsoft profiles in the Premium UI; retained offline records are not managed there. Removing a saved entry does not necessarily end an already active Minecraft session or revoke Microsoft's authorization. Users can manage or revoke application permissions through their Microsoft account, and should close Minecraft when ending use of an active session.

Local backups, user-created copies, operating-system backups and caches may retain previous data. No claim of secure erasure is made. Do not publish account files, backups, crash dumps or logs without checking them for private data.

## This GitHub repository

Only documentation and an exclusion policy are intended for this repository. Do not post passwords, tokens, account files, private configuration or identifiable logs in issues or discussions. GitHub processes visits, account information and contributions under its own [privacy statement](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement).

For general, non-confidential questions about this notice, contact **InFiniityxSweety** through this repository's [GitHub Issues](https://github.com/InFiniityxSweety/InFiniity-Account-Manager/issues). Issues are public: use a general description without personal information or account details. No general private privacy-support channel is currently documented. GitHub Private Vulnerability Reporting is enabled for security vulnerabilities as described in [Security](SECURITY.md); it is not a general private messaging or privacy-support channel. Never send passwords, authentication codes, access or refresh tokens, or complete account files through any reporting route.
