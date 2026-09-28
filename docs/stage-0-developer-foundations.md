# Stage 0 — Developer Setup, Terminal, Git & GitHub

> Hinglish reference / cheat sheet | Based on my Stage 0 NotebookLM practice and AI Systems Engineer roadmap | Updated: 28 Sep 2026

## Contents
1. Goal and mental model
2. Setup, terminal and VS Code
3. Git local workflow and history
4. Branches, merge and conflicts
5. Remote GitHub and pull requests
6. `.gitignore`, secrets and large files
7. GitHub Issues and collaboration
8. Ready-to-use command cheat sheet
9. Troubleshooting and corrections
10. Practice gate and next step

## 1. Goal and mental model

Stage 0 ka goal tools ko blindly memorize karna nahi, balki ek project ko locally edit → safely version → GitHub par publish → branch/PR se review → merge → local sync kar pana hai.

**Git vs GitHub:** Git local version-control system hai. GitHub online hosting/collaboration platform hai. `git init` local repository banata hai; `git push` remote repository update karta hai. Commit ≠ push; push ≠ merge; PR ≠ deployment.

**Four locations:** Working tree (actual files) → staging area/index (next commit ke liye selected changes) → local commit/history (`.git`) → remote branch (`origin` on GitHub). `git add` stage karta hai; `git commit` local snapshot banata hai; `git push` selected local branch ke commits remote branch ko bhejta hai.

**Branch analogy:** `master` is repo ka default branch; har repo mein default branch ka naam `main` ya kuch aur bhi ho sakta hai. `feature-profile` ek independent branch hai. `git push -u origin feature-profile` sirf remote `feature-profile` update karta hai; `master` ko nahi. PR merge ke baad master change hota hai. GitHub par merged hona aur live app deploy hona alag cheezein hain.

**Repository anatomy:** README = project ka entry page; `.gitignore` = untracked files ke patterns; `.git/` = Git metadata (edit mat karo); issue = tracked task; PR = branch changes ko discuss/review/merge karne ka proposal; Actions/workflows = configured automation (automatically exist nahi karte).

## 2. Setup, terminal and VS Code

Stage 0 roadmap: terminal and file navigation, PATH/permissions basics, VS Code editor/terminal/debugger, Git/GitHub, Python environment, simple README and weekly log. Docker/Postgres/Node ko sirf jab actual next project maange tab install/configure karo; tool setup par poora hafta mat kharch karo.

### Mac/zsh terminal basics

```bash
pwd                    # current directory
ls -la                 # hidden files + details
cd path/to/project     # folder ke andar
cd ..                  # parent folder
mkdir -p docs          # folder banao
touch notes.md         # empty file banao
cat notes.md           # file padho
printf 'hello\n' > notes.md   # overwrite; >> append karta hai
open .                 # current folder Finder mein (macOS)
which python3          # executable ka path
python3 --version      # Python version
```

`~` = home; `.` = current folder; `..` = parent; `/` = path separator. Spaces wale path quote karo: `cd "My Projects"`. Terminal ka current directory aur repository root same hon, yeh check karne ke liye `pwd` aur `git rev-parse --show-toplevel` use karo. `rm` irreversible ho sakta hai: copy/paste karne se pehle path check karo. PATH woh directories hain jahan shell commands dhoondta hai; `command not found` aksar installation ya PATH issue hota hai. macOS aur Linux ke kuch commands/flags alag hote hain.

### VS Code basics

Folder ko `code .` se kholo (agar shell command installed hai), built-in terminal use karo, files search karo, Source Control panel mein staged/unstaged diff dekho, breakpoints laga kar debugger run karo, aur formatter/extension sirf need par install karo. Formatters code layout badalte hain; debugger variable values aur execution flow dikhata hai. Save kiya file ≠ committed file: `git status` verify karo.

### First-time Git identity

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git config --global --list
```

Commit author email credentials/authentication se alag hai. Apna real password Git remote URL, code, issue ya screenshot mein mat dalo. HTTPS par credential manager/token ya SSH keys use karo; GitHub account password se Git push generally nahi hota.

### Python environment (Stage 1 ke liye bridge)

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip --version
deactivate
```

`.venv/` ko Git se ignore karo; dependency manifest (`requirements.txt` ya `pyproject.toml`) ko commit karo. `python3`/`python` command environment ke hisab se differ kar sakte hain. VS Code interpreter ko isi venv par select karo.

## 3. Local Git workflow and history

### New repository

