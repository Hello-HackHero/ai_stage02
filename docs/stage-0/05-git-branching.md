# Chapter 05 — Branching and Merging

> Stage 0 / 10 | Hinglish study chapter | Git branches | 28 Sep 2026

## Goal

Branch kyun hota hai, local branching workflow, aur safe merge patterns ko samajhna.

## 1. Branch mental model

Branch = pointer to a commit. `master`/`main` default branch hota hai. Nayi branch se tum parallel line of work banate ho bina main code ko touch kiye.

- `git branch` — local branches list; `*` current branch.
- `git branch -a` — local + remote-tracking branches.
- `git switch -c feature-login` — new branch banao aur switch karo.
- `git switch master` — existing branch par switch.

Older equivalent: `git checkout -b feature-login`; `git checkout master`.

## 2. Safe branching workflow

```bash
git switch master
git pull origin master      # upstream se fresh
git switch -c feature-login # new branch
# edit files
git status
git add .
git commit -m "feat: add login form"
git switch master
git merge feature-login     # local merge
```

`git merge` current branch mein specified branch ke commits combine karta hai. Fast-forward merge tab hota hai jab target branch sirf aage badha hai; three-way merge tab jab dono branches par alag changes hain.

## 3. Common mistakes

- Bina `git status` branch switch karna: uncommitted changes carry ho sakte hain.
- `git checkout -b` se pehle current branch check nahi karna.
- Merge se pehle test na karna.

## 4. Exit gate

Fresh folder: `master` par do commits, `feature-x` par ek commit, `master` par wapas aakar merge, `git log --oneline --graph` se history dekho. Agar tum fast-forward vs three-way merge explain kar sakte ho, toh Chapter 06 ke liye ready ho.

**Reference:** [Git branching docs](https://git-scm.com/docs/git-branch)
