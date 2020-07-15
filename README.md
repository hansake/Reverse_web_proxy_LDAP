# Reverse_web_proxy_LDAP
Reverse TLS web proxy with LDAP authentication.

This reverse web proxy acts as a TLS (HTTPS) frontend towards HTTP web servers in the home network.
The router connecting the home network to Internet is configured to forward port 9443 to the
reverse web proxy.

Nginx is used as proxy web server and the Synology LDAP Server was used for storing user names and passwords.

The reverse web proxy with LDAP authentication was developed because the Safari browser 
in iOS can't save and remember passwords when basic authentication is used on a web site.

Basic authentication is used in a previous project: https://github.com/hansake/Reverse_web_proxy.

To keep the certificate from Let's Encrypt automatically updated some additional configuration is needed,
this will be described here shortly.
