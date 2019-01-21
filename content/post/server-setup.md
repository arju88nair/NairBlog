---
title: "Server Setup with Nginx, PHP, MongoDB, Django and Python"
date: 2019-01-20T21:20:16+05:30
draft: false
tags: [
    "Server",
    "Random",
    "Devops"
]
---

## Creating a sudo user

```
adduser username
usermod -aG sudo username

sudo - username
```

---

## Install nginx

```
    sudo apt-get update
    sudo apt-get install nginx
```

### Adjusting firewalls

`sudo ufw app list`  will give a list of nginx app profiles


-  Nginx Full: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
- Nginx HTTP: This profile opens only port 80 (normal, unencrypted web traffic)
- Nginx HTTPS: This profile opens only port 443 (TLS/SSL encrypted traffic)

Enable Full for 80 and 443

```

sudo ufw allow 'Nginx Full'
sudo ufw enable

```

---

## Install PHP

```
sudo apt-add-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php7.2


sudo apt-get install  php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-mysql php7.2-mbstring php7.2-mcrypt php7.2-zip 

```

### configure phpinfo

```

    server {
        listen 80;
        root /var/www/html;
        index index.php index.html index.htm index.nginx-debian.html;
        server_name ip;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}

// For my portfolio

server {
   listen [::]:80 ;

    root /var/www/html/Portfolio;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name thenair.me www.thenair.me;

    location / {
       # try_files $uri $uri/ =404;
       #  try_files $uri $uri/ /index.php$is_args$args;
      allow all;


    }

    location ~ \.php$ {
        #include snippets/fastcgi-php.conf;
        #fastcgi_pass unix:/run/php/php7.2-fpm.sock;
 try_files $uri /index.php =404;
            fastcgi_pass unix:/run/php/php7.2-fpm.sock;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

   
}
```
---


## Mongodb

> https://docs.mongodb.com/v3.6/tutorial/install-mongodb-on-ubuntu/ 

### Driver

```
sudo apt-get install php-pear
sudo apt-get install php7.2-dev
sudo pecl install mongodb

```

>/etc/php/7.2/fpm/php.ini -> extension=mongodb.so

```
sudo systemctl restart php7.2-fpm.service 
```

---

## [Django Python setup (Python 3)](https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-uwsgi-and-nginx-on-ubuntu-16-04)

Installing Python pip
```
sudo apt-get update
sudo apt-get install python-pip
```

Installing `virtualenv` and `virtualenvwrapper` globally

```
sudo -H pip3 install --upgrade pip
sudo -H pip3 install virtualenv virtualenvwrapper


echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3" >> ~/.bashrc
echo "export WORKON_HOME=~/Env" >> ~/.bashrc
echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc

source ~/.bashrc

pip install django
```

### Install Pymongo

```
python -m pip install pymongo
```

### [Install Redis](http://grainier.net/how-to-install-redis-in-ubuntu/)
After downloading the zip,
```
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install tcl8.5

// After navigating to the redis folder
make 
make test
sudo make install
	
cd utils
sudo ./install_server.sh
sudo service redis_6379 start


pip install django-redis-cache
```

## Installing UWSGI
> uwsgi --http :8080 --home /home/nair/Env/PCweb --chdir /home/nair/PCweb -w PCweb.wsgi

```
sudo apt-get install python3-dev
sudo -H pip3 install uwsgi
```

### Creating configuration file

```
sudo mkdir -p /etc/uwsgi/sites
```
>/etc/uwsgi/sites/PCweb.ini
```
[uwsgi]
project = PCweb
uid = nair
base = /home/%(uid)

chdir = %(base)/%(project)
home = %(base)/Env/%(project)
module = %(project).wsgi:application

master = true
processes = 5


socket = /run/uwsgi/%(project).sock
chown-socket = %(uid):www-data
chmod-socket = 660
vacuum = true
```
## A systemd Unit File for uWSGI

A systemd unit file to manage the uWSGI emperor process and automatically start uWSGI at boot.

> sudo vim /etc/systemd/system/uwsgi.service

```
[Unit]
Description=uWSGI Emperor service

[Service]
ExecStartPre=/bin/bash -c 'mkdir -p /run/uwsgi; chown ubuntu:www-data /run/uwsgi'
ExecStart=/usr/local/bin/uwsgi --emperor /etc/uwsgi/sites
Restart=always
KillSignal=SIGQUIT
Type=notify
NotifyAccess=all

[Install]
WantedBy=multi-user.target

```
### Server config
```
server {
    listen 80;
    server_name culminated.thenair.me;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        root /home/nair/PCweb;
    }

    location / {
        include         uwsgi_params;
        uwsgi_pass      unix:/run/uwsgi/PCweb.sock;
    }
}
```

Start the service
```
sudo systemctl start uwsgi
sudo systemctl enable nginx
sudo systemctl enable uwsgi
```
---

## Add Certbot for SSL

```
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx 



sudo certbot --nginx

```


## Site handling

