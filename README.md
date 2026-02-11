# TryHackMe Linux Fundamentals - Complete Series

Complete documentation of TryHackMe Linux Fundamentals Parts 1, 2, and 3. All three rooms finished with comprehensive notes, command cheatsheets, and hands-on lab evidence.

**Status:** ✅ All 3 Rooms Complete

---

## Series Overview

Linux Fundamentals is a three-part beginner-to-intermediate course covering essential Linux system administration skills. This repository documents the complete series with detailed notes, practical command references, and screenshot evidence from hands-on labs.

### Room 1: Basic Navigation
- Terminal basics and Linux file system structure
- Navigation commands (cd, ls, pwd)
- File searching (find, locate, grep)
- Shell operators and wildcards
- **Skills:** Comfortable navigating Linux systems from command line

### Room 2: File System & Permissions
- File operations (cp, mv, rm, mkdir)
- File permissions (symbolic and numeric)
- File ownership (chown, chgrp)
- Understanding permission security implications
- **Skills:** Managing file access control and troubleshooting permission issues

### Room 3: System Operations & Automation
- Command line text editors (nano, vim)
- Web content download (wget, curl)
- Process management (ps, fg, bg, kill)
- Task automation with cron
- Package management with apt
- Log monitoring and troubleshooting
- **Skills:** Operating Linux systems, automating tasks, diagnosing problems

---

## Repository Structure

```
tryhackme-linux-fundamentals/
├── README.md (this file)
├── LEARNING-LOG.md (progress tracker across all 3 rooms)
│
├── room-01-notes.md
├── room-01-commands-cheatsheet.md
└── room-01-screenshots/
    ├── 01-basic-navigation.png
    ├── 02-file-navigation.png
    └── ... (quiz completion evidence)
│
├── room-02-notes.md
├── room-02-commands-cheatsheet.md
└── room-02-screenshots/
    ├── 01-file-operations.png
    ├── 02-file-permissions.png
    └── ... (quiz completion evidence)
│
├── room-03-README.md
├── room-03-notes.md
├── room-03-commands-cheatsheet.md
└── room-03-screenshots/
    ├── 01-command-line-text-editors.png
    ├── 02-accessing-web-content.png
    ├── 03-running-processes.png
    ├── 04-automating-system-automation.png
    ├── 05-introducing-packages-and-software-repos.png
    └── 06-monitoring-your-system-logs.png
```

---

## Quick Start

**New to Linux?** Start here:
1. Read `LEARNING-LOG.md` for series overview
2. Start with `room-01-notes.md` (navigation)
3. Move to `room-02-notes.md` (permissions)
4. Finish with `room-03-README.md` (operations)

**Need command reference?** 
- `room-01-commands-cheatsheet.md` - Navigation commands
- `room-02-commands-cheatsheet.md` - Permission & file commands
- `room-03-commands-cheatsheet.md` - Process, cron, apt, log commands

**Studying for sysadmin role?**
Focus on Room 2 (permissions) and Room 3 (automation + logs). These are daily sysadmin work.

---

## Key Concepts by Room

### Room 1: Navigation & Exploration
**Master these commands:**
- `cd` - Change directory
- `ls` - List files
- `pwd` - Print working directory
- `find` - Search for files
- `grep` - Search file contents

**Why it matters:** Can't work with a system you can't navigate.

### Room 2: Access Control & Security
**Master these commands:**
- `chmod` - Change file permissions
- `chown` - Change file owner
- `chgrp` - Change file group
- `ls -l` - See permissions and ownership

**Why it matters:** Permissions are core Linux security. Misconfigured permissions cause security issues.

### Room 3: System Operations
**Master these commands:**
- `nano`/`vim` - Edit config files
- `wget`/`curl` - Download files
- `ps aux` - List processes
- `crontab -e` - Schedule tasks
- `apt install` - Install software
- `tail -f` - Watch logs
- `grep` - Search logs

**Why it matters:** Sysadmins automate repetitive tasks, install software, and diagnose problems using logs.

---

## Real-World Sysadmin Applications

After completing this series, you can:

