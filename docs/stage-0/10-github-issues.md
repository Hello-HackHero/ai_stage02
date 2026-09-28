# Chapter 10 — GitHub Issues and Open-Source Workflow

> Stage 0 / 10 | Hinglish study chapter | 28 Sep 2026

## Goal

GitHub Issues se bugs/features/docs tasks track karna, PR ko issue se link karna, aur maintainer/contributor workflow samajhna.

## Issue kya hai?

GitHub Issue ek trackable work item hai: bug report, feature request, documentation task, question, ya planned improvement. Har issue ka unique number hota hai, jaise `#2`. PR aur issue numbering repository mein shared sequence se aa sakti hai; isliye first issue `#2` ho sakta hai if PR `#1` already tha.

## Strong issue format

```md
Title: Docs: add Stage 0 Git cheat sheet

Problem
New learners confuse feature-branch push with master merge.

Done when
- [ ] Explain working tree, staging, commit, remote
- [ ] Show PR + local sync commands
- [ ] Add secret leak warning
```

Good issue mein clear problem, expected outcome, reproduction steps (bug ke liye), acceptance checklist aur relevant screenshots/logs hote hain. Real secrets/private user data paste mat karo.

## Terms

- **Assignee:** task par currently responsible person.
- **Labels:** categories, e.g. `bug`, `enhancement`, `documentation`, `good first issue`.
- **Milestone/project:** planning/grouping context.
- **@mention:** `@username` relevant person ko notify kar sakta hai.
- **Open/closed:** pending vs resolved/not proceeding state. Closed issue delete nahi hota; history/reference saved rehti hai and it may be reopened.

## Linking PR and issue

PR description mein recognized keyword use karo:

```md
Closes #2
```

`Fixes #2` and `Resolves #2` bhi common keywords hain. Linked PR default branch mein merge hone par issue auto-close ho sakta hai. Sirf `#2` mention link bana sakta hai, but auto-close ke liye recognized closing keyword chahiye. Cross-repository issue ke liye owner/repo reference required ho sakta hai.

## Open-source etiquette

1. `README`, `CONTRIBUTING.md`, Code of Conduct aur issue/PR templates padho.
2. Existing issue/PR search karo—duplicate work mat karo.
3. Comment karke intent share karo; assignment project-specific hai, universal rule nahi.
4. Small scoped contribution banao, tests/docs follow karo, respectful PR submit karo.
5. Maintainer final merge decision leta hai; contributor changes propose karta hai.

## Filters

- `is:open` = currently open issues
- `is:closed` = closed history
- `label:bug` = bug label
- `assignee:USERNAME` = particular person

## Practice

Apne repo mein issue create karo: `Docs: improve Stage 0 notes`. Description mein one problem aur 3 done criteria likho. Feature branch/PR bana kar description mein `Closes #<issue-number>` add karo, then merge behavior observe karo.

## Exit gate

Clear issue create kar sako, assignee/label explain kar sako, `Closes #ID` ka effect bata sako, aur maintainer vs contributor difference explain kar sako.

**References:** [GitHub Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues) · [Linking PRs to issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue)
