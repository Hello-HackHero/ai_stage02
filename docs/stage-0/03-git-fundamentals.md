# Chapter 03 — Git Fundamentals: Working Tree → Staging → Commit

> Stage 0 / 10 | Hinglish study chapter | 28 Sep 2026

## Goal

Git ke 3 core states samajhna: working tree, staging area aur local commit. Yeh chapter clear hua toh `git add` aur `git commit` blindly nahi chalaoge.

## Mental model

```text
File edit
  ↓
Working tree      = laptop par current files/changes
  ↓ git add
Staging area      = next commit mein kya jayega, selected snapshot
  ↓ git commit
Local repository  = permanent local history inside .git/
  ↓ git push
Remote repository = GitHub branch
```

**Git** local version-control tool hai. **GitHub** online hosting/collaboration service hai. Commit local hota hai; commit automatic GitHub upload nahi karta. `git push` remote par commits bhejta hai.

## First repository

```bash
mkdir git-practice && cd git-practice
git init
git status
printf '# Git Practice\n' > README.md
git add README.md
git diff --cached
git commit -m "docs: add README"
```

`git init` current folder mein `.git/` metadata banata hai. `.git/` ko manually edit/delete mat karo. `git status` har meaningful step se pehle/baad mein run karo.

## Core commands

```bash
git status                    # state: branch, staged, unstaged, untracked
git diff                      # unstaged changes
git add path/to/file          # selected file stage
git diff --cached             # staged snapshot review
git commit -m "type: message" # local snapshot
git log --oneline             # short local history
git restore --staged file.txt # unstage; working edit remains
git restore file.txt          # discard working edit: destructive
```

## Safe daily workflow

```bash
git status
git diff
git add path/to/file
git diff --cached
git commit -m "feat: add profile field"
git status
```

`git add .` convenient hai but blindly mat chalao—secret, log, large dataset stage ho sakta hai. Specific file stage karo aur staged diff inspect karo.

## Commit messages

Format: `type: clear action`.

- `feat: add login validation`
- `fix: handle missing email`
- `docs: add setup steps`
- `chore: update gitignore`

`changes`, `update`, `final final` jaise messages future mein useless hote hain.

## Common mistakes

- Save kiya file commit nahi hota; `git status` check karo.
- Commit ke baad push missing ho sakta hai; local/remote distinction yaad rakho.
- Wrong files stage hui? `git restore --staged <file>`.
- Working edits permanently discard karne se pehle diff read karo.

## Practice

1. `notes.txt` create karo aur first line add karo.
2. `git status` dekho.
3. File stage karo aur `git diff --cached` dekho.
4. Commit karo.
5. Second line add karo aur `git diff` dekho.
6. `git restore --staged` vs `git restore` ka difference words mein explain karo; destructive restore tabhi use karo jab edit unwanted ho.

## Recall questions

1. Working tree aur staging area mein kya difference hai?
2. `git commit` aur `git push` mein kya difference hai?
3. `git diff` vs `git diff --cached`?
4. `git add .` kab risk create kar sakta hai?
5. `.git/` folder ka role kya hai?

## Exit gate

Fresh folder mein Git init, README create, selective staging, staged diff review aur 2 meaningful commits bina tutorial karo. Har state ko apne words mein explain kar sako toh Chapter 04 ready.

**Reference:** [Pro Git — Getting Started](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)
