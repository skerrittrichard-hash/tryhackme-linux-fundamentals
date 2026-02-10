# TryHackMe Linux Fundamentals - Room 2: Complete

## Room Overview

**TryHackMe Room:** Linux Fundamentals Part 2  
**Status:** ✅ Complete - All quiz questions answered  
**Duration:** ~30 minutes (lab) + hands-on practice  
**Difficulty:** Beginner to Intermediate  
**Hands-On Labs:** Yes (interactive terminal, practical exercises)

## What This Room Covers

Room 2 builds on Room 1 fundamentals and introduces **file system administration**, focusing on permissions, ownership, and practical file management. These are critical skills for sysadmin work.

### Topics Covered

1. **File and Directory Operations**
   - Creating files and directories (touch, mkdir)
   - Copying files and directories (cp, cp -r)
   - Moving and renaming files (mv)
   - Removing files and directories (rm, rmdir, rm -r)
   - Understanding directory structure

2. **File Permissions - Symbolic Format**
   - Understanding read (r), write (w), execute (x)
   - User (u), group (g), others (o)
   - Changing permissions with `chmod` (symbolic)
   - Permission examples: `chmod u+x file` (add execute for user)

3. **File Permissions - Numeric Format**
   - Converting permissions to numbers (4=read, 2=write, 1=execute)
   - Numeric permission format (0-7 for each position)
   - Examples: 755, 644, 777 and what they mean
   - Using `chmod` with numeric values

4. **File Ownership**
   - Understanding user and group ownership
   - Changing owner with `chown`
   - Changing group with `chgrp`
   - Viewing ownership with `ls -l`

5. **Understanding the ls Command**
   - `ls` flags and options (-l, -h, -a, -R, etc.)
   - Interpreting long format output
   - Human-readable sizes (-h flag)
   - Recursive directory listing (-R flag)

6. **Manual Pages and Documentation**
   - Using `man` command for command documentation
   - Reading manual page sections
   - Finding command help (`--help` flag)
   - Understanding command options

7. **Practical File Management**
   - Creating directory structures
   - Managing file ownership
   - Setting appropriate permissions
   - Organizing files efficiently

## Sysadmin Relevance

**Why These Skills Matter for Your Target Role:**

| Skill | Sysadmin Use |
|-------|--------------|
| File operations | Create backup dirs, organize logs, manage configs |
| Permissions (symbolic) | Quick permission fixes (chmod u+x script.sh) |
| Permissions (numeric) | Bulk permission changes, security hardening |
| Ownership | Ensure services run as correct user, prevent privilege issues |
| `ls` flags | Quickly identify file sizes, permissions, ownership issues |
| `man` pages | Self-service learning, understanding command syntax |

**Real-World Scenarios:**
- Fix a script that won't run: `chmod u+x script.sh`
- Check why service won't start: `ls -l` to see if ownership is correct
- Secure a web directory: `chmod 755 /var/www` (user:rwx, group:rx, others:rx)
- Find large log files consuming disk space: `ls -lh /var/log`
- Read command documentation quickly: `man chmod` instead of searching online

## Lab Completion Evidence

✅ **All Quiz Questions Answered Correctly**

### Task Breakdown

**Task 3: Understanding File Permissions - Numeric Format**
- ✅ Converting symbolic to numeric permissions
- ✅ Understanding 4/2/1 numeric values
- ✅ Permission examples (755, 644, 777)

**Task 4: Changing File & Directory Permissions (Part 1)**
- ✅ Creating files and directories
- ✅ Understanding default permissions
- ✅ Modifying permissions with chmod

**Task 5: Changing File & Directory Permissions (Part 2)**
- ✅ Understanding why permissions matter
- ✅ Practical permission examples
- ✅ Security implications of permission choices

**Task 6: Command Ownership Permissions**
- ✅ Understanding ownership (user, group)
- ✅ Using `chown` and `chgrp`
- ✅ Ownership and permissions relationship

**Task 7: User Encountered Issues (Part 1)**
- ✅ Diagnosing permission problems
- ✅ Finding and fixing file access issues
- ✅ Using `ls -l` to troubleshoot

**Task 8: User Encountered Issues (Part 2)**
- ✅ Real-world permission troubleshooting
- ✅ Common permission mistakes
- ✅ Practical problem-solving

## Key Commands Reference

