# Amending the constitutions

These rules govern every change to `CONSTITUTIONS.md`, `INIT.md`, `PYTHON.md`, and `CLOUD.md`.

These documents may state obligations in the imperative or the simple present tense.

A change made during work in another tree must stay uncommitted in this repository for a later review. The agent that made the change must report it once and must not track it as pending work of the other tree.

Every section of `CONSTITUTIONS.md` above the Python rules must be agnostic to any specific project, programming language, framework, and deployment.

A principle may become a new clause of `CONSTITUTIONS.md` only when it is orthogonal to every existing clause and important enough to enforce in any development work. A transient, session-specific action does not qualify.

A clause must be generalized as a first principle that addresses the root cause behind a specific case, without the conditions and details specific to that case. An example may stay only when it stands for a general category that anyone recognizes without any context, and every other example must be deleted. A clause gives the reason for its rule only when a reader cannot see that reason from the rule itself. The clause must hold in any specific tree, and every name in it must be known to any reader of `CONSTITUTIONS.md`. Before a clause is proposed, it must be tested against a case other than the one that prompted it. When it covers only the prompting case, it must be rewritten as the principle behind that case, or withdrawn when no such principle exists.

## Commit types

The documents here are the product, so the Conventional Commits type of a commit must state what happened to the rules rather than stay a constant `docs:`.

- `feat`: a new, broadened, or narrowed rule.
- `fix`: a statement that was wrong about a fact or that its rule did not intend.
- `style`: wording and sentence structure, with every rule keeping its meaning.
- `refactor`: a fact moved between clauses or documents, requiring the same thing afterwards.
- `chore`: repository plumbing that states no rule.
- `docs`: `README.md`, which describes the repository rather than the rules.
