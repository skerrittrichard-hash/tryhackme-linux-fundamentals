# TryHackMe Linux Fundamentals - Room 3: Commands Cheatsheet

Quick reference for all commands covered in Room 3. Organized by task.

---

## Task 1: Text Editors

### nano

```bash
nano filename                 # Open file in nano
Ctrl+X                       # Exit nano
Ctrl+O                       # Save file
Ctrl+K                       # Cut line
Ctrl+U                       # Paste
Ctrl+W                       # Search in file
Ctrl+V                       # Page down
Ctrl+Y                       # Page up
Ctrl+G                       # Go to line number
```

### vim/vi

```bash
vim filename                 # Open file in vim
i                           # Enter insert mode (editing)
Esc                         # Exit insert mode (back to normal)
:w                          # Save (write)
:q                          # Quit
:wq                         # Save and quit
:q!                         # Quit without saving
:e filename                 # Open different file
dd                          # Delete line
yy                          # Copy line
p                           # Paste
u                           # Undo
Ctrl+R                      # Redo
/pattern                    # Search for pattern
n                           # Next search result
N                           # Previous search result
```

---

## Task 2: Accessing Web Content

### wget (download files)

```bash
wget https://example.com/file.tar.gz
# Download file with original name

wget -O custom_name.tar.gz https://example.com/file.tar.gz
# Download with custom filename (-O)

wget -q https://example.com/file.tar.gz
# Quiet mode (no output)

wget --limit-rate=100k https://example.com/largefile.iso
# Limit download speed to 100KB/s

wget -c https://example.com/largefile.iso
# Resume partial download (-c)

wget -r https://example.com/
# Recursive download (entire website)

wget -i urls.txt
# Download multiple URLs from file
```

### curl (fetch content)

```bash
curl https://example.com
# Display webpage content

curl https://example.com > page.html
# Save to file using redirect (>)

curl -o custom_name.html https://example.com
# Save with custom filename (-o)

curl -I https://example.com
# Show headers only (no body) (-I)

curl -L https://example.com
# Follow redirects (-L)

curl -u username:password https://secure.example.com
# Include authentication (-u)

curl -H "User-Agent: MyBot" https://example.com
# Add custom header (-H)

curl -d "key=value" https://example.com
# Send POST data (-d)

curl -v https://example.com
# Verbose (show all details) (-v)
```

---

## Task 3: Running Processes

### ps (list processes)

```bash
ps
# Current user processes

ps aux
# All processes (detailed) - MOST USEFUL

ps aux | grep firefox
# Find specific process

ps aux --sort=-%cpu | head -10
# Top 10 by CPU usage

ps aux --sort=-%mem | head -10
# Top 10 by memory usage

ps -ef
# Different format (same info as ps aux)

ps -p 1234
# Show specific PID
```

### Running in background/foreground

```bash
command &
# Run command in background

Ctrl+Z
# Pause current foreground process

fg
# Bring to foreground (resume if paused)

bg
# Continue paused process in background

jobs
# List background jobs

fg %1
# Bring job number 1 to foreground

bg %2
# Continue job number 2 in background

nohup long_command &
# Run command immune to terminal closing
```

### Process control

```bash
kill 1234
# Terminate process by PID

kill -9 1234
# Force kill (SIGKILL)

killall firefox
# Kill all instances of process

pkill -f "python script.py"
# Kill by pattern matching
```

---

## Task 4: Automation with cron

### crontab commands

```bash
crontab -e
# Edit your crontab (creates or modifies)

crontab -l
# List your cron jobs

crontab -r
# Remove all cron jobs

sudo crontab -u username -e
# Edit another user's crontab

crontab -i -r
# Safely remove (prompts first)
```

### Cron Syntax Reference

```
minute hour day_of_month month day_of_week command
(0-59) (0-23) (1-31)   (1-12) (0-7)      /path/to/command
```

### Cron Examples

```bash
# 2:00 AM every day
0 2 * * * /backup/daily-backup.sh

# 2:30 PM on 1st of every month
30 14 1 * * /report/monthly-report.sh

# Every Sunday at midnight
0 0 * * 0 /cleanup/weekly-cleanup.sh

# Every 15 minutes
*/15 * * * * /check/monitor.sh

# Every 6 hours (0:00, 6:00, 12:00, 18:00)
0 */6 * * * /task/every-six-hours.sh

# Every weekday at 9:00 AM (Mon-Fri)
0 9 * * 1-5 /work/weekday-task.sh

# Every hour on the 15th of every month
0 * 15 * * /task/run.sh

# Midnight Jan 1st every year
0 0 1 1 * /annual/yearly-task.sh

# @reboot (run on system startup)
@reboot /startup/init-service.sh

# @daily (midnight every day)
@daily /maintenance/cleanup.sh

# @hourly (every hour)
@hourly /check/status.sh

# @weekly (Sunday midnight)
@weekly /backup/weekly-backup.sh

# @monthly (1st of month midnight)
@monthly /archive/monthly-archive.sh

# @yearly (Jan 1 midnight)
@yearly /report/annual-report.sh
```

---

## Task 5: Package Management (apt)

### apt commands

```bash
apt update
# Update package list from repositories (run first!)

apt install package_name
# Install package

apt remove package_name
# Remove package (keeps config files)

apt purge package_name
# Remove package + config files

apt autoremove
# Remove unused dependencies

apt upgrade
# Upgrade all installed packages (safe)

apt full-upgrade
# Upgrade including kernel (risky)

apt-cache search keyword
# Search for packages

apt-cache show package_name
# Show package details

apt list --installed
# List installed packages

apt list --upgradable
# List packages that can be upgraded

apt search "web server"
# Search for packages with description
```

