**NGINX**

1.  **Install & Configure NGINX**

    1.  **Install Nginx on Ubuntu**

> \# apt install nginx
>
> \# nginx -v
>
> \# systemctl start nginx
>
> \# systemctl status nginx

2.  **NGINX files and directories**

> \# cd /etc/nginx
>
> \# ls -ltr
>
> <img src="media/image1.png" style="width:5.354in;height:1.22753in" />

- Site-available/default: set up welcome to NGINX page, use to confirm
  the server is installed and configured correctly

> \# cd /var/log/nginx
>
> <img src="media/image2.png" style="width:5.66274in;height:0.80464in" />

- Access.log: records any accesses that web servers process, along with
  details like the time the access occurred, Ip address of the
  requester, and the file that was requested.

- Error.log: records any problems with the web server and other
  operational details

> \# cd /var/www/
>
> <img src="media/image3.png" style="width:5.48669in;height:0.59615in" />

- Store the actual files that get served to a client, including html,
  images, any other documents that are stored on the server.

- Default directory for this is /var/www/html

- If we create and define new server configuration in VHost, we ‘ll be
  creating our own directories in /var/www to accommodate the files that
  get served.

  1.  **CLI**

> \# systemctl start nginx
>
> \# systemctl stop nginx
>
> \# systemctl restart nginx
>
> \# systemctl status nginx
>
> \# systemctl reload nginx
>
> \# nginx -h
>
> \# nginx -t
>
> \# nginx -T
>
> \# nginx -s \<signal\>

2.  **Nginx.conf**

> \# Vi /etc/nginx/nginx.conf very rare to use
>
> \# cd /etc/nginx/sites-enabled/
>
> \# cd /etc/nginx/conf.d/

3.  **Configure a virtual host**

