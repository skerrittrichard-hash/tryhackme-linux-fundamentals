# TryHackMe Linux Fundamentals Room 2 - Detailed Notes

## File and Directory Operations

### Creating Files and Directories

**Creating Files:**
```bash
touch filename           # Create empty file
touch file1 file2       # Create multiple files at once
```

Why use `touch`? It's quick for creating empty files. You can then add content using `echo` or text editors.

**Creating Directories:**
```bash
mkdir directoryname     # Create single directory
mkdir -p a/b/c         # Create nested directories (parent flag creates all intermediate dirs)
```

The `-p` flag is critical. Without it, `mkdir a/b/c` fails if `a/` doesn't exist. With `-p`, it creates `a/`, then `b/` inside it, then `c/` inside that.

### Copying Files and Directories

**Copying Files:**
```bash
cp source destination           # Copy file
cp file1.txt file1_backup.txt  # Copy with new name
cp file1.txt /path/to/dest/    # Copy to directory
```

**Copying Directories:**
```bash
cp -r sourcedir destdir        # Recursive copy (includes all contents)
```

The `-r` flag is essential. Without it, `cp directoryname newname` fails with "is a directory" error.

**Copying Multiple Files:**
```bash
cp file1.txt file2.txt /backup/    # Copy multiple files to directory
```

### Moving and Renaming Files

```bash
mv source destination           # Move file to new location
mv oldname.txt newname.txt     # Rename file (same as moving within directory)
mv source/file.txt dest/       # Move to different directory
```

**Important:** `mv` is move AND rename. It's the same operation in Linux.

### Removing Files and Directories

**Removing Files:**
```bash
rm filename                # Delete single file
rm file1 file2 file3      # Delete multiple files
```

**Removing Empty Directories:**
```bash
rmdir directory           # Only works if directory is empty
```

**Removing Directories with Contents:**
```bash
rm -r directory          # Recursive delete (dangerous!)
```

**Warning:** `rm -r` is permanent. No recycle bin. Be careful.

### Understanding Directory Structure

Important directories:
- `/` - Root directory (top of everything)
- `/home` - User home directories
- `/etc` - Configuration files
- `/var` - Variable data (logs, temp files)
- `/usr` - User programs and utilities
- `/bin` - Essential system commands
- `/root` - Root user's home directory

---

## File Permissions - Symbolic Format

### Understanding Permissions

Three permission types:
- **r (read)** - Can view file contents
- **w (write)** - Can modify file
- **x (execute)** - Can run file (for scripts/programs)

Three permission scopes:
- **u (user)** - Owner of file
- **g (group)** - Members of file's group
- **o (others)** - Everyone else
- **a (all)** - User + group + others

### Reading Permission Notation

Example: `rwxr-xr-x`

```
rwxr-xr-x
^^^       User permissions: read, write, execute (7)
   ^^^    Group permissions: read, execute (5)
      ^^^ Others permissions: read, execute (5)
```

Breakdown:
- Position 1-3: User permissions
- Position 4-6: Group permissions  
- Position 7-9: Others permissions

### Symbolic Permission Changes

**Grant Permission:**
```bash
chmod u+x script.sh          # Add execute for user
chmod g+r file.txt           # Add read for group
chmod o+w file.txt           # Add write for others (usually bad idea)
chmod a+r file.txt           # Add read for all
```

**Remove Permission:**
```bash
chmod u-w file.txt           # Remove write from user
chmod g-x script.sh          # Remove execute from group
chmod o-r file.txt           # Remove read from others
```

**Set Exact Permissions:**
```bash
chmod u=rwx,g=rx,o=rx file   # User: rwx, Group: rx, Others: rx
chmod a=rw file              # Everyone: read and write only
```

### Common Symbolic Examples

