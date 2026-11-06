# Linux Command Cheat Sheet

A practical Linux command reference for Cloud Security and Cybersecurity.

## 1. Basic Navigation Commands

| Command | Description | Example |
|---|---|---|
| `pwd` | Display current directory | `pwd` |
| `ls` | List files and directories | `ls` |
| `ls -l` | Detailed file listing | `ls -l` |
| `ls -la` | Show hidden files | `ls -la` |
| `cd` | Change directory | `cd /var/log` |
| `cd ..` | Move one directory back | `cd ..` |
| `cd ~` | Go to home directory | `cd ~` |
| `clear` | Clear terminal | `clear` |
| `history` | Show command history | `history` |

## 2. File and Directory Management

| Command | Description | Example |
|---|---|---|
| `touch` | Create empty file | `touch test.txt` |
| `mkdir` | Create directory | `mkdir project` |
| `mkdir -p` | Create nested directories | `mkdir -p app/logs` |
| `rmdir` | Remove empty directory | `rmdir project` |
| `cp` | Copy file | `cp a.txt b.txt` |
| `cp -r` | Copy directory | `cp -r app backup` |
| `mv` | Move or rename file | `mv old.txt new.txt` |
| `rm` | Delete file | `rm test.txt` |
| `rm -r` | Delete directory recursively | `rm -r project` |
| `file` | Identify file type | `file test.txt` |
| `stat` | Display file metadata | `stat test.txt` |

**Important:** Be careful with `rm -rf`. It can permanently delete files and directories without confirmation.

## 3. Viewing and Reading Files

| Command | Description | Example |
|---|---|---|
| `cat` | Display file contents | `cat file.txt` |
| `less` | Read file page by page | `less file.txt` |
| `more` | Read file page by page | `more file.txt` |
| `head` | Show first 10 lines | `head file.txt` |
| `head -n 20` | Show first 20 lines | `head -n 20 file.txt` |
| `tail` | Show last 10 lines | `tail file.txt` |
| `tail -n 50` | Show last 50 lines | `tail -n 50 file.txt` |
| `tail -f` | Monitor log continuously | `tail -f /var/log/syslog` |
| `wc -l` | Count lines | `wc -l file.txt` |

## 4. Linux User Management

| Command | Description | Example |
|---|---|---|
| `whoami` | Current logged-in user | `whoami` |
| `id` | Display user and group IDs | `id` |
| `who` | Show logged-in users | `who` |
| `w` | Show logged-in users and activity | `w` |
| `useradd` | Create user | `sudo useradd john` |
| `adduser` | Create user interactively (common on Ubuntu) | `sudo adduser john` |
| `passwd` | Change password | `sudo passwd john` |
| `usermod` | Modify user | `sudo usermod -aG sudo john` |
| `userdel` | Delete user | `sudo userdel john` |
| `groupadd` | Create group | `sudo groupadd developers` |
| `groups` | Display user groups | `groups john` |
| `getent passwd` | List user account entries | `getent passwd` |

## 5. Linux File Permissions

Linux permissions:

- `r` = Read (4)
- `w` = Write (2)
- `x` = Execute (1)

| Command | Description | Example |
|---|---|---|
| `ls -l` | View permissions | `ls -l file.txt` |
| `chmod` | Change permissions | `chmod 755 script.sh` |
| `chmod 644` | Owner read/write, others read | `chmod 644 file.txt` |
| `chmod 700` | Owner has full access only | `chmod 700 private.sh` |
| `chmod +x` | Add execute permission | `chmod +x script.sh` |
| `chown` | Change file owner | `sudo chown john file.txt` |
| `chgrp` | Change group ownership | `sudo chgrp developers file.txt` |

Example:

```bash
chmod 755 script.sh
```

Permission breakdown:

- Owner: 7 = Read + Write + Execute
- Group: 5 = Read + Execute
- Others: 5 = Read + Execute

## 6. Process Management

| Command | Description | Example |
|---|---|---|
| `ps` | Show running processes | `ps` |
| `ps aux` | Show all processes | `ps aux` |
| `top` | Real-time process monitoring | `top` |
| `htop` | Interactive process monitoring | `htop` |
| `pgrep` | Find process ID | `pgrep nginx` |
| `pstree` | Display process tree | `pstree` |
| `kill` | Terminate process | `kill 1234` |
| `kill -9` | Forcefully terminate process | `kill -9 1234` |
| `nice` | Start process with priority | `nice -n 10 command` |
| `nohup` | Run process immune to hangups | `nohup ./script.sh &` |

## 7. Service Management (systemd)

