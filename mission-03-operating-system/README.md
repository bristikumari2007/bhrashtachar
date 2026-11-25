# Mission 3 — Understand the operating system

## 1. Task / objective
Explore the macOS operating system using Terminal commands to inspect system details, user identity, storage usage, running processes, memory statistics, paths, and file permissions, and explain the core responsibilities of an operating system in my own words.

## 2. Work completed

### Task 3.1 — Explore your operating system

| Information explored | What it tells you | Your observation (privacy-safe) |
| --- | --- | --- |
| Operating system / system details (`sw_vers`, `uname -a`) | Shows the macOS version, build number, underlying kernel name, kernel version, and CPU architecture. | `sw_vers`: Product Name `macOS`, Product Version `26.6.2`, Build Version `25G83`. `uname -a`: Kernel name `Darwin`, Kernel version `25.6.0`, Architecture `ARM64` (device name `[redacted]`). |
| Current account identity (`id`) | Shows the numeric user ID, primary group ID, primary group name, and other groups the account belongs to. | User `[redacted]` with UID `501`, primary GID `20`, primary group `staff`, and membership in the `admin` group. |
| Available and used storage (`df -h /`) | Shows the capacity, used space, free space, usage percentage, and mount point of the root filesystem. | Mounted on `/`: Size `460 GiB`, Used `15 GiB`, Available `343 GiB`, Capacity `5%`. |
| System activity snapshot (`ps aux \| head -n 10`, `vm_stat`) | Shows a snapshot of active processes and how virtual memory pages are organised. | Processes observed included `opendirectoryd`, `WindowServer`, `WhatsApp`, and `Visual Studio Code Helper`. `vm_stat` reported a page size of `16,384` bytes. |

**Notes on `uname -a` and `vm_stat` observations:**
- **What `Darwin` and `ARM64` mean:** `Darwin` is the Unix-like core operating system and kernel foundation on which macOS is built. `ARM64` refers to the 64-bit ARM processor architecture used by Apple Silicon Macs, which determines the instruction set the CPU runs.
- **What `vm_stat` page categories mean (`16,384` bytes per page):**
  - **Free pages:** Memory pages that are currently unused and immediately available for programs or the OS to use.
  - **Active pages:** Memory pages currently in use by running processes and recently accessed.
  - **Inactive pages:** Memory pages that hold data from recently used programs or files; they are not actively being used right now and can be reclaimed if needed.
  - **Wired pages:** Memory pages locked in RAM by the operating system kernel that cannot be moved out to disk.
  - **Compressed pages:** Inactive memory data that macOS has shrunk in RAM to save space instead of immediately writing it to disk.

---

### Task 3.2 — Understand processes
Using `ps aux | head -n 10`, I inspected a snapshot of running processes on the Mac (with usernames and personal paths redacted).

- **What is a process?** A process is an instance of a program that is currently running in memory, managed by the operating system.
- **Columns in `ps aux` output:**
  - **PID (Process Identifier):** A unique number assigned by the OS to identify and track each running process.
  - **CPU (`%CPU`):** The percentage of CPU time the process is currently using.
  - **Memory (`%MEM`):** The percentage of physical memory (RAM) the process is using.
  - **COMMAND:** The name or command path of the program or background service running as that process.
- **Examples of processes observed:**
  - **Applications / helper processes:** `WhatsApp` and `Visual Studio Code Helper` (user-facing apps and app helpers).
  - **System / background processes:** `opendirectoryd` (handles directory and account lookups) and `WindowServer` (draws windows and graphics on the screen).

---

### Task 3.3 — Understand paths and permissions

**Current directory and absolute vs. relative paths:**
- Running `pwd` in my home directory displayed `/Users/[redacted]`.
- An **absolute path** gives the full address starting from the root `/` directory, so it points to the same location regardless of where you currently are in Terminal. Example from my assignment folder: `/Users/[redacted]/[workspace]/digital-detective-8552/mission-03-operating-system`.
- A **relative path** describes a location starting from the current working directory. Example: if I am in the repository root `digital-detective-8552`, the relative path to this mission folder is `mission-03-operating-system`.

**Inspecting permissions (without changing system permissions):**
- **Home directory (`ls -ld ~`):**
  - Observed permission string: `drwxr-x---+`, Owner: `[redacted]`, Group: `staff`.
  - The characters `drwxr-x---` show the **basic Unix permissions**, while the trailing `+` indicates **additional Access Control List (ACL) rules**:
    - `d` — Indicates this entry is a **directory** (folder), not a regular file.
    - `rwx` (owner) — Basic Unix permission bits for the owner (`[redacted]`) show read, write, and execute (traverse) bits.
    - `r-x` (group) — Basic Unix permission bits for the `staff` group show read and execute (traverse) bits, without write.
    - `---` (others) — Basic Unix permission bits for other users show no read, write, or execute bits.
    - `+` — Indicates extra ACL rules are attached to this directory. Because ACLs can grant or restrict access beyond the basic Unix bits, exact effective access cannot be confirmed from `drwxr-x---+` alone without inspecting those ACL rules.

