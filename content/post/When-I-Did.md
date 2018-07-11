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