| Task | How | Commands |
|------|-----|----------|
| Edit Apache config | Open in nano | `nano /etc/apache2/apache2.conf` |
| Check running services | List processes | `ps aux \| grep apache2` |
| Find large log files | Search /var/log | `ls -lh /var/log/*.log \| sort -k5 -h` |
| Schedule daily backup | Add cron job | `crontab -e` then `0 2 * * * /backup.sh` |
| Install web server | Use apt | `apt update && apt install nginx` |
| Diagnose failed service | Check logs | `tail -50 /var/log/syslog \| grep error` |
| Fix permission issue | Change permissions | `chmod 755 /var/www` |
| Download security patch | Download file | `wget https://security.patch.com/patch.tar.gz` |

---

## Progression & Learning Path

**Room 1 → Room 2 → Room 3 = Sysadmin Foundation**

```
Room 1: How do I navigate?
    ↓
Room 2: How do I control access?
    ↓
Room 3: How do I operate the system?
    ↓
Junior Sysadmin Ready (with mentorship)
```

Each room builds on the previous:
- Room 1 teaches you the landscape (where files are, how to find them)
- Room 2 teaches you security (who can access what and why it matters)
- Room 3 teaches you operations (automate tasks, install software, troubleshoot)

---

## Completion Evidence

✅ **Room 1:** All quiz questions answered correctly  
✅ **Room 2:** All quiz questions answered correctly  
✅ **Room 3:** All quiz questions answered correctly  

Screenshot evidence stored in `room-01-screenshots/`, `room-02-screenshots/`, and `room-03-screenshots/`.

---

## Time Investment

- **Room 1:** ~30 minutes
- **Room 2:** ~30 minutes
- **Room 3:** ~45 minutes
- **Total:** ~105 minutes (1h 45m)

---

## Next Steps After This Series

1. **Deepen Linux knowledge:** Privilege escalation, networking, services management
2. **Practice on HackTheBox:** Real-world Linux systems to compromise
3. **Windows Server:** Active Directory, Group Policy, system administration
4. **Cloud platforms:** Azure, AWS basics for modern infrastructure
5. **Security certifications:** CompTIA Security+, CEH

This series is the foundation. Real Linux administration requires depth in specialized areas (networking, security hardening, service management), but navigation + permissions + automation cover 70% of daily junior sysadmin work.

---

## Files Included

### Documentation
- **LEARNING-LOG.md** - Progress tracker across all 3 rooms with key learnings
- **room-01-notes.md** - Detailed explanations of Room 1 concepts
- **room-02-notes.md** - Detailed explanations of Room 2 concepts
- **room-03-notes.md** - Detailed explanations of Room 3 concepts
- **room-03-README.md** - Room 3 comprehensive overview

### Cheatsheets
- **room-01-commands-cheatsheet.md** - Quick command reference for Room 1
- **room-02-commands-cheatsheet.md** - Quick command reference for Room 2
- **room-03-commands-cheatsheet.md** - Quick command reference for Room 3

### Evidence
- **room-01-screenshots/** - Quiz completion screenshots
- **room-02-screenshots/** - Quiz completion screenshots
- **room-03-screenshots/** - Task completion screenshots

---

## How to Use This Repository

**As a learner:**
1. Read notes for conceptual understanding
2. Reference cheatsheets while practicing
3. Review your answers against the screenshots

**As interview prep:**
1. Use cheatsheets to refresh commands before interviews
2. Focus on Room 2 (permissions) and Room 3 (automation, logs)
3. Be prepared to explain why commands work

**As documentation:**
Keep this repo as future reference. When you're on the job and forget the exact cron syntax or grep command, these cheatsheets will be faster than searching online.

---

## Sysadmin Relevance

These three rooms cover skills you'll use daily as a Linux sysadmin:

| Daily Task | Skill | Room |
|------------|-------|------|
| Troubleshoot permission issues | chmod, chown, ls -l | 2 |
| Edit config files | nano, vim | 3 |
| Install updates | apt update/upgrade | 3 |
| Check running services | ps aux | 3 |
| Schedule backups | crontab | 3 |
| Diagnose errors | grep, tail, /var/log | 3 |
| Manage users/groups | File ownership | 2 |

**Percentage of real sysadmin work covered by this series:** ~70% (foundation level)

---

## Repository Info

**TryHackMe Course:** Linux Fundamentals (Parts 1, 2, 3)  
**Course Type:** Beginner to Intermediate  
**Status:** ✅ Complete  
**Last Updated:** February 2026

**Purpose:** Document complete learning of Linux Fundamentals series with comprehensive notes, commands references, and hands-on lab evidence for portfolio/recruitment purposes.

---

**Ready to use. All three rooms complete. All documentation included.**