| Permission | Meaning | Example |
| --- | --- | --- |
| `r` — Read | Allows a file's contents to be read (or a folder's contents to be listed). | Opening a text file or listing a folder. |
| `w` — Write | Allows a file to be modified (or files to be added/removed inside a folder). | Editing a text file. |
| `x` — Execute | Allows a file to be run as a program; on a directory, allows entering/traversing it. | Running a script or using `cd` to enter a directory. |

---

### Task 3.4 — Explain operating-system responsibilities

| OS responsibility | Your explanation | Example |
| --- | --- | --- |
| Process management | Starts, schedules, tracks, and stops running programs so multiple apps and background services can share the CPU smoothly. | Assigning PIDs to `WhatsApp`, `Visual Studio Code Helper`, and `WindowServer` at the same time. |
| Memory management | Allocates RAM to running processes, separates each process's memory, and uses virtual memory paging to manage space safely. | `vm_stat` tracking free, active, inactive, wired, and compressed `16,384`-byte pages. |
| Device management | Communicates with hardware devices through drivers so applications do not have to control hardware directly. | Handling keyboard typing, trackpad movement, and screen drawing through `WindowServer`. |
| File management | Organises data into files and directories on storage drives and keeps track of where everything is stored and how much space is left. | Storing files on `/` where `df -h /` shows `15 GiB` used and `343 GiB` available out of `460 GiB`. |
| User interface / shell | Provides ways for the user to interact with the system, either graphically or by typing text commands. | Using macOS Finder (GUI) or Terminal with a shell (CLI) to run `pwd` and `ls`. |
| Security and permissions | Protects user files and system settings by verifying user accounts and enforcing permission rules before allowing access. | Account UID `501` in groups `staff` and `admin`, with `~` showing basic Unix permissions `drwxr-x---+` and additional ACL rules (`+`). |

## 3. Commands / tools used
- `sw_vers` — Displays the macOS product name (`macOS`), version (`26.6.2`), and build (`25G83`).
- `uname -a` — Prints system kernel details including kernel name (`Darwin`), kernel version (`25.6.0`), and hardware architecture (`ARM64`).
- `id` — Shows the current user's numeric UID (`501`), primary GID (`20`), primary group (`staff`), and group memberships (`admin`).
- `df -h /` — Reports total, used, and available disk space on the root `/` filesystem in human-readable units.
- `ps aux | head -n 10` — Lists running processes with PID, `%CPU`, `%MEM`, and command details, trimmed to the first 10 lines with `head`.
- `vm_stat` — Displays macOS virtual memory page size (`16,384` bytes) and categories of virtual memory pages (`free`, `active`, `inactive`, `wired`, `compressed`).
- `pwd` — Prints the current working directory path (`/Users/[redacted]` when in the home directory).
- `ls -ld ~` — Shows detailed basic Unix permissions (`drwxr-x---+`), ACL indicator (`+`), owner, and group for the home directory itself rather than its contents.

## 4. My understanding
Through this mission I saw how macOS works behind the scenes even when I am just opening normal apps. Everything running on the computer—from background services like `opendirectoryd` and `WindowServer` to apps like `WhatsApp`—is tracked as a process with its own PID, CPU share, and virtual memory pages. At the same time, user IDs, groups, basic Unix permission bits (`r`, `w`, `x`), and ACLs help control access to directories like my home folder.

## 5. Difficulties faced
Running commands like `pwd`, `id`, `ps aux`, and `ls -ld ~` included my local username, device details, and personal paths in the raw terminal output, so I had to be careful not to copy private identifiers directly into the README. Also, `vm_stat` reports memory in `16,384`-byte pages rather than simple gigabyte totals, and `ls -ld ~` included a `+` sign after the permission letters, which was unfamiliar at first.

## 6. How I resolved them
I redacted my username, device name, and personal path segments with `[redacted]` before documenting any observations. I also checked what each `vm_stat` page category (`free`, `active`, `inactive`, `wired`, and `compressed`) means and learned that `+` indicates extra ACL rules beyond the basic Unix permission string, so I avoided making guesses about total RAM or exact effective ACL access.

## 7. Evidence / files
- `mission-03-operating-system/README.md`

## 8. Commit details
- Commit message: `Complete operating system and permissions mission`
- Status: Committed on branch `main` and pushed to `origin/main` on GitHub.
