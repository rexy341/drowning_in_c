# Unix for Beginners

A guided tour from OS basics → kernel & shell → how computers boot → Unix deep-dive

---

## 1. What is an Operating System?

> Think of the OS as a **hotel manager**: guests (your programs) don't deal directly with the building (hardware). The manager handles rooms (memory), staff (CPU time), and services (devices).

### What is an OS?
- A collection of *system software* that manages hardware
- Acts as an interface between user, software, and hardware
- The brain/heart of every computing device
- Controls allocation of memory, CPU, and devices

### Key functions
- Memory management
- Process & CPU scheduling
- File management
- Device management
- Security & error detection

### Popular operating systems
Unix · Linux · Windows · macOS · Android · iOS · DOS

---

## 2. What is the Kernel?

> The kernel is the **only program that runs with full hardware access**. Everything else — your browser, your shell, your games — talks to hardware only through the kernel.

### What the kernel does

1. **Memory management** — Allocates RAM to each running process. Ensures process A can't read process B's memory.
2. **Process scheduling** — Decides which program gets CPU time and for how long — switches between processes thousands of times per second.
3. **Device drivers** — Manages communication with hardware: keyboard, disk, network card, display.
4. **System calls** — Provides a safe API for programs to request hardware services, e.g. `read()`, `write()`, `fork()`.
5. **File system** — Abstracts disk storage into files and directories. Handles permissions and ownership.

### Kernel space vs User space

The CPU has two protection rings:

- **Kernel space** — full hardware access, high privilege
- **User space** — restricted access, your apps live here

### Kernel types

- **Monolithic** — Linux, Unix: all services in one binary, fast
- **Microkernel** — minuscule core, services as separate processes
- **Hybrid** — Windows, macOS: mix of both

---

## 3. What is the Shell?

> The shell is like a **translator**: you speak English commands (`ls -l`), the shell translates them into system calls, and the kernel executes them on the hardware.

### How the shell works

1. **You type a command** — e.g. `ls -la /home`
2. **Shell parses it** — splits command name from arguments, expands wildcards like `*.txt`
3. **Shell finds the program** — searches `$PATH` directories to locate `/bin/ls`
4. **Kernel executes it** — shell calls `fork()` + `exec()` system calls; kernel runs the program
5. **Output returned to you** — results printed to your terminal via stdout

### Types of shells in Unix/Linux

| Shell | Name | Key feature |
|-------|------|-------------|
| `sh` | Bourne shell | Original Unix shell, POSIX standard |
| `bash` | Bourne Again Shell | Most common today; scripting power |
| `csh` | C shell | C-like syntax, BSD systems |
| `ksh` | Korn shell | Combined sh + csh features |
| `zsh` | Z shell | Modern features, default on macOS |

### Shell is also a programming language

You can write scripts — files of shell commands — to automate tasks:

```bash
#!/bin/bash
echo "Hello, $USER!"
ls -l /home/$USER
```

---

## 4. How Booting Works — Step by Step

> Booting is a **chain of trust**: each stage loads and hands control to the next. If any link breaks, the system won't start.

1. **Power on → CPU wakes up** — You press the power button. The motherboard sends power to the CPU. The CPU's program counter jumps to a **fixed address in ROM** — the location of the firmware.

2. **BIOS / UEFI firmware runs** — **BIOS** (older) or **UEFI** (modern) firmware initialises the CPU, RAM, and hardware devices. It runs a *Power-On Self Test (POST)* — checking that memory, GPU, and storage are present and working. The beeps you sometimes hear are POST codes.

3. **Boot device selection** — BIOS/UEFI looks at the *boot order* (e.g. SSD first, then USB) and finds a bootable device — one that has a valid **Master Boot Record (MBR)** or **GPT partition table** with an EFI system partition.

4. **Bootloader loads** — The firmware reads the first sector (512 bytes) of the disk — the MBR — and executes the tiny **bootloader** stored there. On Linux this is typically **GRUB**; on macOS it's `boot.efi`. The bootloader shows a menu and loads the OS kernel from disk into RAM.

5. **Kernel initialises** — The kernel takes over. It *decompresses itself*, sets up CPU protection rings, initialises memory management (virtual memory, paging), and loads essential device drivers. At this point the kernel is running but there are still no user processes.

6. **Init system starts (PID 1)** — The kernel spawns the very first user process — **PID 1**. On modern Linux systems this is `systemd` (or `init` on older Unix). PID 1 is the ancestor of every other process on the system.

7. **Services & daemons start** — Init starts system services in parallel: networking, logging (`syslogd`), cron, SSH daemon, display manager, etc. Each is a child process of PID 1.

8. **Login prompt / GUI** — Finally, a **getty** process opens a terminal and displays the login prompt — or the display manager launches the graphical login screen. Boot complete.

### Quick visual summary

```
Power on → BIOS/UEFI → POST → Bootloader → Kernel → PID 1 (init) → Services → Login
```

---

## 5. Introduction to Unix

### Origin story

- **1969** — Ken Thompson and Dennis Ritchie at AT&T Bell Laboratories build Unix. Originally called **UNICS** (Uniplexed Information Computing System).
- **1973** — Unix is rewritten in the C language (also created at Bell Labs), making it *portable* — the first OS written in a high-level language. This was revolutionary.
- **1991** — Linus Torvalds releases Linux — a Unix clone that doesn't use Unix source code. Free and open-source, it spreads globally.

