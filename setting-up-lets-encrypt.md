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



