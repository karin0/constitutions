# CONSTITUTIONS

```bash
git clone git@github.com:karin0/constitutions.git ~/.constitutions
mkdir -p ~/.claude/rules
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.claude/rules/
```

## Commit types

The documents here are the product, so the Conventional Commits type of a commit says what happened to the rules rather than staying a constant `docs:`.

- `feat`: a new or broadened rule.
- `fix`: a statement that was wrong about a fact.
- `style`: wording and sentence structure, with every rule keeping its meaning.
- `refactor`: a fact moved between clauses or documents, requiring the same thing afterwards.
- `chore`: repository plumbing that states no rule.
- `docs`: this README, which describes the repository rather than the rules.
