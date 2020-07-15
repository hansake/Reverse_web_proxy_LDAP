The Python code for the interface towards the LDAP server and the backend with the authentication page
is copied from: https://github.com/nginxinc/nginx-ldap-auth

The backend authentication script backend-auth-app.py is slightly modified.

The code is installed on a Raspberry Pi 3 Model B with Rasbian 9 (stretch).

Nginx was first installed:
* sudo apt-get update
* sudo apt-get install nginx-full

Certificates were obtained by using Let's Encrypt: https://letsencrypt.org

Install needed software libraries:
* sudo apt install libsasl2-dev libldap2-dev libssl-dev
* sudo apt install python-ldap

The files has to be modified with the IP addresses, domain names and host names for the installation.

These files are installed to the directories with the following CLI commands:
* sudo cp nginx-ldap-auth-daemon.py /usr/local/bin
* sudo cp backend-auth-app.py /usr/local/bin
* sudo chmod a+x /usr/local/bin/nginx-ldap-auth-daemon.py
* sudo chmod a+x /usr/local/bin/backend-auth-app.py
* sudo cp gatewayauth.service /etc/systemd/system
* sudo cp gatewaybackend.service /etc/systemd/system 
* sudo chmod a+x /etc/systemd/system/gatewayauth.service
* sudo chmod a+x /etc/systemd/system/gatewaybackend.service
* sudo cp ldapreverseproxy /etc/nginx/sites-available/
* sudo chmod a-x /etc/nginx/sites-available/ldapreverseproxy
* chmod a-x *.html
* sudo cp *.html /var/www/html

The daemons are enabled:
* sudo systemctl enable gatewayauth
* sudo systemctl enable gatewaybackend

Enable the Nginx configuration and reload it:
* sudo ln -s /etc/nginx/sites-available/ldapreverseproxy /etc/nginx/sites-enabled/
* sudo service nginx configtest
* sudo service nginx reload
