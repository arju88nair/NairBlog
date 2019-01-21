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


