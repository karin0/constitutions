# Cloud sessions

* System Packages Belong to the Container: the agent installs a missing system package or toolchain itself.
* Pushes Keep the Work: the agent pushes to a branch other than the default branch whenever the work needs it, without the user's explicit permission, and this includes `git push --force-with-lease --force-if-includes` of a rewritten branch. The agent opens no pull request unless the user asks for one.
* Visibility Before Push: before the first push to a repository, the agent checks whether the repository is public. A push to a public repository carries only content fit for publication, and credentials, personal data, and internal hostnames stay out of it.