```bash
# File and Directory Creation
touch filename              # Create empty file
mkdir directory            # Create directory
mkdir -p dir1/dir2/dir3   # Create nested directories

# Copying and Moving
cp source destination      # Copy file
cp -r source dest         # Copy directory recursively
mv source destination     # Move/rename file
rm filename               # Delete file
rmdir directory           # Delete empty directory
rm -r directory           # Delete directory recursively

# Permission Changes (Symbolic)
chmod u+x file           # Add execute for user
chmod g+r file           # Add read for group
chmod o-w file           # Remove write for others
chmod a=rwx file         # Set full permissions for all

# Permission Changes (Numeric)
chmod 755 file           # rwxr-xr-x (typical for scripts)
chmod 644 file           # rw-r--r-- (typical for files)
chmod 777 file           # rwxrwxrwx (full permissions, rarely used)

# Ownership Changes
chown user file          # Change owner
chown user:group file    # Change owner and group
chgrp group file         # Change group only

# Viewing Information
ls -l                    # Long format (shows permissions)
ls -lh                   # Human-readable sizes
ls -la                   # Show hidden files too
ls -R                    # Recursive (subdirectories)

# Documentation
man command              # View manual page
command --help           # Show help (shorter than man)
```

## Learning Experience

**What Worked Well:**
- Practical exercises with real file operations
- Manual pages teach self-service learning
- Permissions concepts directly applicable to job
- Quiz questions test understanding, not memorization

**Key Insight:**
Permissions are the foundation of Linux security. Every file/directory has owner and access controls. This is why sysadmins need to understand this deeply—misconfigured permissions are a major security risk.

**How This Fits Your Career Path:**
- **Foundation:** File permissions are non-negotiable sysadmin knowledge
- **Interview Prep:** Expect questions on `chmod 755` vs `chmod 644`
- **Job Readiness:** Permission troubleshooting is daily work
- **Security:** Understanding principle of least privilege

## Security+ Alignment

Room 2 supports Security+ in:
- **Access Control:** File-level RBAC (permissions, ownership)
- **Principle of Least Privilege:** Setting minimal necessary permissions
- **Defense-in-Depth:** Permissions as a detective control
- **Configuration Hardening:** Secure file permissions

## Connection to Room 1

**Room 1 → Room 2 Progression:**

| Room 1 | Room 2 |
|--------|--------|
| Navigate filesystem | Manage filesystem contents |
| Search for files | Create/organize files |
| Understand directory structure | Control access to directories |
| Basic commands | Advanced command options |

Room 2 uses Room 1 skills constantly. You're using `ls`, `cd`, directory navigation to work with permissions and ownership.

## Progression to Room 3

Room 3 will cover:
- **Processes & Services** - Managing running applications
- **Process ownership** - Which user runs which service
- **Stopping/starting services** - Using systemctl, service commands
- **Background processes** - Managing long-running tasks
- **Logging** - Where processes write output

Room 2 permissions knowledge is prerequisite for understanding why services must run as specific users.

## Portfolio Relevance

**Why Document Room 2?**
1. **Shows progression:** Room 1 basics → Room 2 admin skills
2. **Demonstrates core competency:** Permissions aren't optional for sysadmins
3. **Proves hands-on learning:** Not just theory
4. **Job preparation:** These exact skills needed for UK junior sysadmin roles

**Recruiter Perspective:**
- "Candidate understands file permissions (critical)"
- "They've progressed beyond basic navigation"
- "Ready for practical sysadmin tasks"
- "Can troubleshoot permission issues"

## Personal Reflection

Room 2 shifted understanding from "Linux is a file system" to "Linux is a permission system." Every file has owner and access controls. This is what makes Linux secure and multi-user. The numeric permission format (755, 644) makes sense now—it's elegant and powerful.

The `man` command revelation was important: I can self-serve answers instead of searching Google. That's a sysadmin skill.

---

**Completed:** February 2026  
**Room Link:** https://tryhackme.com/room/linuxfundamentalspart2  
**Time Investment:** ~30 minutes  
**Skill Level After:** Novice → Early Intermediate Linux user  
**Next Room:** Linux Fundamentals Part 3 (processes, services, logging)

**Repository:** tryhackme-linux-fundamentals  
**Structure:** room-02-notes.md, room-02-commands-cheatsheet.md, LEARNING-LOG.md (updated)