```bash
mkdir demo && cd demo
git init
git status
printf '# Demo\n' > README.md
git add README.md
git diff --cached
git commit -m "docs: add project README"
git log --oneline --decorate -5
```

`git status`: current branch, unstaged/staged/untracked state. `git diff`: unstaged edits. `git diff --cached` or `git diff --staged`: staged changes. `git log --oneline --graph --decorate --all`: short history and branch layout. `git show HEAD`: last commit details. `HEAD` usually current checked-out commit ko refer karta hai. Commit messages action-oriented rakho: `docs: add Stage 0 cheat sheet`, not `changes`.

### Existing changes ka safe cycle

```bash
git status
git diff
git add path/to/file       # selected file; blindly git add . mat chalao
git diff --cached
git commit -m "feat: add profile field"
git status
git log -1 --oneline
```

`git add .` galti se secrets/big files stage kar sakta hai. Stage karne se pehle `git status` aur `git diff --cached` dekho. Stage se file hatao, working edits bachao: `git restore --staged path/to/file`. Working edits discard: `git restore path/to/file` — **destructive**, sirf tab jab change sach mein nahi chahiye. `git stash` temporary work save karta hai, regular commits ka replacement nahi.

## 4. Branches, merge and conflicts

```bash
git branch                         # local branches; * current
git branch -a                      # local + remote-tracking branches
git switch -c feature-profile      # new branch banao aur switch karo
git switch master                  # existing branch par switch
git merge feature-profile          # current branch mein feature branch merge
git branch -d feature-profile      # merged local branch safely delete
git branch -D feature-profile      # FORCE delete: unmerged work lose ho sakta hai
```

Older equivalent: `git checkout -b feature-profile`; `git checkout master`. `git switch` branch selection ke liye clearer hai. Branch switch se pehle `git status` check karo; uncommitted edits carry ho sakte hain ya switching block ho sakti hai.

### Local-only merge

```bash
git switch master
git merge feature-profile
git status
```

Yeh laptop par merge hai; GitHub PR workflow alag. Merge conflict tab aata hai jab Git ko changes automatically combine nahi hote. Conflict markers `<<<<<<<`, `=======`, `>>>>>>>` mein correct final content khud choose/edit karo, markers remove karo, test karo, `git add <file>` aur `git commit` (ya suggested `git merge --continue`) chalao. Merge cancel karna ho aur merge in progress ho: `git merge --abort`. `ours/theirs` bina context samjhe mat select karo.

## 5. GitHub remote, PR and local sync

### Remote basics

```bash
git remote -v                   # remote URL inspect
git remote add origin <REPO_URL> # sirf jab origin absent ho
git push -u origin master        # local master -> remote master, first push
git clone <REPO_URL>             # existing repository local copy
git fetch origin                # remote refs update; current files merge nahi
git pull                        # fetch + integrate current branch upstream
```

`origin` remote ka conventional naam hai, branch nahi. `-u` upstream tracking set karta hai, jiske baad current branch par `git push`/`git pull` usually enough hote hain. `git remote -v`, `git branch -vv`, `git status` se destination verify karo. `git pull` before work tab karo jab branch clean aur upstream correct ho; conflict aaye toh manually resolve karo.

### Team-style PR cycle (is repo mein base branch `master` hai)

```bash
git switch master
git pull origin master
git switch -c docs/stage-0-notes
# file edit karo
git status
git add docs/stage-0-developer-foundations.md
git diff --cached
git commit -m "docs: add Stage 0 notes"
git push -u origin docs/stage-0-notes
```

GitHub par base = `master`, compare = `docs/stage-0-notes` choose karke PR kholo. PR mein kya/kyun/tested kya likho, diff check karo, review comments aur configured checks dekho. Same branch par naya commit + `git push` existing PR ko update karta hai. Merge ke baad:

```bash
git switch master
git pull origin master
ls docs
# agar branch merge ho chuki aur local work saved hai:
git branch -d docs/stage-0-notes
# remote branch GitHub ke Delete branch button se clean kar sakte ho
```

`git push origin docs/stage-0-notes` master update nahi karta. `git merge feature-profile` local branches combine karta hai; GitHub UI par merge ke baad local master update karne ke liye `git switch master` + `git pull origin master` use karo. PR green diff lines added aur red lines removed hoti hain, green = pull/red = reject nahi. Review comments humans likhte hain; automated status checks alag cheez hain. Checks sirf tab run karte hain jab Actions/CI ya external integration configure ho; green checks guarantee nahi dete ki app bug-free ya deploy ho gayi. Solo repo mein direct push technically possible hai; team projects mein PR history/review valuable hota hai.

