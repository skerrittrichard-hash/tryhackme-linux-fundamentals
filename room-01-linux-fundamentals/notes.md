# Room 1: Linux Fundamentals - Detailed Notes

## Task 1: Introduction

Linux is an operating system like Windows or macOS, but it powers much of modern infrastructure:
- Web servers and cloud platforms
- Android devices
- Enterprise servers
- Smart devices (cars, IoT sensors)
- Critical infrastructure (traffic lights, industrial systems)

**Key insight:** Linux is incredibly lightweight—Ubuntu Server can run on just 512MB of RAM, making it ideal for resource-constrained environments.

---

## Task 2: Background on Linux

### Where Linux is Used

Linux isn't just for hackers or servers. It's embedded in everyday systems:

| Use Case | Example |
|----------|---------|
| **Web Infrastructure** | Websites, APIs, cloud services |
| **Point of Sale** | Shop checkout systems, tills, registers |
| **Smart Devices** | Car entertainment systems, home automation |
| **Critical Systems** | Traffic light controllers, industrial sensors |

### Linux Distributions (Flavours)

Linux is an umbrella term. Different distributions are built on the Linux kernel and optimized for different purposes:

- **Ubuntu** - Popular for both servers and desktops; highly extensible
- **Debian** - Lightweight, stable; basis for many other distributions
- **CentOS** - Enterprise-focused
- **Alpine** - Minimal footprint for containerized environments

**For this room:** We're using Ubuntu Linux.

---

## Task 4: First Commands

### The Terminal

Instead of a graphical desktop, Linux systems often use a terminal (text-based interface) for interaction.

Terminal prompt format:
```
username@hostname:location$
```

Example:
```
tryhackme@linux1:~$
```

Where `~` represents the home directory.

### Command 1: `echo`

**Purpose:** Output text to the terminal

**Syntax:**
```bash
echo [text]
echo "text with spaces"
```

**Examples:**
```bash
echo Hello              # Single word, no quotes needed
echo "Hello Friend!"    # Multiple words require quotes
echo TryHackMe          # Answer to quiz question
```

**Why it matters for sysadmin work:**
- Used in scripts to provide feedback
- Helpful for logging output to files
- Essential for scripting workflows

### Command 2: `whoami`

**Purpose:** Identify the current logged-in user

**Syntax:**
```bash
whoami
```

**Output example:**
```
tryhackme
```

