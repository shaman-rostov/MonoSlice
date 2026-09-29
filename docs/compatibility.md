# Compatibility

## macOS

MonoSlice requires **macOS 12.0 Monterey or newer**:

- macOS 12 Monterey
- macOS 13 Ventura
- macOS 14 Sonoma
- macOS 15 Sequoia
- macOS 26 Tahoe

---

## Hardware

| Mac | Architecture kept | Architecture removed |
| --- | --- | --- |
| Apple Silicon (M1, M2, M3, M4) | `arm64` | `x86_64` |
| Intel | `x86_64` | `arm64` |

MonoSlice always keeps the architecture your Mac runs. If it runs under Rosetta 2, MonoSlice detects that and never removes the slice you need.

The command-line tool can also keep a specific architecture with `--keep-arch arm64` or `--keep-arch x86_64`. See [Using MonoSlice](usage.md#command-line-usage).

---

## Which Apps Can Be Optimized

| App type | Result |
| --- | --- |
| Universal app with both `arm64` and `x86_64` | Optimized |
| App with a single architecture | Nothing to remove |
| Mac App Store app | Skipped — re-signing would invalidate its App Store receipt |
| App that needs App Sandbox, app groups, keychain groups or similar entitlements | Skipped — an ad-hoc signature cannot keep them |
| Binary with an `arm64e` slice (when keeping `arm64`) | Left alone — `arm64e` is needed by some system plug-in hosts |
| Apple system app (`/System`, `/Library/Apple`, `com.apple.*`) | Deselected by default; can be included one by one, with a warning |

Some apps show large potential savings, others very little: if most of an app's size comes from images, video or other resources, removing an architecture will not change it much.

---

## What Changes After Optimization

Removing an architecture invalidates an app's code signature, so MonoSlice re-signs it with an ad-hoc signature. As a result:

- macOS asks you to grant permissions such as camera, microphone and Full Disk Access again.
- Keychain items may prompt for access again.
- An app update may bring back both architectures. Run MonoSlice again after updating.

See [Limitations and Risks](limitations-and-risks.md), [Safety](index.md#safety) and the [FAQ](faq.md) for more.

---

## Command-Line Tool

The `monoslice` tool is bundled in the app and supports the same macOS versions and Macs. It skips system apps unless you pass `--include-system`.

---

## Reporting Compatibility Problems

If an optimized app does not launch, restore it from your backup and open a [GitHub Issue](https://github.com/shaman-rostov/MonoSlice/issues) with:

- macOS version and Mac model
- Name and version of the app
- Error message or screenshot
