# Stage 0 — Developer Setup, Terminal, Git & GitHub

> 10 Hinglish chapters for a practical Stage 0 foundation | macOS + VS Code + GitHub | 28 Sep 2026

## Chapter map

1. [01 — Terminal Basics and Navigation](01-terminal-basics.md)
2. [02 — VS Code Setup and Shortcuts](02-vscode-setup.md)
3. [03 — Git Fundamentals: Working Tree → Staging → Commit](03-git-fundamentals.md)
4. [04 — Git Commit History and Inspection](04-git-history.md)
5. [05 — Branching and Merging](05-git-branching.md)
6. [06 — Local Merge and Conflicts](06-local-merge-conflicts.md)
7. [07 — Remote Repositories: origin, push, pull, clone](07-git-remote.md)
8. [08 — GitHub Pull Requests, Code Reviews and Online Merging](08-github-prs.md)
9. [09 — `.gitignore`, Secrets and Large Files](09-gitignore-secrets.md)
10. [10 — GitHub Issues and Open-Source Workflow](10-github-issues.md)

## How to use

- Har chapter read karke commands khud terminal mein practice karo.
- Har chapter ka exit gate pass karke hi next chapter par move karo.
- `git status` ko habit banao: branch switch, add, commit, push, pull se pehle/baad check.
- Real API key, password, token ya client data kabhi Git repository mein commit mat karo.
- Fresh project mein bina tutorial same workflow repeat kar pana real proof hai.

## Full Stage 0 capstone

1. Fresh folder mein Git repo initialize karo.
2. README aur `.gitignore` banao; two meaningful commits karo.
3. Feature branch create karo, ek docs/code change commit karke GitHub push karo.
4. PR open karo, diff inspect karo, follow-up commit push karke PR update karo.
5. PR merge karo, local `master` pull karo, safe local/remote branch cleanup karo.
6. GitHub Issue create karke PR description mein `Closes #ID` link test karo.
7. `git status`, `git log --oneline --graph --decorate --all`, aur fresh clone se final repo verify karo.

## Key corrections

- Commit, push, merge aur deployment same cheezein nahi hain.
- `git branch -d` safe deletion hai; `-D` force deletion hai.
- `.gitignore` only untracked files ko affect karta hai; already tracked secret ko untrack + rotate/revoke karna padta hai.
- PR diff green = added lines, red = removed lines.
- Checks automated validation hain; human review aur production deployment alag verification steps hain.

## References

- [Git documentation](https://git-scm.com/docs)
- [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow)
- [GitHub security guidance](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure)
- [VS Code documentation](https://code.visualstudio.com/docs)
- [MIT Missing Semester](https://missing.csail.mit.edu/)
