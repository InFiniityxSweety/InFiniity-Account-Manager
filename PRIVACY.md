# Privacy Notice

Last updated: October 31, 2026.

This notice describes the current private InFiniity Account Manager implementation. Minecraft AppID approval and real Premium end-to-end acceptance are pending. This repository provides public documentation only; it does not operate an account service.

## Information used by the mod

For Microsoft-authenticated profiles, the mod processes the Minecraft player name, profile UUID, profile/skin information, account type, favorites, Microsoft refresh token, Minecraft Services access token, token expiry and the public application ID that issued the authorization. Short-lived Microsoft, Xbox and XSTS tokens and OAuth state/PKCE values are used during authentication. Microsoft passwords are entered only on Microsoft's sign-in pages and are not requested, received or stored by the mod.

For local offline profiles, it stores the chosen name, derived offline UUID, profile type and favorites. Offline profiles are not Microsoft accounts and do not prove Minecraft ownership.

## Storage and protection

Saved data is held in the current Windows user's local InFiniity Account Manager data directory. Refresh and Minecraft access tokens are encrypted using Windows DPAPI, including their copies in the mod's backup files. Profile metadata such as player names, UUIDs, account type and favorites remains readable in the local account file. The application identifier is public and is not a secret.

Atomic writes, backups, recovery and process locks reduce the risk of accidental data loss. DPAPI is tied to the Windows user and is not protection against malicious software running with that user's access. Sensitive data must be available in process memory when used. Local operating-system, browser and game caches are governed by their own behavior.

## Network communication

When the user adds, renews or uses a Microsoft profile, the client communicates directly with Microsoft's identity platform, Xbox Live/XSTS and Minecraft Services. The local HTTP callback receives the browser's authorization response on a loopback interface; token exchanges use HTTPS. Profile and skin display can use Minecraft's profile and texture services. Joining a multiplayer server also communicates the selected player identity as part of Minecraft's normal connection process.

The mod has no maintainer-operated authentication backend, account synchronization, advertising or analytics service. It does not send saved accounts or tokens to the maintainer. Microsoft, Mojang, hosting providers, browser software and multiplayer server operators process their own traffic under their respective policies. Users should review Microsoft's [privacy statement](https://privacy.microsoft.com/privacystatement).

## Retention and user control

Saved profiles remain available until the user removes them or deletes the local data. Users can remove individual profiles in the mod. Removing a saved entry does not necessarily end an already active Minecraft session or revoke Microsoft's authorization. Users can manage or revoke application permissions through their Microsoft account, and should close Minecraft when ending use of an active session.

Local backups, user-created copies, operating-system backups and caches may retain previous data. No claim of secure erasure is made. Do not publish account files, backups, crash dumps or logs without checking them for private data.

## This GitHub repository

Only documentation and an exclusion policy are intended for this repository. Do not post passwords, tokens, account files, private configuration or identifiable logs in issues or discussions. GitHub processes visits, account information and contributions under its own [privacy statement](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement).

For privacy questions, use the maintainer contact options shown on the repository owner's GitHub profile. If no private contact route is available, post only a general request for contact without personal data. Never send credentials.
