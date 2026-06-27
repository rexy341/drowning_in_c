Unix Introduction
=====================

Description
---------------------
Basic concepts of the Unix Operating System:

- What is the Operating System
- Unix Operating System
- Features of Unix
- Unix System Architecture
- Different variations/flavors of Unix
- Unix File System
- Unix Commands

Topics
---------------------

- unix
- operating-system
- unix-operating-system
- unix-shell
- unix-command
- unix-features
- unix-architecture


- Computer Basics

Index
=====================
1. [Introduction to Operating System](#1-introduction-to-operating-system)
    - 1.1. [What is OS (Operating System)?](#11-what-is-the-operating-system)
    - 1.2. [Functions of Operating System](#12-functions-of-operating-system)
    - 1.3. [Popular Operating System](#13-popular-operating-system)
2. [Introduction to Unix](#2-introduction-to-unix)
    - 2.1. [History of Unix Operating System](#21-history-of-unix-operating-system)
    - 2.2. [Features of Unix](#22-features-of-unix)
    - 2.3. [Compare different Operating System (MS-DOS, MS-Windows, Unix)](#23-compare-different-operating-system)
    - 2.4. [Difference between different Operating System (Unix, MS-DOS, MS-Windows)](#24-difference-between-different-operating-system)
3. [Unix Architecture](#3-unix-architecture)
    - 3.1. [Different flavors/variations/varieties/versions of Unix](#31-different-flavors-of-unix)
    - 3.2. [Unix System Architecture-Structure](#32-unix-system-architecture-structure)
      - 3.2.1. [Kernel](#321-Kernel)
      - 3.2.2. [Shell](#322-shell)
      - 3.2.3. [Programs](#323-programs)
4. [Unix File System](#4-unix-file-system)
    - 4.1. [What is File?](#41-what-is-file)
    - 4.2. [Directories and Sub-directories](#42-directories-and-sub-directories)
    - 4.3. [Types of Files](#43-types-of-files) | [File System in Unix](#43-file-system-in-unix)
    - 4.4. [Representation of File Types](#44-representation-of-file-types)
    - 4.5. [Rules for Naming a File Directory](#45-rules-for-naming-a-file-directory)
    - 4.6. [Terms used in a directory](#46-terms-used-in-a-directory)
    - 4.7. [Types of Path Name](#47-types-of-path-name)
5. [Unix Command](#5-unix-command)
    - 5.1. [What is command?](#51-what-is-command) | [Unix Command usage](#51-unix-command-usage)
    - 5.2. [Rules of using Unix Commands](#52-rules-of-using-unix-commands)
    - 5.3. [Types of Unix Commands](#53-types-of-unix-commands)
    - 5.4. [cal](#54-cal)
    - 5.5. [date](#55-date)
    - 5.6. [history](#56-history)
    - 5.7. [banner](#57-banner)
    - 5.8. [who](#58-who)
    - 5.9. [fg](#59-fg)
    - 5.10. [ls](#510-ls) | [Listing Files](#510-listing-files)
6. [Unix vs Linux](#6-unix-vs-linux) | [Difference between Unix and Linux](#6-difference-between-unix-and-linux)
    - 6.1. [What is Linux?](#61-what-is-Linux)
    - 6.2. [Unix vs Linux](#62-unix-vs-linux)

   
1 Introduction to Operating System
=====================


1.1. What is the Operating System?
---------------------


- OS (Operating System) is a set of programs/package acts as an intermediary/interface between computer software, end-user and computer hardware
- An operating system (OS) is a collection of `system software` that manages `computer hardware, software resources`, and provides common services for computer programs
- Programs which helps to manage/communicate between software and hardware (low-level software manages hardware by controlling the execution of programs)
- Core/brain/heart of machine's/device's software and provide an environment to execute programs
- OS (Operating System) controls the allocation of resources and services such as (Memory, Processor, Devices, Information, controlling attached devices/peripherals)


1.2. Functions of Operating System
---------------------

**List of important functions performed by an Operating System**:

- Co-ordination between Software and Hardware
- Memory Management
- Device Management
- Processor Management
- Security
- Error detection
- Co-ordination between User and Software
- Control over system performance
- Task/Internal Job scheduling
- File Management

1.3. Popular Operating System
---------------------

**Popular and widely used Operating Systems (OS) - Some popular Operating Systems include**:

- Unix
- DOS
- Microsoft Windows
- macOS (Apple mac)
- Linux (Unix clone)
- Android (Mobile OS)
- iOS (Apple Mobile OS - iPhone, iPad, iPod)

1.4. Boot Process Of Operating System
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
**Note 1.4.1: Key Variations: Cold Boot vs. Warm Boot**

- Cold Booting (Hard Boot): Occurs when you power on a device from a completely turned-off state. The machine performs the full routine, including mandatory POST diagnostics and total hardware initialization.
- Warm Booting (Soft Boot): Occurs when you trigger a software restart without cutting the electrical power supply. It speeds up the loading process by bypassing structural hardware checks and some POST sequences.

**Note 1.4.2: How does POST produce screen alerts or audio alerts if the OS has not been loaded yet?**

The Power-On Self-Test (POST) can communicate without an operating system because it relies entirely on firmware and low-level hardware standards that are hardcoded into your computer's components.Before the OS ever loads, the motherboard's BIOS/UEFI acts as a temporary, mini-operating system.

1. *How POST Accesses Sound (Beep Codes)*

- Direct Hardware Control: The motherboard features a tiny, dedicated physical speaker (the piezo speaker) or a buzzer wired directly to the chipset.
- No Drivers Needed: The BIOS/UEFI contains primitive assembly language instructions to send electrical pulses directly to this buzzer at specific frequencies.
- The Result: If the RAM or video card fails to initialize, the firmware triggers specific patterns of short and long electrical pulses (e.g., one long and two short beeps) to tell you exactly what hardware failed.

2. *How POST Accesses the Screen (Display)*

- VGA Legacy Standards: Long before modern graphics drivers load, all video cards (Nvidia, AMD, or Intel integrated graphics) are hardcoded to support an ancient, universal standard called VGA (Video Graphics Array) mode.
- Video BIOS (VBIOS): The graphics card has its own tiny onboard firmware chip. During the first split-second of booting, the main motherboard firmware locates and executes this Video BIOS.
- Basic Text Output: The VBIOS initializes the graphics processor just enough to accept basic, unaccelerated text and simple graphics. It bypasses complex display pipelines and pipes basic pixels straight to your monitor via HDMI, DisplayPort, or VGA.


2 Unix OS
=====================

2.1. History of Unix Operating System
---------------------

- Unix is developed by `Ken Thompson` and `Dennis Richie` at `AT&T Bell Laboratories Research Center, USA` in the year `1969`
- Unix is multi-user, multi-tasking, and multi-processing, high-function, interactive Operating System
- Unix is terminal ie. command prompt based `Command Line Interface/Interpreter (CLI)`, UNIX system also have a `Graphical User Interface (GUI)` similar to Microsoft Windows which provides an easy to use environment
- Initially, Unix was written in Assembly language, First Operating System is written in HLL ie. High-Level Language (C)
- Originally Unix is spelled as `UNICS (Uniplexed Information Computing System/Service)`
- Later Unix is re-written in `C` language and renamed as `Unix`
- Some of Unix OS ie. distributions are Free (Open Source - Linux) and some are not free (license needed)

2.2. Features of Unix
---------------------

**Mentioned below the features and capabilities supported by Unix Operating System**:

- Multi-user capability
- Multi-tasking
- Multi-process
- Hierarchical File Structure / Hierarchical File System
- Open Source System
- Portability
- Programming Utility/Facility
- Communication Facility
- Security
- Tools and Utilities
- Piping (Pipes & Filters)
- Help Facility - Integrated Help
- Modularity
- Unix Shell<br/><br/>
- **Multi-user capability**
  - Multiple ie. many users can use the machine simultaneously supported via terminals/command prompt
- **Multi-tasking**
  - Multiple programs can be run at a time
- **Multi-process/Multi-processing**
  - Each user can execute multiple/many/several processes simultaneously
- **Hierarchical Structure**
  - Unix directories/folders system are present like a tree structure to support, organize and maintain files
- **Open Source System**
  - Some of Unix OS ie. distributions are Free (Open Source - Linux), users can modify source code as per needs and requirements
- **Portability**
  - Unix allows users to transfer data/information/files/folders from one system to another
- **Programming Utility/Facility**
  - Unix Shell can be used as a Programming/Scripting Language
- **Communication Facility**
  - Communication between different users is possible by using/sharing some information
- **Security**
  - Unix Operating System provides System-level security controlled by the system administrator and file-level security controlled by the owner of the file/folder
- **Tools and Utilities**
  - Supports/provide many useful tools/software/utilities used for software development
- **Piping**
  - The output of the current command can be used as an input of next command/process (last-current-next process/command can be linked/chained)
- **Help Facility - Integrated Help**
  - Unix `man` command is used to get/view any command help
- **Modularity**
  - Unix Operating System consists of multiple independent modules/programs/utilities which perform a specific task
- **Unix Shell**
  - Unix Shell a command interpreter that helps to interact with Unix OS ie the Kernel. (Shell takes input/command from a user and executes programs-run command)
  
2.3 Different Operating System
---------------------

**Similarity between Unix and MS-DOS**:

- `Command Line Interface CLI` / Command Terminal Window / Command Prompt
- `I/O (Input Output)` redirection concepts
- `Hierarchical directory` structure (Root directory at the top)
- Read-Write (RW) and execute permissions on files/folder
- Wildcard Character support

**Similarity between Unix and MS-Windows**:

- `Graphical User Interface (GUI) `
- `Multi-tasking` Operating System
- Built-in networking with `TCP/IP` as the standard protocol

2.4. Difference between different Operating System
---------------------

**Difference between Unix and MS-DOS**:

| Unix                               | MS-DOS                            |
| ---------------------------------- | --------------------------------- |
| Unix can have a `GUI (Graphical User Interface)   `                      | MS-DOS does not have a GUI, it is Terminal or Commands base, `CLI (Command Line Interface) `                                                        |
| Unix is `case-sensitive `                                                | DOS is `case-insensitive (NOT case sensitive)`                         |
| Unix is a `Multi-User`, `Multi-Tasking` and `Multi-Process` Operating System | DOS is a `Single-User`, `Single-Tasking` and `Single-Process` Operating System |
| Unix uses `forward slashes (/)` to separate directories                | DOS uses `backslashes (\)` to separate directories                       |
| Unix is mainly used in Servers                                         | DOS is used in Embedded Systems                                          |
| Unix OS uses concepts like Process priorities                          | DOS does NOT use concepts like Process priorities                       | 
| Unix has a `Shell Script`                                                | MS-DOS has a `Batch files`                                             |
| | |

**Difference between Unix and MS-Windows**:

| Unix                               | MS-Windows                        |
| ---------------------------------- | --------------------------------- |
| Unix is a `CUI (Command User Interface)` OS, it can have GUI             | Windows is a `GUI (Graphical User Interface)` OS                       |
| Unix is a` Multi-User` and `Multi-Tasking` OS                          | MS-Windows is a `Single-User` and `Multi-Tasking` OS                     |
| Unix is `case-sensitive`                                                 | MS-Windows is `case-insensitive` (NOT case sensitive)                  |
| Unix is `NOT User friendly as it is not full of GUI` (Graphical User Interface)                                                               | Windows is `User friendly as its fully GUI` based                        |
| Unix is `free, Open Source`, No license needed                           | Windows is a `licensed` OS |
| Unix `supports programming` facility                                   | Windows `do not supports` programming facility                           |
| Unix file system is a `Hierarchical` Model                             | Windows file system is a `Flat` Model |
| Unix has a `dumpty terminals (without HDD Hard Disk)`                  | Windows do not support dumpty terminals                                  |
| Unix is `open source but has many/multiple vendors`, who takes source code add models and create modules/variations/versions/distributions     | Windows have only one owner/vendor ie. `Microsoft Corporation`           |
|  | |

3 Unix Architecture
=====================

3.1. Different flavors of Unix
---------------------

There are many ie. different flavors/variations/variety/versions of UNIX available in the market, although they share common similarities. The most popular varieties of UNIX are Sun Solaris, GNU/Linux, and macOS X:

| Vendor/Organization       | Unix OS flavors/variations/variety  |
| ------------------------- | -------------------------- |
| Amdahi Corporation        | UTS  |
| AT&T                      | Vr4, BSD Unix, DEC Unix, macOS X, SCO Unix |
| Compaq                    | Tru64Unix    |
| HP                        | HP-UX  |
| IBM                       | AIX |
| Microsoft                 | Xenix  |
| Red Hat                   | Linux |
| SGI (Silicon Graphics) | TRIX  |
| SCO (Santa Cruz Operation) | SCO Unix |
| Sun                       | Solaris |
|                           | Ubuntu  |
|                           | Fedoro |
|                           | Novell |
|                           | Xubuntu |
|                           | Kubuntu |
|                           | XandOS  |
|                           | Lunar |
|                           | FreeBSD |
|                           |  |

3.2. Unix System Architecture-Structure
---------------------

An operating system is a collection of software, each designed for a specific function. Here is a basic block diagram of a Unix system Architecture-Structure:


> #### Hardware (Physical Devices)
- The Hardware layer of the Unix Operating System controls the use of physical system resources, such as memory manager, process manager, disk drivers, devices, and so on
- The hardware consists of all input and output peripheral devices (RAM, HDD, CPU and so on)

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

### 3.2.1. Kernel

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

### 3.2.2. Shell 

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

### 3.2.3. Kernel - Shell Layered Architecture

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

**Note 3.2.3.1: Architectural Design Rationale**

*Why the Kernel Decouples Line input*

- **Canonical Editing Support (Line Discipline):** By storing text inside a kernel-managed buffer before handing it over to the user application, the OS natively supports input correction. When a user presses Backspace (`0x7F` or `0x08`), the TTY subsystem catches it, deletes the preceding character from the kernel input queue, and moves the screen cursor back. 
- **Efficiency:** If the system did not use line buffering, every single character typed would force the shell to execute evaluations instantly. Line buffering ensures user space applications only wake up and utilize CPU clock cycles when a fully complete command packet is ready for computational processing.


### 3.2.4. Programs 

- Utility programs and applications are given by the user are handled in this layer
- The commands are themselves called as programs in Unix
- There are various commands and utilities which you can make use of in your day to day activities. `cp, mv, cat` and `grep`, etc.
- Data in Unix are organized into files and files are organized into directories which are further organized into a tree-like structure called as the `file system`

4 Unix File System
=====================

This section will be discussing file management in Unix. We will dive deep into Unix File System - what exactly is the file? Unix file structure, types of files, along with directories and sub-directories.

4.1. What is File?
---------------------

`All data in Unix is organized into files`. All files are organized into directories. These directories are organized into a tree-like structure called the filesystem.

The file system is central to how Unix organizes information, and all the information that needs to be stored and retrieved uses the file system.

When you work with Unix - one way or another, you spend most of your time working with files. This tutorial will help you understand how to create and remove files, copy and rename them, create links to them, etc.

- The file is a `container for storing content, records or details, information`
- `Everything in Unix is considered as a File, including physical devices such as USB devices, CD Drives, DVD-ROMs, Floppy Disk Drives (FDD)` and so on
- Input and Output (I/O) devices are also considered to be files in Unix System
- Every file in the file system has a unique name with a `unique inode number`
- Files in the Unix system grouped into directories, same as folders in Windows environment
- On a Unix system, everything is a file, if something is not a file - it is a `process`
- File attributes are kept in a separate location in the disk, example - programs, services, texts, images and so on

4.2. Directories and Sub-directories
---------------------
- `Directory or Folder within a directory is called a Sub-directory`
- `Each directory can contain multiple directories/folders (called as sub-directories/sub-folders) and/or files (tree structure)`
- In the Unix/Linux operating system, a directory is also a file containing the names of other files
- The structure of directories having sub-directories along with files are called as tree recursive structure
- All type of operations are possible for directories and files such as create, delete, copy, move, link, print, spit, and so on
- A directory can be a file, but a file cannot be a directory since the file contains the information/records (metadata) and directory contains sub-directories and files

4.3. Types of Files
---------------------
4.3. File System in Unix
---------------------

Data in Unix are organized into files and the files are further organized into directories.

The main file types in UNIX are (In Unix, there are three basic types of files):
- Regular or Ordinary File
- Directory file
- Device or Special File
  - Raw or Character Device File
  - Block File
  - Named Pipes or FIFO
  - Link
  - Socket

### 4.3.1. Regular or Ordinary File
> Regular or Ordinary File

- `An ordinary or Regular Files is a file on the system that contains data, text, or program instructions/executable programs`
- Executable programs are the commands (`ls`, `pwd`) or scripts (`a.sh`, `setup.sh`) that we enter on the prompt
- Data can be anything, there is `no specific format enforced` in the way data is being stored
- Ordinary Files contain `ASCII (human-readable)` text, executable program binaries, program data, and much more information
- A regular file is the one that is not a directory or link, It is called as `regular` since there is nothing special about it
- Directories are organized into a tree-like structure called `files system`
- Regular files can be `visualized as the leaves in the Unix tree`

### 4.3.2. Directory file
> Directory file

- Directories are files that `contain other files and sub-directories`
- Directories store both special and ordinary files, For Windows or Mac OS users, Unix directories are equivalent to folders (Directories are just like folders in Windows operating system)
- Directories are used to organize the data by keeping closely related files all at the same place
- Kernel alone can write the directory file. When a file is added or deleted from the directory, the kernel will make an entry
- A directory is a binary file used to track and locate other files and directories
- The binary format is used so that directories containing large numbers of filenames can be searched quickly
- In a directory file, we cannot directly keep contents, records, or any information
- A directory file can be `visualized as a branch of the Unix tree`

### 4.3.3. Device or Special File
> Device or Special File

- Device or special files `represent the physical devices`
- They are used for the device I/O on Unix and Linux systems (external USB drives)
- They appear in the file system just like an ordinary file or a directory
- This type of files allow access to various devices known to the system
- Some special files provide access to hardware such as CD-ROM drives, Tape, Disc/Hard drives, Players, Modems, Ethernet Adapters, Network Interfaces, Scanners, Printers, Terminals and so on
- Other special files are similar to aliases or shortcuts and enable you to access a single file using different names
- When a process writes to a special file, the data is sent to the physical device associated with it
- Special files are not exactly files but are pointers that point to the device drivers located in the kernel
- Protection applicable to files are also applicable for physical devices

> Raw or Character Device File
  - When a character special file is used to the device I/O, `data is transferred one character at a time`
  - This type of access is called raw device access and is present in `/dev`
  - Provides a serial stream of input or output
  - Example - `Terminals`

> Block File
  - Block special file is used for the device I/O, `data is transferred in large fixed-sized blocks`
  - These files are hardware files, most of which are present in `/dev`

> Named Pipes or FIFO
  - The pipe is also called as `Named Pipe` or `FIFO (First In First Out)`
  - Pipes represent one of the simpler forms of Unix Inter-Process Communication
  - The purpose of `Pipe` is to connect I/O of two Unix processes accessing the pipe,  one of the processes uses it for output while the other one uses it for input

> Link
  - it is used for `referencing some other file of the filesystem along with the path to the referenced file`
  - They are either directory or regular file

> Socket
  - A socket file is used to `pass information between applications for communication purpose`
  - We can create a socket file by using `socket()` system call 
  - A UNIX socket also called `IPC socket (Inter-Process Communication socket)`, is a special file that allows for advanced Inter-Process Communication
  - It is similar to network stream/sockets, and all the transactions are local to the filesystem

4.4. Representation of File Types
---------------------
Given below is a table that lists the character representation for each type of files:

| Representation                     |      File Type                       |
| ---------------------------------- | ------------------------------------ |
| -                                  | Ordinary or Regular file              |
| D                                  | Directory                            |
| C                                  | Character Special File               |
| B                                  | Block special File                   |
| L                                  | Symbolic link                        |
| P                                  | Named pipe                           |
| S                                  | Socket                               |
|                                    |                                      | 

```

File types can be determined by using a `file` command

Syntax: $ file filename, 
        $ file *

```

```

ALIPL1008:resources dinanath$ file _1_html-proforma.html

_1_html-proforma.html: HTML document text, ASCII text

```

```

ALIPL1008:resources dinanath$ file *

_1_html-proforma.html:                            HTML document text, ASCII text
_1_notes-proforma.md:                             ASCII text
agile:                                            directory
bootstrap:                                        directory
cloud-computing:                                  directory
devops:                                           directory

```

4.5. Rules for Naming a File Directory
---------------------

File/Directory has a name by which it is identified on the system

Given below are the general rules to be followed for naming a file or a directory:

- The length of a filename should be upto `255 characters/bytes` with combinations of any characters or numbers without givin space or tab
  - File and directory name should not contain any special characters as mentioned below:
    - List of special characters not allowed/used in file/directory naming convensions: ` ~ ! @ # $ % ^ & * ( ) [ ] + = { } | [ ] \ < > ? , . / ; ' : "`
    - `Dash -` or `Underscore _` symbol is used to separate logical words
      > example: file-name.txt, file_name.txt
    - `DOT .` symbol is used to separate a file type extension/the last name
    - File names are case-sensitive, so it can be with the upper case as well as lower case
    - A file or a directory name should not be any UNIX command name
    - The filename starts with a `DOT .` will be a hidden file
    - File names must be unique inside the directory
    - Files and directories should be arranged hierarchically as per the requirements in a tree like-structure

4.6. Terms used in a directory
---------------------

Following are the terms used in a directory:
- Root Directory
- Home Directory
- Current or Present Directory
- The parent or Previous Directory

> Root Directory
  - `Root Directory is the apex/origin directory`
  - In Unix and Unix-like operating systems, the root directory is the `first or top-most directory in a hierarchy`
  - The root directory is a topmost directory, no directory exists above the root directory
  - It is represented by `forward slash /` symbol

> Home Directory
  - `It is the base or login directory provided to the user`
  - `Name of a home directory is usually same the user's login name (login id or user name)`
  - It is the directory on Unix-like operating systems that serves as the repository for a user's personal files, directories, and programs
  - Every user has a home directory
  - In environment variables, `$HOME` is used for displaying the path of the home directory
  - Home Directory is represented by `tilde ~` symbol

> Current or Present Directory
  - Current or Present Directory is a directory in which a `user is currently working in`
  - Command `pwd` is used for displaying the current directory path

> Parent or Previous Directory
  - The parent or previous directory is `one level higher than the current directory`
  - Every directory has a present directory expect the root directory
  - It is represented by `two executive dots ..` symbol
  - Command `cd ..` is used to go to one level up ie Parent or Previous Directory

4.7. Types of Path Name
---------------------

1. Absolute/Full Path
2. Relative/Reference Path
> Absolute/Full Path
  - The pathname that `starts with the root directory` `/` is called Absolute/Full Path (it starts with `c:/`, `d:/` or so on, its hardcoded/static full path)

> Relative/Reference Path
  - Relative path name `begins with the current directory or home directory`
  - A relative path can begin with `..` or `.` for the current directory (its reference path from current directory/location)
  
5 Unix Command
=====================

This section will discuss about UNIX commands - what is a command?, what structure we need to follow while using some of the basic Unix commands. Also will see and use some basic/essential Unix commands:

5.1. What is command?
---------------------
5.1. Unix Command usage
---------------------

- In Unix, a command is a `program that can be executed/run` 
- Basic step is: `Type any Unix command` and then `Press Enter key`
- For Windows and MAC operating system we can resembles command like a `point to the program icon that needs to run by double-clicking on it`

5.2. Rules of using Unix Commands
---------------------
- Unix command may or may not have arguments or parameter (extra options provided with the command)
- An argument can be an option or a filename
- All Unix commands always must be entered in `small case letters (lower case letters)`
- The general format for a Unix command is: `command options(s) filename(s)`
- The option is usually preceded by a `dash OR minus OR -` sign  
- Two or more options available with a command can be combined easily, like this: `ls -l -a OR ls -la`
- There must be a space or tab between the command name and options

5.3. Types of Unix Commands
---------------------

Here is a type of Unix Commands:

- Simple Command
- Complex Command
- Compound  Command

> Simple Command
- A simple command is a `common command` that can be executed by providing the command name in the command prompt
- Example: `date`, `cal`, `who`

> Complex Command
- A Complex command consists of a `command name with a list of arguments that together acts as a single command`
- Example: `who am i`

> Compound Command
- A Compound Command consists of a `list of simple and/or complex commands separated by command separator, semicolon (;)` which indicates where does a command end and begin
- Example: `date; who am i; cal`

5.4. cal
---------------------
- `cal` = `calendar`
- The `cal` command/utility `displays a simple calendar in a traditional format`
- cal command is used to display the current month's calendar
- The `ncal` command offers an alternative layout, more options and the date of Easter
- Example: 
  - command: `cal 3 2020` displays the calendar of month March 2020
  - command: `cal -y` displays calendar for complete/entire year

```

ALIPL1008:~ dinanath$ cal

     April 2020       
Su Mo Tu We Th Fr Sa  
          1  2  3  4  
 5  6  7  8  9 10 11  
12 13 14 15 16 17 18  
19 20 21 22 23 24 25  
26 27 28 29 30        

```

```

ALIPL1008:~ dinanath$ ncal

    April 2020        
Mo     6 13 20 27   
Tu     7 14 21 28   
We  1  8 15 22 29   
Th  2  9 16 23 30   
Fr  3 10 17 24      
Sa  4 11 18 25      
Su  5 12 19 26  

```

```

ALIPL1008:~ dinanath$ cal 3 2020

     March 2020       
Su Mo Tu We Th Fr Sa  
 1  2  3  4  5  6  7  
 8  9 10 11 12 13 14  
15 16 17 18 19 20 21  
22 23 24 25 26 27 28  

```

5.5. date 
---------------------

- date command disp`lay date in different formats and/or set system date and time`
- The date utility displays the date and time read from the kernel clock
- When used to set the date and time, both the kernel clock and the hardware clock are updated

```

ALIPL1008:~ dinanath$ date
Sun Apr 26 18:59:56 IST 2020

```

5.6. history
---------------------

- `history` command displays the history ie. `list of the commands used/executed previously`/in the past with line numbers
- The option `-c` clears the history list by deleting all the entries

```

ALIPL1008:~ dinanath$ history
    9  git status
   10  git pull qa
   11  git pull origin qa
   12  git status
   13  git pull origin qa
   14  clear

```

5.7. banner 
---------------------

- `banner` command `prints a  high-resolution text banner on the system console or printer`
- Banner prints a large, high-quality banner on the standard output
- The output should be printed on paper of the appropriate width, with no breaks between the pages

```

ALIPL1008:~ dinanath$ banner WELCOME

```

5.8. who
---------------------

- The `who` command `display the user details who is logged in`
- `who` command `displays data about all the users who have currently logged into the system `
- The who utility `displays a list of all users currently logged on`, showing for each user the login name, tty name, the date and time of login, and hostname if not local
- `who am i` command displays the effective `username of the current user`

```

ALIPL1008:~ dinanath$ who
dinanath console  Apr  6 18:06 
dinanath ttys001  Apr 27 20:33 


ALIPL1008:~ dinanath$ who am i
dinanath ttys001  Apr 27 20:33 

```

5.9. fg
---------------------
- The `fg` command is used to `stop/cancel all the jobs running in the terminal (in the background)`
- Usually, `fg` command is used just before `exit` command (so that all unwanted jobs canceled and one can exit from terminal easily)
- If `exit` command responds with the message `"There are stopped jobs"` than it is advisable to enter `fg` command and then again enter `exit` command to get out of command window/terminal/prompt/bash

5.10. ls
---------------------
5.10. Listing Files
---------------------

- `ls` command is used to list the files and directories stored in the current directory

Here is the sample output of the `ls` command:

```

ALIPL1008:~ dinanath$ ls

Applications	Downloads	  Music       VirtualBox VMs
Desktop		    Library		  Pictures    mongo
Documents	    Movies		  Public      mongo-data

```

The command `ls` supports the `-l` option which helps you to `get more information about the listed files`

```

ALIPL1008:~ dinanath$ ls -l
total 192

drwxr-xr-x  15 dinanath  staff    480 Jun 16  2019 _examples-angular6-1-demo
drwxr-xr-x  37 dinanath  staff   1184 Jun 14  2019 _images_angular7
-rw-r--r--@  1 dinanath  staff  95050 Jul 23  2019 _notes_angular7.md

```

6 Unix vs Linux
=====================
6 Difference between Unix and Linux
=====================

In this section/module will find head to head differences and similarities between Unix and Linux

6.1. What is Linux?
---------------------

- Linux OS is built by `Linus Torvalds` in the year 1991
- The name `Linux` assigned/came from the `Linux Kernel`
- Linux is an open-source, free to use (Community Developed) operating system widely used for Computer Hardware and Software, Game Development, Tablet PCs, Mainframe computers, etc.
- Linux is replica or duplicate of Unix but does not use the actual source code of Unix

6.2. Unix vs Linux
---------------------

| Unix                               |      Linux                       |
| ---------------------------------- | ------------------------------------ |
| **Use**: <br/> The Unix OS can be used at Internet Servers, Workstations and PCs                              | <br/> Linux is used by Everyone! from Home users to developers and computer enthusiasts like as Linux can be installed easily on any devices                |
| **Development and Distribution**: <br/> Unix systems are mostly developed by AT&T (Bell Laboratories) and various commercial vendors and non-profit organizations                        | Linux is developed by Open Source development community and distributed by various vendors |
| **Architecture**: <br/>  Unix is available on PA-RISC and Itanium machines                             | <br/> Originally developed for Intel's x86 hardware, ports available for several CPU types |
| **Processor**: <br/> Unix supports x86/x64, Sparc, Power, Itanium, PA-RISC, PowerPC, and many others              | Linux has a wider variety of processors!  Several kinds of processors are used                            |
| **File System Support / Supported File Types**: <br/> Unix supports:  `jfs, gpfs, hfs, hfs+, ufs, xfs, zfs and vsfs file formats/systems`  | Linux supports:  `xfs, nfs, ufs, Ex2 to Ex4, jfs, ReiserFS and NTFS etc`  |
| **Shell Interface**: <br/> Unix originally made to work in BASH (Bourne Again SHell), supports multiple command interpreters  | Linux originally made to work in BASH (Bourne Again SHell), Now it is compatible with many including BASH, Karn and C   |
| **GUI Graphical User Interface**: <br/>  Unix initially was a Command based OS, but now it also comes with GUI knows as `Common Desktop Environment` and `Gnome`  | Linx provides two GUIs like `KDE and Gnome, But have many such as LXDE, Xfce, Unity, Mate, TWM` etc.  |
| **License and Pricing**: <br/> Different flavors of Unix have different cost/pricing structures as per the vendors  | <br/> Linux is freely distributed and downloaded through varieties of Magazines, Books and websites, etc. There are some paid versions also but pretty cheaper than windows OS  |
|                                    | |
