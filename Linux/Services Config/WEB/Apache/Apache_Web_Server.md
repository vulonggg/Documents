**Apache Web Server**

1.  **GIỚI THIỆU WEB SERVER**

> **Web server** là máy chủ cài đặt các chương trình phục vụ các ứng
> dụng web. Webserver có khả năng tiếp nhận request từ các trình duyệt
> web và gửi phản hồi đến client thông qua giao thức **HTTP** hoặc các
> giao thức khác.

- Features

<!-- -->

- Virtual hosts

- Access control for users, hosts, and groups

- Dynamically loaded modules

- Integrated config options

- Passwords or digital certificates for authentication

- Data compression

<!-- -->

- Security & Network

<!-- -->

- Intrusion detection & prevention

- Secure connections using SSL & TLS

- Per service config files stored in different locations

- Reversgrepe proxies

- Proxy load balancing

2.  **Cấu trúc Web Server**

> <img src="media/image1.png" style="width:6.42376in;height:2.7049in" />

3.  **Mô hình hoạt động**

> <img src="media/image2.png" style="width:5.07291in;height:3.24198in" />

4.  **CÀI ĐẶT WEB SERVER – APACHE**

- Có thể cài đặt Apache bằng gói yum, rpm

  - httpd-\[version\].rpm

- cài đặt Apache bằng gói source

  - httpd-\[version\].tar.gz

- Khi cài đặt bằng gói source có thể chọn nhiều option để biên dịch
  Apache

  - --enable-proxy

  - --enable-ssl

  - --enable-rewrite

<!-- -->

- Commands:

  - Apachectl: controls apache

  - Htpasswd: create passwords for basic authentication

  - Httpd: server binary

5.  **CẤU HÌNH WEB SERVER – APACHE**

- Thư mục **/etc/httpd**: Thư mục chứa tất cả các file cấu hình của dịch
  vụ Apache:

  - File **/etc/httpd/conf/httpd.conf**: File cấu hình chính của dịch vụ
    Apache.

  - Thư mục **/etc/httpd/conf.d**: chứa các cấu hình bổ sung cho Apache

  - Thư mục **/etc/httpd/conf.modules.d**: Chứa các file cấu hình chịu
    trách nhiệm tải các modules Apache.

  - Để quản lý tốt hơn, nên tạo một tệp cấu hình riêng (vhost) cho mỗi
    tên miền.

- Thư mục **/etc/httpd/conf.d**: Chứa các tệp vhost Apache và được đặt
  tên có kết thúc bằng **.conf**

