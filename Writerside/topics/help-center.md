# help-center

---
title: "Help Center"
---

Help center allows you to create a portal and add articles from the DEP  app dashboard. You can point to these help center portal articles from your main site and display them as your public-facing help center.

## How to get SSL certificate for your custom domain

### Create a Portal in DEP 's dashboard

Follow these step to create your Portal. Refer to [this guide.](https://www.DEP .com/hc/user-guide/articles/1677861202-how-to-setup-a-help-center)

### Point your custom domain to your DEP  domain

1. Go to your DNS provider and add a new CNAME record.
    - For the above example, add docs as a CNAME record and point it to the your selfhosted DEP  domain(FRONTEND_URL).

2. This will ensure that your CNAME record points to the selfhosted DEP  installation. For your custom domain, we have your portal information. In this case, `docs.example.com`

### Setting up SSL

1. Use certbot to generate SSL certificates for your custom domain.

```
certbot certonly --agree-tos --nginx -d "docs.example.com"
```

2. Create a new nginx config to route requests to this domain to DEP . Make a copy of `/etc/nginx/sites-available/nginx_chatwoot.conf` and make necessary changes for the new domain.

3. Restart nginx server.

```
sudo systemctl restart nginx
```

Voila!

`docs.yourdomain.com` is live with a secure connection, and your portal data is visible.


### How does this work?

These are the engineering details to understand `How does docs.yourdomain.com` gets the portal data with SSL certificate.

1. `docs.yourdomain.com` resolves by customers nameserver and redirects to your DEP  domain.
2. DEP  check for the portal record with custom-domain `docs.yourdomain.com`
3. Redirects to the portal records for the domain `docs.yourdomain.com`

Yaay!!

Now you can have your own help-center, product-documentation related portal saved at DEP  dashboard and served at your domain with SSL certificate.