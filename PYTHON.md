# Python toolchain for a new tree

Fires once per tree, from `INIT.md` beside this file. The standing Python rules live in the Python section of `CONSTITUTIONS.md`.

ruff selects `["ALL", "ANN401"]` against a curated ignore list, keeping ANN401 while the rest of the ANN family stays ignored. This skeleton is the starting point; each further ignore is added against a rule that actually fired, with a comment when the reason is not evident from the rule name.

```toml
[tool.ruff]
line-length = 100
target-version = "py314"
# src = ["src"]  # For workspaces only.

[tool.ruff.lint]
select = ["ALL", "ANN401"]
ignore = [
    "A", "ANN", "ARG", "COM812", "CPY", "D", "EM", "ERA", "FAST", "FBT", "PLR", "PTH", "TD",
    "BLE001", "C901", "N818", "PLC0415", "PLW1508", "PLW2901", "RET503", "S101", "SLF001",
    "TC001", "TC002", "TC003", "TC006", "TRY003", "TRY004",
]

[tool.ruff.lint.per-file-ignores]
"*/cli.py" = ["T20"]
"**/tests/*" = ["ANN201", "B018", "INP001", "PLW0108", "PT018", "S101", "SIM105", "T20",
                # Fixtures stand in for credentials, which is what makes them fixtures.
                "S105", "S106"]

[tool.ruff.lint.flake8-tidy-imports.banned-api]
"__future__.annotations".msg = "PEP 649 lazy annotations are the 3.14 default"

[tool.ruff.lint.flake8-quotes]
docstring-quotes = "single"
inline-quotes = "single"
multiline-quotes = "single"

[tool.ruff.lint.isort]
lines-between-types = 1

[tool.ruff.format]
quote-style = "preserve"

[tool.pyright]
# include = ["src"]  # For workspaces only.
typeCheckingMode = "strict"
pythonVersion = "3.14"
```

## uv workspace

A workspace root carries no `requires-python`, which otherwise tells ruff which modules are first-party and which are stdlib. List every member source root in ruff `src` and in pyright `include`, and repeat the list in pyright `extraPaths` so the members resolve as sources rather than as installed libraries.
