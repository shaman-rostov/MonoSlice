# Contributing to MonoSlice

Thanks for your interest in contributing. This repository is MonoSlice's public home: documentation, release downloads, and issue tracking. **It does not contain the app's source code** — MonoSlice is closed-source, so there's no codebase here to submit pull requests against.

That said, there's plenty of useful ways to contribute here.

---

## What You Can Contribute

### Documentation

Everything under [`docs/`](docs/) and the root-level `README.md`, `CHANGELOG.md`, etc. is fair game:

- Fixing inaccurate, outdated, or unclear explanations.
- Improving the FAQ, installation, or usage guides based on questions you've seen or had yourself.
- Adding real-world [benchmark](docs/benchmarks.md) results (app name, version, before/after size, macOS version, Mac model).
- Fixing typos, broken links, or formatting issues.

To propose a change, open a pull request against this repository. Small fixes (typos, broken links) can go straight to a PR; larger rewrites are easier to land if you open an issue first to align on direction.

### Bug Reports

If MonoSlice doesn't work as expected, open a [GitHub Issue](https://github.com/shaman-rostov/MonoSlice/issues) with:

- macOS version and Mac model (Intel or Apple Silicon).
- MonoSlice version (Mac app or CLI).
- The affected application and its version.
- Steps to reproduce, and what you expected vs. what happened.

For security vulnerabilities, follow [SECURITY.md](SECURITY.md) instead of opening a public issue.

### Feature Requests

Open an issue describing the use case, not just the feature — what you're trying to do, and why the current behavior doesn't cover it. This is more useful than a prescriptive spec, since implementation happens outside this repository.

### Translations

The Mac app currently supports English and Russian. If you'd like to help with additional languages or improve existing translations, open an issue describing the language and your proposed strings — translation work happens in the private app repository, but issues here are how it gets triaged and prioritized.

---

## What This Repository Is Not

- **Not a place to submit code changes** — there's no `Sources/` or build system here to patch.
- **Not the issue tracker for the source repository** — since that repository is private, all public bug/feature discussion happens here instead.

---

## License

Contributions to this repository's documentation are made under the terms described in [LICENSE](LICENSE). The MonoSlice application itself remains closed-source and is not affected by contributions here.
