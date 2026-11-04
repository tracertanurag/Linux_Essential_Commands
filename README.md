🐧 Linux Commands Cheat Sheet

<p align="center">
<img src="https://img.shields.io/badge/Linux-Commands-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux Commands"/>
<img src="https://img.shields.io/badge/Level-Beginner%20to%20Advanced-2ea44f?style=for-the-badge" alt="Skill Level"/>
<img src="https://img.shields.io/badge/Documentation-Reference-blue?style=for-the-badge" alt="Documentation"/>
</p>

<p align="center">
<b>A practical, organized, and beginner-friendly reference to essential Linux commands.</b>
<br/>
Learn Linux commands with explanations, real-world examples, useful tips, and practical use cases.
</p>

📌 About This Repository

This repository contains a comprehensive Linux Commands Cheat Sheet designed for:

🐧 Linux beginners and enthusiasts
💻 Developers and system administrators
☁️ DevOps and Cloud Engineers
🔐 Cybersecurity learners
🎯 Linux interview preparation

Whether you're learning Linux for the first time or need a quick command reference, this guide will help you work more efficiently in the terminal.

📚 Table of Contents
#	Topic	Description
01	Navigation & File System	Navigate directories and locate files
02	File & Directory Operations	Create, copy, move, and delete files
03	Viewing & Text Processing	Read, search, and manipulate text
04	Permissions & Ownership	Manage Linux permissions
05	Users & Groups	Manage users and groups
06	Process Management	Monitor and control processes
07	System Monitoring	Monitor system resources
08	Services & Logs	Manage services and system logs
09	Networking	Network troubleshooting and connectivity
10	Quick Revision	Frequently used Linux commands
🖥️ 01. Navigation & File System

Commands for navigating directories, locating files, and inspecting file information.

Command	Description	Example
pwd	Print current directory	pwd
ls	List directory contents	ls -lah /var/log
cd	Change directory	cd ~/projects
cd -	Return to previous directory	cd -
tree	Display directory structure	tree -L 2 /etc
find	Search files and directories	find . -name '*.conf'
locate	Search indexed filenames	locate nginx.conf
updatedb	Update locate database	sudo updatedb
stat	Display file metadata	stat file.txt
file	Identify file type	file /bin/ls
💡 Pro Tip: ls -lah displays hidden files, detailed information, and human-readable file sizes. Use cd - to switch to your previous directory.
📁 02. File & Directory Operations

Commands for creating, copying, moving, renaming, deleting, and synchronizing files.

Command	Description	Example
cp	Copy files and directories	cp -r src/ backup/
mv	Move or rename files	mv old.txt new.txt
rm	Remove files and directories	rm -r build/
mkdir	Create directories	mkdir -p a/b/c
touch	Create files or update timestamps	touch notes.md
ln	Create symbolic or hard links	ln -s /opt/app/bin/app app
rsync	Synchronize files	rsync -avz src/ backup/
⚠️ Warning: Be extremely careful with rm -rf and rsync --delete. These commands can permanently remove files. Always verify source and destination paths before execution.
📝 03. Viewing Files & Text Processing

Commands for reading, searching, filtering, and manipulating text.

Command	Description	Example
cat	Display file contents	cat file.txt
less	Read files page by page	less /var/log/syslog
head	Display first lines	head -n 20 file.txt
tail	Display last lines	tail -n 100 app.log
tail -f	Follow live log updates	tail -f app.log
grep	Search text patterns	grep -rin 'error' /var/log/
sed	Transform text streams	sed 's/foo/bar/g' config.ini
awk	Process text fields	awk -F: '{print $1}' /etc/passwd
cut	Extract selected fields	cut -d',' -f1,3 data.csv
sort	Sort lines	sort access.log
uniq	Remove adjacent duplicates	sort names.txt | uniq
wc	Count lines, words, bytes	wc -l *.py
tr	Translate characters	echo hello | tr a-z A-Z
diff	Compare files	diff -u old.conf new.conf
xargs	Pass input as arguments	find . -name '*.tmp' -print0 | xargs -0 rm
tee	Write output to file and terminal	ls | tee list.txt
🔍 Useful Examples

Search for errors recursively:

bash
grep -rin 'error' /var/log/


