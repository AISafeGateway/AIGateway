# Contributing guide

This guide explains how we work in this repository: branches, commits and Pull Requests (PRs). If you have questions, ask in the team meeting or open a Discussion.

## Basic rules

1. **Nobody pushes directly to `main`.** Everything goes in through a PR.
2. **Every PR is reviewed by someone else**, ideally the *second* person of the module. Nobody approves their own PR.
3. **`main` must always work**: `docker compose up` must never break.
4. **Every PR solves an issue.** If the work has no issue, create one first.
5. **Never commit secrets** (AWS keys, `.env`, tokens). If you commit one by mistake, tell the team and revoke it immediately: deleting it from the commit is not enough.

## Branches

### Naming

Format: `type/issue-number-short-description`, lowercase, words separated by hyphens.

| Type | When to use it | Example |
|---|---|---|
| `feat` | New feature | `feat/12-dni-detection-rule` |
| `fix` | Bug fix | `fix/20-empty-message-block` |
| `docs` | Documentation | `docs/05-upload-proposal` |
| `test` | Tests | `test/22-metrics-script` |
| `refactor` | Code reorganization without behavior change | `refactor/31-split-rules-module` |
| `ci` | GitHub Actions and pipelines | `ci/19-add-bandit` |
| `chore` | Maintenance, dependencies, configuration | `chore/08-pin-terraform-version` |

Rules:
- One branch per issue.
- Always start from an up-to-date `main`.
- Keep branches short-lived (a few days at most).
- Do not reuse a branch after its PR is merged.

### Create your own branch (command line)

```bash
# 1. Go to main and update it
git switch main
git pull origin main

# 2. Create and switch to your new branch
git switch -c feat/12-dni-detection-rule

# 3. Check which branch you are on
git branch --show-current
```

`git checkout -b feat/12-dni-detection-rule` does the same as `git switch -c`.

### Create your own branch (GitHub website)

1. Open the issue.
2. In the right sidebar, under **Development**, click **Create a branch**.
3. Edit the name to follow the format above, choose `main` as the source and click **Create branch**.
4. On your computer:

```bash
git fetch origin
git switch feat/12-dni-detection-rule
```

### Useful branch commands

```bash
git branch                                 # list local branches
git branch -a                              # list local and remote branches
git switch <branch-name>                   # switch to another branch
git push -u origin <branch-name>           # publish the branch (first push)
git branch -m <old-name> <new-name>        # rename the current local branch
git branch -d <branch-name>                # delete a merged local branch
git push origin --delete <branch-name>     # delete the remote branch
```

## Step-by-step workflow

### 1. Pick an issue

Take an issue from the board that is assigned to you (or unassigned), move it to **In progress** and note its number (`#12`).

### 2. Create your branch

See [Branches](#branches).

### 3. Work in small commits

Commit often, and make each commit do one thing. Five clear commits are better than one giant commit.

```bash
git add gateway/rules.py
git commit -m "feat(gateway): add DNI detection rule"
```

### 4. Keep your branch up to date

```bash
git fetch origin
git rebase origin/main
```

If there are conflicts, fix them, run `git add` on the affected files and then `git rebase --continue`. If you are not sure, ask for help before forcing anything.

### 5. Push and open the PR

```bash
git push -u origin feat/12-dni-detection-rule
```

On GitHub, click **Compare & pull request**, fill in the template and request a reviewer.

### 6. Review

- The reviewer comments, requests changes or approves.
- Answer every comment and resolve the threads.
- Make changes with new commits on the same branch.
- Once approved and CI is green, the PR can be merged.

### 7. Merge and clean up

We use **Squash and merge**: all commits in the PR become a single commit on `main`. Then delete the branch.

```bash
git switch main
git pull origin main
git branch -d feat/12-dni-detection-rule
```

## Commit messages

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): short description in imperative mood
```

**Types:**

| Type | Use |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation changes |
| `test` | Adding or changing tests |
| `refactor` | Code changes that do not alter behavior |
| `ci` | Changes to GitHub Actions or the pipeline |
| `chore` | Maintenance tasks (dependencies, configuration) |

**Scopes:** `gateway`, `rag`, `redteam`, `web`, `infra`, `docs`.

**Rules:**
- First line of 72 characters or fewer.
- Imperative mood and no final period: "add rule", not "added rule" or "adding rule".
- Explain *what* and *why*, not *how*.
- If the change breaks existing behavior, add `!` after the scope: `feat(gateway)!: change API format`.

**Good examples:**

```
feat(gateway): add DNI detection rule
fix(redteam): correct false positive calculation
docs(docs): upload the project proposal
test(gateway): add output filter tests
ci: run bandit on every pull request
chore(infra): pin Terraform version
```

**Bad examples:**

```
changes
fixed
update
WIP
```

If you need more detail, leave a blank line and write a body:

```
fix(gateway): prevent system prompt leak in error responses

The error handler returned the full prompt text when the model
failed. It now returns a generic message.
```

## Pull Requests

**Title:** same format as a commit message (`feat(gateway): add DNI detection rule`), because it becomes the squash commit message.

**Description:**
- What changes and why.
- How to test it.
- A link to the issue with `Closes #12`, so it closes automatically on merge.

**Size:** keep them small. A PR under about 300 lines is easy to review; a huge one is not.

**Before requesting a review:**
- [ ] `docker compose up` works.
- [ ] Tests pass.
- [ ] No secrets or personal data.
- [ ] Affected documentation is updated.

**If you are the reviewer:**
- Review within 48 hours.
- Run the change, don't just read it.
- Be clear and kind: comment on the code, not the person.
- Mark optional suggestions with "(optional)".

## Releases

Each important milestone is tagged (`v0.1`, `v0.2`...) with a GitHub release. The Team Lead creates them when `main` is stable.

## Documentation and meetings

- Meeting notes go in `docs/meeting-notes/` using the template.
- Important technical decisions go in `docs/decisions/`.
- Changes in `docs/` also go through a PR.

## License

By contributing to this repository, you agree that your contributions are licensed under the [Apache License 2.0](LICENSE).

## Security

This project is about security, so we lead by example:
- Fictional data only.
- Test attacks only against our own system.
- If you find a vulnerability in the project, tell the team privately before opening a public issue.
