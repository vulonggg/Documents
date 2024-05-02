<img src="media/image1.png" style="width:6.5in;height:4.38611in"
alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="media/image2.png" style="width:6.5in;height:3.19028in"
alt="Text Description automatically generated" />

<img src="media/image3.png" style="width:6.5in;height:0.87708in"
alt="Text, letter Description automatically generated" />

<img src="media/image4.png" style="width:6.12656in;height:0.30186in" />

<img src="media/image5.png" style="width:6.5in;height:2.54861in"
alt="Text Description automatically generated" />

<img src="media/image6.png" style="width:6.5in;height:2.16667in"
alt="Graphical user interface, text Description automatically generated" />

<img src="media/image7.png" style="width:6.5in;height:1.81736in"
alt="Text Description automatically generated" />

<img src="media/image8.png" style="width:6.5in;height:2.18958in"
alt="Text Description automatically generated" />

<img src="/media/imageb.png" style="width:6.5in;height:2.40417in"
alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="/media/imagec.png" style="width:6.5in;height:3.83542in"
alt="Text Description automatically generated" />

<img src="/media/image12.png" style="width:5in;height:1.66667in" />

<img src="/media/image13.png"
style="width:4.21875in;height:2.10937in" />

<img src="/media/image14.png" style="width:5in;height:2.39583in" />

<img src="/media/image15.png" style="width:5in;height:1.42708in" />

<img src="/media/image16.png"
style="width:4.78125in;height:1.84277in" />

<img src="/media/imagee.png" style="width:5in;height:2.14583in" />

<img src="/media/imagef.png" style="width:5in;height:2.55208in" />

Install packages for encrypted websites

\#yum install –y mod_ssl openssl

\# less /etc/httpd/conf.d/ssl.conf

/VirtualHost =\> 443

\# openssl list-standard-commands

\# openssl list-cipher-commands

\# openssl list-message-digest-commands

\# openssl genpkey

**Generating keypairs & self-signed certificates**

\# cd /etc/pki/tls/certs

\# openssl genpkey –algorithm rsa –pkeyopt rsa_keygen_bits:2048 –out
secure.localnet.com.key

\# openssl req –new –key secure.localnet.com.key -out
secure.localnet.com.csr

\# openssl x509 –req –days 120 –signkey secure.localnet.com.key -in
secure.localnet.com.csr -out secure.localnet.com.crt

\# chmod 600 secure.localnet.com.key

\# mv secure.localnet.com.key ../private/

\# systemctl restart httpd

\# openssl s_client -connect localhost:443 –state

**Configure a secure virtual host**

\# mkdir /var/www/html/secure

\# vi /etc/httpd/conf.d/ssl.conf

/VirtualHost

DocumentRoot “/var/www/html/secure”

ServerName secure.localnet.com:443

/SSLCertificateFile

SSLCertificateFile /etc/pki/tls/certs/secure.localnet.com.crt

SSLCertificateKeyFile /etc/pki/tls/private/secure.localnet.com.key

\# httpd –D DUMP_VHOSTS

\# vi /var/www/html/secure/index.html

\<Content\>

\# restorecon –Rv /var/www/html/secure

\# firewall-cmd –permanent –add-service https

\# firewall-cmd –reload

\# systemctl restart httpd

<img src="/media/image10.png"
style="width:6.59933in;height:4.08333in" />

\# nc \<remote_IP\> 80

\# netcat \<remote_IP\> 80

OPTIONS /HTTP/1.0

Or

OPTIONS /HTTP/1.0

Or

HEAD HTTP/1.0, HTTP/1.1

Or

TRACE / HTTP/1.0

Or

HEAD /HTTP/1.0

Or

PUT /HTTP/1.0

Or

GET / HTTP/1.0

Or

DELETE / HTTP/1.0

<img src="/media/image11.png"
style="width:6.41186in;height:2.60482in" />
