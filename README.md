Linux Commands Cheat Sheet
Part 1 · Linux Commands by Usage Domain

A practical reference guide to commonly used Linux commands, including their purposes, syntax examples, and useful tips. Suitable for beginners, system administrators, and Linux interview preparation.

Table of Contents
Navigation and File System

File and Directory Operations

Viewing Files and Processing Text

Permissions and Ownership

Users and Groups

Process Management

System Information and Monitoring

Services, Boot, and Logs

Networking

1. Navigation and File System
Commands for navigating directories, locating files, and inspecting file information.

Command

Purpose

Example

pwd

Print current working directory

pwd

ls

List directory contents

ls -lah /var/log

cd

Change directory

cd ~/projects

cd -

Return to previous directory

cd -

tree

Display directory structure

tree -L 2 /etc

find

Search files by name, size, time, etc.

find / -name '*.conf' -mtime -7 2>/dev/null

locate

Search indexed filenames

locate nginx.conf

updatedb

Update the locate database

sudo updatedb

stat

Display detailed file metadata

stat file.txt

file

Detect file type

file /bin/ls

Useful tips:

ls -lah displays hidden files, detailed information, and human-readable file sizes.

cd - switches back to the previous working directory.

find searches the filesystem directly, whereas locate searches an indexed database.

2. File and Directory Operations
Commands for creating, copying, moving, renaming, deleting, and synchronizing files and directories.

Command

Purpose

Example

cp

Copy files and directories

cp -r src/ backup/

mv

Move or rename files

mv old.txt new.txt

rm

Remove files and directories

rm -r build/

mkdir

Create directories

mkdir -p a/b/c

touch

Create an empty file or update its timestamp

touch notes.md

ln

Create hard or symbolic links

ln -s /opt/app/bin/app app

rsync

Synchronize files locally or remotely

rsync -avz src/ backup/

Important safety warnings:

rm -rf can permanently delete files and directories without prompting. Always verify the target path.

rsync --delete removes destination files that do not exist in the source.

Check source and destination paths before executing synchronization or deletion commands.

3. Viewing Files and Processing Text
Commands for reading, searching, filtering, editing, comparing, and processing text.

Command

Purpose

Example

cat

Display or concatenate files

cat a.txt b.txt

less

Read files page by page

less /var/log/syslog

head

Display the first lines

head -n 20 file.txt

tail

Display the last lines

tail -n 100 app.log

tail -f

Follow a file as it grows

tail -f app.log

grep

Search text using patterns

grep -rin 'error' /var/log/

sed

Transform text streams

sed 's/foo/bar/g' config.ini

awk

Process fields and columns

awk -F: '{print $1}' /etc/passwd

cut

Extract selected fields

cut -d',' -f1,3 data.csv

sort

Sort lines

sort access.log

uniq

Remove adjacent duplicate lines

sort names.txt \| uniq

wc

Count lines, words, and bytes

wc -l *.py

tr

Translate or delete characters

echo hello \| tr a-z A-Z

diff

Compare two files

diff -u old.conf new.conf

xargs

Pass input as command arguments

find . -name '*.tmp' -print0 \| xargs -0 rm

tee

Write output to a file and terminal

ls \| tee list.txt

Useful examples:

Search recursively for errors:


bash
grep -rin 'error' /var/log/
Count occurrences of duplicate lines:


bash
sort access.log | uniq -c | sort -nr
Extract usernames from /etc/passwd:


bash
awk -F: '{print $1}' /etc/passwd
Convert lowercase text to uppercase:


bash
echo hello | tr a-z A-Z
Important tips:

Use grep -r for recursive searching.

Use grep -i for case-insensitive searching.

Use tail -f to monitor logs in real time.

Test sed replacements without -i before modifying files in place.

Use find -print0 with xargs -0 to safely handle filenames containing spaces and special characters.

4. Permissions and Ownership
Commands for managing file permissions, ownership, and administrative privileges.

Command

Purpose

Example

chmod

Change file permissions

chmod 755 script.sh

chown

Change owner and group

sudo chown -R www-data:www-data /var/www

chgrp

Change group ownership

chgrp devs project/

umask

Set the default permission mask

umask 022

sudo

Execute commands with elevated privileges

sudo systemctl status nginx

sudo -u

Run a command as another user

sudo -u postgres psql

Linux Permission Values
Linux uses three basic permission types:

Permission

Symbol

Numeric Value

Read

r

4

Write

w

2

Execute

x

1

Common permission combinations:

Numeric

Symbolic

Meaning

777

rwxrwxrwx

Everyone has full permissions

755

rwxr-xr-x

Owner has full access; others can read and execute

644

rw-r--r--

Owner can read/write; others can read

700

rwx------

Only owner has full access

600

rw-------

Only owner can read/write

Example:


bash
chmod 755 script.sh
This gives:

Owner: Read, Write, Execute.

Group: Read, Execute.

Others: Read, Execute.

5. Users and Groups
Commands for creating, modifying, deleting, and managing Linux users and groups.

Command

Purpose

Example

whoami

Display current username

whoami

id

Display user and group IDs

id alice

useradd

Create a user

sudo useradd -m -s /bin/bash alice

adduser

Create a user (interactive on many distributions)

sudo adduser alice

usermod

Modify an existing user

sudo usermod -aG docker alice

userdel

Delete a user

sudo userdel -r alice

passwd

Set or change a password

sudo passwd alice

groupadd

Create a group

sudo groupadd devs

su

Switch users

