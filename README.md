# MonoSlice

**A free macOS utility that reclaims disk space by stripping the unused CPU architecture from Universal (fat) binaries.**

Most Mac apps ship as *Universal Binaries* containing both `arm64` (Apple Silicon) and `x86_64` (Intel) code. On any given Mac you only ever run one of them. MonoSlice detects your host architecture, scans `/Applications` (or any folder) for apps that carry the slice you don't need, and removes it with the native `lipo` tool — then re-signs each app so it still launches.

- **Mac app** (SwiftUI, English/Russian) — scans and slims apps interactively, with batch selection across all your apps. Runs as a regular Dock app or, optionally, from the menu bar.
- **CLI** (`monoslice`) — for scripting and one-off use.
- Built on the system `lipo` and `codesign` tools.
- **Free to use.** MonoSlice is closed-source; this repository hosts public documentation and release downloads, not the app's source code.

Requires **macOS 12.0+** (Monterey or newer).

<p align="center">
  <img src="docs/images/scan-results.png" alt="MonoSlice lists apps with Universal Binaries and the space each one can free" width="640">
</p>

See [docs](docs/index.md) for full documentation, and [Limitations and Risks](docs/limitations-and-risks.md) before optimizing important apps.
