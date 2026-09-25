# Security policy

## Reporting a vulnerability

If you find a security problem in any Aman Labs app, in the store, in the catalog or in the download mirror, please report it privately first.

- Use GitHub's private vulnerability reporting on this repository ("Report a vulnerability" under the Security tab), or
- write to the WhatsApp number published on [amanlabs.app](https://amanlabs.app) and say it is a security report.

Include the app and version (Settings → About), the device and Android version, and steps or a proof of concept. You will get an acknowledgement within 72 hours and a fix or a clear answer within 30 days for anything confirmed. We will credit you in the release notes unless you prefer not to be named.

## Scope

- All packages under `org.amanlabs.*` listed in `catalog.json`.
- `catalog.json` itself and the way the store verifies it.
- The mirror at `dl.amanlabs.app`.

Out of scope: issues in upstream projects we build on (FlorisBoard, KeePassXC, LocalSend) that are not caused by our changes; please report those upstream, and tell us so we can pick up the fix.

## What a genuine build looks like

Every app is signed with its own key. The SHA-256 fingerprints of the signing certificates are listed in [README.md](README.md#verify-what-you-downloaded) and in `catalog.json` under `signerSha256`. The store refuses any package whose certificate or file hash does not match. If you ever see a package claiming to be ours with a different fingerprint, that is itself a report we want.

## Supported versions

Only the latest version of each app, as listed in `catalog.json`, receives fixes. The store updates all installed apps to it.
