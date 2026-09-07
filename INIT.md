# Initializing a new tree

These steps fire once, when a project tree is created. The standing constraints live in `CONSTITUTIONS.md` beside this file.

## Static toolchain before implementation

Wire the strictest available static toolchain into a script or CI check before any implementation, so it gates changes rather than relying on discipline: formatter, strict linting, and type checking with a consciously curated ignore list. uv, ruff and pyright for Python, following `PYTHON.md` beside this file; `cargo fmt` and `clippy` for Rust, at the levels below; the ecosystem equivalent elsewhere.

In languages that allow both quote styles (Python, TypeScript, Shell), string literals and docstrings use single quotes, and the toolchain carries that from the first commit rather than the prose. A string that would escape many single quotes of its own, or a shell string whose variables must expand, keeps double quotes.

### Rust lint levels and release profile

In `Cargo.toml`:

```toml
[lints.rust]
warnings = 'deny'

[lints.clippy]
pedantic = { level = 'warn', priority = -1 }
```

The negative priority ranks the group below individual lints, so a later entry can relax one lint of the group.

`warnings = 'deny'` covers clippy's pedantic warnings as well, so `cargo build` stops at the first warning while developing. `RUSTFLAGS='--warn warnings' cargo build` relaxes that for one command.

A binary target generally adds:

```toml
[profile.release]
lto = true
strip = true
codegen-units = 1
```

## Supply chain cooldown

Every package manager in the tree refuses dependency versions published within the last 15 days.

uv, in `pyproject.toml`, or at the top level of `uv.toml`:

```toml
[tool.uv]
exclude-newer = '15 days'
```

pnpm, in `pnpm-workspace.yaml`, in minutes:

```yaml
minimumReleaseAge: 21600
```

Cargo ignores `registry.global-min-publish-age` with a warning unless it runs under nightly `-Zmin-publish-age`, so a stable toolchain has no cooldown gate yet. Check the publication dates that a `cargo update` brings in manually until the feature stabilizes.

A version inside the window is admitted per package, through `exclude-newer-package` or `minimumReleaseAgeExclude`.
