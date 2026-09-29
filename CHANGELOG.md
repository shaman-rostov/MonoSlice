# Changelog

All notable changes to MonoSlice are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

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
- Mac app (SwiftUI, English/Russian) with batch scanning and selection across `/Applications`.
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
