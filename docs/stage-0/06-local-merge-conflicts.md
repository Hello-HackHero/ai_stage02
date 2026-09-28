# Chapter 06 — Local Merge and Conflicts

> Stage 0 / 10 | Hinglish study chapter | Merge conflicts, resolution | 28 Sep 2026

## Goal

Merge conflict ko normal samajhna, markers ko manually fix karna, aur safe abort/continue commands.

## 1. Merge conflict kyun aata hai?

Jab Git do branches ke same lines ko automatically combine nahi kar pata, conflict markers dalta hai:

```text
<<<<<<< HEAD
old content from current branch
=======
new content from merging branch
>>>>>>> feature-x
```

## 2. Resolution steps

1. Conflicted file kholo, markers hata kar final content decide karo.
2. Test karo (agar applicable).
3. `git add <file>`
4. `git merge --continue` (ya `git commit` purane Git mein).

Abort: `git merge --abort`.

## 3. Safety rules

- Markers kabhi commit mat karo.
- `ours/theirs` bina context samjhe mat use karo.
- Conflict ke baad tests/formatting zaroor run karo.

## 4. Mini exercise

- Do branches mein same file ki same line alag-alag edit karo.
- Merge karo, conflict resolve karo, commit karo.

## 5. Exit gate

Bina notes: ek conflict create karo, resolve karo, `git status` se verify karo ki working tree clean hai.

**References:** [Git Merge](https://git-scm.com/docs/git-merge) · [Atlassian: Resolving Conflicts](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
