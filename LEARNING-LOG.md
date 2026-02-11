# TryHackMe Linux Fundamentals - Learning Log

Track progress through all three Linux Fundamentals rooms, including completion dates, key concepts, and skill progression.

---

## Room 1: Linux Fundamentals - Basic Navigation
**Status:** ✅ Complete  
**Completed:** February 2026  
**Time Investment:** ~30 minutes  
**Difficulty:** Beginner  

### Topics Covered
- Terminal basics and navigation
- Directory structure and file system
- Basic commands (cd, ls, pwd, cat, etc.)
- File searching (find, locate, grep)
- Shell operators and wildcards

### Key Learnings
- Linux file system is hierarchical (/home, /etc, /var, etc.)
- Navigation with cd and understanding pwd shows current location
- ls with different flags (-l, -la, -h, -R) provides detailed file info
- grep is powerful for finding content in files
- Shell operators (>, >>, |) redirect and pipe output

### Skills Gained
- Comfortable navigating filesystem from command line
- Can find files using find and locate
- Can search file contents with grep
- Understand basic command syntax and flags

### Progression
Foundation for all Linux work. Comfortable navigating filesystem means you can work with files, configs, and logs efficiently.

---

## Room 2: Linux Fundamentals - File System & Permissions
**Status:** ✅ Complete  
**Completed:** February 2026  
**Time Investment:** ~30 minutes  
**Difficulty:** Beginner to Intermediate  

### Topics Covered
- File and directory operations (cp, mv, rm, mkdir)
- File permissions (symbolic and numeric format)
- File ownership (chown, chgrp)
- Understanding long format output (ls -l)
- Manual pages and documentation (man command)

### Key Learnings
- Permissions (rwx) control access: read (4), write (2), execute (1)
- Numeric permissions (755, 644) are elegant: u(7), g(5), o(5)
- File ownership matters for service security
- chmod with symbolic (+, -, =) is intuitive for quick fixes
- Man pages are self-service documentation instead of Google

### Skills Gained
- Can change permissions (both symbolic and numeric)
- Understand permission implications for security
- Can troubleshoot permission-based issues
- Can use man pages to learn command syntax

### Progression
Room 1 teaches navigation, Room 2 teaches control. You don't just navigate files—you manage access to them. Essential for understanding Linux security model.

---

## Room 3: Linux Fundamentals - System Operations & Automation
**Status:** ✅ Complete  
**Completed:** February 2026  
**Time Investment:** ~45 minutes  
**Difficulty:** Intermediate  

### Topics Covered
- Command line text editors (nano, vim)
- Web content download (wget, curl)
- Process management (ps, fg, bg, kill)
- Task automation (cron, crontab)
- Package management (apt)
- Log monitoring and troubleshooting (/var/log, grep, tail)

### Key Learnings
- nano for quick edits, vim for power-user workflows
- wget and curl are essential for downloading from command line
- ps aux shows all running processes with detailed information
- cron automates repetitive tasks (backups, cleanup)
- apt handles package installation and updates with dependency resolution
- /var/log contains diagnostic information for every issue
- grep and tail are indispensable for log analysis

### Skills Gained
- Can edit config files efficiently with nano/vim
- Can download files and tools from internet
- Can find and manage running processes
- Can schedule automated tasks with cron
- Can install software packages and manage dependencies
- Can diagnose problems using logs

### Progression
Rooms 1-2 were foundation (navigation + security model). Room 3 is operations. You now know:
1. Navigate the system (Room 1)
2. Control access to files (Room 2)
3. Operate the system (Room 3)

This is the sysadmin skillset.

---

## Series Progression Summary

| Skill | Room 1 | Room 2 | Room 3 |
|-------|--------|--------|--------|
| **Knowledge** | How to navigate | How to control access | How to operate |
| **Main tools** | cd, ls, find | chmod, chown | cron, apt, logs |
| **Real-world use** | Find config files | Secure permissions | Automate + troubleshoot |
| **Readiness level** | User mentality | Admin mentality beginning | Admin operations |

---

## Overall Learning Reflection

### What Worked Well
- Practical exercises with real commands
- Progressive difficulty (navigation → permissions → operations)
- Each room built on previous knowledge
- Real-world examples from day-to-day sysadmin work
- Quiz questions test understanding, not memorization

### Skill Progression
- **Start (Room 1):** User trying to find files
- **Middle (Room 2):** Admin understanding security model
- **End (Room 3):** Sysadmin automating tasks and troubleshooting

### Career Readiness
After three rooms:
- ✅ Can navigate Linux systems confidently
- ✅ Understand file permissions and security implications
- ✅ Can manage processes and automate with cron
- ✅ Can install software and manage packages
- ✅ Can diagnose problems using logs

**Ready for:** Junior sysadmin role with mentorship

---

## Next Steps

1. **Security+ Exam Preparation** (primary focus)
   - Weak areas: CIA Triad distinctions, PATA strategy, control type classifications
   - Target: 80%+ on practice exams (currently 65-70%)
   - Timeline: 3-month job search deadline

2. **Hands-on Labs** (complement to Security+)
   - Continue TryHackMe rooms (Privilege Escalation, Network Security)
   - HackTheBox labs for penetration testing practice
   - Windows Server and Active Directory homelab

3. **Technical Depth** (after Security+)
   - Linux system administration (deeper)
   - Networking fundamentals
   - Cloud platforms (Azure, AWS basics)

---

## Repository Structure

```
tryhackme-linux-fundamentals/
├── README.md
├── LEARNING-LOG.md (this file)
├── room-01-notes.md
├── room-01-commands-cheatsheet.md
├── room-01-screenshots/
│   ├── 01-basic-navigation.png
│   ├── 02-file-navigation.png
│   ├── 03-wildcards-operators.png
│   └── ...
├── room-02-notes.md
├── room-02-commands-cheatsheet.md
├── room-02-screenshots/
│   ├── 01-file-operations.png
│   ├── 02-file-permissions.png
│   ├── 03-file-ownership.png
│   └── ...
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

**Last Updated:** February 2026  
**Series Status:** Complete (3 of 3 rooms finished)  
**Next Review:** Before Security+ exam preparation
