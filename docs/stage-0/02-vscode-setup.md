# Chapter 02 — VS Code Setup and Shortcuts

> Stage 0 / 10 | Hinglish study chapter | macOS + VS Code | 28 Sep 2026

## Goal

VS Code ko editor/terminal/debugger ke roop mein use karna, file navigation aur search shortcuts se speed badhana, aur VS Code + Git integration ko samajhna.

## 1. VS Code actually kya hai?

VS Code ek text editor hai jo code, markdown, config files wagaira edit karta hai. Yeh terminal nahi hai, lekin built-in terminal aur Git integration deta hai. VS Code ke features: file explorer, search, multi-cursor editing, integrated terminal, debugger, extensions.

## 2. Installation aur workspace

- [VS Code download](https://code.visualstudio.com/)
- `code .` command install karo (Command Palette → "Shell Command: Install 'code' command").
- Project folder ko VS Code mein kholne ke liye: terminal se `code ai_stage02` ya VS Code → File → Open Folder.

Workspace = tumne jo folder open kiya hai. VS Code usi folder ke files dikhayega; parent files direct visible nahi honge.

## 3. Essential shortcuts (macOS)

| Kaam | Shortcut | Yaad rakho |
| --- | --- | --- |
| Command Palette | `Cmd+Shift+P` | har feature ka search bar |
| Quick Open (file) | `Cmd+P` | file search |
| Find in files | `Cmd+Shift+F` | project-wide search |
| Toggle terminal | `Ctrl+`` | integrated terminal |
| New file | `Cmd+N` | unsaved buffer |
| Save | `Cmd+S` | save current file |
| Save all | `Cmd+Option+S` | sab files save |
| Go to line | `Ctrl+G` | `line:column` bhi |
| Toggle sidebar | `Cmd+B` | explorer hide/show |
| Multi-cursor | `Option+click` | multiple edit points |
| Duplicate line | `Shift+Option+↓` | quick copy |
| Move line up/down | `Option+↑/↓` | reorder |
| Comment toggle | `Cmd+/` | language-aware |
| Format document | `Shift+Option+F` | formatter required |
| Rename symbol | `F2` | safe rename |

Shortcuts OS/keymap par differ kar sakte hain. Command Palette se "Preferences: Open Keyboard Shortcuts" dekh sakte ho.

## 4. Integrated terminal aur Git

- Terminal toggle: `Ctrl+``. Default shell usually `zsh` (macOS).
- Terminal se `git status`, `git add`, `git commit` chalao; VS Code Source Control panel bhi same changes dikhayega.
- Terminal ka current directory VS Code ke open folder ke barabar hona chahiye; mismatch ho toh `cd` se adjust karo.

## 5. Extensions: minimal and safe

- **Python** (Microsoft)
- **Prettier** ya language-specific formatter
- **GitLens** (optional, advanced Git UI)
- **Markdown All in One** (optional)

Har extension permissions aur network access check karo. Unknown publisher se avoid karo.

## 6. Common mistakes

- Save kiya file ≠ committed file: `git status` verify karo.
- Formatter ne code style badal diya: `.prettierrc`/settings check karo.
- Terminal ka directory aur project root alag: `pwd` aur VS Code Explorer compare karo.

## 7. Quick practice

1. Project folder `code ai_stage02` se kholo.
2. `Ctrl+`` se terminal kholo, `pwd` check karo.
3. `Cmd+P` se `README.md` kholo, ek line add karo, `Cmd+S`.
4. Source Control panel mein change dekho, message likh kar commit karo.

## 8. Exit gate

Bina notes: VS Code kholo, terminal toggle karo, ek nayi file banao, do lines likho, save karo, Git panel se commit karo. Agar tum shortcuts aur terminal-directory relation explain kar sakte ho, toh Chapter 03 ke liye ready ho.

**References:** [VS Code docs](https://code.visualstudio.com/docs) · [VS Code shortcuts](https://code.visualstudio.com/docs/getstarted/keybindings)
