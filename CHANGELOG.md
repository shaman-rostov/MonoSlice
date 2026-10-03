# Changelog

All notable changes to MonoSlice are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

---

# Version 1.2.0

### Added

- German, Spanish, Polish and Czech translations. The Mac app is now available in English, Russian, German, Spanish, Polish and Czech.

### Changed

- The administrator-permission prompt now describes what actually needs administrator rights: replacing an optimized app in a protected location. `lipo` and `codesign` never run as administrator.

---

# Version 1.1.1

### Fixed

- Changing the language in Settings no longer closes an open dialog (such as the "Optimize selected apps?" confirmation), and keeps the app list's scroll position and filter.

---

# Version 1.1.0

### Added

- Localized interface: English and Russian.
- **Settings → Language.** *System* (the default) follows the language set for MonoSlice in **System Settings → General → Language & Region → Applications**, otherwise the macOS language, and falls back to English when that language isn't translated. An explicit choice switches the app right away; menus provided by macOS (Edit, Window, Quit…) follow after MonoSlice is relaunched.

### Fixed

- The scan banner no longer reads "Scanning Enumerating apps……" while apps are being listed.

---

# Version 1.0.1

### Fixed

- The administrator password is now requested once per run instead of once per app. Apps that need administrator rights are prepared first and installed together in a single step; a failure in one app rolls back only that app.
- Optimizing apps owned by root (for example those installed with a package installer) no longer fails with `Operation not permitted`.
- Permission errors now start with a hint on how to fix them instead of a long list of file names.

---

# Version 1.0.0

## Initial Release

### Added

- First public release of MonoSlice.
- Remove unused CPU architectures from macOS Universal Applications.
- Support for Intel Macs and Apple Silicon Macs.
- Mac app (SwiftUI) with batch scanning and selection across `/Applications`.
- `monoslice` command-line tool for scripting and one-off use.
- Optional menu-bar mode alongside the regular Dock app.
- Local application processing — free to use, distributed as closed-source software.

### Security

- No file uploads.
- No background monitoring.
- No external processing.
- Mac App Store apps, and system apps by default, are skipped from optimization.

---

# Unreleased

## Planned

### Added

- Finder Quick Action.
- Detailed optimization reports.
- Improved progress information.
- Additional compatibility checks.

### Improved

- Better user feedback during optimization.
- Improved error handling.
- More detailed diagnostics.

---

## Version Format

MonoSlice follows semantic versioning:

```
MAJOR.MINOR.PATCH
```

Example:

```
1.2.3
```

Meaning:

- MAJOR — breaking changes.
- MINOR — new features.
- PATCH — bug fixes.
