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

The UNIX operating system is made up of three parts named as `the Kernel, the Shell and the Programs`:
1. Kernel
2. Shell
3. Programs

> #### 1. Kernel
- The kernel is the hub/heart/core of Unix Operating System

> #### 2. Shell
- Shell is an interface between a User/User application and Kernel

> #### 3. Programs / User-Application Program
- Utility programs and applications are given by the user are handled in this layer

### 2. Kernel

- The kernel is the hub/heart/core of Unix Operating System
- It acts as an interface between the Hardware and Shell layer
- It allocates the time and memory to the programs and handles the communications in response to the system calls
- Most of the tasks such as memory management, task scheduling, file management, and so on are performed by Kernel
- It manages external commands in Unix
- Manages system resources, and enforce the security scheme
- Manages the machine's memory and allocates it to each active/currently running process
- Manages processor interrupts, and takes care of error handling
- Schedules the work is done by the Central Processing Unit CPU and controls how processes are executed
- Manages the creation and terminations of processes, and the communication between processes
- Allocates and manages resources used by each user
- Allows user processes, including shell commands to run Kernel instructions

### 3. Shell 

- Shell is an interface between a User/User application and Kernel
- Shell is the `command interpreter in Unix`, it supports a Command Line Interface, and also allows scripting
- It serves as the interface between the User and the Kernel, helps to interact with Unix OS ie the Kernel (Shell takes input/command from a user and executes programs-run command)
- The Shell is a Command Line Interface (CLI), As and when we type a command at the terminal, the shell interprets the command and calls the corresponding program
- The Shell layer processes the user request
- Shell uses standard syntax for all the commands
- It provides a rich set of commands
- Shell is an environment in which we can run our commands, programs and shell scripts
- A file `"/etc/shells"` contains a list of all the Shells supported and available in the system

**Different Shells available with most of the Unix variants/flavors: (Shell Types / Shell variants)**
- Bourne shell (sh)
- C shell (csh)
- Korn shell (ksh)
- TelShell (wish)
- Bourne Again Shell (bash)

### Kernel - Shell Layered Architecture

**Technical Notes: Terminal Input Subsystem & Command Execution Architecture**

In a UNIX-like architecture (including Cygwin), command-line input and execution are decoupled into two distinct kernel-level operations: **Character Echoing** and **Line Buffering**. This is managed via the Kernel's **TTY (Teletype) Subsystem** operating in **Canonical (Line-Disciplined) Mode**.

---

*Phase 1: Asynchronous Character Echoing (Per-Keystroke Loop)*

When a user interacts with the keyboard, the system relies on a low-level asynchronous feedback loop to display text before execution.

```text
[Keyboard Matrix] ──(IRQ)──> [CPU / ISR] ──> [TTY Buffer] ──> [Video Framebuffer]
```

- Technical Workflow:
    - **Hardware Interrupt Generation:** Pressing a key (e.g., `a`) pulls down a voltage line on the motherboard, triggering a hardware -     Interrupt Request (IRQ) on the CPU.
    - **Interrupt Service Routine (ISR):** The CPU suspends user-space execution and jumps to the kernel's keyboard driver ISR. The driver reads the raw hardware scancode from the I/O register.
    - **Scancode Translation:** The kernel translates the hardware scancode into its corresponding ASCII/UTF-8 character code (e.g., `0x61` for `a`).
    - **TTY Line Discipline Processing:** The character is passed into the Kernel's TTY Subsystem Because the terminal is in Canonical Mode the kernel holds the character inside a temporary kernel ring-buffer (the TTY input queue).
    - **Character Echoing:** If the `ECHO` flag is enabled in the terminal configuration (`termios`), the TTY driver immediately writes the character code back out to the Standard Output (stdout) buffer.
    - **Video Rendering:** The kernel routes this output to the active display/graphics driver, which modifies the pixel matrix in the video Frame Buffer rendering the character visually on the monitor.

---

*Phase 2: Synchronous Command Execution (Line Buffering & Handshake)*