> \# cd /etc/nginx/sites-enabled/
>
> \# unlink default
>
> \# cd ../sites-available/
>
> \# vim /etc/nginx/conf.d/lol.local.conf
>
> Server {
>
> Listen 80;
>
> Root /var/www/lol.local;
>
> }
>
> \# nginx -t
>
> \# systemctl reload nginx
>
> \# systemctl status nginx
>
> \# mkdir /var/www/lol.local
>
> \# echo “Site coming soon” \> /var/html/lol.local/index.html
>
> \# vim /etc/nginx/conf.d/lol.local.conf
>
> Server {
>
> Listen 80 default_server;
>
> Server_name lol.local [www.lol.local](http://www.lol.local);
>
> Index index.html index.htm index.php;
>
> Root /var/www/lol.local;
>
> }
>
> \# nginx -t
>
> \# systemctl reload nginx
>
> \# curl localhost

4.  **Add files to the root directory**

> \# apt install unzip
>
> \# unzip \<.zip\> -d /var/www/lol.local/
>
> \# cd /var/www/lol.local/
>
> \# find /var/www/lol.local/ -type f -exec chmod 644 {} \\ find files
> and execute 644 on them

5.  **Configure Locations**

> <img src="media/image4.png" style="width:4.90122in;height:2.15266in" />
>
> <img src="media/image5.png" style="width:4.88996in;height:3.48984in" />
>
> \# nginx -t
>
> \# systemctl reload nginx

6.  **Configure Logs**

> <img src="media/image6.png" style="width:6.04741in;height:1.03891in" />
>
> <img src="media/image7.png" style="width:6.0639in;height:0.54743in" />
>
> \# nginx -t
>
> \# systemctl reload nginx
>
> <img src="media/image8.png" style="width:5.95943in;height:1.55671in" />
>
> \# for I in {1..10}; do curl localhost \> /dev/null; done
>
> <img src="media/image9.png" style="width:5.79946in;height:2.70208in" />

7.  **Trobleshooting NGINX**

> <img src="media/image10.png" style="width:4.15325in;height:1.20515in" />
>
> <img src="media/image11.png" style="width:4.11555in;height:1.55212in" />
>
> <img src="media/image12.png" style="width:5.59863in;height:2.68866in" />
>
> <img src="media/image13.png" style="width:4.93721in;height:1.34507in" />
>
> <img src="media/image14.png" style="width:5.2851in;height:0.9599in" />

2.  **LEMP Stack**

> <img src="media/image15.png" style="width:4.49032in;height:2.46536in" />
>
> <img src="media/image16.png" style="width:4.84708in;height:2.62447in" />
>
> <img src="media/image17.png" style="width:5.02798in;height:2.50217in" />

- **Install PHP on NGINX**

> \# apt install php-fpm php-mysql
>
> \# php –version
>
> \# systemctl status php7.2-fpm
>
> \# vi …./lol.local.conf
>
> <img src="media/image18.png" style="width:5.62853in;height:1.09143in" />
>
> \# vi /var/www/lol.local/info.php
>
> <img src="media/image19.png" style="width:5.73612in;height:0.46156in" />

- **Install MariaDB**

> \# apt install mariadb-server mariadb-client
>
> \# systemctl start mysqld.service
>
> <img src="media/image20.png" style="width:5.47958in;height:2.22754in" />
>
> \# mysql_secure_installation
>
> \# mysql -u root -p
>
> \# mysql -u admin -p
>
> \# vi index.php

3.  **Security with NGINX**

> <img src="media/image21.png" style="width:6.29097in;height:2.46463in" />

1.  **Configure allow and deny directives**

> \# vim /etc/nginx/conf.d/lol.local.conf
>
> <img src="media/image22.png" style="width:5.09014in;height:0.89458in" />
>
> <img src="media/image23.png" style="width:5.07384in;height:1.07169in" />
>
> \# nginx -t
>
> \# systemctl reload nginx

2.  **Create a 403 page**

> \# vim /etc/nginx/conf.d/lol.local.conf
>
> <img src="media/image24.png" style="width:3.92721in;height:0.78251in" />
>
> <img src="media/image25.png" style="width:3.5647in;height:0.62227in" />
>
> \# nginx -t
>
> \# systemctl reload nginx
>
> \# cp /var/www/lol.local/404.html /var/www/lol.local/403.html
>
> \# vi /var/www/lol.local/403.html

3.  **Configure password authentication**

> \# apt install -y apache2-utils
>
> \# htpasswd -c /etc/nginx/passwords admin
>
> \# htpasswd /etc/nginx/passwords user1
>
> \# htpasswd /etc/nginx/passwords user2
>
> \# htpasswd -D /etc/nginx/passwords user2
>
> \# cat /etc/nginx/passwords
>
> \# chown www-data /etc/nginx/passwords
>
> \# chmod 600 /etc/nginx/passwords
>
> \# vim /etc/nginx/conf.d/lol.local.conf
>
> <img src="media/image26.png" style="width:5.37798in;height:2.59246in" />
>
> \# nginx -t
>
> \# systemctl reload nginx

4.  **Configure HTTPS**

> <img src="media/image27.png" style="width:4.86374in;height:2.01305in" />
>
> <img src="media/image28.png" style="width:4.63607in;height:0.89108in" />

5.  **Create an SSL Certificate**

> \# apt install -y openssl
>
> \# openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout
> /etc/ssl/private/nginx.key -out /etc/ssl/certs/nginx.crt
>
> \# openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout
> /etc/ssl/private/nginx.key -out /etc/ssl/certs/nginx.crt -batch
>
> <img src="media/image29.png" style="width:5.43254in;height:0.84622in" />

6.  **Install an SSL certificate on NGINX**

\# vim /etc/nginx/conf.d/lol.local.conf

<img src="media/image30.png" style="width:5.2002in;height:1.84896in" />

> \# nginx -t
>
> \# systemctl reload nginx

4.  **Reverse Proxies and Load Balancers**

    1.  **Reverse Proxies and Load Balancing**

> <img src="media/image31.png" style="width:5.39992in;height:2.49169in" />

<img src="media/image32.png" style="width:4.1389in;height:2.64001in" />

> <img src="media/image33.png" style="width:4.22558in;height:2.71072in" />

2.  **Configure NGINX as a reverse proxy**

> <img src="media/image34.png" style="width:4.32262in;height:2.56686in" />
>
> \# vi /etc/nginx/conf.d/upstream.conf
>
> <img src="media/image35.png" style="width:5.57995in;height:2.29338in" />
>
> \# nginx -t
>
> \# systemctl reload nginx

3.  **Configure NGINX as a load balancers**

> <img src="media/image36.png" style="width:5.89942in;height:3.17157in" />
>
> \# vi /etc/nginx/conf.d/upstream.conf
>
> <img src="media/image37.png" style="width:5.20312in;height:4.49806in" />
>
> <img src="media/image38.png" style="width:5.63646in;height:4.06416in" />
>
> <img src="media/image39.png" style="width:5.83893in;height:3.49088in" />
