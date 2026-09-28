# Chapter 05 — Branching and Merging

> Stage 0 / 10 | Hinglish study chapter | Git branches, merge, conflicts | 28 Sep 2026

## Goal

Branches ko parallel timeline samajhna, safe branching workflow, aur local merge ka basic flow.

## 1. Branch kya hai?

Branch = commits ki ek independent line. `master` default branch hoti hai (ya `main`). Nayi branch current commit se start hoti hai; uspar naye commits `master` ko affect nahi karte jab tak merge na ho.

## 2. Core commands

```bash
git branch                 # local branches; * current
git branch -a              # local + remote-tracking
git switch -c feature-x    # new branch + switch
git switch master          # existing branch par switch
git merge feature-x        # current branch mein feature merge
git branch -d feature-x    # merged branch delete
git branch -D feature-x    # force delete (unmerged work lose ho sakta)
```

Older: `git checkout -b feature-x`; `git checkout master`. `git switch` clearer hai.

## 3. Safe branching workflow

1. `git status` — clean working tree?
2. `git switch master`
3. `git pull` (agar remote sync chahiye)
4. `git switch -c feature-x`
5. Edits → `git add` → `git commit`
6. `git switch master`
7. `git merge feature-x`

Branch switch se pehle `git status` check karo; uncommitted edits carry ho sakte hain.

## 4. Common mistakes

- Galat branch par commit: `git log --oneline --decorate -3` se verify karo.
- `-D` blindly use: pehle `git branch --merged` dekho.
- Merge se pehle tests/formatting skip karna.

## 5. Mini exercise

- `feature-login` branch banao, ek file add karo, commit karo.
- `master` par wapas aakar merge karo, phir branch delete karo.

## 6. Exit gate

Bina notes: new branch banao, commit karo, `master` par merge karo, branch delete karo, aur har step par `git branch`/`git log` se state verify karo.

**References:** [Git Branching](https://git-scm.com/book/en/v2/Git-Branching) · [Atlassian: Merging vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
