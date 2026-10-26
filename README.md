# KeyKeeper

**Types your text keystroke-by-keystroke, so it goes through where paste is
blocked.** Password fields, banking portals, RDP/VNC clients, VM consoles,
kiosk browsers — KeyKeeper types the characters as if you were at the keyboard,
so the paste-block becomes irrelevant. Free, native, no account. macOS & Windows.

> Part of **[labforge.tech](https://labforge.tech)** — free native utilities
> for macOS & Windows. No accounts, no telemetry, no sales.

**Download → [labforge.tech/apps/keykeeper](https://labforge.tech/apps/keykeeper)** ·
or grab the binaries from [Releases](../../releases).

---

## What it does

Some apps and websites deliberately disable paste in their input fields, and
sometimes a long string in your clipboard is simply refused. KeyKeeper types
that text character by character, the same way you would on the keyboard — the
receiving field cannot tell it apart from real typing.

- **Get past paste-blocked fields** — password managers' export forms, banking
  portals, RDP/VNC, VMware/Parallels/Citrix guests, kiosk-mode browsers.
- **Remote / VM mode** — injects raw hardware key events (scancodes on Windows,
  positional key codes on macOS) so it works in remote viewers and VM consoles
  that drop injected Unicode, including the Windows UAC password prompt.
- **Keyboard-layout independent** — types the intended character on non-US/IT
  layouts (DE, FR, ES, …).
- **Trigger modes** — double-click-to-start, focus-change-to-start, optional
  "press Enter after typing" (macOS).
- **Themes** — 8 themes (ReForge, Night, labforge, Graphite, High contrast) with
  Auto / Light / Dark mode; settings in a dedicated window.
- **Encrypted clipboard history** — key stored in the macOS Keychain / Windows
  DPAPI (this-device-only), never derived from hardware IDs.
- **Fully localized** — every UI string in Italian and English.

## Privacy

All data stays on your device. Clipboard history is encrypted with a random
key sealed in the system keystore (Keychain on macOS, DPAPI on Windows). Zero
telemetry, zero trackers, no network connections to third parties.

## Requirements & platform notes

- **macOS 13.0 or later** (Apple Silicon & Intel). Signed with a Developer ID
  certificate and **notarized by Apple** — no Gatekeeper warnings.
- **Windows 10/11** (x64 and ARM64), self-contained builds. Runs at standard
  user integrity (no UAC). The Windows binaries are **not yet Authenticode
  signed**, so SmartScreen shows "Unknown publisher" on first run — choose
  *More info → Run anyway*. Verify the checksum below to confirm integrity.

## Install & verify

Download from [Releases](../../releases) or
[labforge.tech/apps/keykeeper](https://labforge.tech/apps/keykeeper), then
verify before opening:

**macOS**
```
shasum -a 256 KeyKeeper_v1.2.0.dmg
# c9844ba5cdefddce8e66ef1c28ee734ed6dad71a0de4a8969cc04c1747c6d6ca
```

**Windows x64**
```
CertUtil -hashfile KeyKeeper-v1.2.0-Windows-x64.zip SHA256
# 011774db78b3cc326ddc564aaa012b6db595aaf6d66d9ab3a03595e64752a907
```

**Windows ARM64**
```
CertUtil -hashfile KeyKeeper-v1.2.0-Windows-ARM64.zip SHA256
# fc93985692328c3fb6b94a98e87ddb44a3cb59f4bd412365f53ae19b096dba64
```

## Changelog

See [CHANGELOG.md](CHANGELOG.md). Latest: **v1.2.0** (build 20261026).

## Issues

Found a bug or have a request? Open an
[issue](../../issues) — this repo is the public tracker for KeyKeeper.

## Support the forge

labforge.tech is free by design. If KeyKeeper saves you time, a small donation
helps keep the lights on (Apple Developer code-signing, VPS, domain).

**[Donate via PayPal](https://www.paypal.com/donate/?business=3lemontree%40gmail.com&currency_code=EUR)**
— free and voluntary, no benefit or service in exchange.

## License

Proprietary. © 2026 Iuri Vaccari — labforge.tech. All rights reserved.
The application binaries are distributed free of charge for personal use under
the EULA presented on first launch. The source code is not open.
Third-party components remain under their own licenses: Poppins typeface
(SIL Open Font License 1.1, OFL.txt included), KeyboardShortcuts (MIT, macOS),
.NET/WPF and CommunityToolkit.Mvvm (MIT, Windows), Hardcodet.NotifyIcon.Wpf
(CPOL 1.02, Windows).

- Website: <https://labforge.tech>
- Support: support@labforge.tech
