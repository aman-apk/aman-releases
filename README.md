<p align="center">
  <img src="https://amanlabs.app/media/aman-store.png" width="360" alt="Aman Store">
</p>

# Aman Labs — signed builds and catalog

Arabic-first Android apps that keep your data on your phone. No accounts, no ads, no analytics. Everything is in Arabic first and English second, and the apps are designed for right-to-left reading rather than translated afterwards.

This repository is the distribution point for the whole family:

- `catalog.json` — the machine-readable list of apps, versions, download URLs, file hashes and signing-certificate fingerprints. Aman Store reads it. So can you.
- [Releases](../../releases) — the signed APKs themselves.

Website: [amanlabs.app](https://amanlabs.app) ([English](https://amanlabs.app/en/)) · Downloads mirror: `dl.amanlabs.app` (the same files, served through Cloudflare for regions where GitHub is slow or blocked).

## The apps

Fourteen apps and the store. Six of them have had a public launch so far; the rest are finished and installable through the store but have not been announced yet. All of them are listed here.

| | App | Package | What it does |
|---|---|---|---|
| <img src="https://amanlabs.app/media/icons/kalamboard.svg" width="36"> | **KalamBoard** — كلام بورد | `org.amanlabs.kalamboard` | Arabic/English keyboard with on-device word prediction and dialect dictionaries (Levantine, Egyptian, Gulf). Has no internet permission at all. Built on [FlorisBoard](https://github.com/florisboard/florisboard). |
| <img src="https://amanlabs.app/media/icons/mihrab.svg" width="36"> | **Mihrab** — محراب | `org.amanlabs.mihrab` | Prayer times, athan, qibla and Hijri calendar. No internet permission, no location permission: you pick your city from a bundled database. |
| <img src="https://amanlabs.app/media/icons/tayf.svg" width="36"> | **Tayf** — طيف | `org.amanlabs.tayf` | Browser with tracker blocking inside the engine, private tabs, reader mode, and a downloader that grabs the video or audio on the page at the quality you choose. Also runs on Windows. |
| <img src="https://amanlabs.app/media/icons/jisr.svg" width="36"> | **Jisr** — جسر | `org.amanlabs.jisr` | Moves files between your own devices over the local network. No server, no size limit, works without internet. Speaks the [LocalSend](https://github.com/localsend/localsend) protocol, so it talks to LocalSend devices too. Android and Windows. |
| <img src="https://amanlabs.app/media/icons/album.svg" width="36"> | **Album** — ألبوم | `org.amanlabs.album` | Photo and video gallery with on-device face grouping, a video player, an editor and an encrypted vault. Nothing is uploaded anywhere. |
| <img src="https://amanlabs.app/media/icons/hisn.svg" width="36"> | **Hisn** — حصن | `org.amanlabs.hisn` | Password manager on the KeePass KDBX format, with autofill, TOTP codes and direct Wi-Fi sync to the desktop app. Built on [KeePassXC](https://keepassxc.org); [source](https://github.com/aman-apk/hisn). Your vault is one encrypted file that never leaves your devices. |
| | **Daftar** — دفتر | `org.amanlabs.daftar` | Notes and notebooks with reminders and an encrypted backup. Nothing you write leaves the phone. |
| | **Jezdan** — جزدان | `org.amanlabs.jezdan` | Expense and income tracker in any currency, with debts, dues and monthly reports. |
| | **Diwan** — ديوان | `org.amanlabs.diwan` | Dual-pane file manager with an encrypted vault, a disk map, and a trash that restores files to where they were. |
| | **Sitr** — سِتر | `org.amanlabs.sitr` | Photo vault with per-photo encryption. Requests zero permissions. |
| | **Wathaiq** — وَثائق | `org.amanlabs.wathaiq` | Scans IDs, passports and certificates, keeps them encrypted on the device and reminds you before each one expires. No internet permission. |
| | **Ruznama** — رزنامة | `org.amanlabs.ruznama` | Calendar that opens the `.ics` invitations from your email and saves them in one tap; replies go out through your own mail app. No internet permission. |
| | **Sijil** — سِجِلّ | `org.amanlabs.sijil` | Notification history: keeps what you swiped away or missed while the phone was locked, searchable. Carries no permission and no internet. |
| | **Qamariya** — قمرية | `org.amanlabs.qamariya` | Period tracker with predictions and reminders, encrypted, with an option to disguise the app. |
| <img src="https://amanlabs.app/media/icons/store.svg" width="36"> | **Aman Store** — متجر أمان | `org.amanlabs.store` | Installs and updates the family. Verifies every APK against the catalog before installing. Can also hand apps to a nearby phone offline. |

## Install

**Recommended: Aman Store.** Download [`amanstore-1.29.0.apk`](https://dl.amanlabs.app/amanstore-1.29.0.apk) (2 MB), install it, and take the rest from there. The store checks the SHA-256 of each download and the signing certificate of each package against the catalog and refuses anything that does not match. Updates for all apps arrive through it.

**Direct APKs.** Every file in `catalog.json` is also on the [Releases](../../releases) page and on the mirror at `https://dl.amanlabs.app/<file>`. Jisr and Album have per-ABI splits next to the universal APK (`-arm64-v8a`, `-armeabi-v7a`, `-x86_64`); the store picks the right one, you can too.

**Obtainium.** Point it at this repository. The APK names are stable (`<app>-<version>.apk`).

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
org.amanlabs.daftar      93:84:6C:CD:78:17:10:D5:77:1F:6C:0E:81:BB:07:21:0D:9B:AE:7B:F0:A9:22:62:2A:45:58:B9:58:AD:10:D5
org.amanlabs.jezdan      93:F6:51:F1:A6:27:DE:76:2B:B3:44:90:DF:05:7F:47:53:CF:A8:61:C0:16:95:80:76:C3:EB:D8:B6:3E:C9:B2
org.amanlabs.diwan       F2:D9:BC:1D:97:05:42:75:7B:98:33:5D:61:58:DC:97:71:89:A6:41:A2:AF:48:D2:71:E6:7F:B8:89:B1:30:01
org.amanlabs.sitr        70:A8:D1:30:25:7B:20:1E:80:51:0F:A4:FD:4E:EF:99:E1:37:43:7C:31:CB:1D:26:16:55:02:61:9A:D7:1D:63
org.amanlabs.wathaiq     27:69:98:25:61:9B:1D:34:55:41:8D:05:E9:F9:5A:2E:5E:D7:40:A8:AB:7D:6B:0C:BC:71:C1:87:19:69:AC:87
org.amanlabs.ruznama     67:15:F8:5A:8E:D1:AC:E0:15:81:E0:6A:22:F9:DF:42:18:A1:87:E7:A7:28:CB:8F:86:9B:89:0D:55:30:27:5A
org.amanlabs.sijil       43:99:5D:32:69:2F:96:B2:BF:A8:D7:A6:91:14:7F:61:07:D6:6A:22:8B:33:14:88:23:FC:F0:40:8E:05:BF:B5
org.amanlabs.qamariya    2B:3E:16:0B:74:A9:84:A2:E2:1B:53:80:54:01:3E:08:BF:46:49:6D:9A:27:4A:DF:7B:5E:1C:C5:6D:7C:2F:12
```

If a fingerprint differs from the one above, the file is not ours. Do not install it, and tell us.

## Privacy, in one paragraph

The apps that can work offline have no `INTERNET` permission in their manifest, and a build step fails the build if a networking library or the permission slips in. You can confirm this yourself under Settings → Apps → *app* → Permissions. The apps that need the network for their actual job (Tayf browses, Jisr transfers, the store downloads) have no server of ours to talk to: there is no account, no telemetry endpoint, no crash reporter. Backups are a single encrypted file the store writes for the whole family, unlocked by a passphrase only you know.

## Source code and licenses

This account publishes the builds; the sources are moving into public repositories one app at a time, starting with the ones derived from other free software, because their licenses ask for it:

- **Hisn** is derived from [KeePassXC](https://github.com/keepassxreboot/keepassxc) (GPL-2.0 / GPL-3.0). Its complete source, desktop and Android, is published at [aman-apk/hisn](https://github.com/aman-apk/hisn) under the same license.
- **KalamBoard** is derived from [FlorisBoard](https://github.com/florisboard/florisboard) (Apache-2.0). Source, with the NOTICE describing our changes: [aman-apk/kalamboard](https://github.com/aman-apk/kalamboard).
- **Jisr** is derived from [LocalSend](https://github.com/localsend/localsend) (Apache-2.0). Source: [aman-apk/jisr](https://github.com/aman-apk/jisr).

The rest (Tayf, Mihrab, Album, the store and the unannounced members) are our own code and will be published as they are cleaned up for it. Until a repository exists for an app, the fingerprints above and the catalog are its verification anchor.

## Support the work

Aman Labs is one developer and the people who test the apps on their own phones. Everything is free and will stay free; there are no paid tiers and nothing hidden behind a paywall.

Donations are not open yet. We are arranging a fiscal host so that money is handled in the open and can pay for what the project actually needs: the domain and mirror, test devices, and time. When that is in place it will be announced here, on the website and in the store. Until then, the most useful support is using the apps, reporting what breaks, and telling people who read Arabic that these exist.

## Reporting problems

- Bugs and requests: [Issues](../../issues). Say which app, which version (Settings → About), and which phone.
- Security issues: see [SECURITY.md](SECURITY.md). Please do not open a public issue for those.
- WhatsApp: the number on [amanlabs.app](https://amanlabs.app).

## License of this repository

`catalog.json`, `announcements.json` and this document are released under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/). The APKs are covered by each app's own license; see the About screen inside the app.