Count duplicate entries:

bash
sort access.log | uniq -c | sort -nr


Extract usernames:

bash
awk -F: '{print $1}' /etc/passwd


Convert lowercase to uppercase:

bash
echo hello | tr a-z A-Z

💡 Pro Tip: Use grep -r for recursive searching and grep -i for case-insensitive searches. Test sed replacements before using its in-place editing option.
🔐 04. Permissions & Ownership

Commands for managing Linux file permissions and ownership.

Command	Description	Example
chmod	Change file permissions	chmod 755 script.sh
chown	Change owner and group	sudo chown user:group file.txt
chgrp	Change group ownership	chgrp devs project/
umask	Set default permission mask	umask 022
sudo	Execute commands with elevated privileges	sudo systemctl status nginx
sudo -u	Execute as another user	sudo -u postgres psql
Permission Reference
Permission	Symbol	Value
Read	r	4
Write	w	2
Execute	x	1
Common Permission Combinations
Permission	Meaning
777	Full permissions for everyone
755	Owner: full; others: read and execute
644	Owner: read/write; others: read
700	Full permissions for owner only
600	Read/write for owner only

Example:

bash
chmod 755 script.sh


This provides read, write, and execute permissions to the owner, and read and execute permissions to the group and others.

👥 05. Users & Groups

Commands for creating, modifying, deleting, and managing users and groups.

Command	Description	Example
whoami	Display current username	whoami
id	Display user and group IDs	id alice
useradd	Create a user	sudo useradd -m -s /bin/bash alice
adduser	Interactive user creation	sudo adduser alice
usermod	Modify user properties	sudo usermod -aG docker alice
userdel	Delete a user	sudo userdel -r alice
passwd	Change user password	sudo passwd alice
groupadd	Create a group	sudo groupadd devs
su	Switch users	su - alice
who	Show logged-in users	who
w	Show user activity	w
last	Show login history	last -n 10
💡 Important: Use usermod -aG when adding a supplementary group. The -a option appends the group without replacing existing supplementary group memberships.
⚙️ 06. Process Management

Commands for monitoring, controlling, and managing running processes.

Command	Description	Example
ps	Display running processes	ps aux
top	Interactive process monitoring	top
htop	Advanced process monitoring	htop
kill	Send a signal to a process	kill -15 1234
killall	Signal processes by name	killall firefox
pkill	Signal processes by pattern	pkill -f myapp
pgrep	Find process IDs	pgrep -l python
jobs	List shell jobs	jobs
bg	Resume job in background	bg %1
fg	Bring job to foreground	fg %1
nohup	Keep process running after terminal hangup	nohup ./server.sh > out.log 2>&1 &
nice	Set process priority	nice -n 10 ./script.sh
renice	Change process priority	renice +10 -p 1234
lsof	List open files	lsof -i :8080
strace	Trace system calls	strace -p 1234
Process Signals
Signal	Number	Description
SIGTERM	15	Graceful termination request
SIGKILL	9	Force termination
SIGSTOP	19	Stop process
SIGCONT	18	Resume process
💡 Pro Tip: Prefer kill -15 PID before using kill -9 PID. SIGTERM allows a process to shut down gracefully, while SIGKILL cannot be caught or handled.
📊 07. System Information & Monitoring

Commands for monitoring CPU, memory, storage, hardware, and system performance.

Command	Description	Example
uname	Display kernel information	uname -a
uptime	Display uptime and load average	uptime
free	Display memory usage	free -h
df	Check filesystem disk space	df -h
du	Estimate directory size	du -sh *
vmstat	Display system statistics	vmstat 2 5
iostat	Display CPU and disk I/O statistics	iostat
dmesg	Display kernel messages	dmesg -T | tail
lscpu	Display CPU information	lscpu
lsblk	List block devices	lsblk -f
lspci	Display PCI devices	lspci
lsusb	Display USB devices	lsusb
hostnamectl	Display hostname and OS information	hostnamectl
💡 Pro Tip: df -h checks filesystem space, whereas du -sh estimates how much storage files and directories consume.
🔧 08. Services, Boot & Logs

Commands for managing systemd services, scheduling tasks, and troubleshooting system logs.