**Why it matters for sysadmin work:**
- Essential before making system changes (confirms you're the right user)
- Critical for security auditing
- Helps troubleshoot permission issues

---

## Task 5: Interacting With the Filesystem

### Command 1: `ls` (Listing)

**Purpose:** Display contents of a directory

**Syntax:**
```bash
ls                    # List current directory
ls [directory_name]   # List specific directory without navigating
```

**Example output:**
```
Important Files  My Documents  Notes  Pictures
```

**Sysadmin use:**
- Quickly inventory files in directories
- Check what's in `/etc/` for configuration files
- Monitor backup directories

### Command 2: `cd` (Change Directory)

**Purpose:** Navigate between directories

**Syntax:**
```bash
cd [directory_name]   # Navigate to specific directory
cd ..                 # Go up one level (parent directory)
cd ../..              # Go up two levels
cd ~                  # Return to home directory
cd -                  # Return to previous directory
```

**Example:**
```bash
tryhackme@linux1:~$ cd Pictures
tryhackme@linux1:~/Pictures$ ls
dog_picture1.jpg  dog_picture2.jpg  dog_picture3.jpg
```

**Sysadmin use:**
- Navigate to `/var/log/` to analyze logs
- Access `/home/` to manage user directories
- Browse `/etc/` for system configuration

### Command 3: `cat` (Concatenate)

**Purpose:** Display contents of files (or multiple files)

**Syntax:**
```bash
cat [filename]                    # View single file
cat [directory/filename]          # View file in another directory without navigating
```

**Example:**
```bash
tryhackme@linux1:~/Documents$ cat todo.txt
Here's something important for me to do later!
```

**Sysadmin use:**
- View configuration files (e.g., `cat /etc/hostname`)
- Extract passwords/credentials from files (during security audits)
- Retrieve flags or sensitive data from log files
- Display system information from `/proc/` files

### Command 4: `pwd` (Print Working Directory)

**Purpose:** Show the full path to current directory

**Syntax:**
```bash
pwd
```

**Example output:**
```
/home/ubuntu/Documents
```

**Sysadmin use:**
- Confirm your current location before running commands
- Document paths for scripts and automation
- Avoid accidentally running commands in wrong directories

---

## Task 6: Searching for Files

### Command 1: `find`

**Purpose:** Search for files across directories

**Syntax:**
```bash
find -name [filename]           # Search by exact filename
find -name [pattern]            # Search using wildcards
find [path] -name [pattern]     # Search from specific path
```

**Examples:**
```bash
find -name passwords.txt         # Find specific file
find -name *.txt                 # Find all .txt files
find /home -name *.log          # Find all logs in /home
```

**Output:**
```
./folder1/passwords.txt
./Documents/todo.txt
```

**Sysadmin use:**
- Locate configuration files across the system
- Find all log files for analysis
- Identify large files consuming disk space
- Search for security-related files during audits

### Command 2: `grep`

**Purpose:** Search within file contents for specific text

**Syntax:**
```bash
grep [search_term] [filename]
grep "search phrase" [filename]  # Multi-word searches need quotes
```

**Example:**
```bash
grep "81.143.211.90" access.log
```

**Output:**
```
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417
```

**Sysadmin use:**
- Analyze web server access logs
- Search system logs for errors
- Identify specific user activity
- Monitor failed login attempts in authentication logs
- Critical for incident response investigations

---

## Task 7: Shell Operators

### Operator 1: `&` (Background Execution)

**Purpose:** Run commands in the background, freeing up terminal

**Syntax:**
```bash
command &
```

**Example:**
```bash
cp large_file.iso backup.iso &
```

**Sysadmin use:**
- Run long-running backups without blocking terminal
- Execute multiple tasks in parallel
- Monitor system while processes run

---

### Operator 2: `&&` (Logical AND)

**Purpose:** Chain commands; second command runs only if first succeeds

**Syntax:**
```bash
command1 && command2 && command3
```

**Example:**
```bash
cd /var/www && ls           # List /var/www only if cd succeeds
mkdir backup && cp file backup/
```

**Sysadmin use:**
- Build reliable automation scripts
- Ensure dependencies are met before proceeding
- Prevent cascading errors in scripts

---

### Operator 3: `>` (Output Redirection - Overwrite)

**Purpose:** Redirect output to a file, **overwriting** existing contents

**Syntax:**
```bash
command > filename
echo "text" > filename
```

**Example:**
```bash
echo "password123" > passwords    # Creates/overwrites file with content
cat access.log > filtered.txt     # Redirect cat output to file
```

**Sysadmin use:**
- Create configuration files from scripts
- Redirect command output for processing
- Backup log files before manipulation
- Capture system information snapshots

**⚠️ Warning:** The `>` operator **overwrites** files—use with caution!

---

### Operator 4: `>>` (Output Redirection - Append)

**Purpose:** Redirect output to a file, **appending** to existing contents

**Syntax:**
```bash
command >> filename
echo "text" >> filename
```

**Example:**
```bash
echo "hello" >> welcome    # Adds "hello" to end of file
echo "world" >> welcome    # File now contains: hey / hello / world
```

**Sysadmin use:**
- Build log files gradually
- Append monitoring data over time
- Add entries to configuration files
- Create cumulative reports

---

## Conceptual Relationships

### File Structure Hierarchy

Linux uses a hierarchical directory structure starting from `/` (root):

```
/ (root)
├── home/
│   └── username/
│       ├── Documents/
│       ├── Pictures/
│       └── [user files]
├── etc/ (configuration files)
├── var/ (variable data like logs)
├── tmp/ (temporary files)
└── usr/ (user programs)
```

**Sysadmin relevance:** Different directories have different purposes. Knowing the structure is essential for:
- Finding configuration files (`/etc/`)
- Analyzing logs (`/var/log/`)
- Managing user data (`/home/`)
- Running backups

### Command Chaining Pattern

```bash
find /var/log -name *.log > log_list.txt
grep "error" log_list.txt >> errors.txt
```

This demonstrates how commands work together:
1. `find` searches for files
2. `>` captures the list
3. `grep` searches within captured data
4. `>>` appends results to another file

---

## Key Distinctions for Sysadmin Work

| Concept | Purpose | Sysadmin Relevance |
|---------|---------|-------------------|
| **Navigation** (`cd`, `pwd`) | Know where you are | Prevents accidents; critical before making changes |
| **Viewing** (`cat`, `ls`) | See what exists | Audit system state; troubleshoot issues |
| **Searching** (`find`, `grep`) | Locate specific data | Log analysis; security investigations |
| **Redirection** (`>`, `>>`) | Capture output | Automation; reporting; data processing |
| **Chaining** (`&&`, `&`) | Execute workflows | Build reliable scripts; parallel processing |

---

## Completed Quiz Questions (Room 1)

1. ✅ Output "TryHackMe" → `echo TryHackMe`
2. ✅ Replace file contents with "password123" → `echo "password123" > passwords` or `sed -i 's/.*/password123/' passwords`
3. ✅ Append "tryhackme" to file → `echo "tryhackme" >> passwords`
4. ✅ Run command in background → `&`
5. ✅ Find files with .txt extension → `find -name *.txt`
6. ✅ Search within files for patterns → `grep`

---

## Reflection

Room 1 provides the foundational commands needed for all Linux work. These aren't advanced—they're essential muscle-memory skills used dozens of times daily in sysadmin work. The shift from GUI navigation to command-line efficiency is where Linux sysadmins gain speed and power.

Next steps: Room 2 will cover file permissions, user/group management, and process control—the building blocks of system administration.
