---
title: "Nginx Server Block"
date: 2018-07-11T17:31:55+05:30
tags : [
    "Nginx",
    "Python",
    "PHP",
    "Random"
   ]
---

# Nginx

This is just a copy of the server configuration of my EC2 instance which contains a Django, PHP and a static applications.

The Django application is served by the help of Uwsgi and Nginx courtesy of this [article](https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-uwsgi-and-nginx-on-ubuntu-16-04)
To quote the article,

>This will serve as an interface to our applications which will translate client requests using HTTP to Python calls that our application can process. We will then set up Nginx in front of uWSGI to take advantage of its high performance connection handling mechanisms and its easy-to-implement security features.

```

server {
    server_name culminated.co www.Cuminated.co;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        root /home/ubuntu/PCweb;
    }

    location / {
        include         uwsgi_params;
        uwsgi_pass      unix:/run/uwsgi/PCweb.sock;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/culminated.co/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/culminated.co/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
    if ($host = culminated.co) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;
    server_name culminated.co www.Cuminated.co;
    return 404; # managed by Certbot


}


server {
   # listen [::]:80 default_server;

    root /var/www/html/Portfolio;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name thenair.tk www.thenair.tk;

    location / {
       # try_files $uri $uri/ =404;
       #  try_files $uri $uri/ /index.php$is_args$args;
      allow all;


    }

    location ~ \.php$ {
        #include snippets/fastcgi-php.conf;
        #fastcgi_pass unix:/run/php/php5.6-fpm.sock;
 try_files $uri /index.php =404;
            fastcgi_pass unix:/run/php/php5.6-fpm.sock;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/thenair.tk/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/thenair.tk/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}


server {
   # listen [::]:80 default_server;

    root /var/www/html/Blog/public;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name hush.thenair.tk;

    location / {
       # try_files $uri $uri/ =404;
         try_files $uri $uri/ /index.php$is_args$args;

    }

    location ~ \.php$ {
        #include snippets/fastcgi-php.conf;
        #fastcgi_pass unix:/run/php/php5.6-fpm.sock;
 try_files $uri /index.php =404;
            fastcgi_pass unix:/run/php/php5.6-fpm.sock;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/thenair.tk/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/thenair.tk/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}




server {
    if ($host = thenair.tk) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;

    server_name thenair.tk www.thenair.tk;
    return 404; # managed by Certbot


}


server {
    if ($host = hush.thenair.tk) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;

    server_name hush.thenair.tk;
    return 404; # managed by Certbot


}

```