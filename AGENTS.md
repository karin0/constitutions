# Amending the constitutions

These rules govern every rule document in this repository, which may state obligations in the imperative or the simple present tense.

A change made during work in another tree stays uncommitted in this repository for a later review. The agent that made the change reports it once and does not track it as pending work of the other tree. An agent working in this repository may create commits, which follow the commit types below.

`CONSTITUTIONS.md` holds the engineering rules and the conventions of collaboration, and `WRITING.md` holds the rules for natural text, divided into what a text contains and how its sentences are written. The sentence rules draw on https://github.com/anthropics/claude-code/issues/77136 and https://github.com/programasweights/claudish/blob/main/specs/claudish-to-english.md. Every section of `CONSTITUTIONS.md` above the Python rules, and all of `WRITING.md`, is agnostic to any specific project, programming language, framework, and deployment.

A principle may become a new clause of `CONSTITUTIONS.md` or `WRITING.md` only when it is orthogonal to every existing clause and important enough to enforce in any development work. A transient, session-specific action does not qualify.

A clause is generalized as a first principle that addresses the root cause behind a specific case, without the conditions and details specific to that case. An example may stay only when it stands for a general category that anyone recognizes without any context, and every other example is deleted. A clause gives the reason for its rule only when a reader cannot see that reason from the rule itself. The clause holds in any specific tree, and every name in it is known to any reader of `CONSTITUTIONS.md`. Before a clause is proposed, it is tested against a case other than the one that prompted it. When it covers only the prompting case, it is rewritten as the principle behind that case, or withdrawn when no such principle exists.

## Commit types

The rule documents are the product of this repository, so the Conventional Commits type of a commit must state what happened to the rules rather than stay a constant `docs:`.

- `feat`: a new, broadened, or narrowed rule.
- `fix`: a statement that was wrong about a fact or that its rule did not intend.
- `style`: wording and sentence structure, with every rule keeping its meaning.
- `refactor`: a fact moved between clauses or documents, requiring the same thing afterwards.
- `chore`: repository plumbing that states no rule.
- `docs`: `README.md` and `AGENTS.md`, which describe the repository rather than the rules.
