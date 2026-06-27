# Vi & Cygwin Shell Commands Cheatsheet

---

## Vi / Vim Editor

### Modes
| Key | Action |
|-----|--------|
| `i` | Insert mode (before cursor) |
| `a` | Insert mode (after cursor) |
| `o` | Insert mode (new line below) |
| `O` | Insert mode (new line above) |
| `Esc` | Return to Normal mode |
| `v` | Visual mode (character select) |
| `V` | Visual mode (line select) |
| `Ctrl+v` | Visual block mode (column select) |
| `:` | Command-line mode |

---

### Navigation
| Key | Action |
|-----|--------|
| `h / j / k / l` | Left / Down / Up / Right |
| `w` | Jump forward one word |
| `b` | Jump backward one word |
| `0` | Go to start of line |
| `$` | Go to end of line |
| `gg` | Go to first line |
| `G` | Go to last line |
| `:n` | Go to line number n (e.g. `:25`) |
| `Ctrl+f` | Page down |
| `Ctrl+b` | Page up |
| `%` | Jump to matching bracket |

---

### Editing
| Key | Action |
|-----|--------|
| `x` | Delete character under cursor |
| `dd` | Delete (cut) current line |
| `dw` | Delete word |
| `d$` | Delete to end of line |
| `D` | Delete from cursor to end of line |
| `r<char>` | Replace single character |
| `cw` | Change (replace) word |
| `cc` | Change entire line |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last command |

---

### Copy, Cut & Paste
| Key | Action |
|-----|--------|
| `yy` | Yank (copy) current line |
| `y2y` or `2yy` | Yank 2 lines |
| `yw` | Yank word |
| `y$` | Yank to end of line |
| `p` | Paste after cursor / current line |
| `P` | Paste before cursor / current line |
| `dd` | Cut current line |
| `dw` | Cut word |
| `"ay` | Yank into named register `a` |
| `"ap` | Paste from named register `a` |

**Visual mode copy/cut/paste:**
1. Press `v` to enter Visual mode
2. Move cursor to select text
3. Press `y` to yank (copy) or `d` to cut
4. Move to destination, press `p` to paste

---

### Search & Replace
| Command | Action |
|---------|--------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `:%s/old/new/g` | Replace all occurrences in file |
| `:%s/old/new/gc` | Replace with confirmation |
| `:s/old/new/g` | Replace on current line |
| `:10,20s/old/new/g` | Replace in lines 10–20 |

---

### Split Windows
| Command | Action |
|---------|--------|
| `:split` or `:sp` | Horizontal split (same file) |
| `:sp filename` | Horizontal split with another file |
| `:vsplit` or `:vsp` | Vertical split |
| `:vsp filename` | Vertical split with another file |
| `Ctrl+w w` | Switch between windows |
| `Ctrl+w h/j/k/l` | Move to left/down/up/right window |
| `Ctrl+w =` | Make all windows equal size |
| `Ctrl+w +` | Increase window height |
| `Ctrl+w -` | Decrease window height |
| `:close` | Close current window |
| `:only` | Close all windows except current |

---

### Tabs
| Command | Action |
|---------|--------|
| `:tabnew` | Open new tab |
| `:tabnew filename` | Open file in new tab |
| `gt` | Go to next tab |
| `gT` | Go to previous tab |
| `:tabclose` | Close current tab |
| `:tabs` | List all tabs |

---

### Save & Quit
| Command | Action |
|---------|--------|
| `:w` | Save file |
| `:w filename` | Save as new filename |
| `:q` | Quit (fails if unsaved changes) |
| `:q!` | Force quit without saving |
| `:wq` or `ZZ` | Save and quit |
| `:wqa` | Save and quit all windows |
| `:qa!` | Force quit all windows |

---

### Useful Extras
| Command | Action |
|---------|--------|
| `:set number` | Show line numbers |
| `:set nonumber` | Hide line numbers |
| `:set hlsearch` | Highlight search results |
| `:set ignorecase` | Case-insensitive search |
| `:set syntax=on` | Enable syntax highlighting |
| `:!command` | Run a shell command from Vi |
| `=G` | Auto-indent entire file |
| `>>` | Indent current line |
| `<<` | Un-indent current line |

---

## Cygwin / Bash Shell Commands

### File & Directory Basics
| Command | Action |
|---------|--------|
| `ls` | List files |
| `ls -l` | List with details (permissions, size, date) |
| `ls -la` | List all including hidden files |
| `ls -lh` | List with human-readable sizes |
| `pwd` | Print working directory |
| `cd dir` | Change to directory |
| `cd ..` | Go up one level |
| `cd ~` | Go to home directory |
| `mkdir dir` | Create directory |
| `mkdir -p a/b/c` | Create nested directories |
| `rmdir dir` | Remove empty directory |
| `rm file` | Remove file |
| `rm -rf dir` | Remove directory and all contents |

---

