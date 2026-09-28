# Chapter 08 — GitHub Pull Requests, Code Reviews and Online Merging

> Stage 0 / 10 | Hinglish study chapter | 28 Sep 2026

## Goal

PR workflow samajhna: feature branch push → GitHub compare/diff → review/checks → merge → local master sync.

## PR kya hai?

Pull Request (PR) base branch mein changes merge karne ka proposal hai. Usually feature branch se `master`/`main` mein open hoti hai. PR code review, discussion, automated checks aur clean history ka place hai.

```text
local feature branch
  ↓ git push -u origin feature-x
remote feature-x
  ↓ create PR on GitHub
review + configured checks
  ↓ merge PR
remote master updated
  ↓ git switch master && git pull
local master updated
```

## Standard workflow

```bash
git switch master
git pull origin master
git switch -c feature-profile
# edit files
git add profile.txt
git commit -m "feat: add user profile"
git push -u origin feature-profile
```

GitHub par base branch `master`, compare branch `feature-profile` choose karo. Title specific rakho, description mein **what changed**, **why**, aur **how tested** likho.

## Diff colors

- Green `+` lines = added lines.
- Red `-` lines = removed lines.
- Diff traffic signal nahi hai; yeh old vs new code ka comparison hai.

## Updating an open PR

Same PR branch par fix karo:

```bash
# feature-profile branch par
git add path/to/file
git commit -m "fix: address review feedback"
git push
```

Open PR automatically new commit se update hoti hai; delete/close karke nayi PR banana zaroori nahi.

## Review, checks and merge

Human review comments code/style/logic ko inspect karte hain. **Checks** (GitHub Actions/CI or connected services) configured automated tests, builds, linting, security checks ya deployment validation ho sakte hain. Checks tabhi exist/run karte hain jab repository mein workflow/integration configured ho. Green checks useful hain, but production bug-free guarantee nahi.

Merge button: usually **Merge pull request**, then **Confirm merge**. Merge ke baad remote base branch update hoti hai. App automatically live tabhi hoga jab separate deployment pipeline configured ho.

## Local sync after online merge

```bash
git switch master
git pull origin master
git branch -d feature-profile
```

GitHub website se remote feature branch **Delete branch** button use karke delete kar sakte ho after merge. Local `git branch -d` safe delete hai; `-D` force delete hai.

## Common mistakes

- `git push -u origin feature-profile` ko master push samajhna: yeh only feature remote branch update karta hai.
- Review comments aur CI checks ko same samajhna.
- Online merge ke baad local master par pull bhool jana.
- PR merge ko production deployment samajhna.

## Practice

`feature-docs` branch banao, ek docs file add karo, GitHub push karo, PR open karo, Files changed diff dekho, same branch se one follow-up commit push karo, merge karo, local master pull karo.

## Exit gate

Bina notes: feature branch push karna, PR open/update/merge, diff colors aur checks explain karna, aur merge ke baad local master sync karna aana chahiye.

**References:** [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow) · [Status checks](https://docs.github.com/en/pull-requests/reference/status-checks)
