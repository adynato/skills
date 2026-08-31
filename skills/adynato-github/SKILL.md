---
name: adynato-github
description: GitHub workflow conventions for Adynato projects. Covers creating PRs with gh CLI, writing thorough descriptions, and using stacked PRs for large deliverables. Use when creating pull requests, managing branches, or breaking down large features.
---

# GitHub Skill

Use this skill when working with GitHub on Adynato projects.

## Always Use gh CLI

Use the `gh` CLI for all GitHub operations instead of the web interface:

```bash
# Create PR
gh pr create --title "Title" --body "Description"

# View PR
gh pr view 123

# Check PR status
gh pr checks 123

# Merge PR
gh pr merge 123 --squash
```

## PR Descriptions

Every PR must have a thorough description. Use this template:

```bash
gh pr create --title "feat: add user authentication" --body "$(cat <<'EOF'
## Summary

Brief description of what this PR does and why.

- Added JWT-based authentication flow
- Implemented login/logout endpoints
- Added auth middleware for protected routes

## Changes

- `lib/auth.ts` - Auth utilities and token management
- `app/api/auth/login/route.ts` - Login endpoint
- `app/api/auth/logout/route.ts` - Logout endpoint
- `middleware.ts` - Route protection

## Testing

### Automated
- [ ] Login with valid credentials returns token
- [ ] Login with invalid credentials returns 401
- [ ] Protected routes reject unauthenticated requests
- [ ] Logout invalidates token

### Manual
1. Sign in with a test account
2. Open a protected route
3. Confirm authenticated access works
4. Log out and confirm access is revoked

## Screenshots

(if UI changes)

## Related

- Closes #123
- Part of #456
EOF
)"
```

### Required Sections

| Section | When Required | Purpose |
|---------|---------------|---------|
| **Summary** | Always | What and why in 2-3 sentences |
| **Changes** | Always | List of files/areas modified |
| **Testing** | Always | Automated coverage and explicit manual testing steps |
| **Screenshots** | UI changes | Visual proof of changes |
| **Related** | If applicable | Linked issues/PRs |

Manual testing steps are required in every PR description. Be specific about the exact flow, commands, requests, accounts, or environment used to verify the change.

## Stacked PRs

For large deliverables, break work into small, stacked PRs that build on each other.

### Why Stack PRs

- **Easier review** - Reviewers can focus on one concern at a time
- **Faster merges** - Small PRs get approved faster
- **Lower risk** - Each PR is independently deployable
- **Better history** - Clear progression of changes

### Stacking Strategy

For a feature like "Add user dashboard":

```
PR 1: Add user API endpoints (base)
  ↓
PR 2: Add dashboard data fetching (stacked on PR 1)
  ↓
PR 3: Add dashboard UI components (stacked on PR 2)
  ↓
PR 4: Add dashboard tests (stacked on PR 3)
```

### Creating Stacked PRs

Use `<default-base-branch>` for the repository's integration branch: `dev` when it exists, otherwise `main`.

```bash
# PR 1: Base branch
git checkout -b feat/user-api
# ... make changes ...
git push -u origin feat/user-api
gh pr create --base <default-base-branch> --title "feat: add user API endpoints"

# PR 2: Stack on PR 1
git checkout -b feat/dashboard-data feat/user-api
# ... make changes ...
git push -u origin feat/dashboard-data
gh pr create --base feat/user-api --title "feat: add dashboard data fetching"

# PR 3: Stack on PR 2
git checkout -b feat/dashboard-ui feat/dashboard-data
# ... make changes ...
git push -u origin feat/dashboard-ui
gh pr create --base feat/dashboard-data --title "feat: add dashboard UI"
```

### Stack Description

In stacked PRs, note the relationship:

```markdown
## Summary

Adds dashboard UI components.

## Stack

This PR is part of a stack:
1. #101 - Add user API endpoints ← **merged**
2. #102 - Add dashboard data fetching ← **base**
3. **#103 - Add dashboard UI** ← you are here
4. #104 - Add dashboard tests

Please review and merge in order.
```

### Updating Stacked PRs

When the base PR changes:

