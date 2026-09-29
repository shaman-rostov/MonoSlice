# Frequently Asked Questions

## What is MonoSlice?

MonoSlice is a macOS utility that removes unnecessary CPU architectures from Universal Binary applications.

Many macOS applications include support for both:

- Apple Silicon (`arm64`)
- Intel (`x86_64`)

MonoSlice removes the architecture you do not need and helps reduce application size.

---

## Is MonoSlice safe?

Yes, with one important caveat: removing an architecture invalidates the app's code signature, so MonoSlice re-signs it with an ad-hoc signature. This means macOS will ask you to re-grant permissions like camera, microphone, or Full Disk Access, and Keychain items will re-prompt for access. MonoSlice warns you about this before optimizing.

MonoSlice does not:

- modify macOS system files;
- collect personal data;
- upload applications;
- change application settings beyond what re-signing requires.

All processing happens locally on your Mac, and the original app is only replaced once a verified copy is confirmed to work.

---

## Will optimized applications still work?

In most cases, yes.

MonoSlice keeps the architecture required by your Mac and removes only the unused one.

For example:

Apple Silicon Mac:

Before:

```
arm64 + x86_64
```

After:

```
arm64
```

The application continues running natively.

---

## Can I restore an optimized application?

MonoSlice does not provide a reverse conversion.

To restore the original Universal Binary:

1. Replace the optimized application with a backup copy.
2. Download the original application again from the official source.

We recommend keeping backups of important applications.

---

## Does MonoSlice work with all applications?

MonoSlice works with applications that use macOS Universal Binary format.

However, some applications may not benefit from optimization.

Examples:

- Applications already containing only one architecture.
- Applications where most of the size comes from resources.
- Applications with special protection mechanisms.

---

## Does MonoSlice work with App Store applications?

No — Mac App Store apps are skipped automatically.

Re-signing would invalidate their App Store receipt, so they would refuse to launch. MonoSlice detects this and leaves them untouched.

---

## Does MonoSlice require an internet connection?

No.

MonoSlice works completely offline.

Internet access is only required for:

- downloading updates;
- downloading the application itself.

---

## Does MonoSlice send my applications anywhere?

No.

Your applications stay on your Mac.

MonoSlice does not upload files or application data.

---

## Why did my application size not change?

Possible reasons:

- The application already contains only one architecture.
- Most of the application size comes from images, videos, or other resources.
- The application uses compression.

MonoSlice only removes unused CPU architecture code.

---

## Why did the application become large again after an update?

Application updates replace the optimized application with a new version.

The new version may contain both architectures again.

Simply run MonoSlice on the updated application.

---

## Can I optimize system applications?

MonoSlice is designed primarily for user applications. System apps (in `/System`, `/Library/Apple`, or with a `com.apple.*` identifier) are deselected by default, though you can include them individually, with a warning.

We recommend avoiding modifications to macOS system components.

---

## Does MonoSlice support Intel Macs?

Yes.

On Intel Macs, MonoSlice can remove the unused Apple Silicon (`arm64`) architecture.

Example:

Before:

```
arm64 + x86_64
```

After:

```
x86_64
```

---

## Does MonoSlice support Apple Silicon Macs?

Yes.

On Apple Silicon Macs, MonoSlice can remove the unused Intel (`x86_64`) architecture.

Example:

Before:

```
arm64 + x86_64
```

After:

```
arm64
```

---

## Is MonoSlice open source?

No.

MonoSlice is free to use but distributed as closed-source software.

This repository provides:

- documentation;
- downloads;
- issue tracking;
- project information.

---

## Found a problem?

If you encounter an issue:

1. Open a GitHub Issue.
2. Include your Mac model.
3. Include your macOS version.
4. Include the application name and version.
5. Describe what happened.

This helps improve MonoSlice.
