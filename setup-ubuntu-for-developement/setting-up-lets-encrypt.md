---
description: Guide for setting up ssl certs with
---

# Setting up Let's Encrypt

## Install certbot

1. Add certbot repository

```bash
sudo add-apt-repository ppa:certbot/certbot
```

{% hint style="info" %}
certbot in default repository is usually not up-to date
{% endhint %}

1. Now you can install certbot package

```bash
sudo apt install python-certbot-nginx
```

## Check firewall settings

Make sure firewall has nginx and ssh settings enabled

```bash
sudo ufw status
```

> Output
>
> ```bash
> Status: activeTo Action FromOpenSSH ALLOW Anywhere Nginx Full ALLOW Anywhere OpenSSH (v6) ALLOW Anywhere (v6) Nginx Full (v6) ALLOW Anywhere (v6)
> ```

Enable firewall by using following command

```bash
sudo ufw enable
```

Alternately same can be disabled using

```bash
sudo ufw disable
```

{% hint style="info" %}
These commands also enable/disable the ufw on startup
{% endhint %}

## Obtain ssl certificate

```bash
sudo certbot --nginx -d mysite.com -d www.mysite.com
```

## Verify auto renewal

```bash
sudo certbot renew --dry-run
```

