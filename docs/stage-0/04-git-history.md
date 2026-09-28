# Chapter 04 — Git Commit History and Inspection

> Stage 0 / 10 | Hinglish study chapter | 28 Sep 2026

## Goal

Git history ko read karna, exact change inspect karna, branch/commit state confirm karna, aur troubleshooting start karna.

## Why history matters

Git commit history sirf backup nahi hai. Isse tum dekh sakte ho: kya change hua, kab hua, kis branch par hua, aur kab bug introduce hua. Clear commits future-you aur teammates dono ko help karte hain.

## Core commands

```bash
git status -sb
git log --oneline --decorate -10
git log --oneline --graph --decorate --all
git show HEAD
git show <commit-sha>
git diff
git diff --cached
git diff HEAD~1 HEAD
```

- `HEAD` usually current checked-out commit ko refer karta hai.
- `git log --oneline` short commit list dikhata hai.
- `--decorate` branch/tag names dikhata hai.
- `--graph --all` parallel branches ko visualize karta hai.
- `git show HEAD` latest commit ka diff aur metadata dikhata hai.

## Read history safely

```bash
git log --oneline --graph --decorate --all
git show --stat HEAD
git show HEAD -- README.md
```

Pehle history dekho, phir exact commit/file inspect karo. SHA ka short prefix usually command mein enough hota hai, but copied SHA verify karo.

## Useful state checks

```bash
git branch --show-current
git branch -vv
git remote -v
git status
```

`git branch -vv` local branch ka upstream tracking dikhata hai. Isse pata chalta hai `git push`/`git pull` kis remote branch ke saath linked hain.

## Common mistakes

- `git log` dekhkar assume karna ki GitHub bhi updated hai: local commits aur remote commits alag ho sakte hain.
- Long history mein lost feel ho: `git log --oneline -20` use karo.
- `git reset`, `rebase`, `revert` ko without purpose use mat karo; yeh chapter inspection ke liye hai, history rewrite ke liye nahi.

## Practice

1. Do commits banao: README add aur notes update.
2. `git log --oneline --decorate -5` se list dekho.
3. Last commit ka `git show HEAD` dekho.
4. Older commit ka short SHA lekar `git show <sha>` karo.
5. `git status -sb` se clean/dirty state explain karo.

## Recall questions

1. `HEAD` kya indicate karta hai?
2. `git show` aur `git log` mein difference?
3. `git status -sb` se kya quick information milti hai?
4. Local history se remote sync ka guarantee kyun nahi milta?

## Exit gate

Kisi repository ke last 3 commits, current branch, staged/unstaged changes aur ek commit ka exact diff bina tutorial inspect kar sako toh Chapter 05 ready.

**Reference:** [Git log documentation](https://git-scm.com/docs/git-log) · [Git show documentation](https://git-scm.com/docs/git-show)