## 6. `.gitignore`, secrets and large files

`.gitignore` plain-text **file** hai, folder nahi. Usmein names/patterns likhte hain; ignored file ko uske andar move nahi karte. Is file ko khud commit karna normal hai, isliye public repo mein ignore patterns sab dekh sakte hain. Git ignore rules sirf intentionally untracked files par apply hote hain; already tracked file automatically untrack nahi hoti.

### Example `.gitignore` for Python + macOS

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

`.env.example` mein fake placeholders rakho, real API keys nahi. `data/*.csv` sirf specified matching paths ko ignore karta hai; apne dataset layout ke hisab se pattern edit karo. `*.log` + `!important.log` exception possible hai agar parent directory ignored nahi hai. **Important:** `logs/` ignore karke sirf `!logs/important.log` likhne se file automatically wapas track nahi hoti; ignored parent directory ko bhi unignore karna padega, ya `logs/*` pattern use karke exception do:

```gitignore
logs/*
!logs/important.log
```

`git check-ignore -v logs/important.log` se matching rule inspect karo; `git status --ignored` se ignored paths dekho.

### File pehle se tracked hai?

```bash
printf '.env\n' >> .gitignore
git rm --cached .env     # local file rakhta hai, index se remove karta hai
git add .gitignore
git status
git commit -m "chore: stop tracking local environment"
```

Agar `.env` ya API token kabhi commit/push hua hai, sirf `.gitignore` aur `git rm --cached` enough **nahi**: old Git history mein secret reh sakta hai. Turant provider par secret **revoke/rotate** karo; phir need ho toh GitHub ke sensitive-data-removal guide ke according history cleanup plan karo. History rewrite/force push bina backup/team coordination ke mat karo. `.gitignore` privacy/security boundary nahi: secret ko first place mein repo mein mat rakho; hosting secrets/CI secret store mein rakho. Ignore pattern ko bypass karke explicit force-add (`git add -f`) possible hai, isliye commit se pehle review zaroori hai.

Large dataset (e.g. 10 GB) ko normal Git repo mein commit na karo; `.gitignore` mein filename/pattern add karo, authorized storage par rakho, README mein acquisition instructions do. Git LFS sirf tab evaluate karo jab versioned binaries ki actual zaroorat aur storage/bandwidth budget clear ho. Kisi private user dataset ko public GitHub par publish mat karo.

## 7. GitHub Issues and collaboration

Issue = bug/feature/documentation task with title, reproducible details, checklist, labels, assignee and comments. Issue and PR numbers repository mein shared sequence se aate hain; first issue `#2` ho sakta hai agar PR `#1` tha. Closed issue deleted nahi hota, discussion dekh sakte ho; it can also be reopened where permitted. Issue ka label sirf category hai; assignee responsibility batata hai; `@username` mention relevant person ko notify kar sakta hai. Open source mein kaam start se pehle contribution guide, existing issue/PR aur maintainer expectations check karo; assignment har project mein mandatory nahi hota.

### Good issue example

```md
Title: Docs: add Stage 0 Git cheat sheet
Problem: Branch push vs master merge confusion.
Done when:
- [ ] Explain working tree, stage, commit, remote
- [ ] Show PR and local-sync commands
- [ ] Add `.gitignore` and secret-leak warning
```

PR description mein `Closes #2` ya `Fixes #2` likhne se linked issue usually PR default branch mein merge hone par auto-close hota hai; cross-repo issue ke liye owner/repo reference chahiye. Sirf issue number mention karna link kar sakta hai, auto-close ke liye recognized keyword use karo. `is:open` / `is:closed` se issues filter karo. Issue #2 ko sach mein close karna ho to existing issue ki actual state aur content pehle check karo; assume mat karo.

## 8. Ready-to-use command cheat sheet

| Kaam | Command | Dhyan rahe |
| --- | --- | --- |
| Kahan ho? | `pwd`; `git rev-parse --show-toplevel` | terminal vs repo root |
| Files dekho | `ls -la` | dotfiles included |
| Git state | `git status -sb` | branch + changed files |
| Unstaged diff | `git diff` | add se pehle |
| Staged diff | `git diff --cached` | commit se pehle |
| File stage | `git add path/to/file` | deliberate selection |
| Unstage file | `git restore --staged path/to/file` | edit bachti hai |
| Local commit | `git commit -m "docs: clarify PR"` | push nahi hota |
| History | `git log --oneline --graph --decorate --all` | branch graph |
| New branch | `git switch -c feature-name` | current commit se |
| Branch switch | `git switch master` | unsaved work check |
| Remote check | `git remote -v` | owner/destination verify |
| First push | `git push -u origin feature-name` | feature branch only |
| Sync remote refs | `git fetch origin` | no automatic merge |
| Update current branch | `git pull origin master` | master par hote hue |
| Safe branch delete | `git branch -d feature-name` | merged work only |
| Ignore rule inspect | `git check-ignore -v path/to/file` | why ignored |
| Stop tracking file | `git rm --cached path/to/file` | old history remains |

