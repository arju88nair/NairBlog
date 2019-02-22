---
title: "When I Did"
date: 2018-07-11T21:20:13+05:30
tags : [
    "Hacks",
    "Random",
    "Stupid",
   ]
---

# Trifle hacks I did

## Bash commands for lazying

### Lazy git
> For easy git add, commit and push
```
function gitl() {
    git add .
    git commit -a -m "$*"
    git push origin master
}

```
---

### PHP switches
> Switching between PHP versions 

```
function on7() {
   sudo a2dismod php5.6 && sudo a2enmod php7.1 && sudo service apache2 restart
}
```

```
function on5() {
   sudo a2dismod php7.1 && sudo a2enmod php5.6 && sudo service apache2 restart
}
```
---
> Goes without saying, you have to run
```
source ~/.bashrc
```
---

## For fixing mysql login which works only with sudo

- Access with sudo: `sudo mysql -u root -p`
- Delete the root user: drop user `'root'@'localhost';`
- Create the root user again: create user `'root'@'%' identified by 'your_password';`
- Give permissions: `grant all privileges on *.* to 'root'@'%' with grant option;`
- Update permission tables: `flush privileges;`
- Exit MYSQL and try to reconnect without sudo.


## Changing mac address using macchanger


- `service network-manager stop`
- `ifconfig wlan0 down`
- `macchanger -r wlan0`
- `service network-manager start  `
- `ifconfig wlan0 up`


---

## Fixing mysql `Error 2002: Can't connect to local MySQL server through socket '/tmp/mysql.sock'`

```
sudo ln -s /var/run/mysqld/mysqld.sock /tmp/mysql.sock
```