su - alice

who

Display logged-in users

who

w

Show logged-in users and their activity

w

last

Show login history

last -n 10

Important tip:

When adding a user to a supplementary group, use:


bash
sudo usermod -aG docker alice
The options mean:

-a: Append the group.

-G: Specify supplementary groups.

Without -a, existing supplementary group memberships may be replaced.

A new login session may be required for group membership changes to take effect.

6. Process Management
Commands for viewing, monitoring, controlling, and managing running processes.

Command

Purpose

Example

ps

Display running processes

ps aux

top

Monitor processes interactively

top

htop

Interactive process monitoring

htop

kill

Send a signal to a process

kill -15 1234

killall

Send signals to processes by name

killall firefox

pkill

Find and signal processes by pattern

pkill -f myapp

pgrep

Find process IDs by name

pgrep -l python

jobs

List shell background jobs

jobs

bg

Resume a job in the background

bg %1

fg

Bring a job to the foreground

fg %1

nohup

Keep a command running after terminal hangup

nohup ./server.sh > out.log 2>&1 &

nice

Start a process with adjusted priority

nice -n 10 ./script.sh

renice

Change process priority

renice +10 -p 1234

lsof

List open files and network sockets

lsof -i :8080

strace

Trace system calls

strace -p 1234

Understanding process signals:

Signal

Number

Purpose

SIGTERM

15

Request graceful process termination

SIGKILL

9

Force immediate process termination

SIGSTOP

19

Stop a process

SIGCONT

18

Resume a stopped process

Important tip:

Prefer graceful termination first:


bash
kill -15 1234
Use forced termination only when necessary:


bash
kill -9 1234
SIGKILL cannot be caught or handled by the target process.

7. System Information and Monitoring
Commands for checking system specifications, resource usage, hardware, and performance.

Command

Purpose

Example

uname

Display kernel/system information

uname -a

uptime

Show system uptime and load averages

uptime

free

Display memory usage

free -h

df

Display filesystem disk space

df -h

du

Estimate directory disk usage

du -sh *

vmstat

Report memory, CPU, and process statistics

vmstat 2 5

iostat

Display CPU and disk I/O statistics

iostat

dmesg

Display kernel messages

dmesg -T \| tail

lscpu

Display CPU information

lscpu

lsblk

List block devices

lsblk -f

lspci

Display PCI devices

lspci

lsusb

Display USB devices

lsusb

hostnamectl

Display or manage hostname and OS information

hostnamectl

Useful distinction:

df -h shows available and used space on mounted filesystems.

du -sh estimates how much space files and directories consume.

These commands answer different questions and may show different results.

8. Services, Boot, and Logs
Commands for managing system services, scheduling jobs, inspecting logs, and controlling system shutdown.

Command

Purpose

Example

systemctl

Manage systemd services

sudo systemctl restart nginx

systemctl status

Check service status

sudo systemctl status nginx

systemctl enable

Enable a service at boot

sudo systemctl enable nginx

systemctl disable

Disable a service at boot

sudo systemctl disable nginx

journalctl

View systemd logs

journalctl -u nginx

journalctl -f

Follow logs in real time

journalctl -u nginx -f

crontab

Schedule recurring jobs

crontab -e

at

Schedule a one-time job

echo 'echo hello' \| at 23:00

shutdown

Shut down or restart the system

sudo shutdown -r +5

reboot

Restart the system

sudo reboot

Enable and start a service immediately:


bash
sudo systemctl enable --now nginx
View logs from the last hour:


bash
journalctl -u nginx --since '1 hour ago'
Understanding Cron Scheduling
Cron uses five fields:


text
* * * * *
│ │ │ │ │
│ │ │ │ └── Day of week
│ │ │ └──── Month
│ │ └────── Day of month
│ └──────── Hour
└────────── Minute
Example:


bash
30 2 * * *
This runs a scheduled job every day at 2:30 AM.

9. Networking
Commands for inspecting network interfaces, testing connectivity, managing connections, transferring files, and troubleshooting network issues.

Command

Purpose

Example

ip

Inspect interfaces and routes

ip a

ip route

Display routing table

ip route

ping

Test network reachability

ping -c 4 8.8.8.8

ss

Inspect network sockets

ss -tulnp

netstat

Inspect network connections

netstat -tulnp

curl

Make HTTP requests

curl -I https://example.com

wget

Download files

wget https://example.com/file.zip

dig

Query DNS records

dig +short example.com

nslookup

Query DNS information

nslookup example.com

traceroute

Trace network paths

traceroute google.com

mtr

Combine ping and traceroute functionality

mtr google.com

ssh

Connect to a remote system

ssh user@host

scp

Securely copy files

scp file.txt user@host:/tmp/

sftp

Secure file transfer

sftp user@host

nc

Test TCP/UDP connections

nc -zv host 22

tcpdump

Capture network packets

sudo tcpdump -i eth0 port 80

ufw

Manage firewall rules

sudo ufw allow 22/tcp

iptables

Configure firewall rules

sudo iptables -L

nft

Manage firewall rules using nftables

sudo nft list ruleset

Useful networking examples:

Check network interfaces:


bash
ip a
Check listening ports:


bash
ss -tulnp
Test website connectivity:


bash
curl -I https://example.com
Check DNS resolution:


bash
dig +short example.com
Test whether a remote TCP port is reachable:


bash
nc -zv example.com 443
Important tip:

For a quick port check, use ss -tulnp. Elevated privileges may be required to see process details for all sockets.