## 9. Troubleshooting and NotebookLM corrections

- **"Everything up-to-date" after push?** `git status -sb`, `git branch -vv`, `git remote -v`; shayad wrong branch, no new commit, ya wrong remote.
- **`src refspec master does not match any`?** Check `git branch --show-current` and whether first commit exists; default branch `main` bhi ho sakti hai.
- **`remote origin already exists`?** Naya remote blindly add mat karo; `git remote -v` dekho, zarurat ho toh `git remote set-url origin <correct-url>` carefully.
- **Push rejected (non-fast-forward)?** Remote par naye commits hain; `git fetch`, `git status`, appropriate branch par `git pull`, conflicts resolve, then push. `--force` se casually overwrite mat karo.
- **Authentication failed?** Correct account/repo permission aur HTTPS credentials/SSH setup check karo; token/password kabhi share mat karo.
- **File `.gitignore` ke baad bhi track ho rahi hai?** `git ls-files -- <path>` check karo; tracked ho toh `git rm --cached <path>`. Public secret hua ho toh key rotate karo.
- **PR checks green but app broken?** Automated checks configured tests tak limited hain. Human review, manual testing and deployment verification alag hain.
- **Prior quiz ne `git branch -D` ko perfect kaha tha:** merged branch ke liye `-d` safer; `-D` force delete hai.
- **Prior lesson ne `logs/` + `!logs/important.log` suggest kiya tha:** ignored parent ke andar exception directly work nahi karega; `logs/*` + `!logs/important.log` use karo.
- **Prior lesson ne `.env` ignored hone par 100% safe kaha tha:** only if secret kabhi tracked/pushed nahi hua, aur doosre channels se leak nahi hua. Leaked key revoke/rotate karo.
- **Prior lesson ne PR merge ko live kaha tha:** GitHub branch mein merged ≠ production deploy. Deployment pipeline alag verify karo.
- **NotebookLM ke reported 92%/100% score:** learning-session assessment hai, production-grade proficiency ka proof nahi; fresh-folder practical gate khud pass karo.

## 10. Stage 0 practical gate and next step

**45–60 minute no-tutorial capstone:**

- [ ] Fresh folder mein `git init`, README, `.gitignore`, two meaningful commits.
- [ ] Working tree, staging, local commit, remote ko apne words mein explain karo.
- [ ] Feature branch par change karo, remote push karo, PR diff read karo.
- [ ] PR ke same branch par correction push karo, merge karo, local `master` sync karo.
- [ ] Issue create karo aur issue-PR link demonstrate karo; auto-close blindly assume mat karo.
- [ ] Ignored `.env` verify karo; tracked file case explain karo; real secrets kabhi test mein mat dalo.
- [ ] `git status`, `git log` aur fresh clone se final files verify karo.

**My practice record (NotebookLM transcript; actual repo state can change):** `ai_stage02`, base `master`, `feature-profile` push/PR merge/local sync, GitHub Issue `#2`, `.gitignore` lesson, ten concepts completed. Transcript ko memory aid samjho; current GitHub state ko verify karo. Roadmap versions different hain: detailed version Stage 1 = web foundations; final merged career book Stage 1 = Python engineering. Apne current chosen roadmap ka gate select karke wahi follow karo, dono ko simultaneously mix mat karo.

**Next habit:** Har naye project ke README mein problem, setup, run/test commands, limitations, and one honest screenshot/demo add karo. Har week ek chhota concept → exercise → project change → commit → 2-minute explanation. Copy-paste fluency nahi; bina tutorial fresh repo aur PR bana paana actual Stage 0 proof hai.

### Official references

- [Git documentation](https://git-scm.com/docs)
- [Git ignore patterns](https://git-scm.com/docs/gitignore)
- [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow)
- [Linking PRs to issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue)
- [Removing sensitive data](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [VS Code documentation](https://code.visualstudio.com/docs)
