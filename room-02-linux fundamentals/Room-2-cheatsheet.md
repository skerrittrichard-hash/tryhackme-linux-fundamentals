# TryHackMe Linux Fundamentals Room 2 - Command Cheatsheet

Quick reference for all Room 2 commands and usage.

## File and Directory Operations

### Create

```bash
touch filename              # Create empty file
touch file1 file2 file3    # Create multiple files
mkdir directory            # Create directory
mkdir -p a/b/c             # Create nested directories
```

### Copy

```bash
cp source destination       # Copy file
cp file1.txt file2.txt     # Copy with new name
cp -r directory newdir     # Copy directory recursively
cp file1 file2 /backup/    # Copy multiple files to directory
```

### Move/Rename

```bash
mv oldname.txt newname.txt # Rename file
mv file.txt /new/location/ # Move file
mv directory newlocation   # Move directory
mv source dest             # Move (same as mv/rename)
```

### Delete

```bash
rm filename                # Delete file
rm file1 file2 file3       # Delete multiple files
rmdir directory            # Delete empty directory only
rm -r directory            # Delete directory with contents (recursive)
rm -rf directory           # Force delete (use carefully!)
```

---

## File Permissions - Symbolic Format

### Add Permissions

```bash
chmod u+r file             # Add read for user
chmod u+w file             # Add write for user
chmod u+x file             # Add execute for user
chmod g+r file             # Add read for group
chmod o+r file             # Add read for others
chmod a+r file             # Add read for all (user, group, others)
chmod u+rwx file           # Add all permissions for user
```

### Remove Permissions

```bash
chmod u-r file             # Remove read from user
chmod u-w file             # Remove write from user
chmod u-x file             # Remove execute from user
chmod g-x file             # Remove execute from group
chmod o-rwx file           # Remove all from others
chmod a-x file             # Remove execute from all
```

### Set Exact Permissions

```bash
chmod u=r file             # User: read only
chmod u=rw file            # User: read and write
chmod u=rwx file           # User: read, write, execute
chmod g=rx file            # Group: read and execute
chmod o= file              # Others: no permissions
chmod a=r file             # All: read only
chmod u=rwx,g=rx,o=rx file # User: rwx, Group: rx, Others: rx
```

### Common Symbolic Examples

```bash
chmod u+x script.sh              # Make script executable
chmod g+r document.txt           # Let group read file
chmod o-r secret.txt             # Remove others' read permission
chmod go-rwx file                # Remove all permissions from group and others
chmod a=rw file                  # Everyone: read and write only
chmod u+x,g+x,o+x script         # Everyone can execute
```

---

## File Permissions - Numeric Format

### Single Digit Permissions

```
4 = read (r)
2 = write (w)
1 = execute (x)
```

### Common Permission Values

```
7 = rwx (read + write + execute = 4+2+1)
6 = rw- (read + write = 4+2)
5 = r-x (read + execute = 4+1)
4 = r-- (read only = 4)
3 = -wx (write + execute = 2+1)
2 = -w- (write only = 2)
1 = --x (execute only = 1)
0 = --- (no permissions)
```

### Three-Digit Permission Format

```
chmod 755 file      = User: 7 (rwx), Group: 5 (r-x), Others: 5 (r-x)
chmod 644 file      = User: 6 (rw-), Group: 4 (r--), Others: 4 (r--)
chmod 700 file      = User: 7 (rwx), Group: 0 (---), Others: 0 (---)
chmod 777 file      = User: 7 (rwx), Group: 7 (rwx), Others: 7 (rwx)
chmod 600 file      = User: 6 (rw-), Group: 0 (---), Others: 0 (---)
```

### Common Permission Patterns

```bash
chmod 755 script.sh         # Executable script (owner: full, others: read+execute)
chmod 644 file.txt          # Regular file (owner: read+write, others: read)
chmod 700 secret.txt        # Private file (owner only)
chmod 600 password.txt      # Password file (owner read+write only)
chmod 777 file              # Everyone full access (rarely needed, security risk)
chmod 755 directory         # Typical directory (searchable by all)
chmod 700 directory         # Private directory (owner only)
```

### Recursive Permission Changes

```bash
chmod -R 755 /directory/    # Change permissions recursively (directory + contents)
chmod -R 644 /var/www/html/ # Make all files readable
chmod -R +x /usr/bin/       # Add execute permission to all files
```

---

## File Ownership

### Change Owner

```bash
chown user file                     # Change owner
chown user:group file               # Change owner and group
chown :group file                   # Change group only (shorthand)
chown -R user:group directory/      # Recursive (directory and contents)
sudo chown root:root file           # Usually requires sudo
```

### Change Group Only

```bash
chgrp group file                    # Change group
chgrp -R group directory/           # Recursive group change
```

### Common Ownership Patterns

```bash
chown www-data:www-data /var/www/html/          # Web server files
chown backup:backup /backups/                    # Backup directory
chown root:root /etc/sudoers                     # System config (root only)
chown $USER:$USER ~/.ssh/                        # User SSH directory
sudo chown -R postgres:postgres /var/lib/postgresql/  # Database directory
```