### Key features of Unix

- Multi-user & multi-tasking
- Portable & open source
- Hierarchical file system
- Piping & scripting
- Security & modularity
- CLI + GUI support

### Unix flavors / distributions

| Vendor | Unix flavor |
|--------|-------------|
| AT&T / Bell Labs | Original Unix, BSD Unix |
| Sun / Oracle | Solaris |
| IBM | AIX |
| HP | HP-UX |
| Apple | macOS (BSD-based) |
| Community | Linux, Ubuntu, Fedora, FreeBSD |

---

## 6. Unix Architecture

> Unix's layered design is its superpower. Each layer is **independent** — you can swap the shell without touching the kernel, or add programs without changing the OS.

```
┌─────────────────────────────────────┐
│   User programs & applications      │
│   cp, mv, ls, grep, vim, gcc...     │
├─────────────────────────────────────┤
│   Shell (command interpreter)       │
│   bash, sh, ksh, zsh               │
├─────────────────────────────────────┤
│   Kernel (core OS)                  │
│   Memory, processes, files, devices │
├─────────────────────────────────────┤
│   Hardware                          │
│   CPU, RAM, Disk, Network, Display  │
└─────────────────────────────────────┘
```

- **Programs layer** — Your apps and utilities. They talk to the kernel through *system calls*, never directly to hardware.
- **Shell layer** — Reads your typed command → parses it → calls the right kernel functions → shows you the output.
- **Kernel layer** — Hub of Unix. Manages CPU, memory, files, processes. Only piece with direct hardware access.

### Unix piping — the killer feature

Chain small tools into powerful pipelines:

```bash
$ cat access.log | grep "404" | sort | uniq -c | sort -rn
```

Reads a log file, filters for 404 errors, counts unique entries, and sorts by frequency — four simple tools chained together.

---

## 7. Unix File System

> **"Everything is a file"** is Unix's central philosophy. Disks, terminals, network sockets, processes — all accessed through the same file interface.

### Directory tree structure

```
/                    # Root directory — top of everything
├── bin/             # Essential commands: ls, cp, mv
├── etc/             # System config files
├── home/            # User home directories
│   └── alice/       # Alice's home
├── var/             # Logs, temp files
├── tmp/             # Temporary files
└── usr/             # User programs and libraries
```

### Types of files

| Symbol | Type |
|--------|------|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `p` | Named pipe |

### File permissions

```
-rwxr-xr-x 1 alice staff
```

- `rwx` = owner: read, write, execute
- `r-x` = group: read, execute
- `r-x` = others: read, execute

Change with `chmod`, ownership with `chown`.

### Path types

**Absolute path** — always starts with `/`, works from anywhere:
```
/home/alice/documents/notes.txt
```

**Relative path** — relative to current location (`.` = current dir, `..` = parent):
```
documents/notes.txt
```

---

## 8. Essential Unix Commands

### Navigation & listing

| Command | What it does | Example |
|---------|-------------|---------|
| `ls` | List files in directory | `ls -la` |
| `pwd` | Print working directory | `pwd` |
| `cd` | Change directory | `cd /home/alice` |
| `tree` | Show directory as tree | `tree -L 2` |

### File operations

| Command | What it does | Example |
|---------|-------------|---------|
| `cat` | Print file contents | `cat file.txt` |
| `cp` | Copy file/directory | `cp a.txt b.txt` |
| `mv` | Move or rename | `mv old.txt new.txt` |
| `rm` | Remove file | `rm -rf dir/` |
| `mkdir` | Create directory | `mkdir mydir` |
| `touch` | Create empty file | `touch notes.txt` |

### System & info commands

| Command | What it does |
|---------|-------------|
| `who` | Show logged-in users |
| `date` | Display current date & time |
| `cal` | Show calendar (`cal 3 2024` for March) |
| `history` | List previously run commands |
| `man` | Manual page for any command: `man ls` |
| `grep` | Search text in files: `grep "error" log.txt` |
| `fg` | Bring background job to foreground |

> **Pro tip:** When stuck, type `man <command>` to read the manual. `man ls`, `man grep`, `man bash` — every Unix command is documented this way.

---

## 9. Unix vs Linux vs Ubuntu

### The family tree

```
Unix (1969)   → original OS from Bell Labs, proprietary
└── Linux (1991)  → free Unix clone by Linus Torvalds
    └── Ubuntu (2004)  → popular Linux distribution
```

### Unix vs Linux — key differences

| | Unix | Linux |
|-|------|-------|
| **Cost** | Mostly paid/licensed | Free (open source) |
| **Source code** | Proprietary | Open, modifiable |
| **Developer** | AT&T + vendors | Community worldwide |
| **Portability** | Limited hardware | Runs on almost anything |
| **GUI** | CDE, Gnome | KDE, Gnome, LXDE, many more |
| **File system** | jfs, hfs, zfs | ext2–ext4, xfs, btrfs |

### Ubuntu

- Most popular Linux distribution
- Free and open source
- Updated every 6 months
- Name from Zulu: *"humanity to others"*
- Great for beginners — easy install
- Runs on PC, laptop, servers, cloud

### What they share

- Same core commands (`ls`, `cp`, `grep`...)
- Same shell (`bash`/`sh`)
- Hierarchical file system
- Multi-user, multi-tasking
- POSIX standard compliance
- Piping and redirection
