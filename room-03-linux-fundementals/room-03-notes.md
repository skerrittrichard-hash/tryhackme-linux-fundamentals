# TryHackMe Linux Fundamentals - Room 3: Detailed Notes

## Task 1: Command Line Text Editors

### Why Text Editors Matter

As a sysadmin, you'll spend significant time editing configuration files. You can't always use a GUI text editor. Text editors are essential.

### nano Editor

**Best for:** Quick edits, beginners, simple configuration changes

nano is user-friendly. When you open a file, the controls are displayed at the bottom.

```bash
nano /etc/apache2/apache2.conf
```

**Inside nano:**
- `Ctrl+X` - Exit (prompts to save)
- `Ctrl+O` - Save (write out)
- `Ctrl+K` - Cut line
- `Ctrl+U` - Paste
- `Ctrl+W` - Search
- `Ctrl+V` - Page down
- `Ctrl+Y` - Page up

**Example workflow:**
1. Open file: `nano myfile.txt`
2. Edit text (just type)
3. Save: `Ctrl+O` then press Enter
4. Exit: `Ctrl+X`

If you try to exit without saving, nano asks: "Save modified buffer?" Say yes or no.

### vi/vim Editor

**Best for:** Power users, scripting, configuration at scale

vim is powerful but has a learning curve. It has two modes:

1. **Insert mode** (editing text)
2. **Normal mode** (running commands)

```bash
vim /etc/network/interfaces
```

**Normal mode commands:**
- `i` - Enter insert mode
- `Esc` - Exit insert mode (return to normal)
- `:w` - Save (write)
- `:q` - Quit
- `:wq` - Save and quit
- `:q!` - Quit without saving
- `dd` - Delete line
- `yy` - Copy line
- `p` - Paste
- `/pattern` - Search

**Example workflow:**
1. Open file: `vim config.conf`
2. Press `i` to enter insert mode
3. Edit text
4. Press `Esc` to exit insert mode
5. Type `:wq` and press Enter to save and quit

