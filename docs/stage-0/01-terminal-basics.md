# Chapter 01 — Terminal Basics and Navigation

> Stage 0 / 10 | Hinglish study chapter | Mac Terminal (zsh) examples | 28 Sep 2026

**Is chapter ka goal:** Bina VS Code/Finder ke terminal mein project folder find karna, files dekhna/banana/padhna, paths samajhna, aur dangerous commands se bachna. Git commands se pehle yeh foundation aani chahiye.

## 1. Terminal actually kya hai?

Terminal ek text-based interface hai: tum command type karte ho, shell (macOS par usually `zsh`) usse interpret karke program run karta hai, aur output/error dikhata hai. Terminal koi alag cloud nahi: commands tumhare laptop ke files aur processes par kaam karti hain. Prompt par laptop/user/folder ka naam aa sakta hai; woh command ka hissa nahi hota.

**Current working directory (CWD)** = tum abhi kis folder ke andar ho. Relative commands isi location se resolve hoti hain. Kisi command ka result unexpected ho toh sabse pehle `pwd` chalao.

## 2. Mental model: folder tree and paths

```text
/Users/yourname/                  ← home (~)
└── projects/
    └── ai_stage02/              ← repository folder
        ├── README.md
        ├── login.py
        └── docs/
```

- `pwd` current folder ka full path print karta hai.
- `~` tumhara home folder; `cd ~` home jaata hai.
- `.` current folder; `..` parent folder; `/` path separator.
- Absolute path `/Users/yourname/projects/ai_stage02` root `/` se start hota hai; relative path `projects/ai_stage02` current location se.
- `README.md` aur `readme.md` same maan kar mat chalo; case sensitivity disk/configuration par depend karti hai.
- Spaces ko quote karo: `cd "My Projects"`; warna shell path ko alag arguments samajh sakta hai.
- Dotfiles (`.gitignore`, `.env`) normal `ls` mein hidden ho sakti hain; `ls -la` se dekho.

## 3. Daily command cheat sheet

| Kaam | Command | Yaad rakho |
| --- | --- | --- |
| Current location | `pwd` | edit/delete se pehle check |
| Visible files | `ls` | hidden files nahi dikhengi |
| Details + hidden files | `ls -la` | permissions aur dotfiles |
| Folder change | `cd foldername` | existing folder hona chahiye |
| Parent folder | `cd ..` | one level up |
| Home folder | `cd ~` | Mac user home |
| New folder | `mkdir -p practice/notes` | `-p` missing parents bhi banata hai |
| Empty file | `touch practice/notes/day-1.md` | existing file ke content ko replace nahi karta |
| File read | `cat README.md` | long files ke liye `less README.md` |
| File first lines | `head -n 10 README.md` | first ten lines |
| File last lines | `tail -n 10 README.md` | last ten lines |
| Print text | `printf 'hello\n'` | predictable newline |
| Current folder in Finder | `open .` | macOS-specific |
| Command location | `command -v git` | PATH/debugging |
| Clear screen | `clear` | files delete nahi hote |
| Help | `git --help`; `man ls` | quit manual with `q` |

Terminal flags ka exact behavior OS par differ kar sakta hai. `ls -la` mein `l` detailed listing, `a` hidden entries hai. `cat` ko terminal output ke liye use karo; binary ya bahut large file par avoid karo.

## 4. One practical exercise, step by step

Safe temporary practice folder banao. Apna home path assume mat karo:

```bash
cd ~
mkdir -p terminal-practice/notes
cd terminal-practice
pwd
ls -la
touch notes/day-1.md
printf 'Aaj terminal practice ki.\n' > notes/day-1.md
cat notes/day-1.md
ls -la notes
cd notes
pwd
cd ..
pwd
```

Expected behavior: `day-1.md` file `notes` ke andar hogi, `cat` ek line dikhayega, aur last `pwd` `terminal-practice` par return karega. Commands chalane se pehle predict karo: kis command ke baad tum kis folder mein hoge?

**Important:** `>` file content replace karta hai; `>>` existing file ke end mein add karta hai. Check:

```bash
printf 'Second line.\n' >> notes/day-1.md
cat notes/day-1.md
```

## 5. PATH, permissions and errors

Shell command ka executable PATH mein listed folders mein dhoondta hai. `command -v python3` ya `command -v git` path batata hai. `command not found` ka matlab command absent ho sakti hai, PATH galat ho sakta hai, ya spelling mistake ho sakti hai; bina diagnose kiye random installer mat run karo.

`ls -l` mein permission bits (`r` read, `w` write, `x` execute) dikh sakte hain. `Permission denied` aane par `sudo` blindly mat chalao: pehle `pwd`, `ls -l <file>`, aur command ka target check karo. `sudo` admin privileges deta hai aur galat path ko nuksan pahucha sakta hai.

Shell special characters: space arguments split karta hai; `*` glob hai (matching file names); `>` output redirect/overwrite; `>>` append; `|` ek command ka output doosre ko deta hai. Characters ka effect samjhe bina destructive command paste mat karo.

## 6. Safety rules and common mistakes

- Prompt ko command mein paste mat karo. Sirf `pwd`, `ls` jaise actual command type karo.
- `cd` fail hua ho toh aage file banane se pehle `pwd` check karo; galat folder mein files create ho sakti hain.
- `rm` delete karta hai; Trash mein jaane ki guarantee nahi. `rm -rf` kabhi bina path inspect kiye run mat karo.
- `.env` jaisi hidden files `ls -la` se dikh sakti hain; hidden ka matlab secret/safe nahi.
- Existing file par `>` accidental overwrite kar sakta hai; pehle `cat`/`ls` se check karo.
- Spaces wale path ko quotes do; beginner ke liye simple folder names convenient hain.
- NotebookLM transcript ka terminal practice summary tumhare skill ka record hai, terminal command behavior ka proof fresh practice se aata hai.

## 7. Quick recall quiz (notes band karke)

1. `pwd` aur `ls` mein kya fark hai?
2. `cd ..` aur `cd ~` tumhe kahan le jaate hain?
3. `.gitignore` dekhne ke liye `ls` ki jagah kya use karoge?
4. `printf 'hi\n' > file.txt` aur `>> file.txt` mein kya difference hai?
5. `cd "My Projects"` mein quotes kyun hain?
6. `command not found` par first 2 checks kya honge?
7. `rm -rf` bina inspect kiye kyun dangerous hai?
8. Absolute aur relative path ka ek-ek example do.

### Self-check answers

1. `pwd` location, `ls` current folder ke entries.
2. `..` parent folder; `~` user home.
3. `ls -la`.
4. `>` overwrite/create; `>>` append/create.
5. Folder name mein space ko ek argument rakhne ke liye.
6. Spelling aur `command -v <name>`/installation-PATH check.
7. Recursive force deletion; wrong path par data loss.
8. `/Users/yourname/projects` absolute; `projects` relative (from current folder).

## 8. Chapter 01 exit gate

Bina notes dekhe: home se practice folder banao, usmein subfolder aur text file create karo, do lines add karo, file read karo, parent/home par wapas jao, aur har step par `pwd` se location confirm karo. Agar tum confidently explain kar sakte ho ki `>` vs `>>` aur hidden files kaise kaam karti hain, toh Chapter 02 — VS Code Setup ke liye ready ho.

**Official reference:** [MIT Missing Semester: The Shell](https://missing.csail.mit.edu/2020/course-shell/) · [Apple Terminal User Guide](https://support.apple.com/guide/terminal/welcome/mac)
