---
title: Azure Webapp DNS, SSL Configuration Using Cloudflare
date: '2021-11-12 02:53:41'
author: tmacharia
---

Easily map your custom domain to an app service running on Azure, attach an SSL certificate for the same, and also do multiple subdomains; all at no additional costs.

1. Setup domain on cloudflare
2. Add site on azure
3. Verify domain under *Settings* >*Custom Domains* by copying A,TXT,and CNAME records from azure to cloudflare DNS management.
4. Time to do SSL Bindings 
5. Go to cloudflare *SSL/TLS* > *Origin Server*, click on Create certificate
6. On your root project folder, create a subfolder called **.ssl** 
7. Copy the generated pem key & certificate and add them as files in your **.ssl** folder using the names **private.pem** and **cert.cer** respectively.
8. Since Azure needs a PKCS#7 type of certificate to import for SSL binding, we will need to use what we have to generate that.
9. Inside the **.ssl** folder, open a terminal, make you have `openssl` installed and configured it as an environment variable.
10. Run the following command. Read more about [How to convert a certificate into the appropriate format](https://knowledge.digicert.com/solution/SO26449.html)
```
openssl pkcs12 -export -in cert.cer -inkey private.pem -out cert.pfx
```
You will be prompted for a password, enter it & confirm. Finally, a .pfx file is generated.
11. Go back to Azure, and click Add Binding
12. Select the pfx file and enter the password you used.
13. On the next page, pick the correct certificate thumbprint that matches your current azure web app.
14. Finish, and that's it.