Command	Description	Example
systemctl	Manage system services	sudo systemctl restart nginx
systemctl status	Check service status	sudo systemctl status nginx
systemctl enable	Enable service at boot	sudo systemctl enable nginx
systemctl disable	Disable service at boot	sudo systemctl disable nginx
journalctl	View system logs	journalctl -u nginx
journalctl -f	Follow logs live	journalctl -u nginx -f
crontab	Schedule recurring tasks	crontab -e
at	Schedule one-time tasks	echo 'echo hello' | at 23:00
shutdown	Shut down or restart system	sudo shutdown -r +5
reboot	Restart system	sudo reboot
Start a Service and Enable It at Boot
bash
sudo systemctl enable --now nginx

View Logs From the Last Hour
bash
journalctl -u nginx --since '1 hour ago'

Cron Job Scheduling

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


Runs a scheduled task every day at 2:30 AM.

🌐 09. Networking

Commands for network configuration, connectivity testing, troubleshooting, and secure file transfers.

Command	Description	Example
ip	Display interfaces and addresses	ip a
ip route	Display routing table	ip route
ping	Test connectivity	ping -c 4 8.8.8.8
ss	Inspect sockets and ports	ss -tulnp
netstat	Display network connections	netstat -tulnp
curl	Make HTTP requests	curl -I https://example.com
wget	Download files	wget https://example.com/file.zip
dig	Query DNS records	dig +short example.com
nslookup	Perform DNS lookup	nslookup example.com
traceroute	Trace network path	traceroute google.com
mtr	Network diagnostic tool	mtr google.com
ssh	Connect to remote systems	ssh user@host
scp	Securely copy files	scp file.txt user@host:/tmp/
sftp	Secure file transfer	sftp user@host
nc	Test TCP/UDP connectivity	nc -zv host 22
tcpdump	Capture network packets	sudo tcpdump -i eth0 port 80
ufw	Manage firewall rules	sudo ufw allow 22/tcp
iptables	Configure firewall rules	sudo iptables -L
nft	Manage nftables firewall rules	sudo nft list ruleset
Useful Networking Commands

Check IP addresses:

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


Test a remote TCP port:

bash
nc -zv example.com 443

💡 Pro Tip: Use ss -tulnp to inspect listening sockets. Root privileges may be required to see process details for all sockets.
🚀 10. Quick Revision

A quick reference to the most frequently used Linux commands.

Task	Command
Current directory	pwd
List all files	ls -lah
Change directory	cd /path
Find files	find . -name filename
Create directory	mkdir -p directory
Copy directory	cp -r source destination
Remove directory	rm -r directory
Read file	cat file.txt
Search text	grep -i 'text' file.txt
Monitor logs	tail -f app.log
Change permissions	chmod 755 file
Current user	whoami
List processes	ps aux
Monitor processes	top
Check memory	free -h
Check disk space	df -h
Check service	systemctl status nginx
View logs	journalctl -xe
Check IP address	ip a
Check listening ports	ss -tulnp
Test connectivity	ping -c 4 google.com
Connect remotely	ssh user@host
⭐ Linux Best Practices
Always verify paths before executing destructive commands.
Use sudo only when necessary.
Read command documentation using man command.
Use command --help to understand available options.
Understand permissions before modifying files.
Prefer graceful process termination.
Monitor disk space and memory regularly.
Check logs when troubleshooting errors.
Use SSH keys for secure remote authentication.
Practice commands in a safe environment before using them in production.
📖 How to Use This Repository
Clone the repository:
bash
git clone <YOUR-REPOSITORY-URL>

Navigate into the project:
bash
cd linux-commands-cheat-sheet

Open the README and explore each section.
Practice commands in your Linux terminal.
🤝 Contributing

Contributions are welcome!

If you have useful Linux commands, corrections, or improvements:

Fork this repository.
Create a new branch.
Make your changes.
Submit a Pull Request.

Let's make Linux learning easier for everyone!

📜 License

This project is available for educational and learning purposes. You may use, share, and contribute to this resource.

<p align="center">
<b>🐧 Learn Linux. Practice Daily. Master the Terminal.</b>
<br/>
If you find this repository helpful, consider giving it a ⭐ Star!
</p>
