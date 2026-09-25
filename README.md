<p align="center">
  <img src="https://amanlabs.app/media/aman-store.png" width="360" alt="Aman Store">
</p>

# Aman Labs — signed builds and catalog

Arabic-first Android apps that keep your data on your phone. No accounts, no ads, no analytics. Everything is in Arabic first and English second, and the apps are designed for right-to-left reading rather than translated afterwards.

This repository is the distribution point for the whole family:

- `catalog.json` — the machine-readable list of apps, versions, download URLs, file hashes and signing-certificate fingerprints. Aman Store reads it. So can you.
- [Releases](../../releases) — the signed APKs themselves.

Website: [amanlabs.app](https://amanlabs.app) · Downloads mirror: `dl.amanlabs.app` (the same files, served through Cloudflare for regions where GitHub is slow or blocked).

## The apps

| | App | Package | What it does |
|---|---|---|---|
| <img src="https://amanlabs.app/media/icons/kalamboard.svg" width="36"> | **KalamBoard** — كلام بورد | `org.amanlabs.kalamboard` | Arabic/English keyboard with on-device word prediction and dialect dictionaries (Levantine, Egyptian, Gulf). Has no internet permission at all. Built on [FlorisBoard](https://github.com/florisboard/florisboard). |
| <img src="https://amanlabs.app/media/icons/mihrab.svg" width="36"> | **Mihrab** — محراب | `org.amanlabs.mihrab` | Prayer times, athan, qibla and Hijri calendar. No internet permission, no location permission: you pick your city from a bundled database. |
| <img src="https://amanlabs.app/media/icons/tayf.svg" width="36"> | **Tayf** — طيف | `org.amanlabs.tayf` | Browser with tracker blocking inside the engine, private tabs, reader mode, and a downloader that grabs the video or audio on the page at the quality you choose. Also runs on Windows. |
| <img src="https://amanlabs.app/media/icons/jisr.svg" width="36"> | **Jisr** — جسر | `org.amanlabs.jisr` | Moves files between your own devices over the local network. No server, no size limit, works without internet. Speaks the [LocalSend](https://github.com/localsend/localsend) protocol, so it talks to LocalSend devices too. Android and Windows. |
| <img src="https://amanlabs.app/media/icons/album.svg" width="36"> | **Album** — ألبوم | `org.amanlabs.album` | Photo and video gallery with on-device face grouping, a video player, an editor and an encrypted vault. Nothing is uploaded anywhere. |
| <img src="https://amanlabs.app/media/icons/hisn.svg" width="36"> | **Hisn** — حصن | `org.amanlabs.hisn` | Password manager on the KeePass KDBX format, with autofill, TOTP codes and direct Wi-Fi sync to the desktop app. Built on [KeePassXC](https://keepassxc.org). Your vault is one encrypted file that never leaves your devices. |
| <img src="https://amanlabs.app/media/icons/store.svg" width="36"> | **Aman Store** — متجر أمان | `org.amanlabs.store` | Installs and updates the family. Verifies every APK against the catalog before installing. Can also hand apps to a nearby phone offline. |

More members exist in the catalog but are not announced yet; they show up blurred in the store until they are.

## Install

**Recommended: Aman Store.** Download [`amanstore-1.28.1.apk`](https://dl.amanlabs.app/amanstore-1.28.1.apk) (2 MB), install it, and take the rest from there. The store checks the SHA-256 of each download and the signing certificate of each package against the catalog and refuses anything that does not match. Updates for all apps arrive through it.

**Direct APKs.** Every file in `catalog.json` is also on the [Releases](../../releases) page and on the mirror at `https://dl.amanlabs.app/<file>`. Jisr and Album have per-ABI splits next to the universal APK (`-arm64-v8a`, `-armeabi-v7a`, `-x86_64`); the store picks the right one, you can too.

**Obtainium.** Point it at this repository. Releases are tagged and the APK names are stable (`<app>-<version>.apk`).

Android will ask once to allow installs from this source. Google Play Protect may warn about the store itself; that is the generic warning every third-party installer gets for holding `REQUEST_INSTALL_PACKAGES`, not a finding about the code.

## Verify what you downloaded

Each entry in `catalog.json` carries `sha256` (the file) and `signerSha256` (the signing certificate). Check both:

```
sha256sum tayf-0.1.16.apk
apksigner verify --print-certs tayf-0.1.16.apk
```

Signing-certificate fingerprints (SHA-256). Each app has its own key; none of them will change.

```
org.amanlabs.store       0D:69:C5:D8:0E:24:E5:87:55:9E:9C:96:03:5D:AB:56:13:5A:4E:70:DA:D1:72:CD:A1:DF:B3:08:0E:E6:90:AF
org.amanlabs.kalamboard  F1:19:8E:06:08:E7:99:7A:60:4F:78:4F:F8:C8:3A:78:88:63:B6:00:33:C3:8C:E8:B0:50:C6:DF:95:77:C9:BB
org.amanlabs.mihrab      6A:82:DF:42:F8:BD:11:E5:CB:AB:F2:FA:B8:EB:AE:D3:E5:E5:FA:AA:1F:C9:30:F8:A5:60:54:1D:14:7B:36:C1
org.amanlabs.tayf        64:54:0F:E2:A9:4B:23:86:F2:E5:50:6C:79:BE:0E:53:36:C7:35:90:7A:52:E0:A1:24:09:51:9B:11:5F:C1:A5
org.amanlabs.jisr        26:2A:B0:8C:36:16:F8:62:12:71:EE:DB:04:C9:86:A5:CD:11:C0:78:9D:5D:DE:66:D3:97:AD:70:B9:40:BE:A8
org.amanlabs.album       16:42:D0:99:53:A8:13:5F:E3:02:79:47:07:DB:C4:8A:09:4A:B5:2A:55:3F:7A:DA:1D:25:A4:72:F7:2A:88:A2
org.amanlabs.hisn        D9:94:42:0E:BA:AC:BF:51:B2:90:24:B1:B9:AE:0E:AD:61:23:52:43:0B:EF:ED:B4:2C:E9:FA:39:FD:2A:65:E1
```

If a fingerprint differs from the one above, the file is not ours. Do not install it, and tell us.

## Privacy, in one paragraph

The apps that can work offline have no `INTERNET` permission in their manifest, and a build step fails the build if a networking library or the permission slips in. You can confirm this yourself under Settings → Apps → *app* → Permissions. The apps that need the network for their actual job (Tayf browses, Jisr transfers, the store downloads) have no server of ours to talk to: there is no account, no telemetry endpoint, no crash reporter. Backups are a single encrypted file the store writes for the whole family, unlocked by a passphrase only you know.

## Source code

Right now this account publishes builds, not sources. KalamBoard, Jisr and Hisn are built on FlorisBoard, LocalSend and KeePassXC respectively, and their licenses are honoured in each app's About screen and license file. Moving the sources into public repositories is the next step for the project; until then, the fingerprints above and the catalog are the verification anchor.

## Support the work

Aman Labs is one developer and the people who test the apps on their own phones. Everything is free and will stay free; there are no paid tiers and nothing hidden behind a paywall.

Donations are not open yet. We are arranging a fiscal host so that money is handled in the open and can pay for what the project actually needs: the domain and mirror, test devices, and time. When that is in place it will be announced here, on the website and in the store. Until then, the most useful support is using the apps, reporting what breaks, and telling people who read Arabic that these exist.

## Reporting problems

- Bugs and requests: [Issues](../../issues). Say which app, which version (Settings → About), and which phone.
- Security issues: see [SECURITY.md](SECURITY.md). Please do not open a public issue for those.
- WhatsApp: the number on [amanlabs.app](https://amanlabs.app).

## License of this repository

`catalog.json`, `announcements.json` and this document are released under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/). The APKs are covered by each app's own license; see the About screen inside the app.
