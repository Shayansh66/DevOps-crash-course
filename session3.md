# Linux & DevOps Comprehensive Guide

*A complete beginner's guide to Linux system administration and DevOps fundamentals*

---

## Table of Contents

1. [File Creation and Basic Operations](#file-creation-and-basic-operations)
2. [Text Manipulation and File Content](#text-manipulation-and-file-content)
3. [Advanced Text Processing](#advanced-text-processing)
4. [Input/Output Redirection](#input-output-redirection)
5. [Package Management](#package-management)
6. [Process Management](#process-management)
7. [System Monitoring](#system-monitoring)
8. [Best Practices and Tips](#best-practices-and-tips)

---

## File Creation and Basic Operations

### Creating Files

The `touch` command is your go-to tool for creating new empty files or updating timestamps of existing files.

```bash
# Create a single file
touch filename.txt

# Create multiple files at once
touch file1.txt file2.txt file3.txt

# Create files with different extensions
touch script.sh config.json data.csv
```

**💡 Pro Tip:** `touch` is also useful for updating file modification timestamps without changing content.

---

## Text Manipulation and File Content

### File Concatenation with `cat`

The `cat` command reads and displays file contents, and can concatenate multiple files together.

```bash
# Display single file content
cat filename.txt

# Concatenate multiple files
cat file1.txt file2.txt file3.txt

# Create a new file by concatenating others
cat header.txt content.txt footer.txt > complete.txt
```

### File Viewing with `less`

`less` is a powerful pager that allows you to view file contents in a controlled manner, especially useful for large files.

```bash
# Open a file with less
less largefile.log

# Open multiple files
less file1.txt file2.txt
```

#### `less` Navigation Commands

| Command | Action |
|---------|--------|
| `q` | Exit less |
| `Space`, `f`, `Page Down` | Move one page forward |
| `b`, `Page Up` | Move one page backward |
| `↑`, `Enter` | Move one line up |
| `↓` | Move one line down |
| `g` | Go to beginning of file |
| `G` | Go to end of file |
| `/<pattern>` | Search forward for pattern |
| `?<pattern>` | Search backward for pattern |
| `n` | Next search result |
| `N` | Previous search result |

### File Head and Tail Operations

#### `head` Command

Display the first lines of a file - perfect for previewing large files without opening them completely.

```bash
# Show first 10 lines (default)
head filename.txt

# Show first 5 lines
head -n 5 filename.txt

# Show first 20 lines of multiple files
head -n 20 file1.txt file2.txt
```

| Option | Description |
|--------|-------------|
| `-n <number>` | Specify number of lines to display |
| `-c <bytes>` | Display first N bytes instead of lines |
| `-q` | Suppress headers when multiple files |
| `-v` | Always show headers |

#### `tail` Command

Display the last lines of a file - excellent for monitoring log files.

```bash
# Show last 10 lines (default)
tail filename.txt

# Show last 20 lines
tail -n 20 logfile.log

# Follow file changes (live monitoring)
tail -f /var/log/system.log
```

| Option | Description |
|--------|-------------|
| `-n <number>` | Specify number of lines to display |
| `-f` | Follow file changes (live monitoring) |
| `-F` | Follow with retry (handles file rotation) |
| `-c <bytes>` | Display last N bytes instead of lines |

**💡 Pro Tip:** Use `tail -f` to monitor log files in real-time. This is invaluable for debugging and system monitoring.

---

## Advanced Text Processing

### Word Count with `wc`

Analyze text files by counting lines, words, and characters.

```bash
# Count lines, words, and characters
wc filename.txt

# Count only lines
wc -l filename.txt

# Count multiple files
wc -l *.txt
```

| Option | Description | Example Output |
|--------|-------------|----------------|
| `-l` | Count lines only | `150 filename.txt` |
| `-w` | Count words only | `1200 filename.txt` |
| `-c` | Count characters only | `8500 filename.txt` |
| `-m` | Count characters (multibyte) | `8500 filename.txt` |

### Sorting with `sort`

Organize file contents in various orders.

```bash
# Basic alphabetical sort
sort filename.txt

# Numerical sort
sort -n numbers.txt

# Reverse sort
sort -r filename.txt

# Remove duplicates while sorting
sort -u filename.txt
```

| Option | Description |
|--------|-------------|
| `-n` | Numeric sort (treats numbers as values, not strings) |
| `-r` | Reverse order |
| `-R` | Random order |
| `-u` | Remove duplicates (unique) |
| `-k <field>` | Sort by specific column/field |
| `-t <delimiter>` | Specify field delimiter |

### Remove Duplicates with `uniq`

Process sorted data to handle duplicate lines.

```bash
# Remove consecutive duplicate lines
sort filename.txt | uniq

# Count occurrences of each line
sort filename.txt | uniq -c

# Show only duplicate lines
sort filename.txt | uniq -d
```

| Option | Description |
|--------|-------------|
| `-c` | Count occurrences of each line |
| `-d` | Show only duplicate lines |
| `-u` | Show only unique lines (opposite of -d) |
| `-i` | Case insensitive comparison |
| `-f <n>` | Skip first N fields |

### Column Extraction with `cut`

Extract specific columns or fields from structured text.

```bash
# Extract specific columns (comma-separated)
cut -d ',' -f 1,3 data.csv

# Extract character ranges
cut -c 1-10 filename.txt

# Extract fields using tab delimiter (default)
cut -f 2-4 tabular_data.txt
```

| Option | Description |
|--------|-------------|
| `-f <list>` | Select specific fields (columns) |
| `-d <delimiter>` | Specify field delimiter (default: TAB) |
| `-c <list>` | Select specific character positions |
| `--complement` | Select all fields except specified |

### Pattern Searching with `grep`

Search for patterns in text files using regular expressions.

```bash
# Basic pattern search
grep "error" logfile.txt

# Case insensitive search
grep -i "ERROR" logfile.txt

# Recursive search in directories
grep -r "TODO" /path/to/project/

# Show only filenames with matches
grep -l "pattern" *.txt
```

| Option | Description |
|--------|-------------|
| `-i` | Case insensitive search |
| `-r` | Recursive search in directories |
| `-l` | Show only filenames containing matches |
| `-n` | Show line numbers with matches |
| `-v` | Show lines NOT matching pattern |
| `-c` | Count matching lines |
| `-A <n>` | Show N lines after match |
| `-B <n>` | Show N lines before match |
| `-C <n>` | Show N lines around match |

### Stream Editing with `sed`

Edit text streams and files using powerful pattern matching.

```bash
# Replace first occurrence per line
sed 's/old/new/' filename.txt

# Replace all occurrences
sed 's/old/new/g' filename.txt

# Edit file in-place
sed -i 's/old/new/g' filename.txt

# Delete lines containing pattern
sed '/pattern/d' filename.txt
```

| Option | Description |
|--------|-------------|
| `-i` | Edit files in-place (save changes) |
| `-n` | Suppress default output |
| `-e` | Execute multiple commands |
| `s/old/new/` | Substitute old with new |
| `s/old/new/g` | Global substitution (all occurrences) |
| `/pattern/d` | Delete lines matching pattern |

### Getting Help with `man`

Access comprehensive manual pages for any command.

```bash
# View manual for a command
man ls

# Search for commands related to a topic
man -k network

# View specific manual section
man 5 passwd
```

**💡 Pro Tip:** Use `man -k <keyword>` to find commands related to specific topics when you don't know the exact command name.

---

## Input/Output Redirection

Understanding standard channels is crucial for effective Linux administration.

### Standard Channels

| Channel | Description | File Descriptor |
|---------|-------------|-----------------|
| `stdin` | Standard Input | 0 |
| `stdout` | Standard Output | 1 |
| `stderr` | Standard Error | 2 |

### Redirection Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `>` | Redirect stdout to file (overwrite) | `ls > filelist.txt` |
| `>>` | Redirect stdout to file (append) | `echo "new line" >> file.txt` |
| `2>` | Redirect stderr to file | `command 2> errors.txt` |
| `2>>` | Redirect stderr to file (append) | `command 2>> errors.txt` |
| `&>` | Redirect both stdout and stderr | `command &> output.txt` |
| `<` | Redirect file to stdin | `sort < unsorted.txt` |
| `|` | Pipe stdout to another command | `ls | grep ".txt"` |

### Practical Examples

```bash
# Save command output to file
ls -la > directory_listing.txt

# Append to existing file
echo "$(date): System check" >> system.log

# Redirect errors only
find /etc -name "*.conf" 2> find_errors.txt

# Redirect both output and errors
gcc program.c &> compilation_results.txt

# Use input redirection
mysql -u user -p database < schema.sql
```

### The `tee` Command

`tee` allows you to both display output and save it to a file simultaneously.

```bash
# Display and save output
ls -la | tee directory_listing.txt

# Append while displaying
echo "New entry" | tee -a logfile.txt

# Multiple output files
ps aux | tee process_list.txt system_snapshot.txt
```

| Option | Description |
|--------|-------------|
| `-a` | Append to file instead of overwriting |
| `-i` | Ignore interrupt signals |

**💡 Pro Tip:** Command history can be navigated using `↑` and `↓` arrow keys. Use `Ctrl+R` for reverse search through command history.

---

## Package Management

Different Linux distributions use different package management systems.

### Distribution Families

| Distribution Family | Package Manager | Package Format | Base Commands |
|-------------------|----------------|----------------|---------------|
| Debian/Ubuntu | `apt`, `apt-get` | `.deb` | `dpkg` |
| Red Hat/CentOS/Fedora | `yum`, `dnf` | `.rpm` | `rpm` |
| SUSE/openSUSE | `zypper` | `.rpm` | `rpm` |

### APT Commands (Debian/Ubuntu)

```bash
# Update package index
sudo apt update

# Upgrade all packages
sudo apt upgrade

# Install a package
sudo apt install package_name

# Remove a package
sudo apt remove package_name

# Remove package and configuration files
sudo apt purge package_name

# Search for packages
apt search keyword

# Show package information
apt show package_name
```

### YUM/DNF Commands (Red Hat/CentOS/Fedora)

```bash
# Update package database
sudo yum update
# or
sudo dnf update

# Install a package
sudo yum install package_name
# or
sudo dnf install package_name

# Remove a package
sudo yum remove package_name
# or
sudo dnf remove package_name

# Search for packages
yum search keyword
# or
dnf search keyword
```

### Common Package Operations

| Operation | APT (Debian/Ubuntu) | YUM (Red Hat) | DNF (Fedora) |
|-----------|-------------------|---------------|--------------|
| Update package list | `apt update` | `yum check-update` | `dnf check-update` |
| Upgrade packages | `apt upgrade` | `yum update` | `dnf upgrade` |
| Install package | `apt install pkg` | `yum install pkg` | `dnf install pkg` |
| Remove package | `apt remove pkg` | `yum remove pkg` | `dnf remove pkg` |
| Search packages | `apt search term` | `yum search term` | `dnf search term` |

**🔐 Security Note:** Package management requires superuser permissions. Always use `sudo` with package management commands.

---

## Process Management

Every command and program runs as a process in Linux. Understanding process management is essential for system administration.

### Basic Process Concepts

- **Process ID (PID)**: Unique identifier for each running process
- **Parent Process ID (PPID)**: PID of the process that started this process
- **Process States**: Running, Sleeping, Stopped, Zombie

### Background Processes

```bash
# Run command in background
long_running_command &

# Run command immune to hangups
nohup long_running_command &

# Check background jobs
jobs

# Bring background job to foreground
fg %1

# Send job to background
bg %1
```

### Process Control Signals

| Signal | Number | Description | Keyboard Shortcut |
|--------|--------|-------------|-------------------|
| SIGINT | 2 | Interrupt (graceful termination) | `Ctrl+C` |
| SIGTSTP | 20 | Stop (suspend process) | `Ctrl+Z` |
| SIGTERM | 15 | Terminate (default kill signal) | - |
| SIGKILL | 9 | Kill (force termination) | - |
| SIGHUP | 1 | Hangup | - |

### Viewing Processes

#### `ps` Command

```bash
# Show current user processes
ps

# Show all processes (detailed)
ps aux

# Show process tree
ps axjf

# Show processes for specific user
ps -u username
```

| Option | Description |
|--------|-------------|
| `a` | Show processes for all users |
| `u` | Display user/owner column |
| `x` | Show processes not attached to terminal |
| `f` | Show process hierarchy (ASCII art tree) |
| `j` | Jobs format |

#### `top` Command - Interactive Process Viewer

```bash
# Launch top
top

# Launch with specific refresh interval
top -d 5
```

| Key | Action |
|-----|--------|
| `q` | Quit top |
| `k` | Kill a process (enter PID) |
| `Shift+M` | Sort by memory usage |
| `Shift+P` | Sort by CPU usage |
| `Shift+T` | Sort by running time |
| `u` | Show processes for specific user |
| `1` | Toggle individual CPU cores |

### Killing Processes

```bash
# Graceful termination (SIGTERM)
kill PID
kill -15 PID

# Force kill (SIGKILL)
kill -9 PID

# Kill by process name
killall process_name

# Kill with pattern matching
pkill pattern
```

---

## System Monitoring

### System Uptime and Load

```bash
# Show system uptime and load averages
uptime

# Show boot time
uptime -s
```

**Understanding Load Averages:**
- Three numbers represent load average for last 1, 5, and 15 minutes
- Values equal to CPU core count indicate full utilization
- Values above core count indicate system overload

### Memory Information

```bash
# Show memory usage
free

# Human-readable format
free -h

# Show in MB
free -m
```

| Column | Description |
|--------|-------------|
| `total` | Total installed memory |
| `used` | Used memory |
| `free` | Free memory |
| `shared` | Memory used by tmpfs |
| `buff/cache` | Buffer and cache memory |
| `available` | Available memory for new processes |

**💡 Memory Tip:** Focus on "available" memory rather than "free" memory. Linux uses free memory for caching, which improves performance.

### Monitoring Commands

```bash
# Monitor command output every 2 seconds
watch df -h

# Custom interval (every 5 seconds)
watch -n 5 'ps aux | head'

# Highlight differences between updates
watch -d free -h
```

### Sleep Command

```bash
# Pause for 5 seconds
sleep 5

# Pause for 2 minutes
sleep 2m

# Pause for 1 hour
sleep 1h
```

---

## Best Practices and Tips

### Command Line Efficiency

1. **Use Tab Completion**: Press `Tab` to auto-complete commands and file names
2. **Command History**: Use `↑`/`↓` arrows to navigate history, `Ctrl+R` for search
3. **Keyboard Shortcuts**:
   - `Ctrl+A`: Beginning of line
   - `Ctrl+E`: End of line
   - `Ctrl+U`: Clear line
   - `Ctrl+L`: Clear screen

### File Operations Safety

```bash
# Always backup before making changes
cp important_file.conf important_file.conf.backup

# Use -i flag for interactive mode
rm -i file_to_delete.txt
mv -i source.txt destination.txt
```

### Process Management Best Practices

1. **Graceful Termination**: Always try `kill -15` before `kill -9`
2. **Background Jobs**: Use `nohup` for long-running tasks
3. **Resource Monitoring**: Regular use of `top`, `htop`, and `ps`

### Security Considerations

1. **Principle of Least Privilege**: Don't run as root unless necessary
2. **sudo Usage**: Use `sudo` for administrative tasks
3. **File Permissions**: Understand and properly set file permissions

### Log File Management

```bash
# Monitor logs in real-time
tail -f /var/log/syslog

# Search through logs
grep "error" /var/log/messages

# Rotate logs to prevent disk space issues
logrotate /etc/logrotate.conf
```

---

## Quick Reference Summary

### Essential Commands Quick List

| Category | Commands |
|----------|----------|
| **File Operations** | `touch`, `cat`, `less`, `head`, `tail` |
| **Text Processing** | `grep`, `sed`, `sort`, `uniq`, `cut`, `wc` |
| **Process Management** | `ps`, `top`, `kill`, `jobs`, `nohup` |
| **System Monitoring** | `uptime`, `free`, `watch` |
| **Package Management** | `apt`/`yum`/`dnf`, `sudo` |
| **I/O Redirection** | `>`, `>>`, `|`, `tee` |

### Common Patterns

```bash
# Find and process files
find /path -name "*.log" | xargs grep "error"

# Monitor system resources
watch -n 1 'free -h && echo && uptime'

# Process log files
tail -f /var/log/app.log | grep -i error

# Backup and compress
tar -czf backup_$(date +%Y%m%d).tar.gz /important/directory
```

---

*This guide provides a solid foundation for Linux system administration and DevOps practices. Practice these commands regularly to build muscle memory and confidence in system management.*

**📚 Next Steps**: Explore shell scripting, advanced text processing with awk, and system administration automation to further enhance your DevOps skills.