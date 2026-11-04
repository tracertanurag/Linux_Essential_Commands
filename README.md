Linux Commands Cheat Sheet

A practical reference guide to commonly used Linux commands, organized by usage domain, with explanations and examples.

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
Command	Purpose	Example
pwd	Print current working directory	pwd
ls	List directory contents	ls -lah /var/log
cd	Change directory	cd ~/projects
tree	Display directory tree	tree -L 2 /etc
find	Search files and directories	find . -name '*.conf'
locate	Search indexed filenames	locate nginx.conf
stat	Show file metadata	stat file.txt
file	Detect file type	file /bin/ls

Tip: ls -lah displays hidden files, detailed information, and human-readable sizes. cd - returns to the previous directory.

2. File and Directory Operations
Command	Purpose	Example
cp	Copy files and directories	cp -r src/ backup/
mv	Move or rename files	mv old.txt new.txt
rm	Remove files and directories	rm -r build/
mkdir	Create directories	mkdir -p a/b/c
touch	Create files or update timestamps	touch notes.md
ln	Create hard or symbolic links	ln -s /opt/app/bin/app app
rsync	Synchronize files locally or remotely	rsync -avz src/ backup/

Warning: rm -rf can permanently delete files without prompting. Always verify paths before executing destructive commands. Similarly, rsync --delete removes destination files that are absent from the source.

3. Viewing Files and Processing Text
Command	Purpose	Example
cat	Display or concatenate files	cat a.txt b.txt
less	Read files page by page	less /var/log/syslog
head	Display first lines	head -n 20 file.txt
tail	Display last lines	tail -n 100 -f app.log
grep	Search text patterns	grep -rin 'error' /var/log/
sed	Transform text streams	sed 's/foo/bar/g' config.ini
awk	Process fields and columns	awk -F: '{print $1}' /etc/passwd
cut	Extract selected fields	cut -d',' -f1,3 data.csv
sort	Sort lines	sort access.log
uniq	Remove adjacent duplicates	sort names.txt | uniq
wc	Count lines, words, and bytes	wc -l *.py
tr	Translate or delete characters	echo hello | tr a-z A-Z
diff	Compare files	diff -u old.conf new.conf
xargs	Pass input as command arguments	find . -name '*.tmp'
tee	Write output to a file and terminal	ls | tee list.txt

Tip: Use grep -r for recursive searching and -i for case-insensitive matching. Test sed replacements without -i before modifying files in place.

4. Permissions and Ownership
Command	Purpose	Example
chmod	Change file permissions	chmod 755 script.sh
chown	Change owner and group	sudo chown user:group file.txt
chgrp	Change group ownership	chgrp devs project/
umask	Set default permission mask	umask 022
sudo	Execute with elevated privileges	sudo systemctl status nginx
Linux Permission Values

| Permission | Numeric

##
