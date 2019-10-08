---
description: Guide for setting up ssl certs with
---

# Setting up Let's Encrypt

## Install certbot

Add certbot repository

```bash
$ sudo add-apt-repository ppa:certbot/certbot
```

{% hint style="info" %}
 certbot in default repository is usually not up-to date
{% endhint %}

Now you can install certbot package

```bash
$ sudo apt install python-certbot-nginx
```

## Configure server block in nginx config file
1. Make directory
```bash
$ sudo mkdir -p /var/www/mysite.com/html
```
2. Change owenership to non root
```bash
$ sudo chown -R $USER:$USER /var/www/mysite.com/html
```
3. Set the permisions for the directory
```bash
$ sudo chmod -R 755 /var/www/example.com
```
4. Create a test page
```bash
nano /var/www/mysite.com/html/index.html
```
> Code
```html
<html>
    <head>
        <title>Welcome!!!!</title>
    </head>
    <body>
        <h1>Wow the site works!</h1>
    </body>
</html>
```
5. Create server conf 
```bash
$ nano /var/www/mysite.com/html/index.html
```
Add the following config
```javascript
server {
        listen 80;
        listen [::]:80;

        root /var/www/mysite.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name mysite.com www.mysite.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
6. Create a link to this file as nginx config file
```bash
$ sudo ln -s /etc/nginx/sites-available/mysite.com /etc/nginx/sites-enabled/
```
7. To avoid hash bucket memory problem enable the setting to accomodate more than one names
```bash
$ sudo nano /etc/nginx/nginx.conf
```
And ucomment the line `server_names_hash_bucket_size 64;`
8. Check changes before restarting the server
```bash
$ sudo nginx -t
```
9. Restart nginx
```bash
$ sudo systemctl restart nginx
```