```bash
# Update your branch with changes from base
git checkout feat/dashboard-ui
git rebase feat/dashboard-data
git push --force-with-lease
```

When base PR merges:

```bash
# Rebase onto new base
git checkout feat/dashboard-data
git rebase <default-base-branch>
git push --force-with-lease

# Update PR base branch
gh pr edit 102 --base <default-base-branch>
```

## PR Size Guidelines

| Size | Lines Changed | Review Time | Recommendation |
|------|---------------|-------------|----------------|
| XS | < 50 | Minutes | Ideal |
| S | 50-200 | < 1 hour | Good |
| M | 200-500 | 1-2 hours | Acceptable |
| L | 500-1000 | 2-4 hours | Split if possible |
| XL | > 1000 | Days | Must split |

**Target: Keep PRs under 300 lines changed.**

## Commit Messages

Use conventional commits:

```bash
feat: add user authentication
fix: resolve login redirect loop
docs: update API documentation
refactor: extract auth utilities
test: add auth endpoint tests
chore: update dependencies
```

Format:
```
<type>: <short description>

<optional body explaining why>

<optional footer with references>
```

## Branch Naming

```
feat/short-description    # New features
fix/issue-description     # Bug fixes
refactor/what-changed     # Code refactoring
docs/what-documented      # Documentation
test/what-tested          # Test additions
```

## Starting New Work

When a new prompt arrives:

- If the current branch already matches the work, continue on that branch
- Otherwise, switch back to the repository's integration branch: prefer `dev`, otherwise `main`
- Pull that branch before starting the new task
- Create a fresh branch for the new work and open a new PR back into that same branch
- Do not create a new git worktree unless the user explicitly requests one

```bash
git checkout <default-base-branch>
git pull --ff-only
git checkout -b feat/my-change
gh pr create --base <default-base-branch> --title "feat: describe change"
```

## PR and CI Loop

Create open PRs by default. Use draft PRs only when the user explicitly asks for a draft, work-in-progress PR, or an intentionally unready review surface.

After opening or updating a PR:

1. Check whether CI exists for the PR.
2. If checks are pending, wait for the CI loop to complete.
3. If checks fail, inspect the failing job logs.
4. Fix valid issues, commit the fixes, push the branch, and wait for CI again.
5. Repeat until checks pass, no checks are configured, or the remaining failure is clearly outside the PR's code changes.

```bash
gh pr create --base <default-base-branch> --title "feat: describe change"
gh pr checks <pr-number> --watch
gh run view <run-id> --log-failed
```

When a failure is a real code or test issue, fix it before reporting completion. When a failure is a flaky, infrastructure, permission, quota, or environment issue, state that clearly and leave the PR open unless the user explicitly asks for a different path.

If the user asks you to merge the PR, merge only after the PR is mergeable and any configured required checks have passed. If repository policy, review requirements, branch protection, or permissions block the merge, report the exact blocker.


## Common gh Commands

```bash
# Create PR with labels
gh pr create --title "feat: thing" --label "enhancement" --label "needs-review"

# Create open PR
gh pr create --title "feat: thing"

# Request reviewers
gh pr edit 123 --add-reviewer @username

# Check CI status
gh pr checks 123 --watch

# View PR diff
gh pr diff 123

# Checkout PR locally
gh pr checkout 123

# Close PR
gh pr close 123

# Reopen PR
gh pr reopen 123

# List open PRs
gh pr list

# View PR comments
gh pr view 123 --comments
```

## Review Process

1. **Self-review first** - Read your own diff before requesting review
2. **CI loop must complete** - Wait for configured checks and fix valid failures before handing off
3. **Respond to feedback** - Address or discuss all comments
4. **Squash on merge** - Keep default branch history clean

```bash
# Merge with squash (preferred)
gh pr merge 123 --squash --delete-branch

# Merge with rebase (for stacks)
gh pr merge 123 --rebase --delete-branch
```

## Addressing PR Comments

When fixing review comments, follow this workflow for **each comment**.

If you are given a direct GitHub comment URL, treat it as an instruction to handle that exact thread end-to-end: inspect it, reply on that thread, resolve it if fixed or invalid, and explicitly tell the user if it remains unresolved.

