# Amending the constitutions

These rules govern every change to `CONSTITUTIONS.md`, `INIT.md`, and `PYTHON.md`.

These documents state obligations in the imperative or the simple present tense.

A change made during work in another tree stays uncommitted in this repository for a later review.

Every section of `CONSTITUTIONS.md` above the Python rules is agnostic to any specific project, programming language, framework, and deployment.

A principle becomes a new clause of `CONSTITUTIONS.md` only when it is orthogonal to every existing clause and important enough to enforce in any development work. A transient, session-specific action does not qualify.

A clause is phrased as the general principle behind the case that prompted it, with every condition and detail that held only in that case removed. An example stays only when it stands for a general category that anyone recognizes without any context, and every other example is deleted. The clause holds in any specific tree, and every name in it is known to any reader of `CONSTITUTIONS.md`.

## Commit types

The documents here are the product, so the Conventional Commits type of a commit says what happened to the rules rather than staying a constant `docs:`.

- `feat`: a new, broadened, or narrowed rule.
- `fix`: a statement that was wrong about a fact.
- `style`: wording and sentence structure, with every rule keeping its meaning.
- `refactor`: a fact moved between clauses or documents, requiring the same thing afterwards.
- `chore`: repository plumbing that states no rule.
- `docs`: `README.md`, which describes the repository rather than the rules.
