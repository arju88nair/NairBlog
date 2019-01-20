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