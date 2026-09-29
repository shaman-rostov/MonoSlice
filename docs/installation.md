# Installing MonoSlice

MonoSlice is distributed as a signed and notarized DMG through GitHub Releases.

---

## Requirements

- macOS 12.0 Monterey or newer
- An Intel or Apple Silicon Mac
- Administrator rights, to optimize apps in `/Applications`

See [Compatibility](compatibility.md) for details.

---

## Install the Mac App

1. Download the latest `MonoSlice-<version>.dmg` from [GitHub Releases](https://github.com/shaman-rostov/MonoSlice/releases).
2. Optionally [verify the download](download.md#verify-download).
3. Open the DMG.
4. Drag **MonoSlice** to the **Applications** folder.
5. Eject the DMG and launch MonoSlice from Applications.

MonoSlice is signed with an Apple Developer ID certificate and notarized by Apple. On first launch macOS may show the standard "downloaded from the Internet" prompt — click **Open**.

---

## Allow MonoSlice to Modify Apps

On recent macOS versions, an app can only change other apps if you allow it:

1. Open **System Settings → Privacy & Security → App Management**.
2. Turn on **MonoSlice**.

![MonoSlice enabled in App Management](images/app-management.png)

If the toggle is off, optimization of some apps fails with a permission error. See [Troubleshooting](usage.md#troubleshooting).

When MonoSlice replaces an app in a protected location such as `/Applications`, macOS asks for your administrator password. Only that final swap runs with administrator rights.

---

## Install the Command-Line Tool

The `monoslice` command-line tool is bundled inside the app:

```text
/Applications/MonoSlice.app/Contents/MacOS/monoslice
```

To run it as `monoslice` from any terminal, create a symbolic link:

```bash
mkdir -p ~/.local/bin
ln -s /Applications/MonoSlice.app/Contents/MacOS/monoslice ~/.local/bin/monoslice
```

Make sure `~/.local/bin` is in your `PATH`, then check the installation:

```bash
monoslice --help
```

Usage examples are in [Using MonoSlice](usage.md#command-line-usage).

---

## Update

1. Download the new DMG from [GitHub Releases](https://github.com/shaman-rostov/MonoSlice/releases).
2. Quit MonoSlice.
3. Drag the new **MonoSlice** to **Applications** and choose **Replace**.

---

## Uninstall

1. Quit MonoSlice.
2. Move **MonoSlice** from **Applications** to the Trash.
3. If you created the command-line link, remove it: `rm ~/.local/bin/monoslice`.

Apps you have already optimized stay optimized. To get their original Universal Binaries back, see [Can I restore an optimized application?](faq.md#can-i-restore-an-optimized-application).

---

## Need Help?

- Check the [FAQ](faq.md).
- Open a [GitHub Issue](https://github.com/shaman-rostov/MonoSlice/issues) and include your macOS version and Mac model.