### 1. Make Individual Commits

Create a separate conventional commit for each review comment fix:

```bash
# Fix first comment
git add src/auth.ts
git commit -m "fix: add null check for user token

Addresses review comment about potential null reference"

# Fix second comment
git add src/api/users.ts
git commit -m "refactor: extract validation logic to separate function

Addresses review comment about function complexity"

# Fix third comment
git add src/utils.ts
git commit -m "fix: handle edge case for empty array

Addresses review comment about missing edge case handling"
```

**Do NOT batch multiple comment fixes into one commit.** Each fix should be atomic and traceable.

### 2. Always Reply

Every linked comment must get a thread reply. Do not fix code silently and move on.

**If fixed or otherwise addressed:**
```
Fixed in <commit-sha>
```

Or with more context:
```
Fixed in abc1234 - added null check before accessing token property.
```

**If the comment is not valid or no code change is needed:**
```
I do not think this change is needed because [reason].

Current behavior is intentional/correct for [explanation], so I am resolving this thread.
```

**If the comment is still valid or not yet addressed:**
- Leave the thread open in GitHub
- If a thread reply is useful, keep it focused on status, reasoning, or a clarifying question
- Explicitly tell the user that this comment remains unresolved and why


### 3. Resolve Only When Appropriate

After replying:

- Resolve the conversation if the requested change was made
- Resolve the conversation if the comment is invalid and you explained why no change is needed
- Do not resolve the conversation if the comment is still valid, blocked, or needs follow-up
- When a thread remains open, explicitly flag that unresolved status to the user
- Do not post "this is unresolved" in GitHub just to satisfy this rule

```bash
# View comments to get comment IDs
gh api repos/{owner}/{repo}/pulls/{pr}/comments

# Resolve fixed or invalid conversations after replying
# Leave unresolved conversations open
```

In the GitHub web UI: Click "Resolve conversation" only after your reply if the thread is addressed or invalid.

### Complete Workflow Example

```bash
# 1. Read all comments
gh pr view 123 --comments

# 2. For each valid comment, fix and commit individually
git add src/auth.ts
git commit -m "fix: validate token expiry before use

Addresses review feedback on auth token handling"

# 3. Push all fixes
git push

# 4. Reply to each linked comment thread in GitHub UI or via API
gh api repos/adynato/myrepo/pulls/123/comments/456789/replies \
  -f body="Fixed in $(git rev-parse --short HEAD)"

# 5. Resolve only threads that are fixed or invalid
# Leave still-valid threads open and tell the user they remain unresolved
```

### Comment Response Templates

| Scenario | GitHub reply | User report |
|----------|--------------|-------------|
| Fixed | "Fixed in `abc1234`" | "Resolved." |
| Fixed with explanation | "Fixed in `abc1234` - moved validation to middleware as suggested" | "Resolved." |
| Invalid / no change needed | "Current behavior is intentional because [reason], so I am resolving this thread." | "Resolved as invalid / no change needed." |
| Still open / blocked | "I’m looking into this. [status or blocker]" | "This comment is still unresolved because [reason]." |
| Needs discussion | "I see your point, but [reasoning]. What do you think about [alternative]?" | "This comment is still unresolved pending discussion." |
| Won't fix (out of scope) | "Good catch, but out of scope for this PR. Created #456 to track." | "This comment is still unresolved for this PR; follow-up tracked in #456." |
| Question/clarification | "Good question - [explanation of why code works this way]" | "Resolved after clarification." |

### Rules

1. **One commit per comment** - Makes it easy to trace what fixed what
2. **Always reply on the linked thread** - Never leave comment URLs unaddressed
3. **Resolve only when fixed or invalid** - Do not close valid open feedback
4. **If still valid, flag it to the user** - Leave the thread open and report the unresolved status back to the user
5. **Reference commits** - Include SHA so reviewer can verify the fix
6. **Be respectful** - Even when disagreeing, explain your reasoning
7. **Create issues for scope creep** - If a comment suggests something bigger, create an issue instead
