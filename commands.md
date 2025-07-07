# Linux Server Hardening – Commands

## 1. Create Full System Backup
```bash
sudo tar -cvpzf /baker_street_backup.tar.gz --exclude=/baker_street_backup.tar.gz --exclude=/proc --exclude=/tmp --exclude=/mnt --exclude=/sys --exclude=/dev --exclude=/run /
```

## 2. Audit and Remove Users
```bash
sudo userdel -r lestrade
sudo userdel -r irene
sudo userdel -r mary
sudo userdel -r gregson

getent passwd lestrade irene mary gregson
```

## 3. Lock Unauthorized Accounts
```bash
sudo passwd -l moriarty
sudo passwd -l mrs_hudson

sudo passwd -S moriarty
sudo passwd -S mrs_hudson
```

## 4. Unlock Valid Users
```bash
sudo passwd -u sherlock
sudo passwd -u watson
sudo passwd -u mycroft
sudo passwd -u toby
sudo passwd -u adler
```

## 5. Group Management
```bash
addgroup research
delgroup marketing
```

## 6. Enforce Strong Password Policy
```bash
sudo nano /etc/login.defs
# Set: PASS_MIN_LEN 12

sudo nano /etc/pam.d/common-password
# Add: password requisite pam_pwquality.so retry=3 minlen=12 difok=3
```

## 7. Harden sudo Permissions (Restrict who can sudo)
```bash
sudo visudo
# Edit: Only allow authorized users or groups like '%admin' or 'sherlock'
```

## 8. Audit and Correct File Permissions
```bash
sudo find /home -type f -perm -o=w -exec chmod o-w {} \;
sudo chown :research /opt/scripts/research/*
sudo chmod 770 /opt/scripts/research/*
```

## 9. Update System and Packages
```bash
sudo apt update && sudo apt upgrade -y
```

## 10. Remove Unnecessary Services
```bash
sudo systemctl disable mysql
sudo apt purge mysql-server -y

sudo systemctl disable smbd
sudo apt purge samba -y
```

## 11. Harden SSH
```bash
sudo nano /etc/ssh/sshd_config
# Set:
# PermitRootLogin no
# PermitEmptyPasswords no
# Protocol 2

sudo systemctl restart ssh
```

## 12. Configure Firewall
```bash
sudo ufw allow ssh
sudo ufw enable
```

## 13. Configure Log Rotation
```bash
sudo nano /etc/logrotate.conf
# Change rotation to daily
# Set rotate 7
```

## 14. Schedule Security Scripts with Cron
```bash
sudo crontab -e
# Add:
# 0 0 1 * * /root/hardening_script1.sh
# 0 0 * * 1 /root/hardening_script2.sh
```

## 15. Enable Automatic Security Updates
```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

## 16. Encrypt Backup (Optional)
```bash
gpg -c /baker_street_backup.tar.gz
