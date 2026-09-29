# Benchmarks

## Real-world space savings

MonoSlice helps reduce application size by removing unused CPU architectures from Universal Binary applications.

The actual savings depend on the application and how it is built.

---

## Example Results

The following examples show typical size reductions after removing an unused architecture.

| Application | Before | After | Saved |
|-------------|--------|-------|-------|
| Example App 1 | 2.4 GB | 1.3 GB | 1.1 GB |
| Example App 2 | 850 MB | 470 MB | 380 MB |
| Example App 3 | 620 MB | 350 MB | 270 MB |

*Results may vary depending on application version and included resources.*

---

## How size reduction works

Universal applications contain multiple versions of the same executable code.

Example:

```
Application.app

Contents
└── MacOS
    └── Application Binary

        ├── arm64
        └── x86_64
```

If you use an Apple Silicon Mac, the Intel code is not required.

MonoSlice removes:

```
x86_64
```

and keeps:

```
arm64
```

---

## What affects the result?

The amount of saved space depends on:

### Application type

Applications with large executable files usually benefit more.

Examples:

- Creative applications
- Development tools
- Games
- Professional software

---

### Included resources

Some applications contain large files that cannot be reduced:

- Images
- Videos
- Language packs
- Templates
- Assets

MonoSlice only removes unused CPU architecture code.

---

### Application architecture

Maximum savings are usually achieved when an application contains two complete architectures:

Before:

```
arm64 + x86_64
```

After:

```
arm64
```

or:

```
x86_64
```

---

## Benchmark methodology

Measurements should be performed using:

1. Original application download.
2. Application size before optimization.
3. MonoSlice optimization.
4. Application size after optimization.

Example:

```text
Original:

Application.app
Size: 2.40 GB


After MonoSlice:

Application.app
Size: 1.35 GB


Saved:

1.05 GB
```

---

## Share your results

Have an interesting result?

Share your benchmark:

- Application name
- Version
- macOS version
- Mac model
- Original size
- Optimized size

Community benchmarks help demonstrate the real-world value of MonoSlice.
