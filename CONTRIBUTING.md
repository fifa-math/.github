# Contributing to `fifa-math` repositories

## Rust-first scripts and automation

**Use Rust for first-party scripts and automation; do not add or extend Python scripts.** This includes build/CI helpers, test infrastructure, code generation, database/schema migration tooling, deployment/release helpers, project administration, and ad-hoc repository maintenance. Prefer maintained Rust CLIs or `cargo xtask`; shell and YAML should be thin wrappers when the platform requires them.

**Existing Python automation is migration debt.** Record each existing script and its callers, then replace with Rust while retaining arguments, exit behavior, data formats, error paths, security checks, and supported platforms. Validate positive and negative regression scenarios and update workflow, hook and documentation entry points before removing an old script. An issue or documentation PR is *not* evidence of completed migration.

**Python application/product code may be approved as a narrow exception** when its owner documents the scope, purpose, tradeoffs, and why Rust is not appropriate. Associated application-specific tests may follow that exception. A build script, CI task, generator, migration runner, or one-off automation cannot be relabeled "application code" to evade the rule.

Document repeatable `cargo` commands; cover meaningful failures and regressions, and use `cargo fmt --check`, `cargo clippy -- -D warnings`, `cargo test`, and appropriate end-to-end checks. Report checks as passed only when actually executed on the changed commit. Do not delete functioning scripts until an equivalent Rust path is tested.

The canonical organization `.github` repository supplies **contributor guidance**; GitHub does not automatically inherit arbitrary `AGENTS.md`, policies, or workflows. Individual repositories should synchronize agent instructions and explicitly enable relevant checks to make the rule enforceable.


## Durable engineering policy

- This repository defines public organization-wide defaults for `fifa-math`.
- Never commit credentials, private keys, access tokens, customer data, or private-repository inventories.
- Resolve Git conflicts semantically: inspect both sides, the merge base, nearby tests and contracts, and normally 3–10 relevant prior commits. Never blindly select all of `ours` or all of `theirs`.
- Prefer focused pull requests, explicit validation, non-destructive Git operations, and documented tradeoffs.
- Cross-repository integration uses versioned interfaces, APIs, SDKs, events, or explicitly owned replicated read models. Services do not reach into another service's database by default.
- `*-infra` repositories and `*-monorepo` application source remain separate. A `*-infra` repository must never appear as a Git submodule under `*-monorepo/apps`.
- Git submodules are reserved for explicitly coordinated editable source composition. Zed packages or immutable artifacts are preferred for package dependencies. Production deploys immutable artifacts or OCI digests, not source clones.

## Pull requests

Keep pull requests focused and reviewable. Describe motivation, changed behavior, interface or migration impact, security considerations, validation performed, and rollback or compatibility plans where relevant.

<!-- ore-org-baseline:begin -->
Thank you for contributing to repositories owned by [`fifa-math`](https://github.com/fifa-math). Repository-local instructions take precedence when they are stricter.

## Before proposing a change

1. Read the repository README, contribution notes, lowercase `agents.md`, architecture documentation, linked issues, and relevant [Linear project](https://linear.app/denman/project/githubcomfifa-math-06015d19054a).
2. Confirm the authoritative source repository and whether files are generated, vendored, mirrored, or owned by another repository.
3. Fetch current remote state and preserve concurrent work. Avoid git rebase in favor of git merge.
4. Do not use `git stash`, `git reset`, `git clean`, `git filter-repo`, force-push, destructive worktree/submodule operations, or broad deletion/rewrite commands without exact authorization.
5. Never include secrets, credentials, customer data, legal records, or other private information in issues, commits, test fixtures, screenshots, or logs.

## Pull requests

Use a focused feature branch and a draft pull request. Link the relevant issue or Linear work; explain behavior, risk, security impact, migration and rollback considerations, tests, and cross-repository dependencies. Resolve conflicts semantically with full context—normally including the merge base and 3–10 relevant commits—rather than selecting one side wholesale. Run all affected checks and scan the complete worktree for conflict markers.

External GitHub Actions must be pinned to full commit SHAs. Workflows must use explicit least-privilege permissions, explicit timeouts, and non-persisted checkout credentials.
<!-- ore-org-baseline:end -->
