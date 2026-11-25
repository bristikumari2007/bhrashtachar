# Mission 4 — How programs run

## 1. Task / objective
Create and run a one-line Python program (`hello.py`) using Python 3 from Terminal, and compare how compilers and interpreters translate and execute programs.

## 2. Work completed

### Task 4.1 — Create and run a Python program
- Created `mission-04-programs/hello.py` containing:
  ```python
  print("Hello from Python")
  ```
- Ran `python3 --version` (`Python 3.14.5`) and executed `python3 mission-04-programs/hello.py` from the repository folder.
- Verified actual Terminal output:
  ```text
  Hello from Python
  ```

---

### Task 4.2 — Compare compiler and interpreter

| Point | Compiler | Interpreter |
| --- | --- | --- |
| When translation / execution happens | Translates the entire program before it runs | Translates and executes instructions at runtime |
| Typical output | Machine code or a standalone executable file | Direct program output without creating a separate executable |
| One example | C (using `gcc`) | Python (using `python3`) |
| One advantage | Compiled programs usually run faster once built | Easy to test edits right away without a separate compile step |

**Explanation in my own words:**
As shown in the comparison table, a compiler translates the entire source program into machine code or an executable file before the program runs, whereas an interpreter reads and executes instructions at runtime without creating a standalone executable. Because a compiled program such as C is already translated ahead of time, it usually runs faster once built, while an interpreted workflow lets me test small changes immediately. In Python, I ran `python3 mission-04-programs/hello.py` directly from Terminal and saw `Hello from Python` without a separate build command. In real language implementations, both approaches can also be combined—for example, standard Python compiles source code into intermediate bytecode behind the scenes and then interprets that bytecode.

## 3. Commands / tools used
- `python3 --version` — Checked the installed Python 3 version (`Python 3.14.5`).
- `python3 mission-04-programs/hello.py` — Ran `hello.py` with Python 3 and displayed `Hello from Python`.
- `print("Hello from Python")` — Built-in Python function used inside `hello.py` to print text output to Terminal.

## 4. My understanding
Writing and running `hello.py` showed me how human-readable source code turns into output on the screen. With Python, I do not need to run a separate compiler step myself because `python3` handles running the `.py` file directly, which makes it simple for beginners to write and test code. At the same time, learning how compilers translate code ahead of time helped me understand why different programming languages trade off build steps, execution speed, and quick testing.

## 5. Difficulties faced
No major difficulties.

## 6. How I resolved them
Not applicable.

## 7. Evidence / files
- `mission-04-programs/hello.py`
- `mission-04-programs/README.md`

## 8. Commit details
- Commit message: `Complete Python program and compiler interpreter mission`
- Status: Committed on branch `main` and pushed to `origin/main` on GitHub.