**Why vim is popular:**
- Works everywhere (included on all Linux systems)
- Incredibly fast once you learn it
- Scriptable and automatable
- Industry standard (you'll see vim used everywhere)

### When to Use Which

**Use nano when:**
- Making quick edits to one config file
- You're new to Linux
- You're in a hurry and want no confusion

**Use vim when:**
- You work with code/configs regularly
- You need advanced editing features
- You want to look professional in technical interviews

**Real sysadmin truth:** Most sysadmins use nano for 80% of edits (it's faster for simple changes) and vim when they need power features.

---

## Task 2: Accessing Web Content

### Why Download from Command Line?

Not all downloads need a browser. You'll often need to:
- Download security patches from vendor websites
- Pull scripts from GitHub
- Grab configuration templates
- Download tools and binaries

### wget Command

**wget = "web get"** — Downloads files from the internet to your local system.

```bash
wget https://example.com/file.tar.gz
```

This downloads the file to your current directory with its original name.

**Common wget options:**
```bash
wget -O custom_name.tar.gz https://example.com/file.tar.gz
# -O saves with custom filename instead of original

wget -q https://example.com/file.tar.gz
# -q runs quietly (no output) useful in scripts

wget --limit-rate=100k https://example.com/largefile.iso
# --limit-rate throttles download speed

wget -c https://example.com/largefile.iso
# -c continues partial downloads (resume)
```

**Practical example:**
```bash
# Download WordPress to web server
wget https://wordpress.org/latest.tar.gz
# File saved as: latest.tar.gz

# Download with better name
wget -O wordpress-latest.tar.gz https://wordpress.org/latest.tar.gz
# File saved as: wordpress-latest.tar.gz
```

### curl Command

**curl = "client URL"** — Fetches content from the internet and displays it (or saves it).

```bash
curl https://example.com
```

This displays the HTML content of the website in your terminal.

**Common curl options:**
```bash
curl https://example.com > page.html
# > saves output to a file

curl -o custom_name.html https://example.com
# -o saves with custom filename

curl -I https://example.com
# -I shows only headers (no body)

curl -L https://example.com
# -L follows redirects

curl -u username:password https://secure.example.com
# -u includes authentication credentials
```

**Practical example:**
```bash
# Check if website is returning correct status code
curl -I https://myapp.example.com
# Returns headers like: HTTP/1.1 200 OK

# Download with basic authentication
curl -u admin:password https://secure-repo.example.com/script.sh -o script.sh
```

### wget vs curl

| Task | wget | curl |
|------|------|------|
| Download file | Better (native) | Works but verbose |
| Display content | Works but saves to file | Better (displays in terminal) |
| Follow redirects | Manual flag needed | Works automatically |
| Simple downloads | Simpler syntax | Slightly more verbose |
| Complex requests | Limited | Better (more options) |

**In practice:** Use wget for straightforward downloads, curl for checking status or doing complex requests.

---

## Task 3: Running Processes

### What's a Process?

A process is a running instance of a program. Every command you run is a process. Every service running is a process.

### ps Command (Process Status)

```bash
ps
```

Shows processes for the current user. Limited output by default.

```bash
ps aux
```

Shows ALL processes with detailed information. This is the most useful version.

**Understanding ps aux output:**

```
USER    PID   %CPU %MEM   VSZ   RSS TTY STAT START TIME COMMAND
root    1     0.1  0.2   191M  15M ?   Ss  10:15 0:05 /sbin/init splash
root    34    0.0  0.1   231M  8.5M ?   Ss  10:15 0:02 /lib/systemd/systemd-journald
user    1234  2.5  3.1  1.2G  250M pts/0 Sl+ 10:20 0:15 /usr/bin/firefox
```

**Key columns:**
- **USER** - Who owns the process
- **PID** - Process ID (unique identifier)
- **%CPU** - CPU usage percentage
- **%MEM** - Memory usage percentage
- **VSZ** - Virtual memory size (kilobytes)
- **RSS** - Resident set size (actual memory used)
- **TTY** - Terminal type (? = background, pts/0 = terminal session)
- **STAT** - Process state (S=sleeping, R=running, s=session leader, l=multi-threaded, +foreground)
- **START** - When process started
- **TIME** - CPU time used
- **COMMAND** - The actual command running

### Finding Specific Processes

```bash
ps aux | grep firefox
```

Pipes ps output to grep, finding anything with "firefox" in the name.

**Real example:**
```bash
# Find Apache web server process
ps aux | grep apache2

# Find what user is using the most memory
ps aux --sort=-%mem | head -10

# Find how many Java processes are running
ps aux | grep java | wc -l
```

### Running Commands in Background

By default, commands run in the foreground (you wait for them to finish).

```bash
long_running_command &
```

The `&` at the end runs the command in the background. You get your prompt back immediately.

**Example:**
```bash
# Start a backup in background
tar -czf backup.tar.gz /home &
# Job [1] 1234
# (prompt returns immediately)

# You can continue working while backup runs
```

### fg and bg Commands

**fg** = foreground (bring background process to front)
**bg** = background (continue paused process in background)

```bash
# List background jobs
jobs

# Bring job 1 to foreground
fg %1

# Pause current foreground process
Ctrl+Z

# Continue paused process in background
bg

# Bring to foreground and resume
fg
```

**Workflow example:**
```bash
# Start download
wget https://large-file.iso
# (downloading in foreground)

# Ctrl+Z to pause
# [1]+ Stopped    wget https://large-file.iso

# Move to background
bg
# [1]+ wget https://large-file.iso &

# Continue working
# Later: bring back to foreground
fg
# wget https://large-file.iso
```

### Process States (STAT column)

- **S** - Sleeping (waiting for something)
- **R** - Running (actively using CPU)
- **Z** - Zombie (dead process, parent hasn't cleaned up)
- **T** - Stopped (paused with Ctrl+Z)
- **D** - Uninterruptible sleep (waiting for disk I/O)

**Zombie processes** are weird—they're technically finished but haven't been cleaned up. They consume almost no resources but indicate a programming error. Usually harmless, but repeated zombies indicate a bug.

---

## Task 4: Automating Your System - Automation

### What's cron?

**cron** is a system daemon (background service) that runs tasks on a schedule. Instead of manually running commands, cron can run them automatically at specified times.

### Understanding crontab Syntax

Crontab has five time fields:

```
minute hour day_of_month month day_of_week command
(0-59) (0-23) (1-31)    (1-12) (0-7)        /path/to/command
```

**Field meanings:**
- **minute** (0-59) - Which minute of the hour
- **hour** (0-23) - Which hour (24-hour format, 0=midnight, 23=11 PM)
- **day_of_month** (1-31) - Which day of the month
- **month** (1-12) - Which month (1=January, 12=December)
- **day_of_week** (0-7) - Which day (0 and 7 = Sunday, 1=Monday, ... 6=Saturday)

### Cron Examples Explained

```bash
0 2 * * * /backup/daily-backup.sh
```
- **0** = at minute 0 (top of hour)
- **2** = at hour 2 (2 AM)
- **\*** = every day of month
- **\*** = every month
- **\*** = every day of week
- **Result: Every day at 2:00 AM**

```bash
30 14 1 * * /report/monthly-report.sh
```
- **30** = at minute 30
- **14** = at hour 14 (2 PM)
- **1** = day 1 of month
- **\*** = every month
- **\*** = every day of week
- **Result: 1st of every month at 2:30 PM**

```bash
0 0 * * 0 /cleanup/weekly-cleanup.sh
```
- **0** = at minute 0
- **0** = at hour 0 (midnight)
- **\*** = every day of month
- **\*** = every month
- **0** = Sunday (day 0)
- **Result: Every Sunday at midnight**

```bash
*/15 * * * * /check/check-disk.sh
```
- **\*/15** = every 15 minutes (0, 15, 30, 45)
- **\*** = every hour
- **\*** = every day of month
- **\*** = every month
- **\*** = every day of week
- **Result: Every 15 minutes, all day**

### Special Directives

Some shortcuts avoid needing the five fields:

```bash
@reboot /startup/init-services.sh        # Run at system boot (once at startup)
@yearly /archive/yearly-archive.sh       # Run Jan 1 at midnight
@monthly /report/monthly-report.sh       # Run 1st of month at midnight
@weekly /cleanup/weekly-cleanup.sh       # Run Sunday at midnight
@daily /backup/daily-backup.sh           # Run daily at midnight
@hourly /check/hourly-check.sh           # Run every hour
```

### Using crontab

```bash
# Edit your crontab
crontab -e

# List your cron jobs
crontab -l

# Remove all cron jobs
crontab -r

# Edit another user's crontab (requires root)
sudo crontab -u username -e
```

When you run `crontab -e`, it opens an editor (nano by default). You add lines like:

```
0 2 * * * /backup/script.sh
@daily /maintenance/cleanup.sh
```

Then save and exit. The cron daemon automatically reads your changes.

### Real Sysadmin Examples

**Daily backup at 2 AM:**
```bash
0 2 * * * /scripts/backup-home.sh
```

**Every Sunday at 3 AM, run updates:**
```bash
0 3 * * 0 apt update && apt upgrade -y
```

**Every 6 hours, check disk space:**
```bash
0 */6 * * * /scripts/check-disk-usage.sh
```

**On boot, start custom service:**
```bash
@reboot /usr/local/bin/my-service start
```

**Every 30 minutes, monitor log file:**
```bash
*/30 * * * * /scripts/check-logs.sh
```

### Important Notes

- **Output:** Cron runs jobs without a terminal. Output is emailed to the user by default (or lost if mail isn't configured)
- **Working directory:** Jobs start in the home directory, not where crontab was edited
- **Full paths required:** Always use full paths to scripts and commands. Don't assume PATH is set.
- **Permissions:** Make sure scripts have execute permission: `chmod +x script.sh`

**Bad (won't work):**
```bash
0 2 * * * backup-script.sh      # Can't find script
0 2 * * * ./backup.sh            # Relative path won't work from home directory
```

**Good (will work):**
```bash
0 2 * * * /home/user/backup-script.sh
0 2 * * * /usr/local/bin/backup.sh
```

---

## Task 5: Introducing Packages & Software Repos

### What's a Package?

A **package** is a bundle of software files plus metadata (name, version, dependencies). Instead of compiling from source, packages are pre-built and ready to install.

### What's a Repository?

A **repository** (repo) is a server hosting hundreds of packages. Your system connects to these repos to find, download, and install software.

### apt (Advanced Package Tool)

**apt** is the package manager for Debian/Ubuntu systems. It handles installation, updates, and removal of software.

```bash
# Update package list (get latest info from repos)
apt update

# Install a package
apt install apache2

# Remove a package
apt remove apache2

# Remove package + config files
apt purge apache2

# Upgrade all installed packages
apt upgrade

# Search for a package
apt-cache search "web server"

# Show package information
apt show apache2
```

### Understanding apt update vs apt upgrade

**apt update:**
- Downloads latest package list from repositories
- Doesn't install anything
- Run before installing or upgrading
- Must run this first to see latest versions

```bash
apt update
# Gets: apache2 version 2.4.58, openssh-server version 8.9, etc.
```

**apt upgrade:**
- Installs newer versions of installed packages
- Only upgrades, doesn't install new packages
- Respects dependencies

```bash
apt upgrade
# Updates apache2 from 2.4.57 to 2.4.58
# Updates openssh-server from 8.8 to 8.9
```

### Dependencies

Packages often need other packages to work. apt handles this automatically.

```bash
apt install apache2
```

This might install:
- apache2 (main package)
- apache2-bin (binaries)
- apache2-data (data files)
- apache2-utils (utilities)
- apr (required library)
- apr-util (required library)

apt automatically figures out what else is needed and installs it. This is much better than compiling from source where you'd manually track dependencies.

### Real Sysadmin Workflow

```bash
# Update package list first
sudo apt update

# Search for what's available
apt-cache search nginx
# nginx - small, powerful, scalable web/proxy server
# nginx-core - nginx web/proxy server (core version)
# etc.

# Install the package
sudo apt install nginx

# Start the service
sudo systemctl start nginx

# Check if it's running
ps aux | grep nginx
```

### Repositories

Your system's repo list is in `/etc/apt/sources.list`:

```bash
cat /etc/apt/sources.list
```

Output might show:
```
deb http://archive.ubuntu.com/ubuntu focal main universe
deb http://security.ubuntu.com/ubuntu focal-security main
```

**deb** = Debian package (Ubuntu uses Debian format)
**http://archive.ubuntu.com/ubuntu** = repo server
**focal** = Ubuntu version (20.04)
**main** = category (main = officially supported)

### Third-Party Repositories

Sometimes software isn't in official repos. You add third-party repos:

```bash
# Add PPA (Personal Package Archive)
sudo add-apt-repository ppa:deadsnakes/ppa

# Update to include new repo
sudo apt update

# Now you can install from it
sudo apt install python3.11
```

---

## Task 6: Monitoring Your System - Logs

### Why Logs Matter

**Logs are your diagnostic tool.** When something goes wrong, logs tell you what happened and when.

- Troubleshot a failed service? Check logs.
- Investigating suspicious login? Check logs.
- Trying to understand why a script failed? Check logs.
- Need to find when something happened? Logs have timestamps.

### Where Are Logs?

All system logs live in `/var/log`:

```bash
ls /var/log/
```

Common log files:
- **syslog** - General system messages
- **auth.log** - Authentication attempts (logins, sudo)
- **kern.log** - Kernel messages
- **apache2/access.log** - Web requests
- **apache2/error.log** - Web server errors
- **mysql/error.log** - Database errors
- **mail.log** - Email system messages

### Reading Logs

```bash
# View entire log file
cat /var/log/syslog

# View last 20 lines
tail -20 /var/log/auth.log

# Watch log in real-time (follow mode)
tail -f /var/log/syslog
# Press Ctrl+C to stop

# Search log for pattern
grep "error" /var/log/apache2/error.log

# Count occurrences
grep -c "Failed password" /var/log/auth.log

# Case-insensitive search
grep -i "warning" /var/log/syslog
```

### Log Format

Most logs follow this format:

```
Feb 10 14:32:15 ubuntu kernel: [12345.678] Out of memory: Kill process firefox (1234) score 567 or sacrifice child
```

Breaking it down:
- **Feb 10 14:32:15** - Timestamp (month day time)
- **ubuntu** - Hostname
- **kernel** - Service that generated log
- **[12345.678]** - Context info (kernel: seconds since boot)
- **Message** - What happened

### Practical Log Troubleshooting Examples

**Example 1: Service won't start**
```bash
# Try starting service
sudo systemctl start apache2
# Job for apache2.service failed because the control process exited with error code.

# Check logs
sudo tail -20 /var/log/apache2/error.log
# AH00526: Syntax error on line 247 of /etc/apache2/apache2.conf
```

Aha! Config file has syntax error on line 247. Fix the config, restart service.

**Example 2: Failed login investigation**
```bash
# Check auth log
grep "Failed password" /var/log/auth.log | tail -10
# Feb 10 14:45:12 ubuntu sshd[1234]: Failed password for invalid user admin from 192.168.1.100 port 54321 ssh2
```

Lots of failed logins from 192.168.1.100. Potential brute force attack. Consider blocking that IP.

**Example 3: Disk space issue**
```bash
# Check system log for clues
grep "disk space" /var/log/syslog
# Feb 10 15:20:00 ubuntu kernel: [54321.123] Kernel panic - not syncing: Attempted to kill init!
```

System is out of disk space. Find large files:
```bash
du -sh /var/log/*
# 5.2G /var/log/application.log
# This log file is huge! Archive or delete old logs.
```

### Using grep with Logs

**grep = global regular expression print** — Searches text files for patterns.

```bash
grep "error" /var/log/syslog          # Lines containing "error"
grep -i "ERROR" /var/log/syslog       # Case-insensitive (ERROR, error, Error all match)
grep -v "warning" /var/log/syslog     # Exclude lines with "warning" (-v = invert)
grep -c "error" /var/log/syslog       # Count matching lines
grep "error" /var/log/syslog | wc -l  # Alternative count method
```

### Real-Time Monitoring

```bash
# Watch Apache access log in real-time
tail -f /var/log/apache2/access.log

# Watch auth log for login attempts
tail -f /var/log/auth.log

# Continuously search for new errors
tail -f /var/log/syslog | grep -i "error"
```

Press Ctrl+C to stop watching.

### Log Rotation

Logs get huge over time. **logrotate** automatically archives old logs:

```bash
# Check logrotate config
cat /etc/logrotate.d/apache2
```

Typical rotation:
- Keep 14 days of daily logs
- Compress logs after rotation
- Old logs moved to apache2.log.1.gz, apache2.log.2.gz, etc.

This prevents `/var/log` from filling the disk.

---

## Summary: The Sysadmin Mindset

After completing Room 3, you have the tools to:
1. **Edit configs** (nano/vim)
2. **Download tools** (wget/curl)
3. **Manage processes** (ps, fg, bg)
4. **Automate tasks** (cron)
5. **Install software** (apt)
6. **Troubleshoot problems** (logs)

These six skills are the foundation of system administration. Master these, and you're ready for junior sysadmin work.