### apt-get (older tool, still works)

```bash
apt-get update
apt-get install package_name
apt-get remove package_name
apt-get upgrade
apt-get clean          # Remove cached package files
apt-get autoclean      # Remove old cached files
```

### Common Installation Scenarios

```bash
# Install web server
sudo apt update
sudo apt install apache2

# Install database
sudo apt install mysql-server

# Install Python3 with pip
sudo apt install python3 python3-pip

# Install Node.js
sudo apt install nodejs npm

# Install text editors
sudo apt install vim nano

# Install networking tools
sudo apt install curl wget netcat nmap

# Install development tools
sudo apt install build-essential git
```

---

## Task 6: Log Monitoring

### Viewing logs

```bash
cat /var/log/syslog
# View entire syslog file

tail /var/log/auth.log
# Last 10 lines of auth log

tail -20 /var/log/auth.log
# Last 20 lines

tail -f /var/log/syslog
# Follow log in real-time (Ctrl+C to stop)

tail -F /var/log/syslog
# Follow with file rotation support

head -20 /var/log/auth.log
# First 20 lines

less /var/log/syslog
# View with pagination (space to page, q to quit)
```

### Searching logs with grep

```bash
grep "error" /var/log/syslog
# Lines containing "error"

grep -i "error" /var/log/syslog
# Case-insensitive search (-i)

grep -v "warning" /var/log/syslog
# Exclude lines with "warning" (-v = invert)

grep "error" /var/log/syslog | wc -l
# Count matching lines

grep -c "error" /var/log/syslog
# Count matching lines (alternative)

grep -n "error" /var/log/syslog
# Show line numbers (-n)

grep "Failed password" /var/log/auth.log
# Find failed login attempts

grep "sudo:" /var/log/auth.log
# Find sudo command executions

grep -E "error|fatal" /var/log/syslog
# Multiple patterns (regex)
```

### Real-time log monitoring

```bash
tail -f /var/log/syslog
# Watch syslog in real-time

tail -f /var/log/auth.log
# Watch login attempts

tail -f /var/log/apache2/access.log
# Watch web requests

tail -f /var/log/apache2/error.log
# Watch web errors

tail -f /var/log/syslog | grep -i "error"
# Watch for errors only

journalctl -f
# Follow system journal (modern systemd)
```

### Common Log Files

```bash
/var/log/syslog                  # System messages
/var/log/auth.log                # Authentication (logins, sudo)
/var/log/kern.log                # Kernel messages
/var/log/apache2/access.log      # Web requests
/var/log/apache2/error.log       # Web server errors
/var/log/mysql/error.log         # MySQL errors
/var/log/mail.log                # Email system
/var/log/dpkg.log                # Package installation history
/var/log/cron                    # Cron job execution (if enabled)
/var/log/user.log                # User activity
```

### Analyzing logs

```bash
# Count errors by type
grep "error" /var/log/syslog | awk '{print $NF}' | sort | uniq -c

# Find most common errors
grep "error" /var/log/syslog | tail -100 | head -10

# Extract IP addresses from access log
grep "GET" /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c

# Find lines from specific time period
grep "10:00:" /var/log/syslog
grep "Feb 10" /var/log/auth.log

# Show entries for specific user
grep "username" /var/log/auth.log
```

---

## Combined Commands (piping)

```bash
# Find memory-hungry process and kill it
ps aux --sort=-%mem | head -2 | tail -1 | awk '{print $2}' | xargs kill

# Watch for new errors as they occur
tail -f /var/log/apache2/error.log | grep -i "error"

# Count failed login attempts per IP
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c

# Find and delete old log files
find /var/log -name "*.log" -mtime +30 -delete

# Monitor process and show every 5 seconds
watch -n 5 'ps aux | grep [p]ython'

# Download file and extract it
wget https://example.com/archive.tar.gz && tar -xzf archive.tar.gz

# Check if service is running
ps aux | grep -q [s]ystemd-resolved && echo "Service running" || echo "Service stopped"
```

---

## Useful System Commands (used in logs/processes)

```bash
uname -a                    # System info
uname -r                    # Kernel version
hostname                    # System hostname
whoami                      # Current user
w                          # Who is logged in
uptime                     # System uptime
df -h                      # Disk space usage
du -sh /path               # Directory size
free -h                    # Memory usage
top                        # Real-time process monitoring
htop                       # Better process monitoring (if installed)
systemctl status service   # Check service status
systemctl start service    # Start service
systemctl stop service     # Stop service
systemctl restart service  # Restart service
```

---

## Tips & Tricks

**Always use full paths in cron jobs:**
```bash
# Bad - won't work
0 2 * * * backup.sh

# Good - will work
0 2 * * * /home/user/backup.sh
```

**Check if command exists before using in script:**
```bash
which apache2    # Show path to command
command -v wget  # Alternative check
```

**Redirect cron output to log file:**
```bash
0 2 * * * /backup/script.sh >> /var/log/backup.log 2>&1
# >> appends to file
# 2>&1 redirects errors to log too
```

**Check cron job execution:**
```bash
grep CRON /var/log/syslog    # See what cron ran
systemctl status cron         # Check if cron is running
```

**Make script executable:**
```bash
chmod +x script.sh
```

**Run with higher privileges if needed:**
```bash
sudo apt install package_name
sudo crontab -e
sudo systemctl restart apache2
```

