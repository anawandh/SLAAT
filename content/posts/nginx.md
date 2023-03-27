---
title: NGINX Proxy Passing & Security
description: NGINX configuration for APCSP
date: 2023-03-24
draft: false
---

If you're running a Flask web application, you might want to consider using Nginx as a reverse proxy to handle requests from the internet. This can help improve the security and scalability of your application by allowing Nginx to handle tasks such as load balancing and caching.

## Setting Up Nginx

To get started, you'll need to install Nginx on your server if it isn't already installed. Once that's done, you can create a new Nginx configuration file in the `/etc/nginx/sites-available/` directory. Let's call this file `myapp`.

Here's a sample configuration file that will proxy requests to a Flask application running on `localhost:5000`:

```nginx
server {
    listen 80;
    server_name myapp.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

This configuration file tells Nginx to listen on port 80 for incoming requests to the `myapp.com` domain. Any requests that come in will be passed along to the Flask application running on `localhost:5000`. We're also setting some headers to provide additional information to the Flask application.

You can enable this configuration file by creating a symbolic link to it in the `sites-enabled` directory:

```bash
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
```

Finally, restart Nginx to apply the changes:

```bash
sudo systemctl restart nginx
```

## Adding SSL with Certbot

Now that we have Nginx set up as a reverse proxy, let's add SSL to our site using Certbot.

Certbot is a tool that can automatically obtain and renew SSL certificates from Let's Encrypt, a free and open certificate authority. To install Certbot, follow the instructions for your operating system on [Certbot's website](https://certbot.eff.org/).

Once Certbot is installed, you can use it to obtain an SSL certificate for your site:

```bash
sudo certbot --nginx -d myapp.com
```

This command will run Certbot in "nginx" mode and ask you for some information about your site. Once you've provided the necessary information, Certbot will automatically configure Nginx to use SSL and obtain an SSL certificate from Let's Encrypt.

You can test that SSL is working by visiting your site using `https://` instead of `http://`. Your browser should display a green lock icon indicating that your site is now using a secure SSL connection.

## Additional Security Headers

Finally, we can add some additional security headers to our site to improve security. Security headers are HTTP headers that instruct the browser to perform certain security-related actions, such as preventing clickjacking attacks or enabling strict transport security.

Here's an example of how to add security headers to our Nginx configuration file:

```nginx
server {
    listen 80;
    server_name myapp.com;

    add_header X-Content-Type-Options nosniff;
    add_header X-Frame-Options SAMEORIGIN;
    add_header X-XSS-Protection "1; mode=block";

    location / {
        proxy_pass http://localhost:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

In this example, we're adding three security headers:

- `X-Content-Type-Options`: Tells the browser not to guess the MIME type of a resource based on its content.
- `X-Frame-Options`: Prevents the site from being loaded in an iframe on another domain, which can help prevent clickjacking attacks.
- `X-XSS-Protection`: Enables the browser's built-in XSS protection.

By adding these headers to your Nginx configuration file, you can help protect your site against common web vulnerabilities.

## Conclusion

Using Nginx as a reverse proxy for a Flask application can help improve the security and scalability of your site. Adding SSL with Certbot and configuring additional security headers can further improve the security of your site.

By following the steps outlined in this blog post, you should now have a Flask application running behind an Nginx reverse proxy with SSL enabled and additional security headers configured.
