# Room 1: Linux Fundamentals - Commands Cheatsheet

Quick reference guide for all commands covered in Room 1. Print or bookmark for terminal practice.

---

## User & System Commands

### `whoami`
Identify the currently logged-in user.

```bash
whoami
# Output: tryhackme
```

**Use case:** Verify you're logged in as the correct user before making system changes.

---

## Output Commands

### `echo`
Output text to the terminal (or redirect to files).

```bash
echo Hello                          # Single word
echo "Hello Friend!"                # Multiple words (use quotes)
echo TryHackMe > output.txt        # Redirect to file
```

**Variations:**
- `echo -n "text"` — print without newline
- `echo "line1" >> file.txt` — append to file

---

## Navigation & Listing

### `pwd`
Print current working directory (show full path).

```bash
pwd
# Output: /home/ubuntu/Documents
```

**Use case:** Always confirm your location before running destructive commands.

---

### `ls`
List directory contents.

```bash
ls                          # List current directory
ls Pictures                 # List specific directory
ls /home/ubuntu/Documents   # List by full path
ls -la                      # List with file details (covered in Part 2)
```

**Output example:**
```
Important Files  My Documents  Notes  Pictures
```

---

### `cd`
Change directory (navigate).

```bash
cd Pictures                 # Enter Pictures directory
cd ..                       # Go up one level (parent directory)
cd ../..                    # Go up two levels
cd ~                        # Return to home directory
cd /home/ubuntu/Documents   # Jump to specific path
cd -                        # Return to previous directory
```

**Pro tip:** `cd` without arguments returns to home directory.

---

## File Operations

### `cat`
Display file contents.

```bash
cat filename.txt                      # View single file
cat Documents/notes.txt               # View file in subdirectory
cat /home/ubuntu/Documents/todo.txt   # View by full path
cat file1.txt file2.txt              # View multiple files
```

**Output example:**
```
Here's something important for me to do later!
```

---

## File Searching

### `find`
Search for files by name.

```bash
find -name passwords.txt              # Search by exact filename
find -name *.txt                      # Search by pattern (all .txt files)
find -name *.log                      # Find all log files
find /var/log -name *.log            # Search from specific path
find -name "*backup*"                 # Search for filename containing "backup"
```

**Output example:**
```
./folder1/passwords.txt
./Documents/todo.txt
```

**Sysadmin example:**
```bash
find /etc -name "*.conf"              # Find all config files
find /home -name "*.ssh"              # Find SSH directories
```

---

### `grep`
Search within file contents.

```bash
grep "search_term" filename.txt                 # Basic search
grep "81.143.211.90" access.log                 # Find specific IP in logs
grep "error" /var/log/syslog                    # Find errors in system logs
grep -i "ERROR" logfile.txt                     # Case-insensitive search
```

**Output example:**
```
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417
```

**Sysadmin examples:**
```bash
grep "Failed password" /var/log/auth.log        # Find failed logins
grep "CRITICAL" /var/log/application.log       # Find critical errors
grep "192.168" access.log                       # Find internal IP activity
```

---

## Shell Operators

### `&` — Background Execution

Run command in background (frees terminal for other tasks).

```bash
command &
cp large_file.iso backup.iso &
long_running_process &
```

---

### `&&` — Logical AND (Chain Commands)

Run second command only if first succeeds.

```bash
command1 && command2
cd Documents && ls                    # List only if cd succeeds
mkdir backup && cp file backup/       # Copy only if mkdir succeeds
```

---

### `>` — Redirect Output (Overwrite File)

Send output to file, **replacing** existing contents.

```bash
echo "text" > filename                # Create/overwrite file
command > output.txt                  # Redirect command output
cat source.txt > destination.txt      # Copy file contents via redirection
```

**⚠️ Warning:** Existing file contents are lost!

**Examples:**
```bash
echo "password123" > passwords        # Quiz answer example
whoami > current_user.txt             # Save username to file
find -name *.log > logfiles.txt       # Save search results
```

---

### `>>` — Redirect Output (Append to File)

Send output to file, **adding** to existing contents.

```bash
echo "text" >> filename               # Append to existing file
command >> output.txt                 # Append command output
```

**Examples:**
```bash
echo "hello" >> welcome               # Add line to file
echo "tryhackme" >> passwords         # Quiz answer example
grep "error" logfile.txt >> errors.txt # Append matching lines
```

---

## Combined Examples (Multi-Step Workflows)

### Example 1: Find and Filter Logs
```bash
find /var/log -name access.log > found_logs.txt && grep "error" found_logs.txt >> errors.txt
```
1. Find access.log files
2. Save results to found_logs.txt
3. Search for "error" within those logs
4. Append matches to errors.txt

### Example 2: Create and Populate File
```bash
echo "Configuration data" > config.txt && echo "Added: $(date)" >> config.txt
```
1. Create config.txt with initial data
2. Append timestamp to it

### Example 3: Background Backup + Continue Work
```bash
cp -r /home/ubuntu /backup/ubuntu-backup &
ls -la /home                            # This runs while backup continues
```

---

## Context: When to Use Which Command

| Task | Command |
|------|---------|
| Know where you are | `pwd` |
| See what's here | `ls` |
| Go somewhere | `cd` |
| Read a file | `cat` |
| Find a file | `find -name` |
| Search in files | `grep` |
| Save output | `>` (overwrite) or `>>` (append) |
| Do multiple things | `&&` (sequence) or `&` (parallel) |

---

## Practice Commands (From Room 1)

```bash
# Basic navigation
pwd
ls
cd Documents
pwd

# File operations
cat todo.txt
echo "test" > newfile.txt
cat newfile.txt

# Searching
find -name *.txt
grep "pattern" filename.txt

# Operators
echo "data" > file.txt
echo "more data" >> file.txt
cat file.txt
```

---

## Notes for Sysadmin Work

**Daily use cases:**
- `pwd` — verify location before running commands
- `ls` — inventory what's in a directory
- `cat` — read configuration files
- `find` — locate config files across system
- `grep` — analyze logs during troubleshooting
- `>` / `>>` — capture output for reports or further processing
- `&&` — build reliable automation scripts

**Security considerations:**
- Use `pwd` to confirm location before destructive operations
- Be careful with `>` — it overwrites without warning
- Use `grep` to audit logs for suspicious activity
- Use `find` to locate files for security scans

---

## Common Mistakes to Avoid

| Mistake | What Happens | Solution |
|---------|--------------|----------|
| `echo text > file` (overwrite by accident) | File contents lost | Use `>>` to append, or back up first |
| `cd` to wrong directory then run command | Wrong location affected | Always run `pwd` first |
| `find` from root `/` | Can be slow/overwhelming | Specify starting directory: `find /home -name` |
| `grep` in huge log | Slow, lots of output | Use `grep "exact_pattern"` or `grep -i` for case-insensitive |
| Forget quotes on multi-word echo | Only first word outputs | Always quote: `echo "multiple words"` |

---

## Quick Reference (Print This)

```
NAVIGATION:  pwd, cd, ls
FILES:       cat, find, grep
OPERATORS:   >, >>, &&, &
OUTPUT:      echo
USER:        whoami
```

---

**Last Updated:** Room 1 Complete (February 2026)  
**Next:** Room 2 - File Permissions, Users, Processes
