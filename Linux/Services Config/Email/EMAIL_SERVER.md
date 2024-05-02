**EMAIL SERVER**

1.  **GIỚI THIỆU VỀ DỊCH VỤ MAIL**

- **Email**: là mộthệ thống chuyển nhận thư từ qua các mạng máy tính.

- **Mail server**: là máy chủ dùng để nhận và gửimail, với các chức năng
  chính: quản lý tài khoản, gửi/nhận email và phân phối cho người dùng
  trong hệ thống.

<img src="media/image1.png" style="width:3.41446in;height:2.0472in" />

2.  **KIẾN TRÚC CỦA HỆ THỐNG MAIL SERVER**

<img src="/media/image17.png"
style="width:6.32417in;height:3.86587in" />

1.  Các thành phần chính của một hệ thống Mail Server:

- **Mail User Agent (MUA)**: Là loại chương trình cho phép gửi và nhận
  email. Chương trình này tương tác trực tiếp với ngườidùng. Các MUA
  đóng vai trò là **SMTP** client khi gửi mail và là **IMAP/POP3**
  client khi truy cập + đọc mail...

- **Mail Transfer Agent (MTA):** còn được gọi với cái tên dễ hiểu khác
  là "**mail server**", làm nhiệm vụ nhận email từ máy khác và chuyển nó
  đến đích cần đến. Các MTA đóng vai trò là **SMTP server**.

- **Mail Delivery Agent (MDA):** là chương trình có nhiệm vụ chính là
  phân phối thư tới hộp thư và lưu trữ email vào đĩa cứng. Ngoài ra, MDA
  có thể lọc, sắp xếp email…

- **Mail Access Agent**: Là chương trình tìm kiếm và lấy email về từ
  mail server.

2.  Các giao thức:

- **SMTP** (Simple Mail Transfer Protocol): là giao thức chuẩn TCP/IP
  được dùng để truyền tải thư điện tử (e-mail) trên mạng Internet. SMTP
  sử dụng port 25 (không mã hóa), port 465/587 (mã hóa TSL/SSL).

- **POP3** (Post Office Protocol version 3): được sử dụng để kết nối tới
  server email và tải email xuống máy tính cá nhân thông qua một ứng
  dụng email, POP3 sử dụng port 110 (không mã hóa), port 995 (mã hóa
  TSL/SSL).

- **IMAP** (Internet Message Access Protocol): cũng đều được dùng để tải
  email về email client, tuy nhiên khác biệt với POP3 là nó chỉ kéo
  email headers về, nội dung email vẫn còn trên server. IMAP sử dụng
  port 143 (không mã hóa), port 993 (mã hóa TSL/SSL).

- **MX Record** (Mail Exchange Record) là record của DNS giúp xác định
  những mail server nào đang chịu trách nhiệm xử lí mail cho tên miền.

3.  **HOẠT ĐỘNG CỦA MAIL SERVER**

<img src="media/image3.png" style="width:7.5913in;height:4.10548in" />

<img src="/media/image7.png" style="width:6.53573in;height:4.60769in" />

<img src="/media/image8.png" style="width:6.42857in;height:3.28125in" />

4.  **CÀI ĐẶT MAIL SERVER**

- Cài đặt Mail Server với các gói sau:

  - **Postfix** – Đảm nhiệm chức năng MTA cung cấp dịch vụ chuyển email
    với SMTP.

  - **Dovecot** – Đảm nhiệm chức năng MAA cung cấp dịch vụ IMAP, POP3.

  - **SquirrelMail** – Đảm nhiệm chức năng như một WebMail

- Các file config cần cấu hình hệ thống mail server gồm những file sau
  trong hệ thống:

  - /etc/dovecot/dovecot.conf

  - /etc/dovecot/conf.d/10-mail.conf

  - /etc/dovecot/conf.d/10-master.conf

  - /etc/postfix/main.cf

  - /etc/httpd/conf/httpd.conf

5.  **Postfix**

**5.1. Services, commands, logging**

<img src="/media/image9.png" style="width:5in;height:2.23958in" />

<img src="/media/imagea.png" style="width:5in;height:1.64583in" />

<img src="/media/imageb.png" style="width:5in;height:2.26042in" />

<img src="/media/imagec.png" style="width:5in;height:2.42708in" />

\# cat /var/log/maillog

\# ps –AZ \| grep postfix

\# semanage port –l \| grep smtp

\# getsebool –a \| grep postfix

**5.2. Configuration files**

\- access file

\# less /etc/postfix/access

\# postmap /etc/postfix/access =\> access.db

\- canonical file

\# less /etc/postfix/canonical

<img src="/media/imaged.png" style="width:5in;height:2.03125in" />

<img src="/media/imagee.png" style="width:5in;height:0.71875in" />

\# postmap /etc/postfix/canonical =\> canonical.db

- Generic file

> \# less /etc/postfix/generic
>
> \# postmap /etc/postfix/generic =\> generic.db

- Relocated file

> <img src="/media/imagef.png" style="width:5in;height:0.53125in" />

- Transport file

<img src="/media/image10.png" style="width:5in;height:0.55208in" />

<img src="/media/image11.png" style="width:5in;height:0.6875in" />

