# Mission 2 — Become comfortable with the Terminal

## 1. Task / objective
Practice basic Terminal commands inside the assignment repository, manage practice files safely inside `terminal-practice/`, understand flags and pipes, and check how package managers work on macOS.

## 2. Work completed

### Task 2.1 — Explore basic Terminal operations

| Operation / command name | What it does | What I observed |
| --- | --- | --- |
| Current-directory display (`pwd`) | Prints the full path of the folder I am currently in. | Inside the repo it printed `/Users/[redacted]/.gemini/antigravity/scratch/digital-detective-8552`. |
| Directory listing (`ls`) | Lists the visible files and folders in the current directory. | Showed `README.md`, `evidence`, and `mission-00-setup` through `mission-08-final-report` in columns. |
| Detailed listing (`ls -l`) | Shows permissions, link count, owner, group, byte size, modification time, and name. | Listed each item on its own line, such as `README.md` at `1729` bytes and folders at `96` or `128` bytes. |
| Change directory (`cd`) | Moves the Terminal's current working directory to another folder. | Running `cd terminal-practice` moved me into that folder, and `cd ..` moved me back up to the parent repository folder. |
| Create directory (`mkdir`) | Creates a new folder at the given name or path. | Running `mkdir -p terminal-practice` created the `terminal-practice` folder inside the repository. |
| Create empty file (`touch`) | Creates an empty file (or updates its timestamp if it already exists). | Running `touch notes.txt` created `notes.txt`, and `ls -l notes.txt` showed its size as `0` bytes. |
| Copy file (`cp`) | Creates a duplicate of an existing file under a new name or location. | Running `cp notes.txt notes_backup.txt` created an `81`-byte copy while keeping `notes.txt` unchanged. |
| Move / rename file (`mv`) | Moves a file to another folder or renames it in place. | Running `mv notes_backup.txt notes_archive.txt` renamed the backup file without leaving `notes_backup.txt` behind. |
| Display file contents (`cat`) | Prints the full text inside a file directly to the Terminal. | Running `cat notes.txt` displayed both lines stored inside `notes.txt`. |

---

### Task 2.2 — Practise file changes safely
All file experiments were performed inside `terminal-practice/` inside the assignment repository:
1. Created `terminal-practice/` and an empty `notes.txt` (`0` bytes).
2. Used `echo "First line: practicing Terminal commands" > notes.txt` to write the first line, and checked with `cat notes.txt`.
3. Used `echo "Second line: added with append operator" >> notes.txt` to add a second line without removing the first line, and verified with `cat notes.txt` that both lines were present (`81` bytes total).
4. Tested overwriting separately on `temp_overwrite.txt`: writing with `>` replaced `"Replaced text"` with `"New text replaces old"`.
5. Copied `notes.txt` to `notes_backup.txt` (`cp`) and renamed `notes_backup.txt` to `notes_archive.txt` (`mv`).

**Answers to Task 2.2 questions:**
- **Difference between creating a file and editing its contents:** `touch` only creates an empty file (0 bytes) or updates its timestamp, whereas redirecting text with `>` or `>>` (or opening it in an editor) actually writes data inside the file.
- **Difference between replacing a file's contents and adding text to the end:** Using `>` overwrites the file and erases any previous content, while `>>` appends new text to the end and keeps existing lines intact.
- **Difference between copying a file and moving a file:** `cp` creates a second independent file so both the original and copy exist, whereas `mv` transfers or renames the existing file so only the destination name remains.
- **Difference between absolute and relative file locations:** An absolute path starts from the root `/` (for example, `/Users/[redacted]/.gemini/antigravity/scratch/digital-detective-8552/terminal-practice/notes.txt`) and works from anywhere, while a relative path is written from the current folder (for example, `notes.txt` when inside `terminal-practice/`, or `terminal-practice/notes.txt` from the repository root).
- **What information does the current-directory display (`pwd`) provide?** It shows the complete path from `/` down to the folder you are currently working in, which prevents running commands in the wrong folder.
- **Why is a directory-listing operation (`ls`) useful?** It confirms which files and folders exist in a location and helps verify that commands like `mkdir`, `touch`, `cp`, and `mv` worked as expected.

