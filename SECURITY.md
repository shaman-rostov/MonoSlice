# Security Policy

## Supported Versions

MonoSlice is under active development. Security fixes are made against the latest release; older versions are not patched separately.

| Version | Supported |
| --- | --- |
| Latest release | ✅ |
| Older releases | ❌ |

---

## Reporting a Vulnerability

If you find a security vulnerability in MonoSlice, please **do not open a public GitHub issue**.

Instead, report it privately using [GitHub Security Advisories](https://github.com/shaman-rostov/MonoSlice/security/advisories/new) for this repository. This creates a private discussion visible only to you and the maintainers until a fix is ready.

Please include:

- A description of the vulnerability and its potential impact.
- Steps to reproduce, or a proof of concept if possible.
- The affected version (Mac app or CLI) and macOS version.

We'll acknowledge reports as soon as possible and keep you updated as the issue is investigated and fixed. Once a fix is released, we'll credit reporters who wish to be credited.

---

## Scope

MonoSlice modifies other applications' binaries and re-signs them, so its security surface mainly concerns:

- **Code signing and verification** — MonoSlice must never leave an app installed with an invalid or unverifiable signature. Any bypass of the `codesign --verify` check after re-signing is a security issue.
- **Privilege escalation** — administrator rights are only used for the final swap into a protected location (e.g. `/Applications`); anything that runs unrelated code with elevated privileges is a security issue.
- **Safeguards for specific app categories** — the checks that skip Mac App Store apps, system apps, and apps whose entitlements an ad-hoc signature can't preserve (App Sandbox, app groups, keychain groups, etc.) exist to prevent broken or insecure apps. A way to circumvent these checks is a security issue.
- **Local file handling** — MonoSlice works entirely on-disk and locally; any code path that sends application data or file contents off the device would be a security issue (MonoSlice does not have or need network access for optimization).

The following are **not** considered security vulnerabilities, but are documented, known trade-offs of the tool itself:

- Ad-hoc re-signing resetting TCC permissions (camera, microphone, Full Disk Access) or Keychain access prompts — this is an unavoidable consequence of re-signing, and MonoSlice warns users before it happens. See the [Safety section](docs/index.md#safety) of the docs.
- Optimized apps losing the Hardened Runtime, notarization and entitlements of their original signature — an ad-hoc signature cannot carry them. See [Limitations and Risks](docs/limitations-and-risks.md#what-changes-in-an-optimized-app).
- An optimized app failing to launch due to app-specific protections not yet recognized by MonoSlice — please report this as a regular [bug](https://github.com/shaman-rostov/MonoSlice/issues), not a security issue.

---

## Disclosure Policy

We follow coordinated disclosure: once a reported vulnerability is confirmed and a fix is available, we'll publish a security advisory describing the issue and crediting the reporter (unless anonymity is requested).
