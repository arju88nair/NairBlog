---
title: "Linux"
date: 2018-11-19T20:19:34+05:30
draft: false
tags : [
    'Linux',
    'TIL'
]
---
`Most of the notes are from LinuxNotesForProfessionals`



- Terminal = text input/output environment
- Console = physical terminal
- Shell = command line interpreter

-----------

`hostname`  - Display hostname of the system

`who` - List of all the users currently logged in as a user.

`w` - Display current system status, time, duration, list of users currently logged in on system and other user information.

`last` -  Who recently used the system.

`lastb` - Shows all bad login attempts into the system.

`find . -name '*.txt` -  Find files

`grep -R blah .` Find text in files

View the contents of a file:`cat yFirstFile`

View the content of a file with pager (one screenful at a time):`less myFirstFile`

View the first several lines of a file:`head myFirstFile`

View the last several lines of a file:`tail myFirstFile`

`ls -sh ` To list with size

`ls -shR ` To list with size and recursively for folders

`history` will show the command history

`history | grep <key-word>` will show all the commands in history having keyword <key-word> 

`alias install='sudo apt-get -y install'`


`locate pem | grep mykey` 

`du -sh *` - In current directory

`du -sh .[!.]* *` - Current directory


`du -sch *`  - Total

`df -h` - Disk space

`free` - Ram usage

` iostat -kx 2 ` - General information about your disk operations in real time

`netstat -ntlp` # open TCP sockets

`netstat -nulp` # open UDP sockets

`netstat -nxlp` # open Unix sockets


`sudo iftop ` -  network traffic in real 
time
----
| Services

`systemctl` -Running services

`service --status-all` - Running services

`systemctl get-default` To find the default target for your system

`systemctl set-default <target-name>` To set the default target for your system

`journalctl -f -t sshd` - Logs for a particular service


----

`passwd` - Changing password

`useradd username`

`userdel -r username` -Delete as root


`groups` - Listing groups the current user is in


-----

| Tee
`tee` - read from standard input and write to standard output and files.

The following command writes the output only to the file and not to the screen.

`ls > file`

The following command (with the help of tee command) writes the output both to the screen (stdout) and to the
file.

` ls | tee file`


To store the output of a command in a file and redirect the same output to another
command.

This will write current crontab entries to a file crontab-backup.txt and pass the crontab
entries to sed command, which will do the substituion. After the substitution, it will be added as a new cron job.

 `crontab -l | tee crontab-backup.txt | sed 's/old/new/' | crontab –`


- `SED` is a powerful text stream editor. Can do insertion, deletion, search and replace(substitution).
- `SED` command in unix supports regular expression which allows it perform complex pattern matching.

`sed 's/old/new/'`  - Replaces old with new

`sed 's/unix/linux/2' blah.txt` - Replace nth

`sed 's/unix/linux/g' blah.txt` - Replace all

`sed 's/unix/linux/3g' blah.txt` - Replace from nth to all

---

`ssh -p port user@server-address`



`scp rocky@arena51.net:/home/rocky/game/data.txt ./ ` - Copy remote file to you current working directory

`scp mars@universe.org:/beacon/light/bitmap.conf jupiter@universe.org:/beacon/night/` - Copy file from one remote location to another remote location


`scp foobar.md user@remotehost.com:/remote/dest` - Copy local file to remote dir

` scp -i my_key.pem foobar.md user@remotehost.com:/remote/dest` - Key files can be used (just like ssh)








-----

`drwxrwxrwx`  d is for directory  and - for rest. The next three rwx are the permissions the user has over the file, the next three are the permissions the
group has over the file, and the last three are the permissions everyone else has over the file

r is represented by a
value of 4, w is represented by 2, and x is represented by a 1.
 So ,

 ```
Owner rwx = 4+2+1 = 7
Group r-x = 4+0+1 = 5
Other r-x = 4+0+1 = 5
```
So the whole command is
`chmod 755 test`

---

`/etc/os-release` -  Details about the release

--- 



`/etc/resolv.conf` contains a list of DNS servers for domain name resolution