- Thư mục **/var/log/httpd/**: Các file log của Apache (**access_log**
  và **error_log**) nằm trong thư mục Bạn nên có file **log** riêng cho
  mỗi **vhost**.

- Thư mục **/var/html/**: là thư mục gốc chứa các file html, images ….
  tạo thành nội dung cho trang web.

- File cấu hình của Apache: **httpd.conf** – Global section:

> <img src="media/image3.png" style="width:5.93232in;height:3.16263in" />
>
> <img src="media/image4.png" style="width:5in;height:1.35417in" />
>
> <img src="media/image5.png" style="width:5in;height:3.08333in" />
>
> <img src="media/image6.png" style="width:5in;height:2.13542in" />
>
> <img src="media/image7.png" style="width:5in;height:2.0625in" />

6.  **VIRTUAL HOST**

- Virtual Hosts là một phương thức lưu trữ cho phép lưu nhiều tên miền
  khác nhau trên cùng một máy chủ Server.

\<VirtualHost \*:80\>

ServerAdmin \<admin@website\>

ServerName \<website\>

ServerAlias [www.website](http://www.website)

DocumentRoot /var/www/html

DirectoryIndex index.php index.html

ErrorLog /var/www/html/error.log

CustomLog /var/www/html/request.log

\</VirtualHost\>

- Virtual Hosts có thể được xem như một giải pháp cho phép bạn cấu hình
  cho phép rất nhiều tên miền sử dụng một địa chỉ IP của một Server duy
  nhất

- **ServerAdmin** khai báo email của quản trị viên.

- **ServerName** khai báo domain mà website sẽ lắng nghe.

- **ServerAlias** (tuỳ chọn) khai báo Alias của domain, thương là www.

- **DirectoryIndex** loại file sẽ được tìm đến để khởi chạy.

- **DocumentRoot** khai báo đường dẫn chứa code của website.

- **ErrorLog** và **CustomLog** khai báo đường dẫn lưu file log của
  website.

7.  **ACCESS CONTROL**

- Access control giúp kiểm tra user nào được phép truy cập trang web.

- User có thể truy cập trang web nào, không thể truy cập trang web nào.

- Có thể giới hạn truy cập qua dãy IP của user.

- Có thể giới hạn truy cập bằng cách chỉ chấp nhận những user đã được
  xác thực (valid user).

- Có thể giới hạn truy cập qua thông tin users. Những user được kiểm tra
  **username/pass** đúng mới được truy cập.

- Tạo username/pass:

  - htpasswd -c /etc/httpd/conf/pwfile \<user_name\>

- Giới hạn truy cập trong file **httpd.conf**

\<Directory "/var/www/html/"\>

AuthType Basic

AuthName "Basic Authentication"

AuthUserFile /etc/httpd/conf/pwfile

Require valid-user

\</Directory\>

<img src="media/image8.png" style="width:5in;height:2.30208in" />

<img src="media/image9.png" style="width:4.47917in;height:1.46506in" />

<img src="media/image10.png" style="width:5in;height:1.34375in" />

<img src="media/image11.png" style="width:5in;height:1.5625in" />

<img src="media/image12.png" style="width:5in;height:1.51042in" />

<img src="media/image13.png" style="width:5in;height:2.1875in" />

<img src="media/image14.png" style="width:5in;height:1.5in" />

<img src="media/image15.png" style="width:5in;height:1.70833in" />

<img src="media/image16.png" style="width:5in;height:1.75in" />

<img src="media/image17.png" style="width:5in;height:1.76042in" />

<img src="media/image18.png" style="width:5in;height:1.67708in" />

8.  **LOG FILES**

- **access_log** – liệt kê từng request truy cập vào trang web.

- **agent_log** – liệt kê những chương trình được web server gọi chạy.
  Log này là option, có thể chọn lúc biên dịch apache, hoặc cấu hình
  trực tiếp trong file cấu hình httpd.conf

- **error_log** – Lỗi phát sinh trong quá trình chạy của web server.

- **refer_log** – liệt kê những URL trước đó browser đã sử dụng. Log này
  cũng là option, có thể chọn trong khi biên dịch, khi cấu hình, hoặc có
  thể không cấu hình.

9.  **PERFORMANCE**

- **StartServers:** số tiến trình con được sinh ra lúc đầu khi web
  server start.

- **MinSpareServers:** số tiến trình con tối thiểu ở trạng thái idle, để
  chờ kết nối.

- **MaxSpareServers**: số tiến trình con tối đa cho phép ở trạng thái
  idle, để chờ kết nối.

- **MaxClient**: web server phục vụ tối đa cho bao nhiêu request đồng
  thời.

\<IfModule mpm_worker_module\>

ServerLimit 40

StartServers 2

MaxClients 1000

MinSpareThreads 25

MaxSpareThreads 75

ThreadsPerChild 25

MaxRequestsPerChild 0

\</IfModule\>

10. **Installation & Configuration**

> <img src="media/image19.png" style="width:5.59447in;height:2.21696in" />

1.  Cài đặt Apache

> \# yum install –y selinux-policy-devel
>
> \# **yum install –y httpd**

2.  Khởi động và kiểm tra dịch vụ Apache

> \# systemctl enable httpd
>
> \# systemctl start httpd
>
> \# systemctl status httpd
>
> \# netstat -nalp\|grep 80

3.  Cấu hình **firewalld** cho phép chạy dịch vụ Apache

> \# firewall-cmd --permanent --zone=public --add-service=http
>
> \# firewall-cmd --permanent --zone=public --add-service=https
>
> \# firewall-cmd --reload

4.  Vào Web Browser để test

5.  Tạo VirtualHost

\# cd /etc/httpd

> \# mkdir sites-available
>
> \# mkdir sites-enabled
>
> \# vi conf/httpd.conf

IncludeOptional sites-enabled/\*.conf

> \# cd sites-available/
>
> \# vi site.com.conf

\<VirtualHost \*:80\>

ServerAdmin admin@site.com

ServerName site.com

ServerAlias www.site.com

DocumentRoot /var/www/html/site

DirectoryIndex index.php index.html

ErrorLog /var/www/html/site/error.log

CustomLog /var/www/html/site/requests.log combined

\</VirtualHost\>

- Non-standard port

> \# vi /etc/httpd/conf/httpd.conf
>
> Listen \<port_num\>
>
> \# semanage port –at http_port_t -p tcp \<port_num\>
>
> \# semanage port –list \| grep ^http_port_t
>
> \# firewall-cmd –permanent –add-port \<port_num\>/tcp
>
> \# firewall-cmd –reload

6.  Tạo một thư mục để lưu trữ dữ liệu cho trang web pnh.com.vn và một
    trang mặc định **index.html**

> \# cd /var/www/html/
>
> \# chmod -R 755 /var/www/html
>
> \# mkdir site \# mkdir -p /var/www/html/site
>
> \# chown apache:apache -R site/
>
> \# chmod -R 770 site/
>
> \# vi site/index.html

\<html\>

\<head\>

\<title\>Day la website cua SITE!\</title\>

\</head\>

\<body\>

\<p\>Welcome all of you\</p\>

\</body\>

\</html\>

> \# apachectl configtest
>
> \# ln -s /etc/httpd/sites-available/site.com.conf
> /etc/httpd/sites-enabled/site.com.conf
>
> \# setenforce 0
>
> \# systemctl restart httpd

7.  Kết hợp khai báo bản ghi www.site.com trên DNS server trỏ về Ip
    của  
    Webserver.

<img src="media/image20.png" style="width:5in;height:2.17708in" />

8.  Kiểm tra và truy vấn bằng **nslookup**

9.  Cấu hình giới hạn truy cập trang web

\# htpasswd -c /etc/httpd/conf/pwfile \<user\>

AuthGroupFile \<group_file\>

Require group \<group_name\>

\# systemctl restart httpd

10. Cấu hình giới hạn performance webserver

\# vi /etc/httpd/conf/httpd.conf

\<IfModule mpm_worker_module\>

ServerLimit 40

StartServers 2

MaxClients 1000

MinSpareThreads 25

MaxSpareThreads 75

ThreadsPerChild 25

MaxRequestsPerChild 0

\</IfModule\>

\# systemctl restart httpd

https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04

**\## Adding Vhost Apache**

mkdir -p /var/www/pnh

chmod -R 755 /var/www

touch /var/www/pnh/index.html

echo "\<center\>\<h1\>This is website pnh.com.vn\</h1\>\</center\>" \>
/var/www/pnh/index.html

mkdir /etc/httpd/sites-available

mkdir /etc/httpd/sites-enabled

vi /etc/httpd/conf/httpd.conf

IncludeOptional sites-enabled/\*.conf \#them vao dong cuoi dung

vi/etc/httpd/sites-available/pnh.com.vn.conf

\<VirtualHost \*:80\>

ServerAdmin admin@pnh.com.vn

ServerName pnh.com.vn

ServerAlias www.pnh.com.vn

DocumentRoot /var/www/pnh

DirectoryIndex index.php index.html

ErrorLog /var/www/pnh/error.log

CustomLog /var/www/pnh/requests.log combined

\</VirtualHost\>

ln -s /etc/httpd/sites-available/pnh.com.vn.conf
/etc/httpd/sites-enabled/pnh.com.vn.conf

systemctl restart apache