---

## The ls Command

### Basic ls

```bash
ls                  # List files in current directory
ls directory        # List files in specific directory
ls /path/to/dir     # List files at full path
```

### Useful ls Flags

```bash
ls -l               # Long format (shows permissions, owner, size, date)
ls -a               # All files (including hidden files starting with .)
ls -h               # Human-readable sizes (K, M, G instead of bytes)
ls -la              # Long format + all files + hidden files
ls -lh              # Long format + human-readable sizes
ls -R               # Recursive (show subdirectories)
ls -S               # Sort by file size (largest first)
ls -t               # Sort by modification time (newest first)
ls -r               # Reverse sort order
ls -d               # List directories themselves, not contents
```

### Combined Flags (Most Useful)

```bash
ls -lh              # Long format with human-readable sizes
ls -la              # Long format with hidden files
ls -lhr             # Long format + readable sizes + reverse order
ls -lhS             # Long format + readable sizes + sort by size
ls -lht             # Long format + readable sizes + sort by time
ls -lR              # Long format + recursive (show all subdirectories)
ls -lRh             # Recursive with human-readable sizes
```

### Interpreting ls -l Output

```
-rw-r--r-- 1 richard students 1024 Feb 10 12:00 file.txt
^ ^^^^^^^^^   ^^^^^^^ ^^^^^^^^ ^^^^  ^^^^^^^^^^^^ ^^^^^^^
| |           |       |        |     |            |
| |           |       |        |     |            +-- Filename
| |           |       |        |     +-- Modification date/time
| |           |       |        +-- File size (bytes)
| |           |       +-- Group owner
| |           +-- User owner
| +-- Permissions (r=read, w=write, x=execute, -=none)
+-- File type (- = regular file, d = directory, l = symlink)
```

### Practical ls Examples

```bash
ls -lh /var/log                     # See log files with readable sizes
ls -la /home/richard                # All files in home (including hidden)
ls -lR /etc/config                  # Show entire directory tree
ls -lhS /home                       # Directories sorted by size
ls -lht /tmp                        # Recently modified files first
ls -l /usr/bin | grep python        # Find python-related commands
```

---

## Manual Pages and Help

### View Manual

```bash
man command         # View full manual for command
man chmod           # Manual for chmod
man chown           # Manual for chown
man ls              # Manual for ls
man 2 chmod         # System call version of chmod (section 2)
```

### Search Manual

```bash
man -k keyword      # Search for commands related to keyword
man -k copy         # Search for commands about copying
man -k permission   # Search for permissions documentation
```

### Quick Help

```bash
command --help      # Brief help (faster than man)
command -h          # Help (not all commands support)
chmod --help        # Help for chmod
ls --help           # Help for ls
```

### Manual Navigation

| Key | Action |
|-----|--------|
| Space | Page down |
| b | Page up |
| / | Search |
| n | Next match |
| q | Quit |

---

## Quick Reference Patterns

### Script File Setup

```bash
# Create, make executable, set permissions
touch myscript.sh
chmod u+x myscript.sh     # or chmod 755 myscript.sh
chown $USER:$USER myscript.sh
./myscript.sh             # Now executable
```

### Regular File Setup

```bash
# Create with standard permissions
touch document.txt
chmod 644 document.txt    # Owner: rw, Others: r
chown $USER:$USER document.txt
```

### Directory Setup

```bash
# Create with standard permissions
mkdir mydirectory
chmod 755 mydirectory     # Owner: rwx, Others: rx
chown $USER:$USER mydirectory
```

### Private File Setup

```bash
# Create secret file
touch secret.txt
chmod 600 secret.txt      # Owner only
chown $USER:$USER secret.txt
```

### Web Server Files

```bash
# Setup for web server
sudo chown www-data:www-data /var/www/html/
sudo chmod 755 /var/www/html/
sudo chmod 644 /var/www/html/*.html
```

---

## Common Mistakes & Fixes

### Mistake: Wrong permissions

```bash
# Script won't run
chmod u+x script.sh         # Fix: add execute

# File not readable
chmod u+r file.txt          # Fix: add read

# Others can read private file
chmod o-r secret.txt        # Fix: remove others' read
```

### Mistake: Wrong owner

```bash
# Web files owned by root
sudo chown www-data /var/www/html/file   # Fix: change to www-data

# Backup owned by wrong user
chown backup:backup /backups/            # Fix: change to backup user
```

### Mistake: Recursive issues

```bash
# Need to change directory AND contents
chmod -R 755 directory/                  # Fix: use -R flag
chown -R user:group directory/           # Fix: use -R flag
```

---

## Helpful One-Liners

```bash
# Find all executable files
ls -l | grep "^-.*x"

# Find all directories
ls -l | grep "^d"

# See total directory size with readable format
du -sh directory/

# Find all files with specific permission
find . -perm 644

# Change all files to 644, directories to 755
find . -type f -exec chmod 644 {} \;
find . -type d -exec chmod 755 {} \;

# Find files owned by specific user
ls -l | grep username
```

---

**Reference this cheatsheet when working with permissions, ownership, and file management.**
