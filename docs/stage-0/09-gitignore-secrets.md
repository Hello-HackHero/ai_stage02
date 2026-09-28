# Chapter 09 — `.gitignore`, Secrets and Large Files

> Stage 0 / 10 | Hinglish study chapter | 28 Sep 2026

## Goal

Sensitive, generated aur large files ko safe tarike se Git history se bahar rakhna; tracked secret ke real remediation steps samajhna.

## `.gitignore` kya hai?

`.gitignore` ek plain-text **file** hai, folder nahi. Ismein patterns likhte hain taaki Git intentionally untracked matching files/folders ko ignore kare. File ko `.gitignore` ke andar move nahi karte. `.gitignore` ko commit karna normal hai; public repo mein ignore patterns visible hote hain.

## Safe starter `.gitignore`

```gitignore
.env
.env.*
!.env.example
.venv/
venv/
__pycache__/
*.py[cod]
.pytest_cache/
.DS_Store
*.log
data/*.csv
```

`.env.example` mein only placeholders rakho, real API key/password nahi.

## Patterns

- `secrets.txt` = one file
- `venv/` = folder
- `*.log` = any `.log` file
- `data/*.csv` = data folder CSVs
- `!important.log` = previous ignore rule ka exception, parent directory ignored na ho tab

Agar `logs/` poora ignored hai, `!logs/important.log` directly enough nahi ho sakta because Git ignored parent directory descend nahi karta. Better:

```gitignore
logs/*
!logs/important.log
```

## Verify ignore rules

```bash
git status --ignored
git check-ignore -v path/to/file
```

`git check-ignore -v` matching ignore file aur rule dikha sakta hai.

## Already tracked file

`.gitignore` tracked file ko automatically untrack nahi karta.

```bash
printf '.env\n' >> .gitignore
git rm --cached .env
git add .gitignore
git commit -m "chore: stop tracking local environment"
```

`git rm --cached` local `.env` ko delete nahi karta; index se remove karta hai.

## If a real secret was committed/pushed

`.gitignore` add karna enough nahi. Old commit history mein key reh sakti hai. Immediately provider dashboard par secret **revoke/rotate** karo. Then GitHub sensitive-data removal guidance follow karo if history cleanup necessary ho. History rewrite/force-push bina backup/team coordination ke mat karo. GitHub public repositories aur leaked credentials ko assume compromised treat karo.

## Large files

10 GB dataset normal Git repository mein commit mat karo. Pattern `.gitignore` mein add karo, authorized storage use karo, README mein retrieval steps do. Git LFS only jab binary versioning ka actual requirement aur quota/billing clear ho. Private user/client data public GitHub par kabhi upload mat karo.

## Common mistakes

- `.gitignore` ko folder samajhna.
- Real `.env` ko sample file samajhkar commit karna.
- Tracked secret ko ignore karne ke baad rotate na karna.
- `git add .` se keys/logs/large files accidentally stage karna.

## Practice

Safe fake file use karo, real password/API key nahi:

```bash
printf 'fake-value-for-practice\n' > secrets.txt
printf 'secrets.txt\n' >> .gitignore
git status
git check-ignore -v secrets.txt
```

## Exit gate

File, folder, wildcard aur exception pattern likh sako; tracked vs untracked distinction explain kar sako; real leaked token ke first action ko **rotate/revoke** bolo.

**References:** [gitignore docs](https://git-scm.com/docs/gitignore) · [GitHub: removing sensitive data](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
