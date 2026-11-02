# CONSTITUTIONS

The rules for changing this repository are in [AGENTS.md](AGENTS.md).

## Install

```bash
git clone https://github.com/karin0/constitutions ~/.constitutions
mkdir -p ~/.claude/rules
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.claude/rules/
```

Pi:

```bash
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.pi/agent/AGENTS.md
```

DeepSeek Harness:

```bash
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.dsh/AGENTS.md
```

## Commit types

The documents that `AGENTS.md` governs are the product, so the Conventional Commits type of a commit must state what happened to the rules rather than stay a constant `docs:`.

- `feat`: a new, broadened, or narrowed rule.
- `fix`: a statement that was wrong about a fact or that its rule did not intend.
- `style`: wording and sentence structure, with every rule keeping its meaning.
- `refactor`: a fact moved between clauses or documents, requiring the same thing afterwards.
- `chore`: repository plumbing that states no rule.
- `docs`: `README.md` and `AGENTS.md`, which describe the repository rather than the rules.
