---
description: nginx settings for Let's encrypt
---

# nginx setup

## Installing NGINX on ubuntu

1. Install nginx

   ```bash
   sudo apt install nginx
   ```

2. check firewall settings

   ```bash
   sudo ufw app list
   ```

   > Output
   >
   > ```text
   > Available applications:
   > Nginx Full
   > Nginx HTTP
   > Nginx HTTPS
   > OpenSSH
   > ```

3. Allow traffic

   ```bash
   sudo ufw allow 'Nginx HTTP'
   ```

4. Check server status

   ```bash
   sudo systemctl status nginx
   ```

5. Open browser and type the ip of the server to see something like below

   ![nginx welcome page](.gitbook/assets/nginx.png)

## Configure server block in nginx config file

1. Make directory

   ```bash
   sudo mkdir -p /var/www/mysite.com/html
   ```

2. Change owenership to non root

   ```bash
   sudo chown -R $USER:$USER /var/www/mysite.com/html
   ```

3. Set the permisions for the directory

   ```bash
   sudo chmod -R 755 /var/www/mysite.com
   ```

4. Create a test page

   ```bash
   nano /var/www/mysite.com/html/index.html
   ```

   > Code
   >
   > ```markup
   > <html>
   >  <head>
   >      <title>Welcome!!!!</title>
   >  </head>
   >  <body>
   >      <h1>Wow the site works!</h1>
   >  </body>
   > </html>
   > ```

5. Create server conf

   ```bash
   sudo nano /etc/nginx/sites-available/mysite.com
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
   sudo ln -s /etc/nginx/sites-available/mysite.com /etc/nginx/sites-enabled/
   ```

7. To avoid hash bucket memory problem enable the setting to accomodate more than one names

   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```

   And ucomment the line `server_names_hash_bucket_size 64;`

8. Check changes before restarting the server

   ```bash
   sudo nginx -t
   ```

9. Restart nginx

   ```bash
   sudo systemctl restart nginx
   ```

