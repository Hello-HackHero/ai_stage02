# Chapter 07 — Remote Repositories (origin, push, pull, clone)

> Stage 0 / 10 | Hinglish study chapter | Git remotes, sync | 28 Sep 2026

## Goal

Local aur remote (GitHub) ke beech sync ko samajhna; `origin`, `push`, `pull`, `clone` ka sahi use.

## 1. Remote basics

```bash
git remote -v                   # remote URLs inspect
git remote add origin <URL>     # sirf jab origin absent ho
git push -u origin master       # first push; upstream set
git clone <URL>                 # existing repo copy
git fetch origin                # remote refs update; files merge nahi
git pull                        # fetch + integrate current branch
```

`origin` remote ka naam hai, branch nahi. `-u` upstream tracking set karta hai.

## 2. Common mistakes

- Wrong remote URL: `git remote -v` verify karo.
- `git pull` galat branch par: `git branch --show-current` check karo.
- Force push bina reason: `--force` se overwrite mat karo.

## 3. Mini exercise

- Local repo par `origin` add karo, ek branch push karo.
- Doosre folder mein `clone` karke sync verify karo.

## 4. Exit gate

Bina notes: `git remote -v`, `git push -u origin <branch>`, `git clone`, `git pull` commands explain karo aur safe use cases batao.

**References:** [Git Remote](https://git-scm.com/docs/git-remote) · [GitHub: Cloning a Repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
