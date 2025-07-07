# Linux Server Hardening - Project 1

## Overview

This project involved securing a vulnerable Linux server (Ubuntu 20.04.1) for a fictional client, Baker Street Corporation. The hardening process focused on reducing the attack surface, enforcing secure access controls, disabling unnecessary services, and improving system auditability.

## Objectives

- Audit users, groups, and password policies
- Remove unnecessary services and packages
- Harden SSH access and disable root login
- Secure file and directory permissions
- Schedule scripts for ongoing system checks
- Improve logging and log rotation
- Document all changes and risks mitigated

## System Info

- Hostname: `Baker_Street_Linux_Server`  
- OS Version: Ubuntu 20.04.1  
- RAM: ~16 GB  
- Status at handoff: Fully hardened, scripts automated via cron

## Tools & Commands Used

- `ufw` (firewall)  
- `fail2ban`  
- `tar` (system backups)  
- `chmod`, `chown`, `find`, `ls -la` (file permissions)  
- `passwd`, `usermod`, `chage` (user auditing)  
- `cron` (script automation)  
- Bash scripting

## Security Risks Identified

- SSH root login and empty password acceptance enabled  
- Unnecessary services running (MySQL, Samba)  
- World-readable files in `/home/`  
- Excessive log retention (weekly rotation, no size limits)  
- System packages outdated and unpatched

## Security Controls Implemented

- **SSH Hardening:** Root login disabled, protocol restricted, and access limited  
- **Service Pruning:** MySQL and Samba uninstalled, dependencies purged  
- **Log Rotation:** Changed to daily with 7-day retention  
- **File Permissions:** Departmental script access limited by group  
- **User Auditing:** Removed unused users and locked unauthorized accounts  
- **Cron Jobs:**  
  - `hardening_script1.sh` runs monthly  
  - `hardening_script2.sh` runs weekly  

## Deliverables

- `hardened-server-report.pdf` — Full hardening summary  
- `scripts/` — `hardening_script1.sh`, `hardening_script2.sh`  
- `screenshots/` — Visual evidence of tasks completed  
- `checklist.md` — Annotated task checklist with command references

## Recommendations

- Enforce MFA for SSH sessions  
- Encrypt OS backups before storage  
- Enable automatic security updates (`unattended-upgrades`)  
- Strengthen password policy (min length, complexity, expiration)

## Summary

This project demonstrates a real-world example of applying secure configuration principles to a Linux host. The result was a hardened, monitored, and automated system environment prepared for enterprise use.
