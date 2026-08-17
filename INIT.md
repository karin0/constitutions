# Initializing a new tree

These steps fire once, when a project tree is created. The standing constraints live in `CONSTITUTIONS.md` beside this file.

## Static toolchain before implementation

Wire the strictest available static toolchain into a script or CI check before any implementation, so it gates changes rather than relying on discipline: formatter, strict linting, and type checking with a consciously curated ignore list. uv, ruff and pyright for Python, `cargo fmt` and `clippy` with `-D warnings -W clippy::pedantic` for Rust, the ecosystem equivalent elsewhere. Where the formatter carries a quote setting, set it to single quotes.

For Python, ruff selects `["ALL", "ANN401"]` against a curated ignore list, keeping ANN401 while the rest of the ANN family stays ignored. `~/lark/dev/money/pyproject.toml` is a working example; drop its unnecessary ignores when copying.

## Propagate the constitutions

```shell
ln -s "$(realpath /path/to/me)" CONSTITUTIONS.md
ln -s CONSTITUTIONS.md AGENTS.md
ln -s CONSTITUTIONS.md CLAUDE.md
```
