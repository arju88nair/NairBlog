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
- `ifconfig wlp4s0 down`
- `macchanger -r wlp4s0`
- `service network-manager start  `
- `ifconfig wlp4s0 up`


---

### bash command


```

function macc()
{
sudo service network-manager stop && sudo ifconfig wlp4s0 down && sudo macchanger -r wlp4s0 && sudo service network-manager start && sudo ifconfig wlp4s0 up

}

```

## Fixing mysql `Error 2002: Can't connect to local MySQL server through socket '/tmp/mysql.sock'`

```
sudo ln -s /var/run/mysqld/mysqld.sock /tmp/mysql.sock
```

---

## Fixing mysql which only allows to login as sudo user



    -  Delete the root user: `drop user 'root'@'localhost';`
    - Create the root user again: `create user 'root'@'%' identified by 'your_password';`
    - Give permissions: `grant all privileges on *.* to 'root'@'%' with grant option;`
    - Update permission tables: `flush privileges;`
    - Exit MYSQL and try to reconnect without sudo.

---

## Fixing “this is incompatible with sql_mode=only_full_group_by” in MySQL


```

## /etc/mysql/my.cnf

[mysqld]
sql_mode = STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
```