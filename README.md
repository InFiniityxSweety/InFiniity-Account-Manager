# InFiniity Account Manager

**NOT AN OFFICIAL MINECRAFT PRODUCT.**  
**NOT APPROVED BY OR ASSOCIATED WITH MOJANG OR MICROSOFT.**

InFiniity Account Manager is an independent client-side Premium account-management mod for **Minecraft: Java Edition 26.2**, **Fabric** and **Java 25** on Windows. Development build **1.0.4-dev.3** is intended to manage the user's own licensed Microsoft/Minecraft Java profiles within an existing Minecraft installation, including CurseForge. The earlier combined Premium/offline implementation is retained separately as described below.

**Status — November 4, 2026:** The original AppID application was declined without a stated reason. An owner-performed real attempt on development build 1.0.4-dev.1 reached `/authentication/login_with_xbox` and failed with HTTP 403, `Invalid app registration`, identified through the specific safe error path. No revised application has been submitted or approved. Completed Minecraft authentication, real Premium switching, renewal, online-mode joins and CurseForge runtime acceptance remain unverified; service access blocks the Premium acceptance steps.

This public repository contains project, privacy and security documentation for the Minecraft AppID review. The implementation remains private. This repository contains no mod binaries, source archives, Minecraft files or account data.

Compared with dev.2, dev.3 adds the two-line independence notice in the existing account-information area. The accepted account list, switch glyph, player heads and Vanilla button positions remain unchanged. Authentication and account-management behavior are unchanged; development diagnostics were extended to verify the notice and actual GUI scale.

## Microsoft-authenticated profiles

The implemented sign-in flow opens the official Microsoft authorization page in the user's system browser. It uses a publisher-owned public desktop application, Authorization Code flow with PKCE/S256, a per-attempt state value and a local loopback callback. Users do not enter passwords, authorization codes, client IDs or client secrets into the mod. Microsoft handles sign-in and consent.

The implemented path exchanges tokens through Xbox Live and XSTS, then requests a Minecraft Services access token. Before saving a Microsoft profile or activating a cached session, it requires a recognized Java entitlement (`game_minecraft` or `product_minecraft`) and a matching authenticated Minecraft profile. A local name, skin or stored Microsoft label is insufficient. These post-login checks are tested with simulated services; the real attempt was blocked before they could be accepted against Minecraft Services.

The application is intended to support multiple personal Microsoft accounts with valid Minecraft Java entitlement, rather than a developer-account whitelist. It uses only its own registered application ID:

`99c1f63b-5374-4f4b-a973-0531329a718d`

The registered desktop redirect is `http://localhost/callback`; each attempt uses an available local port. This public application identifier is not a secret. No client secret is used.

## Sessions and local storage

The implementation provides automatic renewal of an active saved Premium session while disconnected, manual renewal and browser reauthentication. Refresh tokens retain their issuing client ID; rotation is persisted under coordinated vault access before later Xbox/Minecraft requests. Classified application or reauthentication failures pause automatic attempts in the running client. Retries are bounded, and ambiguous refresh POST failures are not blindly replayed. Saved accounts remain available when authorization fails.

Profile activation is designed to replace the Minecraft user and associated services without restarting Minecraft. Network preparation runs off the render thread; commit runs on the client thread while disconnected, with rollback handling. Only internally verified prepared states may commit; copied metadata, stale results and direct apply calls are rejected. The compact list and double-click behavior remain. Successful real Premium commit/rollback is not yet accepted.

Account data is stored locally on Windows. Refresh and Minecraft access tokens are encrypted with Windows DPAPI under the current Windows user. Account names, UUIDs, profile types and favorites are local metadata and are not encrypted by the credential encryption. Storage includes atomic replacement, encrypted credential backups, recovery handling and process locks. See [Privacy](PRIVACY.md) and [Security](SECURITY.md) for limitations.

## Local offline profiles

Earlier versions combined Microsoft and local offline profiles. That implementation is preserved in a separate private development area. Existing offline records are retained in the shared vault to prevent data loss; the Premium UI filters its view without writing back a shortened account list. This Premium main mod does not create, activate or manage those offline records, including through legacy activation paths, and has no offline fallback after a Premium failure.

A separate offline-profile addon is a disclosed future possibility, not an implemented or enabled addon. Offline profiles do not authenticate with Microsoft, prove a license or bypass online-mode server authentication. Any future combination must be disclosed and assessed as a combined use case; separate JARs do not automatically make it permitted or approved.

## What has been tested

For **1.0.4-dev.3**:

- Clean build: **99 Java tests passed**, with no failures, errors or skipped tests.
- The same packaged JAR passed **23 isolated Minecraft-client checks on each of Fabric Loader 0.19.3 and 0.20.1**. These include the existing UI/data-preservation/activation guards, the complete notice with no control overlap, and music volume at 0 %. Actual framebuffer size and effective GUI scale were checked at 640×480/1, 854×480/2, 1280×720/3 and 1920×1080/4.
- These checks use synthetic account records and do not demonstrate a successful authorized Premium session commit, real renewal, online-mode join or CurseForge launch. No new personal Microsoft sign-in was performed.

Earlier evidence for **1.0.4-dev.2**:

- Clean build: **99 Java tests passed**, covering simulated authentication, real local callbacks, state/PKCE, entitlement/profile failures, token rotation, persistence/recovery, concurrent access and the generic rollback kernel. Synthetic-data tests cover at least 30 account records.
- Real Minecraft 26.2 client: **18 isolated checks passed on each of Fabric Loader 0.19.3 and 0.20.1**, covering UI, four GUI/window combinations, data preservation and rejection of forbidden activation paths. They do not exercise a successful authorized Premium session commit or online-mode join.
- The real owner-performed attempt was on **1.0.4-dev.1**, before dev.2's music-startup and error-wording adjustments. It stopped at the Minecraft Services app-registration rejection described above. No raw credential-bearing HTTP log is published here.

Successful real Minecraft sign-in, entitlement/profile acceptance, two-Premium-account switching, renewal, restart persistence of authorized Premium sessions and online-mode joins remain blocked or unverified. Actual CurseForge runtime acceptance is also open; a direct isolated Minecraft launch is not evidence of a CurseForge launch. The existing launcher session is not treated as a source of refresh credentials or indefinitely renewable authorization. No documented CurseForge Minecraft-account broker was found in the public interfaces examined.

## Maintainer and support

Maintained by **InFiniityxSweety**. For general questions, bug reports and feature requests, please use this repository's [GitHub Issues](https://github.com/InFiniityxSweety/InFiniity-Account-Manager/issues).

GitHub Issues are public. Do not include passwords, authentication codes, access or refresh tokens, account files, or personal information. Do not post vulnerability details or sensitive evidence in public issues; see [Security](SECURITY.md) for the current reporting status. No response time or support guarantee is promised.

## Project information

- [Privacy notice](PRIVACY.md)
- [Security policy](SECURITY.md)
- [Microsoft Authorization Code flow and PKCE](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-auth-code-flow)
- [Microsoft loopback redirect rules](https://learn.microsoft.com/en-us/entra/identity-platform/reply-url)
- [Minecraft EULA](https://www.minecraft.net/en-us/eula)

This is an unofficial community project, not an official Minecraft product. It is not approved by or associated with Mojang or Microsoft. Minecraft, Microsoft and Xbox names belong to their respective owners.
