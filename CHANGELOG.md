# KeyKeeper — Release Notes

Versioning: MAJOR.MINOR.PATCH (build YYYYMMDD).

## 1.1.2 — 2026-06-22 (build 20260622)

macOS crash fix, plus a version-aligned Windows build.

### Fixed

**macOS**
- Fixed a crash that ended the app the moment typing started (for example into a browser-based VPS console). The per-target keyboard-layout map introduced in 1.1.1 was rebuilt at the start of each typing action using the system keyboard-layout APIs, which must run on the main thread; the rebuild ran on a background thread and tripped a system assertion. The layout map is now built on the main thread, removing the crash on every target.

**Windows**
- Version-aligned rebuild (1.1.0 → 1.1.2). The Windows binary was not affected by the macOS crash; this build carries the "remote/VM" hardware-key typing mode from 1.1.1 (previously not shipped to the Windows download). No functional regression; the app still runs at standard user integrity (no UAC).

## 1.1.1 — 2026-06-10 (build 20260610)

Reliability fix for typing into targets reached over remote control and into the Windows UAC elevation prompt (administrator password).

### Fixed

**Both platforms**
- New "remote/VM" typing mode injects keys as raw hardware key events — scancodes on Windows, fixed positional ANSI key codes on macOS — instead of simulated Unicode input. Remote-control viewers (Endpoint Central, RDP), VM consoles (vCenter HTML5, VMRC, Citrix/Horizon) and the Windows secure desktop forward physical keys but drop injected Unicode events; the previous path produced nothing in those targets, including the UAC administrator password prompt over remote control.
- Letters and digits are sent layout-independently (QWERTY positional); symbols via the physical key + Shift. Enter, Tab and Space also go through hardware key events in this mode.

### Notes

- Enable in Settings: "Send keystrokes as hardware key codes (remote/VM)". Default OFF; native local typing is unchanged.

## 1.1.0 — 2026-05-12 (build 20260512)

First release prepared for public distribution under the labforge.tech brand.

### Added

**macOS**
- Double-click-to-start mode: arm Type It, then double-click on the target field; typing begins where you clicked.
- Focus-change-to-start mode: arm Type It, switch window or field, typing fires automatically when KeyKeeper loses focus.
- "Press Enter after typing" toggle, useful for login forms.
- Long-text warning threshold and completion-notification toggle surfaced in Settings.

**Windows**
- Keyboard-layout independence: KeystrokeSimulator now derives scan codes from the foreground window's HKL, so non-US/non-IT layouts (DE, FR, ES, …) type the intended character instead of the layout-shifted version.
- Refined localization for ~14 new IT/EN strings.

**Both platforms**
- First-launch EULA modal (License Grant, Prohibited Uses, IP, Governing Law / Courts of Reggio Emilia, No Warranty). Persisted per user; Decline terminates the app.
- "Support the forge" donation panel reachable from the popover header, the About panel and the Help panel. Four preset amounts (1/2/5/10 EUR), free amount, opens PayPal in the default browser.
- Expanded Help: dedicated Keyboard Shortcuts section, explicit Privacy section (what is stored, where, how, what is excluded, GDPR posture), FAQ with the canonical "antivirus flags KeyKeeper" answer, inline Release Notes, donate hook.
- About: copyright now reads "(c) 2026 Iuri Vaccari — labforge.tech" with clickable links to labforge.tech and support@labforge.tech.
- Bilingual interface (English / Italian) for every UI string.

### Changed

- macOS bundle identifier moved to `tech.labforge.keykeeper`.
- macOS clipboard-history key migrated from a hardware-UUID-derived value to a random 32-byte seed stored in the **macOS Keychain** (this-device-only, only-when-unlocked).
- Windows clipboard-history key migrated from a MachineGuid-derived value to a random 32-byte seed sealed with **Windows DPAPI** (CurrentUser scope).
- Security/Privacy copy in About and Help rewritten to match the new storage model.

### Security

A pre-release security audit was performed before this build. Four HIGH and five MEDIUM findings were closed before release:

- macOS Hardened Runtime enforced (blocks dyld injection and cross-process memory read on signed builds).
- macOS history file: 10 MB pre-read size cap; file created with 0600 permissions before the first write.
- Windows history file and settings: ACLs scoped to the current Windows user only (inheritance disabled).
- Windows AES-GCM decrypt: `CryptographicException` now caught — corrupt files are quarantined instead of being silently overwritten.
- Windows settings.json: 256 KB hard cap before read.
- Windows low-level keyboard hook: was installed at startup for the whole process lifetime; now installed only while typing is active.
- Windows global exception handler: no longer echoes `Exception.Message` into a user-visible MessageBox.

### Distribution artifacts

| File | SHA-256 | Size |
|------|---------|------|
| `KeyKeeper_v1.1.0.dmg` (macOS, notarized) | `059d6d39fb75a2cfb3dfe35bbf49deb8af244512934c6dc9da5ffc2c73fab593` | 630 KB |
| `KeyKeeper-v1.1.0-Windows-x64.zip` (self-contained) | `3c16cfb288c45072f81c3688a1f1c93e917c7d78afebe1cc104eaa452ac031c0` | 63 MB |
| `KeyKeeper-v1.1.0-Windows-ARM64.zip` (self-contained) | `6441334a8734cf1771d6192cdbe8ffec17bfc3902beca229e6cbdd77baa96dd0` | 59 MB |

macOS: signed with "Developer ID Application: IURI VACCARI (VLB6AY6VZ3)", notarized and stapled. Gatekeeper reports `accepted / source=Notarized Developer ID` for both the .app bundle and the .dmg.

Windows: binaries are not yet Authenticode-signed. SmartScreen will show "Unknown publisher" on first run until an OV/EV certificate is in place.

(c) 2026 Iuri Vaccari — labforge.tech
