# Mission 0 — Create your GitHub workspace

## 1. Task / objective
Verify that Python 3 and Git are installed, create a local project folder named `digital-detective-8552` with the required mission folders and placeholder files, write the initial root `README.md`, and publish the repository to GitHub.

## 2. Work completed
- Checked the installed tool versions on macOS:
  - Python: `Python 3.14.5`
  - Git: `git version 2.54.0 (Apple Git-157)`
- Created the local folder `digital-detective-8552` and initialized Git on the `main` branch.
- Created the root `README.md`, all nine mission folders (`mission-00-setup` through `mission-08-final-report`) with their `README.md` files, `mission-05-numbers-data/number_converter.py`, and the `evidence/` folder.

## 3. Commands / tools used
- `python3 --version` — Checks which version of Python 3 is installed on the computer.
- `git --version` — Checks whether Git is installed and shows its version number.
- `mkdir -p` — Creates all required project and mission folders at once.
- `touch` — Creates empty placeholder files (`README.md` files and `number_converter.py`).
- `git init -b main` — Turns the project folder into a Git repository with `main` as the starting branch.
- `git add` / `git commit` — Stages the setup files and saves them as a commit snapshot.
- `git remote add origin` / `git push -u origin main` — Connects the local folder to the GitHub repository and uploads the initial commit.

## 4. My understanding
- **What a repository is:** A repository (or "repo") is a project folder tracked by Git. It stores all the project files along with a history of every saved change (commit), and when hosted on GitHub, it can be viewed online and backed up safely.
- **Why the folder structure is organised by mission:** Grouping files into separate folders (`mission-00-setup` through `mission-08-final-report`) keeps each topic neat and easy to find, prevents files from getting mixed up in the root folder, and makes it simple for an instructor to review each mission one by one.

## 5. Difficulties faced
No major difficulties.

## 6. How I resolved them
Not applicable.

## 7. Evidence / files
- `README.md`
- `mission-00-setup/README.md`
- `mission-01-computer-basics/README.md` through `mission-08-final-report/README.md`
- `mission-05-numbers-data/number_converter.py`
- `evidence/.gitkeep`

## 8. Commit details
- Commit message: `Set up Digital Detective mission structure`
- Status: Committed on branch `main` and pushed to `origin/main` on GitHub.
