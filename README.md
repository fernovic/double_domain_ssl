# double_domain_ssl
The command you provided, `acme -d domain1.com -d domain2.com`, seems to refer to using the ACME protocol to obtain SSL certificates for multiple domains, likely through Let's Encrypt or another ACME-compatible Certificate Authority (CA).

To use ACME to obtain and manage SSL certificates, you'll typically use a client like Certbot. Here’s how you can obtain a certificate for multiple domains using Certbot:

1. **Install Certbot:**
   First, ensure Certbot is installed on your system. Instructions vary based on your operating system.

   - For Ubuntu/Debian:
     ```sh
     sudo apt update
     sudo apt install certbot
     sudo apt install python3-certbot-nginx  # If you are using Nginx
     sudo apt install python3-certbot-apache  # If you are using Apache
     ```

2. **Obtain the certificate for multiple domains:**
   Use Certbot with the appropriate plugin for your web server. For example, if you are using Nginx, you would use the following command:

   ```sh
   sudo certbot --nginx -d domain1.com -d domain2.com
   ```

   For Apache, you would use:
   
   ```sh
   sudo certbot --apache -d domain1.com -d domain2.com
   ```

3. **Follow the prompts:**
   Certbot will guide you through the process, including creating necessary verification files and updating your web server configuration. It will automatically obtain and install the SSL certificates for the specified domains.

4. **Verify the installation:**
   Once the process is complete, Certbot will reload your web server to apply the new certificate. You can verify the installation by visiting your domains in a web browser to ensure they are served over HTTPS.

5. **Set up automatic renewal:**
   Certbot typically sets up a cron job or systemd timer to automatically renew your certificates before they expire. You can check if this is set up correctly:

   ```sh
   sudo certbot renew --dry-run
   ```

   This command performs a dry run of the renewal process to ensure everything is working.

Here’s a detailed breakdown of the Certbot command:

- `sudo certbot`: Runs the Certbot client with elevated privileges.
- `--nginx` or `--apache`: Specifies the plugin to use, based on your web server.
- `-d domain1.com -d domain2.com`: Specifies the domains for which you want to obtain the SSL certificate. You can add more domains by including additional `-d domain.com` parameters.

By following these steps, you should be able to obtain and install an SSL certificate for multiple domains using the ACME protocol and Certbot.


To change the key type of the certificate from ECDSA to RSA, you would use the `--key-type rsa` option. However, if you meant to keep the certificate type as ECDSA and include both `s1.tala2005.shop` and `yek.oykala.shop` domains, you don't need to specify `--key-type` since it's already using ECDSA.

If your intention is to switch back to using ECDSA (though it seems unnecessary because your certificate is already ECDSA) while adding a new domain, you can simply run the command without specifying the key type:

```sh
sudo certbot --nginx --cert-name s1.tala2005.shop -d s1.tala2005.shop -d yek.oykala.shop
```

This command will:
- Use the Nginx plugin to manage the SSL certificates.
- Target the existing certificate named `s1.tala2005.shop`.
- Include both `s1.tala2005.shop` and `yek.oykala.shop` domains in the certificate.

If you explicitly want to ensure the key type remains ECDSA, you can specify `--key-type ecdsa`:

```sh
sudo certbot --nginx --cert-name s1.tala2005.shop --key-type ecdsa -d s1.tala2005.shop -d yek.oykala.shop
```

However, since the existing certificates are already ECDSA, this is redundant.

After running the appropriate command, reload Nginx to apply the new certificate:

```sh
sudo systemctl reload nginx
```



**Copy the certificate and key files:**

   Use the `cp` command to copy the certificate and key files from their current location to the target directory. The typical locations for these files are under `/etc/letsencrypt/live/[your-domain]/`.

   Since your certificate name is `s1.tala2005.shop` , you will copy the files from `/etc/letsencrypt/live/s1.tala2005.shop/` to `/var/lib/marzban/certs/`.

   ```sh
   sudo cp /etc/letsencrypt/live/s1.tala2005.shop/privkey.pem /var/lib/marzban/certs/key.pem
   sudo cp /etc/letsencrypt/live/s1.tala2005.shop/fullchain.pem /var/lib/marzban/certs/fullchain.pem
   ```


restart marzban

