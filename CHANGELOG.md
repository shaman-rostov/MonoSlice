# Changelog

All notable changes to MonoSlice are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

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