### File Operations
| Command | Action |
|---------|--------|
| `cp src dest` | Copy file |
| `cp -r src/ dest/` | Copy directory recursively |
| `mv src dest` | Move or rename |
| `touch file` | Create empty file / update timestamp |
| `cat file` | Display file contents |
| `less file` | View file (scrollable) |
| `head file` | First 10 lines of file |
| `head -n 20 file` | First 20 lines |
| `tail file` | Last 10 lines |
| `tail -f file` | Follow file in real time (logs) |
| `wc -l file` | Count lines in file |
| `diff file1 file2` | Show differences between files |

---

### Searching
| Command | Action |
|---------|--------|
| `grep "pattern" file` | Search for pattern in file |
| `grep -i "pattern" file` | Case-insensitive search |
| `grep -r "pattern" dir/` | Recursive search in directory |
| `grep -n "pattern" file` | Show line numbers |
| `grep -v "pattern" file` | Show lines NOT matching |
| `grep -l "pattern" *.c` | List files containing pattern |
| `find . -name "*.txt"` | Find files by name |
| `find . -type f -mtime -1` | Files modified in last 1 day |
| `locate filename` | Fast file search (uses index) |

---

### Permissions
| Command | Action |
|---------|--------|
| `chmod 755 file` | rwx for owner, rx for others |
| `chmod +x file` | Make file executable |
| `chmod -r file` | Remove read permission |
| `chown user file` | Change file owner |
| `ls -l` | View permissions |

**Permission digits:** 4=read, 2=write, 1=execute (e.g. 7=rwx, 5=r-x)

---

### Processes
| Command | Action |
|---------|--------|
| `ps` | List current user's processes |
| `ps aux` | List all processes |
| `top` | Live process monitor |
| `kill PID` | Terminate process by PID |
| `kill -9 PID` | Force kill process |
| `bg` | Resume job in background |
| `fg` | Bring background job to foreground |
| `jobs` | List background jobs |
| `command &` | Run command in background |

---

### Piping & Redirection
| Symbol | Action |
|--------|--------|
| `cmd1 \| cmd2` | Pipe output of cmd1 into cmd2 |
| `>` | Redirect output to file (overwrite) |
| `>>` | Redirect output to file (append) |
| `<` | Read input from file |
| `2>` | Redirect error output |
| `2>&1` | Redirect errors to same as stdout |

**Examples:**
```bash
ls -l | grep ".txt"           # list only .txt files
cat file.txt | sort | uniq    # sort and deduplicate
grep "error" log.txt > errors.txt   # save grep results
ps aux | grep python          # find python processes
```

---

### Text Processing
| Command | Action |
|---------|--------|
| `sort file` | Sort lines alphabetically |
| `sort -n file` | Sort numerically |
| `sort -r file` | Reverse sort |
| `uniq file` | Remove duplicate adjacent lines |
| `sort file \| uniq` | Remove all duplicates |
| `cut -d',' -f1 file` | Cut field 1 from CSV |
| `awk '{print $1}' file` | Print first column |
| `sed 's/old/new/g' file` | Replace text in stream |
| `tr 'a-z' 'A-Z'` | Convert lowercase to uppercase |

---

### Networking
| Command | Action |
|---------|--------|
| `ping host` | Test network connectivity |
| `curl url` | Fetch URL content |
| `wget url` | Download file from URL |
| `ssh user@host` | SSH into remote machine |
| `scp file user@host:/path` | Copy file to remote via SSH |
| `netstat -an` | Show network connections |

---

### Compression & Archives
| Command | Action |
|---------|--------|
| `tar -cvf archive.tar dir/` | Create tar archive |
| `tar -xvf archive.tar` | Extract tar archive |
| `tar -czvf archive.tar.gz dir/` | Create gzipped tar |
| `tar -xzvf archive.tar.gz` | Extract gzipped tar |
| `zip archive.zip files` | Create zip archive |
| `unzip archive.zip` | Extract zip archive |

---

### Useful Shortcuts
| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Cancel / kill running command |
| `Ctrl+Z` | Suspend current process |
| `Ctrl+D` | Exit shell / end of input |
| `Ctrl+L` | Clear terminal screen |
| `Ctrl+A` | Go to beginning of line |
| `Ctrl+E` | Go to end of line |
| `Tab` | Auto-complete file/command name |
| `↑ / ↓` | Scroll through command history |
| `!!` | Repeat last command |
| `!grep` | Repeat last command starting with "grep" |
| `history` | Show command history |
| `clear` | Clear screen |

---

### Environment & Variables
| Command | Action |
|---------|--------|
| `echo $VAR` | Print variable value |
| `export VAR=value` | Set environment variable |
| `env` | List all environment variables |
| `PATH=$PATH:/new/dir` | Add to PATH |
| `alias ll='ls -la'` | Create command alias |
| `which command` | Show command's full path |
| `man command` | Show manual page for command |

---

*Tip: Use `man <command>` or `command --help` for detailed documentation on any command.*