---

### Task 2.3 — Understand flags and pipes
- **Comparing `ls` vs `ls -lah`:**
  - Normal `ls` only prints visible file and folder names in compact columns.
  - Adding `-l` (long format) displays file permissions, owner, group, size, and last modified date/time.
  - Adding `-a` (all) includes hidden entries starting with `.`, revealing `.`, `..`, and `.git` (which normal `ls` hides).
  - Adding `-h` (human-readable) converts byte counts into easier units such as `1.7K` instead of `1729` for `README.md`, and `448B` or `96B` for folders.
  - Privacy-safe snippet of `ls -lah` output (usernames redacted):
    ```text
    drwxr-xr-x@ 14 [redacted]  staff   448B Nov 24 23:55 .
    drwxr-xr-x@  4 [redacted]  staff   128B Nov 24 23:55 ..
    drwxr-xr-x@ 12 [redacted]  staff   384B Nov 25 22:51 .git
    -rw-r--r--@  1 [redacted]  staff   1.7K Nov 25 00:01 README.md
    ```
- **Using a pipe (`ls -l | head -n 5`):**
  - The left side (`ls -l`) generates the full detailed directory listing (`12` lines including `total 8`), and the pipe symbol (`|`) sends that output directly as input into the right side (`head -n 5`), which prints only the first `5` lines (`total 8`, `README.md`, `evidence`, `mission-00-setup`, and `mission-01-computer-basics`).

---

### Task 2.4 — Understand package managers
- Running `brew --version` directly in the shell returned `command not found: brew`, so I checked the standard macOS Apple Silicon Homebrew path (`/opt/homebrew/bin/brew --version`), which returned `Homebrew 7.0.16`.
- Running `/opt/homebrew/bin/brew list` returned an empty list (no Homebrew packages are currently installed). Nothing was installed or uninstalled for this assignment.
- **Why package managers are useful:** A package manager lets you install, update, and remove command-line tools and libraries from one place using simple commands instead of downloading installers manually from websites. It also handles dependencies automatically so required supporting tools are installed and kept up to date safely.

## 3. Commands / tools used
- `pwd` — Prints the current working directory path.
- `ls`, `ls -l`, `ls -lah` — Lists folder contents in plain, detailed, and detailed + hidden + human-readable formats.
- `cd` — Changes the current working directory (including `cd ..` to move up one level).
- `mkdir -p` — Creates the `terminal-practice` folder inside the repository.
- `touch` — Creates an empty file (`notes.txt`).
- `echo`, `>`, `>>` — Writes a line of text by overwriting (`>`) or appending (`>>`).
- `cat` — Displays file contents in Terminal.
- `cp` — Copies a file (`notes.txt` to `notes_backup.txt`).
- `mv` — Renames/moves a file (`notes_backup.txt` to `notes_archive.txt`).
- `|` and `head -n 5` — Connects `ls -l` output to `head` to show only the first five lines.
- `/opt/homebrew/bin/brew --version` and `/opt/homebrew/bin/brew list` — Checks whether Homebrew is installed and lists managed packages without modifying anything.

## 4. My understanding
Working in the Terminal showed me how directly and quickly files and folders can be inspected and managed without using Finder. Understanding the difference between overwriting (`>`) and appending (`>>`), and between copying (`cp`) and moving (`mv`), helps avoid accidentally losing file contents. Flags like `-l`, `-a`, and `-h` make a simple command like `ls` much more informative, and pipes (`|`) let small single-purpose commands work together on the output of another command.

## 5. Difficulties faced
Running `brew --version` in the shell initially returned `command not found: brew` even though Homebrew was present on the system.

## 6. How I resolved them
I checked `/opt/homebrew/bin/brew --version` directly using its full path, which confirmed `Homebrew 7.0.16` is installed on this MacBook without modifying any system configuration or installing packages.

## 7. Evidence / files
- `mission-02-terminal/README.md`
- `terminal-practice/notes.txt`
- `terminal-practice/notes_archive.txt`
- `terminal-practice/temp_overwrite.txt`

## 8. Commit details
- Commit message: `Complete Terminal and file management mission`
- Status: Committed on branch `main` and pushed to `origin/main` on GitHub.
