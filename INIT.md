# Initializing a new tree

These steps fire once, when a project tree is created. The standing constraints live in `CONSTITUTIONS.md` beside this file.

## Static toolchain before implementation

Wire the strictest available static toolchain into a script or CI check before any implementation, so it gates changes rather than relying on discipline: formatter, strict linting, and type checking with a consciously curated ignore list. uv, ruff and pyright for Python, following `PYTHON.md` beside this file; `cargo fmt` and `clippy` with `-D warnings -W clippy::pedantic` for Rust; the ecosystem equivalent elsewhere.

In languages that allow both quote styles (Python, TypeScript, Shell), string literals and docstrings use single quotes, and the toolchain carries that from the first commit rather than the prose. A string that would escape many single quotes of its own, or a shell string whose variables must expand, keeps double quotes.

## Propagate the constitutions

```shell
ln -s ~/.constitutions/CONSTITUTIONS.md .
ln -s CONSTITUTIONS.md AGENTS.md
ln -s CONSTITUTIONS.md CLAUDE.md
```