```
#!/bin/bash

##
#  File:
#    nginx_modsite
#  Description:
#    Provides a basic script to automate enabling and disabling websites found
#    in the default configuration directories:
#      /etc/nginx/sites-available and /etc/nginx/sites-enabled
#    For easy access to this script, copy it into the directory:
#      /usr/local/sbin
#    Run this script without any arguments or with -h or --help to see a basic
#    help dialog displaying all options.
##

# Copyright (C) 2010 Michael Lustfield <mtecknology@ubuntu.com>

# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY AUTHOR AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED.  IN NO EVENT SHALL AUTHOR OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.

##
# Default Settings
##

NGINX_CONF_FILE="$(awk -F= -v RS=' ' '/conf-path/ {print $2}' <<< $(nginx -V 2>&1))"
NGINX_CONF_DIR="${NGINX_CONF_FILE%/*}"
NGINX_SITES_AVAILABLE="$NGINX_CONF_DIR/sites-available"
NGINX_SITES_ENABLED="$NGINX_CONF_DIR/sites-enabled"
SELECTED_SITE="$2"

##
# Script Functions
##

ngx_enable_site() {
    [[ ! "$SELECTED_SITE" ]] &&
        ngx_select_site "not_enabled"

    [[ ! -e "$NGINX_SITES_AVAILABLE/$SELECTED_SITE" ]] && 
        ngx_error "Site does not appear to exist."
    [[ -e "$NGINX_SITES_ENABLED/$SELECTED_SITE" ]] &&
        ngx_error "Site appears to already be enabled"

    ln -sf "$NGINX_SITES_AVAILABLE/$SELECTED_SITE" -T "$NGINX_SITES_ENABLED/$SELECTED_SITE"
    ngx_reload
}

ngx_disable_site() {
    [[ ! "$SELECTED_SITE" ]] &&
        ngx_select_site "is_enabled"

    [[ ! -e "$NGINX_SITES_AVAILABLE/$SELECTED_SITE" ]] &&
        ngx_error "Site does not appear to be \'available\'. - Not Removing"
    [[ ! -e "$NGINX_SITES_ENABLED/$SELECTED_SITE" ]] &&
        ngx_error "Site does not appear to be enabled."

    rm -f "$NGINX_SITES_ENABLED/$SELECTED_SITE"
    ngx_reload
}

ngx_list_site() {
    echo "Available sites:"
    ngx_sites "available"
    echo "Enabled Sites"
    ngx_sites "enabled"
}

##
# Helper Functions
##

ngx_select_site() {
    sites_avail=($NGINX_SITES_AVAILABLE/*)
    sa="${sites_avail[@]##*/}"
    sites_en=($NGINX_SITES_ENABLED/*)
    se="${sites_en[@]##*/}"

    case "$1" in
        not_enabled) sites=$(comm -13 <(printf "%s\n" $se) <(printf "%s\n" $sa));;
        is_enabled) sites=$(comm -12 <(printf "%s\n" $se) <(printf "%s\n" $sa));;
    esac

    ngx_prompt "$sites"
}

ngx_prompt() {
    sites=($1)
    i=0

    echo "SELECT A WEBSITE:"
    for site in ${sites[@]}; do
        echo -e "$i:\t${sites[$i]}"
        ((i++))
    done

    read -p "Enter number for website: " i
    SELECTED_SITE="${sites[$i]}"
}

ngx_sites() {
    case "$1" in
        available) dir="$NGINX_SITES_AVAILABLE";;
        enabled) dir="$NGINX_SITES_ENABLED";;
    esac

    for file in $dir/*; do
        echo -e "\t${file#*$dir/}"
    done
}

ngx_reload() {
    read -p "Would you like to reload the Nginx configuration now? (Y/n) " reload
    [[ "$reload" != "n" && "$reload" != "N" ]] && invoke-rc.d nginx reload
}

ngx_error() {
    echo -e "${0##*/}: ERROR: $1"
    [[ "$2" ]] && ngx_help
    exit 1
}

ngx_help() {
    echo "Usage: ${0##*/} [options]"
    echo "Options:"
    echo -e "\t<-e|--enable> <site>\tEnable site"
    echo -e "\t<-d|--disable> <site>\tDisable site"
    echo -e "\t<-l|--list>\t\tList sites"
    echo -e "\t<-h|--help>\t\tDisplay help"
    echo -e "\n\tIf <site> is left out a selection of options will be presented."
    echo -e "\tIt is assumed you are using the default sites-enabled and"
    echo -e "\tsites-disabled located at $NGINX_CONF_DIR."
}

##
# Core Piece
##

case "$1" in
    -e|--enable)    ngx_enable_site;;
    -d|--disable)   ngx_disable_site;;
    -l|--list)  ngx_list_site;;
    -h|--help)  ngx_help;;
    *)      ngx_error "No Options Selected" 1; ngx_help;;
esac
```

Make this executable 
```
sudo chmod u+x /usr/bin/nginx_modsite
```

To list all the sites  `sudo nginx_modsite -l`

To enable site "test_website"  `sudo nginx_modsite -e test_website`

To disable site "test_website" `sudo nginx_modsite -d test_website`