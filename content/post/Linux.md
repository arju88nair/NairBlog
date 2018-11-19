---
title: "Linux"
date: 2018-11-19T20:19:34+05:30
draft: false
tags : [
    'Linux',
    'TIL'
]
---

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