```bash
chmod u+x script.sh          # Make script executable by owner
chmod 755 script.sh          # (same as above, numeric)

chmod u=rw,g=r,o= file.txt  # Owner: read/write, Group: read only, Others: nothing
chmod 640 file.txt           # (same as above, numeric)

chmod go-rwx file.txt        # Remove all permissions from group and others
chmod 700 file.txt           # (same as above, numeric)
```

---

## File Permissions - Numeric Format

### Understanding Numeric Values

```
4 = read (r)
2 = write (w)
1 = execute (x)
```

Add them together:
- `7` = 4+2+1 = rwx (read, write, execute)
- `6` = 4+2 = rw- (read, write)
- `5` = 4+1 = r-x (read, execute)
- `4` = 4 = r-- (read only)
- `3` = 2+1 = -wx (write, execute)
- `2` = 2 = -w- (write only)
- `1` = 1 = --x (execute only)
- `0` = none

### Reading Numeric Notation

Example: `chmod 755 file`

```
7   5   5
^   ^   ^
|   |   +-- Others: 5 (r-x)
|   +------ Group: 5 (r-x)
+---------- User: 7 (rwx)
```

So `755` means:
- Owner: read, write, execute
- Group: read, execute
- Others: read, execute

### Common Numeric Permissions

```bash
chmod 755 script.sh      # Scripts/programs (owner: full, group/others: read+execute)
chmod 644 file.txt       # Regular files (owner: read+write, group/others: read only)
chmod 700 secret.txt     # Private files (owner only, no access for others)
chmod 777 file           # Everyone has full permissions (rarely used, security risk)
chmod 600 password.txt   # Very private (owner read+write only)
chmod 644 image.jpg      # Public readable file (owner: write, all: read)
```

### Why Numeric Format?

Numeric is faster and more precise. When configuring system files, numeric is standard:
```bash
chmod 644 /etc/config    # Standard config permissions
chmod 755 /usr/bin/command  # Executables
chmod 700 /root/.ssh     # Private SSH keys
```

---

## File Ownership

### Understanding Ownership

Every file has:
- **Owner** - User who owns the file
- **Group** - Group that owns the file

```bash
ls -l file.txt
-rw-r--r-- 1 richard students 1024 Feb 10 12:00 file.txt
                ^^^^^^^ ^^^^^^^
                Owner   Group
```

### Changing Owner

```bash
chown richard file.txt              # Change owner to richard
chown richard:students file.txt     # Change owner and group
sudo chown root:root file.txt       # Usually requires sudo
```

**Why Change Ownership?**
- Run web server as `www-data` user (not root)
- Ensure backup user owns backups
- Fix permissions after copying files
- Security: service runs as limited user, not root

### Changing Group

```bash
chgrp students file.txt             # Change group to students
```

### Practical Ownership Scenarios

**Web Server Configuration:**
```bash
sudo chown www-data:www-data /var/www/html/file.php
sudo chmod 644 /var/www/html/file.php
```

**User Home Directory:**
```bash
sudo chown richard:richard /home/richard/.bashrc
sudo chmod 644 /home/richard/.bashrc
```

**Executable Script:**
```bash
chown richard:richard script.sh
chmod 755 script.sh
```

---

## Understanding the ls Command

### Basic ls Output

```bash
$ ls
file1.txt  file2.txt  directory1
```

### Long Format (ls -l)

```bash
$ ls -l
-rw-r--r-- 1 richard students 1024 Feb 10 12:00 file.txt
drwxr-xr-x 2 richard students 4096 Feb 10 11:00 directory1
```

Breaking this down:
- `-rw-r--r--` - File type and permissions (first char: `-` is regular file, `d` is directory)
- `1` - Number of hard links
- `richard` - Owner
- `students` - Group
- `1024` - File size in bytes
- `Feb 10 12:00` - Last modified date/time
- `file.txt` - Filename

### Useful ls Flags