| Command | Description | Example |
|---|---|---|
| `systemctl status` | Check service status | `systemctl status ssh` |
| `systemctl start` | Start service | `sudo systemctl start nginx` |
| `systemctl stop` | Stop service | `sudo systemctl stop nginx` |
| `systemctl restart` | Restart service | `sudo systemctl restart nginx` |
| `systemctl reload` | Reload service configuration | `sudo systemctl reload nginx` |
| `systemctl enable` | Enable service at boot | `sudo systemctl enable nginx` |
| `systemctl disable` | Disable service at boot | `sudo systemctl disable nginx` |
| `systemctl list-units` | List active units | `systemctl list-units` |
| `systemctl is-active` | Check if service is active | `systemctl is-active ssh` |

## 8. Linux Logs and Troubleshooting

Important Linux log locations:

| Log file | Purpose |
|---|---|
| `/var/log/syslog` | General system logs (Ubuntu/Debian) |
| `/var/log/messages` | General system logs (RHEL-based systems) |
| `/var/log/auth.log` | Authentication logs (Ubuntu/Debian) |
| `/var/log/secure` | Authentication logs (RHEL-based systems) |
| `/var/log/kern.log` | Kernel logs (where configured) |
| `/var/log/dmesg` | Boot and kernel messages (where available) |

Commands:

| Command | Description | Example |
|---|---|---|
| `journalctl` | View systemd logs | `journalctl` |
| `journalctl -xe` | View recent detailed logs | `journalctl -xe` |
| `journalctl -u` | View service logs | `journalctl -u ssh` |
| `journalctl -f` | Follow live logs | `journalctl -f` |
| `dmesg` | View kernel messages | `dmesg` |
| `grep` | Search log entries | `grep "Failed" /var/log/auth.log` |
| `tail -f` | Monitor logs live | `tail -f /var/log/syslog` |

## 9. Networking Commands

| Command | Description | Example |
|---|---|---|
| `ip addr` | Display IP addresses | `ip addr` |
| `ip link` | Display network interfaces | `ip link` |
| `ip route` | Display routing table | `ip route` |
| `ping` | Test network connectivity | `ping google.com` |
| `ss -tulnp` | Display listening ports and processes | `sudo ss -tulnp` |
| `netstat -tulnp` | Display network connections (if installed) | `sudo netstat -tulnp` |
| `curl` | Send HTTP requests | `curl https://example.com` |
| `wget` | Download files | `wget https://example.com/file.zip` |
| `dig` | DNS lookup | `dig google.com` |
| `nslookup` | DNS lookup | `nslookup google.com` |
| `traceroute` | Trace network path | `traceroute google.com` |
| `hostname` | Display hostname | `hostname` |
| `hostname -I` | Display assigned IP addresses | `hostname -I` |

## 10. SSH Commands

| Command | Description | Example |
|---|---|---|
| `ssh` | Connect to remote server | `ssh user@192.168.1.10` |
| `ssh -p` | Connect using custom port | `ssh -p 2222 user@server` |
| `ssh-keygen` | Generate SSH key pair | `ssh-keygen -t ed25519` |
| `ssh-copy-id` | Copy public key to remote server | `ssh-copy-id user@server` |
| `scp` | Copy file to remote server | `scp file.txt user@server:/tmp/` |
| `scp -r` | Copy directory | `scp -r folder user@server:/tmp/` |

## 11. Disk and Storage Management

| Command | Description | Example |
|---|---|---|
| `df -h` | Display disk usage | `df -h` |
| `du -sh` | Display directory size | `du -sh /var/log` |
| `du -h` | Display file/directory sizes | `du -h /home` |
| `lsblk` | List block devices | `lsblk` |
| `blkid` | Display block device UUIDs | `sudo blkid` |
| `mount` | Mount filesystem | `sudo mount /dev/sdb1 /mnt` |
| `umount` | Unmount filesystem | `sudo umount /mnt` |
| `free -h` | Display memory usage | `free -h` |
| `fdisk -l` | List disk partitions | `sudo fdisk -l` |

## 12. Package Management

### Ubuntu / Debian

```bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
sudo apt purge nginx
sudo apt autoremove
```

### RHEL / Amazon Linux / Fedora

```bash
sudo dnf check-update
sudo dnf upgrade
sudo dnf install nginx
sudo dnf remove nginx
sudo dnf list installed
```

Older RHEL-based systems may use `yum`.

## 13. Search Commands

| Command | Description | Example |
|---|---|---|
| `find` | Search files and directories | `find /home -name "test.txt"` |
| `grep` | Search text | `grep "error" app.log` |
| `grep -i` | Case
