**Tomcat**

Tomcat is an open-source Java implementation package developed by the
Apache Software Foundation.

JRE is java runtime environment – the software that runs the JVM, used
to run an existing Java application.

JDK has everything needed to start developing Java applications,
including a compiler. The most popular free open-source version of Java
is named OpenJDK

1.  **Check if Java is Installed**

> \# yum install default-jdk
>
> \# java -version
>
> \# yum install java-1.8.0-openjdk-devel
>
> \# vi /etc/environment
>
> JAVA_HOME=”/usr/lib/jvm/default-java”

2.  **Install Tomcat**

> \# sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat
>
> \# cd /tmp
>
> \# wget
> https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.80/bin/apache-tomcat-9.0.80.tar.gz
>
> \# sudo tar xzvf apache-tomcat-9\*tar.gz -C /opt/tomcat
> --strip-components=1
>
> \# sudo chown -R tomcat:tomcat /opt/tomcat
>
> \# sudo sh -c 'chmod +x /opt/tomcat/bin/\*.sh'
>
> \# readlink -f \$(which java) \# Find the Java location
>
> Copy the parent folder of ***/jre/bin/java*** for the following step.
>
> Paste the path from the previous step in the **JAVA_HOME=\<path\>**
>
> \# sudo vi /etc/systemd/system/tomcat.service
>
> \[Unit\]
>
> Description=Apache Tomcat Web Application Container
>
> After=network.target
>
> \[Service\]
>
> Type=oneshot
>
> RemainAfterExit=yes
>
> User=tomcat
>
> Group=tomcat
>
> Environment="JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.el7_9.x86_64/"
>
> Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom
> -Djava.awt.headless=true"
>
> Environment="CATALINA_BASE=/opt/tomcat"
>
> Environment="CATALINA_HOME=/opt/tomcat"
>
> Environment="CATALINA_PID=/opt/tomcat/temp/tomcat.pid"
>
> Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server
> -XX:+UseParallelGC"
>
> ExecStart=/opt/tomcat/bin/startup.sh
>
> ExecStop=/opt/tomcat/bin/shutdown.sh
>
> \[Install\]
>
> WantedBy=multi-user.target
>
> \# sudo systemctl daemon-reload
>
> \# sudo systemctl enable tomcat
>
> \# sudo systemctl start tomcat
>
> \# sudo systemctl status tomcat

3.  **Adjust Firewalll**

> \# firewall-cmd --zone=public --permanent --add-port=8080/tcp
>
> \# firewall-cmd –reload
>
> \# <http://server_ip:8080> (<http://localhost:8080>)

4.  **Set Up Web Management Interface**

> \# sudo nano /opt/tomcat/conf/tomcat-users.xml
>
> \<tomcat-users\>
>
> \<!--
>
> Comments
>
> --\>
>
> \<role rolename="admin-gui"/\>
>
> \<role rolename="manager-gui"/\>
>
> \<user username="admin" password="good_password"
> roles="admin-gui,manager-gui"/\>
>
> \</tomcat-users\>
>
> <http://server_ip:8080/manager/html>
>
> <https://stackoverflow.com/questions/36703856/access-tomcat-manager-app-from-different-host>
>
> <https://serverfault.com/questions/796960/how-to-access-tomcat-manager-gui-from-another-machine>

5.  **Configure Remote Access (Optional)**

> \#sudo nano /opt/tomcat/webapps/manager/META-INF/context.xml
>
> \<Valve className="org.apache.catalina.valves.RemoteAddrValve"
>
> allow="127\\\d+\\\d+\\\d+\|::1\|0:0:0:0:0:0:0:1\|192.168.0.\*" /\>
>
> \#sudo nano /opt/tomcat/webapps/host-manager/META-INF/context.xml
>
> \<Valve className="org.apache.catalina.valves.RemoteAddrValve"
>
> allow="127\\\d+\\\d+\\\d+\|::1\|0:0:0:0:0:0:0:1\|192.168.0.\*" /\>
>
> [How to Enable Tomcat Manager GUI or Login
> Functionality](https://www.youtube.com/watch?v=AJveWYXLR3g)

<img src="/media/image.jpg"
title="Video titled: How to Enable Tomcat Manager GUI or Login Functionality"
style="width:6.3125in;height:3.65625in" />

> [How to Enable Tomcat Manager GUI or Login
> Functionality](https://www.youtube.com/watch?v=2xqwswo6idU)

<img src="/media/image2.jpg"
title="Video titled: How to Enable Tomcat Manager GUI or Login Functionality"
style="width:6.3125in;height:3.65625in" />

6.  **Logging**

> \# cp /vagrant/logit.war /var/lib/tomcat8/webapps
>
> \# cat /var/log/tomcat8/localhost...
>
> \# cat /etc/tomcat8/context.xml

7.  **Web Encryption**

- **SSL:** layer of encryption between your browser and a server.
  Without it, anyone on the same network as you can easily listen in on
  what’s being sent and received (public Wifi)

- **Sending Encrypted Data**:

  - Public key: use to encrypt your data

  - Private key: only the server itself can have

<!-- -->

- Process

  - Server sends its public key

  - Server is the only one that can unlock anything encrypted with that
    public key because it has the matching private key

  - Computer generates a unique key for that session

  - Then it encrypts it using the server’s public key & send it over.

> =\> encrypt & decrypt communication
>
> \# sudo keytool –genkey –alias tomcat –keyalg RSA –keystore
> /etc/tomcat8/keystore
>
> \# vi /etc/tomcat8/server.xml
>
> Uncomment \<Connector port=”8443” …...
>
> KeystoreFile=” /etc/tomcat8/keystore” keystorePass=”password”
>
> \# systemctl restart

8.  **Tomcat Manager**

\# sudo apt install tomcat8-admin tomcat8-docs tomcat8-examples

\# sudo vi /etc/tomcat8/tomcat-users.xml

\<user username=”admin” password=”password” roles=”manager-gui”/\>

\# sudo systemctl restart tomcat8

\<IP\>:8443/manager

Desktop\tomcat\hello##feature.war

9.  **Check Version**

\# cd /usr/share/tomcat/lib  
\# java -cp catalina.jar org.apache.catalina.util.ServerInfo

[How To Install Apache Tomcat 8 on CentOS 7 \|
DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-centos-7) -
Tomcat 8

[Install and Use Apache Tomcat on CentOS 7 - IONOS -
IONOS](https://www.ionos.com/digitalguide/server/configuration/apache-tomcat-on-centos/) -
Tomcat 7

[Sự khác biệt giữa Apache Tomcat server và Apache web server -
QuanTriMang.com](https://quantrimang.com/cong-nghe/so-sanh-apache-tomcat-server-va-apache-web-server-176522)

[Sự khác biệt giữa web server và app server -
QuanTriMang.com](https://quantrimang.com/cong-nghe/so-sanh-web-server-va-app-server-176140)