```bash
ls -l              # Long format (shows permissions)
ls -h              # Human-readable sizes (1K, 2M, 1G instead of bytes)
ls -lh             # Combine: long format with human-readable sizes
ls -a              # All files (including hidden files starting with .)
ls -la             # Long format with hidden files
ls -R              # Recursive (show subdirectories and their contents)
ls -S              # Sort by file size
ls -t              # Sort by modification time
ls -r              # Reverse sort order
```

### Practical Examples

```bash
ls -lh /var/log                    # See log files with readable sizes
ls -la /home/richard               # See all files in home directory
ls -lR /etc                        # See entire /etc directory tree
ls -lhS /home                      # See user directories, largest first
```

---

## Manual Pages and Documentation

### Using man Command

```bash
man command              # View full manual for command
man chmod              # Manual for chmod command
man ls                 # Manual for ls command
```

### Manual Page Navigation

- **Space** - Page down
- **b** - Page up
- **/searchterm** - Search for text
- **n** - Next search result
- **q** - Quit manual page

### Understanding Manual Sections

Manual is organized into sections:
1. Commands (shell commands)
2. System calls
3. Library functions
4. Special files/devices
5. File formats
6. Games
7. Miscellaneous
8. System administration

Example:
```bash
man chmod              # Shows chmod command (section 1)
man 2 chmod            # Shows chmod system call (section 2)
```

### Quick Help

```bash
command --help         # Brief help (usually shorter than man)
command -h             # Help (not all commands support this)
```

### Finding Command Documentation

```bash
man -k copy            # Search for manual pages about "copy"
man -k permission      # Search for pages about "permission"
```

---

## Putting It All Together: Real Scenarios

### Scenario 1: Fix Script Permission

Problem: Script won't run
```bash
$ ./myscript.sh
bash: ./myscript.sh: Permission denied

$ ls -l myscript.sh
-rw-r--r-- 1 richard students 256 Feb 10 12:00 myscript.sh
                   ^ No execute permission

$ chmod u+x myscript.sh
$ ./myscript.sh
Script runs successfully!
```

### Scenario 2: Setup Web Directory

```bash
# Create web directory structure
mkdir -p /var/www/html/{css,js,images}

# Set ownership to web server user
sudo chown -R www-data:www-data /var/www/html

# Set permissions: owner can edit, web server can serve, public can read
sudo chmod 755 /var/www/html
sudo chmod 644 /var/www/html/*.html
sudo chmod 644 /var/www/html/css/*
```

### Scenario 3: Backup User Access

```bash
# Create backup directory
mkdir /backups

# Change ownership to backup user
chown backup:backup /backups

# Only backup user can access
chmod 700 /backups

# Other users can't see or access backups
$ ls -l /backups
drwx------ 1 backup backup 4096 Feb 10 12:00 /backups
```

### Scenario 4: Configuration File Hardening

```bash
# Database configuration (sensitive)
chmod 600 /etc/database/config.ini      # Owner read/write only
sudo chown root:root /etc/database/config.ini

# Service configuration (readable by service)
chmod 644 /etc/nginx/nginx.conf         # Owner edit, others read
sudo chown root:root /etc/nginx/nginx.conf

# SSH private keys (critical security)
chmod 600 ~/.ssh/id_rsa                 # Owner only
chown $USER:$USER ~/.ssh/id_rsa
```

---

## Key Takeaways

1. **Permissions are Security:** Every file has access controls. Wrong permissions = security risk.
2. **Symbolic vs Numeric:** Both do the same thing. Numeric is faster for common patterns.
3. **Ownership Matters:** Services should run as unprivileged users, not root.
4. **755/644 Principle:**
   - `755` for executable files and directories
   - `644` for regular files
   - `600` for secrets
5. **Least Privilege:** Give only the permissions needed.
6. **Manual Pages:** Use `man` command—it's your self-service documentation.

---

**These skills are fundamental for sysadmin work. You'll use `chmod`, `chown`, `ls -l` daily.**