\# postmap /etc/postfix/transport

- Virtual file

\# less /etc/postfix/virtual

<img src="/media/image12.png" style="width:5in;height:0.58333in" />

<img src="/media/image13.png" style="width:5in;height:0.67708in" />

\# less /etc/postfix/virtual

\# postmap /etc/postfix/virtual

- Aliases file

> \# less /etc/aliases

- Master file

\# less /etc/postfix/master.cf

**5.3. Main configuration file**

<img src="/media/image14.png" style="width:5in;height:2.28125in" />

\# less /etc/postfix/main.cf

/queue /mail_owner /inet_interfaces

/mydestination /mynetworks /relayhost /mail_spool

\# postconf –d/-e

6.  **Install & Configuration**

<img src="/media/image5.png" style="width:6.39151in;height:2.82292in" />

- **Pre-install**

\# yum remove sendmail

\# vi /etc/sysconfig/selinux

SELINUX=disabled

SELINUXTYPE=targeted

\# systemctl stop firewalld

- **Cài đặt Postfix**

\# yum install -y postfix

- Cấu hình cấu hình Postfix và kiểm tra dịch vụ

\# vi /etc/postfix/main.cf

<img src="/media/image15.png" style="width:5in;height:2.88542in" />

- Optional:

disable_dns_lookups = yes

\# postfix check

\# firewall-cmd --permanent --add-service smtp

\# firewall-cmd --reload

\# systemctl enable postfix

\# systemctl restart postfix

\# alternatives -set mta /usr/sbin/sendmail.postfix

\# useradd lpi

\# passwd lpi

\# useradd pnh

\# passwd pnh

\# yum install -y telnet

\- Kiem tra dich vu Postfix

telnet localhost smtp

ehlo localhost

mail from:lpi

rcpt to:lpi

- Chuyển đến thư mục của user ‘lpi để xem mail đã nhận đc

\# cd /home/lpi/Maildir/new/

\# cat 1645980180.Vfc02I1817bfM123445.lpi

- **Cài đặt Dovecot**

\# yum install -y dovecot

- Cấu hình Dovecot

\# vi /etc/dovecot/dovecot.conf  
\## Umcomment##

> protocols = imap pop3 lmtp
>
> \# vi /etc/dovecot/conf.d/10-mail.conf
>
> \## Uncomment \##
>
> mail_location = maildir:~/Maildir
>
> \# vi /etc/dovecot/conf.d/10-auth.conf
>
> \## Uncomment \##
>
> disable_plaintext_auth = yes
>
> \## Thêm từ : "login" \##
>
> auth_mechanisms = plain login
>
> \# vi /etc/dovecot/conf.d/10-master.conf
>
> \## Uncomment và thêm "postfix"
>
> mode = 0600
>
> user = postfix
>
> group = postfix
>
> \# systemctl enable dovecot
>
> \# systemctl start dovecot

- Kiem tra dich vu Dovecot

\# telnet localhost pop3

- **Cài đặt & Cấu hình SquirrelMail**

\#wget
http://downloads.sourceforge.net/project/squirrelmail/stable/1.4.22/squirrelmail-webmail-1.4.22.zip

\#unzip squirrelmail-webmail-1.4.22.zip -d /var/www/html/

\#mv /var/www/html/squirrelmail-webmail-1.4.22/
/var/www/html/squirrelmail

yum -y install squirrelmail

\# cd /usr/share/squirrelmail/config/

\# ./conf.pl

- Một list các lựa chọn cài đặt sẽ hiện ra . Bạn chọn số ‘**2**‘ để vào
  phần cài đặt server

- Phần cài đặt server , bạn tiếp tục chọn ‘**3**‘ để thay đổi Sendmail
  thành SMTP

<https://www.rosehosting.com/blog/how-to-install-squirrelmail-on-centos-7/>

<https://www.server-world.info/en/note?os=CentOS_7&p=httpd&f=21>

https://www.osradar.com/install-and-configure-squirrelmail-in-centos-7/

- Tạo Squirrelmail Virtualhost trong apache config

\# vi /etc/httpd/conf/httpd.conf

Alias /webmail /var/www/html/squirrelmail/

\<Directory /var/www/html/squirrelmail\>

Options Indexes FollowSymLinks

RewriteEngine On

AllowOverride All

DirectoryIndex index.php

Order allow,deny

Allow from all

\</Directory\>

\# systemctl restart httpd

\# chown -R apache: /var/www/html/ squirrelmail /

\# chmod -R 755 /var/www/html/ squirrelmail/

Truy cập vào webmail đểkiểm tra http://58.186.205.148/squirrelmail

Mail Relay

<img src="/media/image16.png" style="width:5in;height:2.42708in" />

\# vi /etc/postfix/main.cf

Myhostname

Mydomain

Myorigin

Mydestination

Relayhost

\# systemctl restart postfix

Mail Gateway

\# vi /etc/postfix/main.cf

Myhostname

Inet_interfaces=all

Mydestination = \$Myhostname, localhost,\$Mydomain, localhost

mynetworks

relayhost

https://tel4vn.edu.vn/blog/configure-postfix-for-smtp-relay-mailjet-centos8/
