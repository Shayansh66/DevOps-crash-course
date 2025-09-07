# Linux & DevOps Fundamentals Guide

> **A comprehensive beginner's guide to Linux essentials and DevOps foundations**

---

## 📋 Table of Contents

1. [SSH and Remote Connections](#ssh-and-remote-connections)
2. [Linux File Hierarchy Standard (FHS)](#linux-file-hierarchy-standard-fhs)
3. [Essential Navigation Commands](#essential-navigation-commands)
4. [File Operations](#file-operations)
5. [Text Editors in Terminal](#text-editors-in-terminal)
6. [Quick Reference Tables](#quick-reference-tables)

---

## 🔐 SSH and Remote Connections

SSH (Secure Shell) is a cryptographic network protocol that allows secure remote access to Linux systems. It's an essential tool for system administrators and DevOps engineers.

### SSH Components

**Required Packages:**
- `openssh-client` - For connecting to remote servers
- `openssh-server` - For accepting incoming SSH connections

### Popular SSH Clients

| Client | Platform | Description |
|--------|----------|-------------|
| **OpenSSH** | Linux/macOS/Windows | Built-in terminal client |
| **PuTTY** | Windows | Lightweight GUI client |
| **Termius** | Cross-platform | Modern GUI with sync features |
| **MobaXterm** | Windows | Advanced terminal with X11 |

### Basic SSH Usage

```bash
# Find your machine's IP address
ip -br a

# Connect to a remote server
ssh <IP_ADDRESS>
ssh <USERNAME>@<IP_ADDRESS>

# Example
ssh john@192.168.1.100
```

> 💡 **Pro Tip:** On Windows systems, if you don't specify a username, SSH will use your current Windows username as the default.

### SSH Connection Process

1. **Host Key Verification**: First connection prompts for public key confirmation
2. **Authentication**: Enter password or use SSH keys
3. **Session Establishment**: Secure encrypted connection established

---

## 📁 Linux File Hierarchy Standard (FHS)

The FHS defines the directory structure and directory contents in Linux distributions. Understanding this hierarchy is crucial for effective system navigation and administration.

```
/
├── bin/          # Essential user binaries
├── boot/         # Boot loader files, kernel
├── etc/          # System configuration files
├── home/         # User home directories
├── root/         # Root user's home directory
├── tmp/          # Temporary files
└── var/          # Variable data (logs, caches)
```

### Key Directories Explained

| Directory | Purpose | Examples |
|-----------|---------|----------|
| **`/`** | Root directory - top of hierarchy | Everything stems from here |
| **`/home`** | User personal files and settings | `/home/john`, `/home/jane` |
| **`/bin`** | Essential executable programs | `ls`, `cp`, `mv`, `cat` |
| **`/var`** | Variable data (logs, caches, mail) | `/var/log/syslog`, `/var/cache` |
| **`/etc`** | System-wide configuration files | `/etc/passwd`, `/etc/hosts` |
| **`/tmp`** | Temporary files | Session files, temp downloads |
| **`/boot`** | Boot process files | Kernel, bootloader config |
| **`/root`** | Root user's home directory | Superuser's personal space |

> ⚠️ **Important:** The root user (`/root`) has the highest permissions with full system access. Handle with extreme care!

> 📝 **Note:** Ubuntu removes `/tmp` contents after each reboot, but policies vary across distributions.

### The "Everything is a File" Philosophy

In Linux, **everything is treated as a file** - including:
- Regular files and directories
- Hardware devices (`/dev/sda1`, `/dev/tty`)
- Process information (`/proc/cpuinfo`)
- System information (`/sys/class/net`)

---

## 🧭 Essential Navigation Commands

Master these fundamental commands to efficiently navigate the Linux filesystem.

### Core Navigation Commands

#### `pwd` - Print Working Directory
Shows your current location in the filesystem.

```bash
pwd
# Output: /home/username/Documents
```

#### `ls` - List Directory Contents
The most versatile command for viewing files and directories.

```bash
# Basic listing
ls

# Show hidden files (starting with .)
ls -a

# Detailed listing with permissions, ownership, size, date
ls -l

# Human-readable file sizes
ls -l -h

# Combine options
ls -a -l -h
```

#### `cd` - Change Directory
Navigate between directories efficiently.

```bash
# Go to specific directory
cd /var/log

# Go to home directory
cd ~
# or simply
cd

# Go to parent directory
cd ..

# Go to previous directory
cd -

# Navigate relative to current location
cd Documents/Projects
```

### Special Directory Symbols

| Symbol | Meaning | Example |
|--------|---------|---------|
| **`~`** | Current user's home directory | `cd ~` → `/home/username` |
| **`.`** | Current directory | `ls .` |
| **`..`** | Parent directory | `cd ..` |
| **`-`** | Previous directory | `cd -` |

> ⌨️ **Keyboard Shortcut:** Use `Ctrl + C` to cancel any command that's currently typing or running.

> 🎯 **Auto-completion Tip:** Type the first few letters of a file/directory name and press `Tab` for automatic completion!

---

## 📄 File Operations

### Copying Files and Directories

The `cp` command copies files and directories with various options for different scenarios.

```bash
# Copy file to new location
cp source.txt destination.txt

# Copy file to directory (keeps original name)
cp file.txt /path/to/directory/

# Copy directory recursively
cp -r source_directory/ destination_directory/

# Interactive mode (asks before overwriting)
cp -i file.txt backup.txt

# Verbose mode (shows what's being copied)
cp -v *.txt /backup/
```

### Moving and Renaming Files

The `mv` command both moves and renames files - there's no separate rename command in Linux.

```bash
# Move file to new location
mv oldfile.txt /new/path/

# Rename a file
mv oldname.txt newname.txt

# Move and rename simultaneously
mv /old/path/file.txt /new/path/newname.txt

# Interactive mode (asks before overwriting)
mv -i important.txt backup/
```

### Removing Files and Directories

The `rm` command permanently deletes files and directories.

```bash
# Remove single file
rm filename.txt

# Remove multiple files
rm file1.txt file2.txt

# Remove directory and contents recursively
rm -r directory_name/

# Interactive mode (asks for confirmation)
rm -i important.txt

# Force removal (no confirmation)
rm -f stubborn_file.txt

# Verbose mode (shows what's being deleted)
rm -v old_files.txt
```

> ⚠️ **Warning:** `rm -f` and `rm -i` are opposites! Use `-i` for safety, `-f` for force.

### Viewing File Contents

The `cat` command displays file contents in the terminal.

```bash
# Display file contents
cat filename.txt

# Show line numbers
cat -n script.py

# Show line numbers (skip empty lines)
cat -b document.txt

# Display multiple files
cat file1.txt file2.txt
```

---

## ✏️ Text Editors in Terminal

### Nano - The Beginner-Friendly Editor

Nano is perfect for beginners with its intuitive interface and helpful shortcuts displayed at the bottom.

```bash
# Open file in nano
nano filename.txt

# Open with line numbers
nano -l filename.txt
```

#### Nano Essential Shortcuts

> 📝 **Note:** The `^` symbol represents the `Ctrl` key

| Shortcut | Action |
|----------|--------|
| **`Ctrl + O`** | Save file (WriteOut) |
| **`Ctrl + X`** | Exit nano |
| **`Ctrl + K`** | Cut/delete current line |
| **`Ctrl + U`** | Paste from clipboard |
| **`Ctrl + Shift + 6`** | Mark text for selection |

### Vi/Vim - The Power User's Choice

Vim is a modal editor that's incredibly powerful once mastered. It operates in different modes for different tasks.

> 💡 **Note:** If you have Vim installed, the `vi` command will open Vim. Some systems have only `vi` (with fewer features) without full Vim.

#### Vim Modes

| Mode | Purpose | How to Enter |
|------|---------|--------------|
| **Normal Mode** | Navigation and commands | `Esc` (default mode) |
| **Insert Mode** | Text editing | `i`, `I`, `a`, `A`, `o`, `O` |
| **Visual Mode** | Text selection | `v` (character), `V` (line) |
| **Visual Block** | Column selection | `Ctrl + V` |
| **Command Mode** | File operations | `:` from Normal mode |

#### Entering Insert Mode

```bash
# Different ways to enter Insert Mode
i     # Insert before cursor
I     # Insert at beginning of line
a     # Insert after cursor
A     # Insert at end of line
o     # Insert new line below cursor
O     # Insert new line above cursor
```

#### Navigation in Normal Mode

| Key | Action |
|-----|--------|
| **`h`** | Move left |
| **`j`** | Move down |
| **`k`** | Move up |
| **`l`** | Move right |
| **`gg`** | Go to first line |
| **`G` (Shift + G)** | Go to last line |
| **`0` (zero)** | Go to beginning of line |
| **`$` (Shift + 4)** | Go to end of line |
| **`^` (Shift + 6)** | Go to first non-blank character |

#### Text Manipulation

##### Copying (Yanking)
```bash
yy        # Copy current line
y3y       # Copy 3 lines from cursor
y$        # Copy from cursor to end of line
ygg       # Copy from cursor to beginning of file
yG        # Copy from cursor to end of file
```

##### Cutting (Deleting)
```bash
dd        # Cut/delete current line
d3d       # Cut/delete 3 lines from cursor
dw        # Delete word
x         # Delete character under cursor
d$        # Delete from cursor to end of line
d^        # Delete from cursor to beginning of line
dgg       # Delete from cursor to beginning of file
dG        # Delete from cursor to end of file
```

##### Pasting
```bash
p         # Paste after cursor/below current line
P         # Paste before cursor/above current line
```

#### File Operations in Command Mode

```bash
:w        # Save file
:q        # Quit (if no unsaved changes)
:q!       # Force quit (discard changes)
:wq       # Save and quit
:x        # Save and quit (same as :wq)
ZZ        # Save and quit (from Normal mode)
```

#### Search and Replace

```bash
# Search for text
/<search_term>    # Search forward

# Examples
/function         # Search for "function"
/error           # Search for "error"
//               # Repeat last search
```

#### Undo and Redo

```bash
u         # Undo last change
Ctrl + R  # Redo last undone change
```

---

## 📊 Quick Reference Tables

### `ls` Command Options

| Option | Description | Example |
|--------|-------------|---------|
| **`-a`** | Show all files (including hidden) | `ls -a` |
| **`-l`** | Long format (detailed info) | `ls -l` |
| **`-h`** | Human-readable sizes | `ls -lh` |
| **`-t`** | Sort by modification time | `ls -lt` |
| **`-r`** | Reverse order | `ls -lr` |
| **`-S`** | Sort by file size | `ls -lS` |
| **`-R`** | List recursively | `ls -R` |
| **`--color`** | Colorize output | `ls --color=auto` |

### `cp` Command Options

| Option | Description | Example |
|--------|-------------|---------|
| **`-r`** | Copy directories recursively | `cp -r src/ dest/` |
| **`-i`** | Interactive (prompt before overwrite) | `cp -i file.txt backup.txt` |
| **`-v`** | Verbose (show copied files) | `cp -v *.txt /backup/` |
| **`-u`** | Update (copy only newer files) | `cp -u src/* dest/` |
| **`-p`** | Preserve attributes (timestamps, permissions) | `cp -p important.txt backup/` |
| **`-n`** | No clobber (don't overwrite) | `cp -n file.txt existing.txt` |

### `rm` Command Options

| Option | Description | Example | ⚠️ Warning Level |
|--------|-------------|---------|------------------|
| **`-i`** | Interactive (ask confirmation) | `rm -i file.txt` | 🟢 Safe |
| **`-f`** | Force (no confirmation) | `rm -f file.txt` | 🔴 Dangerous |
| **`-r`** | Recursive (delete directories) | `rm -r folder/` | 🟡 Caution |
| **`-v`** | Verbose (show deleted files) | `rm -v old*.txt` | 🟢 Safe |
| **`-rf`** | Force recursive deletion | `rm -rf folder/` | 🔴 Very Dangerous |

> ⚠️ **Critical Warning:** `rm -rf` can permanently delete entire directory structures without confirmation. Always double-check your command before pressing Enter!

### `cat` Command Options

| Option | Description | Example |
|--------|-------------|---------|
| **`-n`** | Show line numbers | `cat -n script.py` |
| **`-b`** | Number non-empty lines only | `cat -b document.txt` |
| **`-A`** | Show all characters (including non-printing) | `cat -A config.txt` |
| **`-s`** | Suppress repeated empty lines | `cat -s file.txt` |

### Vim Navigation Quick Reference

#### Movement Commands

| Command | Action | Mnemonic |
|---------|--------|----------|
| **`h`** | Left | **H**and points left |
| **`j`** | Down | **J**umps down |
| **`k`** | Up | **K**icks up |
| **`l`** | Right | **L**ast direction (right) |
| **`w`** | Next word | **W**ord forward |
| **`b`** | Previous word | **B**ack word |
| **`e`** | End of word | **E**nd |

#### Mode Switching

| Command | Mode | Description |
|---------|------|-------------|
| **`i`** | Insert | Insert before cursor |
| **`I`** | Insert | Insert at beginning of line |
| **`a`** | Insert | Insert after cursor |
| **`A`** | Insert | Insert at end of line |
| **`o`** | Insert | Insert new line below |
| **`O`** | Insert | Insert new line above |
| **`v`** | Visual | Character selection |
| **`V`** | Visual Line | Line selection |
| **`Ctrl + V`** | Visual Block | Column selection |
| **`Esc`** | Normal | Return to normal mode |

---

## 📚 Summary

This guide covers the essential building blocks of Linux system navigation and file management. These skills form the foundation for all DevOps activities, from server administration to deployment automation.

**Key Takeaways:**
- SSH enables secure remote system access
- FHS provides a logical structure for the Linux filesystem
- Master the trinity: `pwd`, `ls`, `cd` for navigation
- Practice file operations with safety flags first
- Choose an editor and gradually build proficiency

Remember: **Practice makes perfect!** Set up a virtual machine or use a cloud instance to practice these commands safely.

---

*Happy Learning! 🐧*