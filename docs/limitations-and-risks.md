# Limitations and Risks

MonoSlice changes other applications on your Mac. That is only possible outside the restrictions Apple places on Mac App Store apps, and it has consequences for the apps you optimize.

This page lists all of them in one place so you can decide what to optimize.

---

## Why MonoSlice Is Not on the Mac App Store

MonoSlice is distributed as a Developer ID app (signed and notarized by Apple) through [GitHub Releases](https://github.com/shaman-rostov/MonoSlice/releases). It cannot be published on the Mac App Store without losing its core function, because the App Store requires things MonoSlice fundamentally can't do:

| App Store requirement | Why MonoSlice can't meet it |
| --- | --- |
| Apps must run in the **App Sandbox** | A sandboxed app can't modify other apps' binaries, run `lipo`/`codesign` on them or replace bundles in `/Applications`. |
| Apps must **not request administrator privileges** | Apps in `/Applications` are often owned by `root`; replacing them needs an administrator password. |
| Apps may only modify other apps' data through **appropriate macOS APIs** | There is no public API for removing an architecture from another app and re-signing it. |
| Updates must come **only through the Mac App Store** | MonoSlice updates are downloaded from GitHub Releases. |

As long as MonoSlice keeps its current design, it will stay a direct download. This is a deliberate choice, not a temporary state.

---

## What MonoSlice Needs From Your Mac

### No App Sandbox

MonoSlice runs without the App Sandbox so it can read any app you point it at and write the optimized copy. It only reads and modifies apps you select. See [Privacy](privacy.md) and the [Security Policy](../SECURITY.md).

### App Management permission

On recent macOS versions, **System Settings → Privacy & Security → App Management** must be turned on for MonoSlice. Without it, optimizing some apps fails with a permission error. See [Installation](installation.md#allow-monoslice-to-modify-apps).

### Administrator password

When an app lives in a protected location (for example a `root`-owned app in `/Applications`), MonoSlice asks for your administrator password through the standard macOS prompt. Only the final step runs with administrator rights: the verified copy is swapped in, and the original is kept until the swap is confirmed. Everything else runs as your user.

MonoSlice uses AppleScript (`osascript`) to show this prompt, so macOS may also ask you to allow MonoSlice to control other apps via Apple Events.

### Manual updates

MonoSlice does not update itself. Check [GitHub Releases](https://github.com/shaman-rostov/MonoSlice/releases) for new versions and [verify the download](download.md#verify-download) before installing.

---

## What Changes in an Optimized App

Removing an architecture invalidates an app's code signature. MonoSlice re-signs the app with an **ad-hoc signature** (`codesign --sign -`), which is valid on your Mac but no longer tied to the original developer. This has several consequences.

| Before | After optimization |
| --- | --- |
| Signed with the developer's Developer ID | Ad-hoc signature, no developer identity |
| Notarized by Apple | No longer notarized |
| Hardened Runtime enabled (for most apps) | Hardened Runtime **not** enabled |
| Entitlements from the developer | Entitlements removed |
| Permissions (camera, microphone, Full Disk Access…) granted | Must be granted again |
| Keychain items accessible silently | Keychain may prompt for access again |

### Permissions and Keychain

macOS identifies an app by its signature. After re-signing, it treats the optimized app as a new app: you'll be asked again for camera, microphone, Full Disk Access, Accessibility, Screen Recording and similar permissions, and Keychain items may prompt for access. MonoSlice warns you about this before optimizing.

### Weaker runtime protection

Most apps from established developers are signed with the **Hardened Runtime**, which, among other things, stops unsigned code from being injected into the app. An ad-hoc signature does not keep it. The optimized app works the same way, but it has less protection against tampering by other software on your Mac.

If an app handles sensitive data (password managers, banking, crypto wallets, VPN and security software), we recommend **not** optimizing it.

### Apps MonoSlice refuses to optimize

To avoid breaking apps, MonoSlice skips:

- **Mac App Store apps.** Re-signing invalidates their App Store receipt, so they would refuse to launch.
- **Apps that depend on entitlements an ad-hoc signature can't keep:** App Sandbox, app groups, keychain access groups, `com.apple.developer.*` capabilities, virtualization and hypervisor. Without them the app would lose its data, or macOS would stop it at launch.
- **`arm64e` slices** when keeping `arm64`. Some system plug-in hosts need them.
- **Apple system apps** (`/System`, `/Library/Apple`, `com.apple.*`), which are deselected by default. You can include them one by one, with a warning. We don't recommend it.

---

## Risks to Consider

MonoSlice checks every optimized app with `codesign --verify` before it replaces the original, and leaves the original untouched if anything fails. Some problems can still only show up later, when you use the app.

### No undo

MonoSlice does not keep the removed architecture and cannot restore it. To get the original Universal app back, reinstall it from the developer or restore it from a backup. **Keep a backup of any app you can't easily download again.**

### App updates

- An update usually replaces the optimized app with a new Universal build, so the space comes back. Run MonoSlice again after updating.
- Built-in updaters sometimes check that the installed app is signed by the same developer as the update. Because the optimized app has an ad-hoc signature, such an updater may refuse to install the update. If that happens, download the new version from the developer's website.

### Apps that check themselves

Some apps check their own signature or files at launch: license and copy-protection systems, anti-cheat in games, some security and enterprise software. After optimization they may refuse to start, report that they are "damaged", or lose their license activation. Restore the original if this happens and [report it](https://github.com/shaman-rostov/MonoSlice/issues) so MonoSlice can learn to skip that app.

### Rosetta and Intel-only plug-ins

On an Apple Silicon Mac, MonoSlice removes the Intel (`x86_64`) code. After that, the app **can no longer run under Rosetta 2**. This matters for apps you sometimes open with "Open using Rosetta" to load Intel-only plug-ins, such as audio plug-ins in DAWs or older extensions in creative tools. Don't optimize those apps.

### Moving to another Mac

An optimized app contains code for one architecture only. If you migrate to a Mac with a different processor (for example from an Intel Mac to Apple Silicon with Migration Assistant, or restore from a Time Machine backup made on another Mac), the optimized apps won't launch there. Reinstall them from their developers.

### Copying optimized apps to other people

An optimized app is signed ad-hoc and is not notarized. If you send it to another Mac (AirDrop, download, archive), Gatekeeper will block it there. Share the original installer instead.

### Apps that are running

Quit an app before optimizing it. Replacing the files of a running app can make it crash or behave unexpectedly until it is restarted.

### Managed Macs

On company-managed Macs, security software or device-management policies may flag or block apps with ad-hoc signatures. Ask your IT department before using MonoSlice on a work Mac.

### System apps

Changing Apple's own apps can break system features or be undone by a macOS update. MonoSlice deselects them by default, and we recommend leaving them alone.

---

## Recommendations

1. Keep backups of important apps, or make sure you can download them again.
2. Start with large apps you don't rely on for sensitive work, and check that they launch and work normally.
3. Don't optimize apps that handle passwords, money or security, apps you run under Rosetta, or apps with copy protection.
4. Re-run MonoSlice after app updates instead of expecting the savings to persist.
5. Before migrating to a Mac with a different processor, reinstall optimized apps from their developers.

---

## See Also

- [Compatibility](compatibility.md): which apps can be optimized
- [FAQ](faq.md)
- [Security Policy](../SECURITY.md)