The terminal shell remains completely decoupled from individual keystrokes until a termination sequence is reached.

```text
[User Hits Enter] 
       │
       ▼
 [Kernel Buffer Closes] ---> Locks the raw character array inside TTY queue
       │
       ▼
 [Shell Wakes Up]       ---> unblocks read() system call; copies string to user space
       │
       ▼
 [Shell Parses Text]    ---> Tokenizes string into argv[] array (Command vs Arguments)
       │
       ▼
 [System Call Made]     ---> Executes fork() and execve() to load binary into memory
```

- Technical Workflow:
    - **Delimiter Detection:** The process shifts when the user presses `Enter`. The keyboard sends the `\n` (Line Feed / Newline, `0x0A`) control character.
    - **Buffer Flushing & Context Switch:** The TTY line discipline detects the newline delimiter, closes the current line buffer packet, and changes the state of the blocked shell process from Waiting (Sleeping to Runnable
    - **The `read()` System Call Handshake:** The Shell (e.g., Bash) had previously issued a blocking `read()` system call on its Standard Input File Descriptor (`fd 0`). The kernel now satisfies this call, copying the complete character string from the Kernel Space TTY buffer into the User Space memory allocation of the Shell.
    - **Command Tokenization (Parsing):** The shell performs lexical analysis on the string. It splits the text on whitespace delimiters into an argument vector array (`argv[]`):
           * `argv[0]` = `"awk"` (The target executable binary)
           * `argv[1]` = `"{print \$0}"` (The AWK execution script argument)
           * `argv[2]` = `"test.txt"` (The target file parameter)
    - **Process Creation & Execution (Fork-Exec Pattern):**
           * `fork()`: The shell issues a `fork()` system call to clone itself, creating a child process with a new unique Process ID (PID).
           * `execve()`: The child process invokes the `execve()` system call, passing `argv[]`. The kernel wipes the child's memory space, searches the system `PATH` env variables for the `awk` binary machine instructions on disk, copies those bytes into RAM, and points the CPU program counter to the `main()` entry function of the new program.

---

**Note 2.1 Architectural Design Rationale**

*Why the Kernel Decouples Line input*

- **Canonical Editing Support (Line Discipline):** By storing text inside a kernel-managed buffer before handing it over to the user application, the OS natively supports input correction. When a user presses Backspace (`0x7F` or `0x08`), the TTY subsystem catches it, deletes the preceding character from the kernel input queue, and moves the screen cursor back. 
- **Efficiency:** If the system did not use line buffering, every single character typed would force the shell to execute evaluations instantly. Line buffering ensures user space applications only wake up and utilize CPU clock cycles when a fully complete command packet is ready for computational processing.


**Note 3.1 How the shell works**

1. *You type a command* — e.g. `ls -la /home`
2. *Shell parses it* — splits command name from arguments, expands wildcards like `*.txt`
3. *Shell finds the program* — searches `$PATH` directories to locate `/bin/ls`
4. *Kernel executes it* — shell calls `fork()` + `exec()` system calls; kernel runs the program
5. *Output returned to you* — results printed to your terminal via stdout

-- **Types of shells in Unix/Linux**

| Shell | Name | Key feature |
|-------|------|-------------|
| `sh` | Bourne shell | Original Unix shell, POSIX standard |
| `bash` | Bourne Again Shell | Most common today; scripting power |
| `csh` | C shell | C-like syntax, BSD systems |
| `ksh` | Korn shell | Combined sh + csh features |
| `zsh` | Z shell | Modern features, default on macOS |

-- **Shell is also a programming language**

You can write scripts — files of shell commands — to automate tasks:

```bash
#!/bin/bash
echo "Hello, $USER!"
ls -l /home/$USER
```

---

## 4. Boot Process Of Operating System
---------------------

**The standard boot process follows six critical, sequential phases:**

1. *Power On and Initialization*

- Power Supply: Pressing the power button sends electricity from the Power Supply Unit (PSU) to the motherboard.
- CPU Activation: The central processing unit starts up and seeks instructions. Because the RAM is empty, the CPU executes a hardcoded instruction that points directly to the system firmware.

2. *BIOS / UEFI Firmware Execution*

- Firmware Load: The computer runs its low-level built-in software, either traditional BIOS (Basic Input/Output System) or modern UEFI (Unified Extensible Firmware Interface).
- POST (Power-On Self-Test): The firmware runs a diagnostic check to verify that essential hardware components—like the CPU, RAM, storage drives, and keyboard—are functional. If it detects failures, it halts and reports errors via screen alerts or audio beep codes.

3. *Finding the Bootloader*

- Boot Order: Once hardware checks pass, the firmware scans available storage devices (SSD, HDD, or USB) based on a preconfigured priority list.
- Sector Search:
- On Legacy BIOS systems, it targets the MBR (Master Boot Record) located in the first sector of the boot drive.
- On UEFI systems, it targets the GPT (GUID Partition Table) and identifies the dedicated EFI System Partition.
- Execution: The firmware finds a tiny program called the bootstrap loader and copies it into the RAM.

4. *Loading the Bootloader*

- Intermediate Step: The small bootstrap program initializes and fetches a more advanced, primary bootloader (such as GRUB for Linux or Windows Boot Manager for Windows).
- OS Selection: If multiple operating systems are installed on different disk partitions (dual booting), the bootloader pauses to display a menu allowing you to choose your desired OS.

5. *Kernel and Driver Initialization*

- Kernel Load: The bootloader locates the core component of the operating system—the kernel—and transfers it to the RAM. Control of the machine is officially handed over to the OS.
- Hardware Drivers: The kernel takes control of the CPU and memory. It then mounts necessary filesystems and loads essential device drivers so the OS can cleanly communicate with system hardware.

6. *Starting Core Services and User Authentication*

- Background Daemons: The kernel initiates the root system process (like systemd in Linux) to launch vital background services. These include network connections, security modules, and print managers.
- User Login: Finally, the system initiates the graphical interface, presenting the desktop environment or a user authentication screen. Once logged in, the system is fully prepared for use.

------------------------------
**Note 4.1: Key Variations: Cold Boot vs. Warm Boot**

- Cold Booting (Hard Boot): Occurs when you power on a device from a completely turned-off state. The machine performs the full routine, including mandatory POST diagnostics and total hardware initialization.
- Warm Booting (Soft Boot): Occurs when you trigger a software restart without cutting the electrical power supply. It speeds up the loading process by bypassing structural hardware checks and some POST sequences.

**Note 4.2: How does POST produce screen alerts or audio alerts if the OS has not been loaded yet?**

The Power-On Self-Test (POST) can communicate without an operating system because it relies entirely on firmware and low-level hardware standards that are hardcoded into your computer's components.Before the OS ever loads, the motherboard's BIOS/UEFI acts as a temporary, mini-operating system.

1. *How POST Accesses Sound (Beep Codes)*

- Direct Hardware Control: The motherboard features a tiny, dedicated physical speaker (the piezo speaker) or a buzzer wired directly to the chipset.
- No Drivers Needed: The BIOS/UEFI contains primitive assembly language instructions to send electrical pulses directly to this buzzer at specific frequencies.
- The Result: If the RAM or video card fails to initialize, the firmware triggers specific patterns of short and long electrical pulses (e.g., one long and two short beeps) to tell you exactly what hardware failed.

2. *How POST Accesses the Screen (Display)*

- VGA Legacy Standards: Long before modern graphics drivers load, all video cards (Nvidia, AMD, or Intel integrated graphics) are hardcoded to support an ancient, universal standard called VGA (Video Graphics Array) mode.
- Video BIOS (VBIOS): The graphics card has its own tiny onboard firmware chip. During the first split-second of booting, the main motherboard firmware locates and executes this Video BIOS.
- Basic Text Output: The VBIOS initializes the graphics processor just enough to accept basic, unaccelerated text and simple graphics. It bypasses complex display pipelines and pipes basic pixels straight to your monitor via HDMI, DisplayPort, or VGA.


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
