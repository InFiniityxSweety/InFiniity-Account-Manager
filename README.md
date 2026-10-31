# InFiniity Account Manager

InFiniity Account Manager is an independent client-side account-management mod for **Minecraft: Java Edition 26.2**, using **Fabric** and **Java 25**. Its purpose is to let players manage their own Microsoft-authenticated Minecraft profiles and local offline profiles within an already installed Minecraft client.

**Development status: Minecraft AppID approval is pending. Real Microsoft sign-in, token renewal and Premium session switching have not yet completed end-to-end acceptance. No approved Premium release is offered here.**

This public repository contains project, privacy and security documentation for the Minecraft AppID review. The implementation remains private. This repository contains no mod binaries, source archives, Minecraft files or account data.

## Microsoft-authenticated profiles

The implemented sign-in flow opens the official Microsoft authorization page in the user's system browser. It uses a publisher-owned public desktop application, Authorization Code flow with PKCE/S256, a per-attempt state value and a local loopback callback. Users do not enter passwords, authorization codes, client IDs or client secrets into the mod. Microsoft handles sign-in and consent.

After authorization, the implementation exchanges tokens through Xbox Live and XSTS, then requests a Minecraft Services access token. Before saving a Microsoft profile, it checks the authenticated Minecraft entitlements endpoint and retrieves that account's Minecraft Java profile and UUID. A local profile name or skin is not proof of game ownership.

The application is intended to support multiple personal Microsoft accounts with valid Minecraft Java entitlement, rather than a developer-account whitelist. It uses only its own registered application ID:

`99c1f63b-5374-4f4b-a973-0531329a718d`

The registered desktop redirect is `http://localhost/callback`; each attempt uses an available local port. This public application identifier is not a secret. No client secret is used.

## Sessions and local storage

The implementation provides automatic renewal of expiring saved sessions, manual renewal and browser reauthentication when required. Refresh-token rotation is persisted before subsequent Xbox or Minecraft requests. Temporary failures retain saved accounts; revoked authorization requires Microsoft sign-in again.

Profile activation is designed to replace the Minecraft client session and associated authentication services without restarting Minecraft. Switching is restricted to a disconnected client and includes rollback on failure. The account list supports double-click activation and shows the actual active session.

Account data is stored locally on Windows. Refresh and Minecraft access tokens are encrypted with Windows DPAPI under the current Windows user. Account names, UUIDs, profile types and favorites are local metadata and are not encrypted by the credential encryption. Storage includes atomic replacement, encrypted credential backups, recovery handling and process locks. See [Privacy](PRIVACY.md) and [Security](SECURITY.md) for limitations.

## Local offline profiles

Local offline profiles contain a locally chosen name and a derived offline UUID. They do not sign in to Microsoft, hold a Minecraft Services access token, prove a Minecraft license or establish ownership of a Microsoft account or player name. They are displayed separately from Microsoft-authenticated profiles.

They are intended for local play and permitted testing, including servers explicitly configured by their operators to accept offline identities. They cannot authenticate to servers that require a valid Microsoft/Minecraft session. The mod does not change a server's authentication settings or bypass Microsoft, Xbox, Minecraft Services or server authentication. Offline profiles are not a substitute for obtaining Minecraft through authorized channels and complying with its terms.

## What has been tested

As of October 31, 2026, the private development build has completed:

- A clean Gradle build and 79 automated Java tests, including simulated Microsoft/Xbox/Minecraft responses, real local HTTP callbacks, PKCE and state checks, encrypted persistence, refresh rotation, failure handling and rollback.
- 21 isolated runtime checks on each of Fabric Loader 0.19.3 and 0.20.1 with the registered application configured, including actual local offline-server joins with two selected identities, persistence and UI regression checks.
- An unauthenticated live Microsoft authorization check: the provider redirected to the registered localhost callback with `login_required`. This confirms callback routing without signing in or obtaining tokens.

Simulated services and offline joins do **not** demonstrate a successful real Microsoft login or Premium session switch. Minecraft AppID review has not yet been submitted. Real acceptance still needs authorized test accounts and must cover multiple Premium profiles, renewal, restart persistence, Premium/offline switching and authenticated server joins. Approval will only be stated after it is actually granted; release readiness depends on successful real acceptance.

## Project information

- [Privacy notice](PRIVACY.md)
- [Security policy](SECURITY.md)
- [Microsoft Authorization Code flow and PKCE](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-auth-code-flow)
- [Microsoft loopback redirect rules](https://learn.microsoft.com/en-us/entra/identity-platform/reply-url)
- [Minecraft EULA](https://www.minecraft.net/en-us/eula)

This is an unofficial community project, not an official Minecraft product. It is not approved by or associated with Mojang or Microsoft. Minecraft, Microsoft and Xbox names belong to their respective owners.
