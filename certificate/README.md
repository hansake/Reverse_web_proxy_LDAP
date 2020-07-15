To create a certificate the certbot program from Let's Encrypt is used: https://letsencrypt.org

A domain name has to be created. I have used Duck DNS https://www.duckdns.org/
mainly because it is free and seems stable. The installation is described
here: https://www.duckdns.org/install.jsp

Install certbot to create the certificate:
* sudo apt-get update
* sudo apt-get install certbot

Create an Nginx configuration file that allows for downloading and automatic
update the certificate. An example of such a file is named "certnginx" here.

To work with this example configuration, port forwarding for ports 80 and 443 must
be configured.

When a new certificate is generated and downloaded, Nginx must re-read the configuration.
This is done by creation a script:
* /etc/letsencrypt/renewal-hooks/deploy/01-reload-nginx
That contains:
* #! /bin/sh
* set -e
* 
* /etc/init.d/nginx configtest
* /etc/init.d/nginx reload
Make this script executable:
* sudo chmod a+x /etc/letsencrypt/renewal-hooks/deploy/01-reload-nginx
