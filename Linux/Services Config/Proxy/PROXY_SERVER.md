**PROXY SERVER**

1.  **GIỚI THIỆU VỀ PROXY SERVER**

- Proxy là một Internet server làm nhiệm vụ chuyển tiếp, kiểm soát thông
  tin giữa client (bên truy cập tài nguyên) và server (cung cấp tài
  nguyên). Proxy gồm một địa chỉ IP và một cổng truy cập cố định.

> <img src="/media/imagec.png" style="width:5.61288in;height:3.11198in" />
>
> \- Proxy server bảo vệ và ẩn máy tính đối với mạng bên ngoài
>
> \- Nó tập trung vào port, theo dõi và giám sát lưu lượng vào ra của
> mỗi port
>
> \- Proxy server cũng có thể được sử dụng cho việc lọc các yêu cầu
> (request)

2.  **KIẾN TRÚC CỦA PROXY SERVER**

<img src="/media/image8.png" style="width:3.34233in;height:4.44615in" />

3.  **CÁC LOẠI PROXY SERVER**

> <img src="media/image3.png" style="width:3.54392in;height:3.17126in" />

<img src="/media/imaged.png" style="width:4.63918in;height:2.92524in" />

- Proxy server xác định những yêu cầu từ phía client và quyết định đáp
  ứng hay không đáp ứng

- nếu yêu cầu được đáp ứng, proxy server sẽ kết nối tới server thật thay
  cho client và tiếp tục chuyển tiếp đến những yêu cầu từ client đến
  server, cũng như đáp ứng những yêu cầu của server đến client.

4.  **LỢI ÍCH CỦA PROXY SERVER**

- Tăng tốc độ duyệt Internet (caching)

- Cải thiện an ninh

- Kiểm soát truy cập Internet

- Để chia sẻ kết nối Internet qua mạng LAN

5.  **CÀI ĐẶT PROXY SERVER VỚI SQUID**

- Có thể cài đặt Squid bằng gói yum, rpm

  - **squid\[version\].rpm**

- Có thể cài đặt Squid bằng gói source

  - **squid\[version\].tar.gz**

- Squid server gồm những file sau trong hệ thống

  - **/etc/squid**

  - **/usr/lib/squid**

  - **/usr/sbin/squid**

  - **/var/log/squid**

6.  **CÀI ĐẶT PROXY SERVER VỚI SQUID**

- option chính cấu hình Squid server:

  - **http_port**: port Squid server lắng nghe request để phục vụ. Mặc
    định là port 3128.

  - **cache_dir**: định nghĩa Squid server sẽ chứa cache ở đâu

    - cache_dir storage_type directory-name megabytes L1 L2 \[options\]

> <img src="media/image5.png" style="width:4.18389in;height:1.5366in" />

- **cache_mem**: Squid server sẽ sử dụng bao nhiêu memory của RAM.

- **cache_access_log**: Squid server ghi nhận lại các request đã query
  Squid.

- **acl**: đây là phần phức tạp nhất của Squid server, cho phép người
  nào sẽ được truy cập Web, truy cập những trang nào.

acl intranet src 192.168.1.0/24

http_access allow intranet

http_access deny all

- Dùng **acl** để giới hạn truy cập bằng nhiều cách

  - Giới hạn truy cập theo thời gian.

  - Giới hạn truy cập theo IP.

  - Giới hạn truy cập theo port.

  - Giới hạn truy cập theo giao thức.

  - Giới hạn truy cập theo trang web.

  - Giới hạn file được phép download.

  - Giới hạn băng thông tối đa được sử dụng.

<img src="media/image6.png" style="width:5.43847in;height:4.21137in" />

- Để sử dụng Squid, user phải có username/pass hợp lệ =\> Squid
  Authentication.

- Để sử dụng tính năng Squid Authentication, cần biên dịch **ncsa_auth**
  với Squid.

- Tạo password cho user:

> ***\# /opt/apache/bin/htpasswd -c /opt/squidusers.htpasswd demouser***

- Cấu hình Squid hỗ trợ tính năng Squid Authentication

> <img src="media/image7.png" style="width:5.97419in;height:1.61451in" />

7.  **Installation & Configuration**

- Cài đặt Squid

\# yum -y install squid

- Khởi động và kiểm tra dịch vụ Squid

> \# systemctl start squid
>
> \# systemctl enable squid
>
> \# netstat -nalp \|grep 3128
>
> \# systemctl status squid

Một số tệp quan trọng sau khi cài đặt squid:

\- File configuration của squid: **/etc/squid/squid.conf**

\- File Accesss log của squid: **/var/log/squid/access.log**

\- File Cache log của squid: **/var/log/squid/cache.log**

- Cấu hình Squid cho phép dải IP được phép truy cập

> \# cp squid.conf squid.conf.backup
>
> \# vi /etc/squid/squid.conf

<img src="/media/image9.png" style="width:5in;height:2.48958in" />

- Mở Squid proxy port

<img src="/media/imagea.png" style="width:5in;height:1.70833in" />

- Cấu hình xác thực squid authentication, chúng ta cần cài đặt gói
  **httpd-tools**

> \# yum -y install httpd-tools
>
> \# touch /etc/squid/passwd
>
> \# chown squid: /etc/squid/passwd
>
> \# htpasswd /etc/squid/passwd pnh
>
> \# vi /etc/squid/squid.conf

\# systemctl restart squid

- Cấu hình block website

> \# touch /etc/squid/blacklist_site.acl
>
> ***.test1.com***
>
> ***.test2.vn***
>
> ***.test3.net***
>
> \# vi /etc/squid/squid.conf
>
> ***\#Cau hinh them***
>
> ***acl bad_urls dstdomain "/etc/squid/blacklist_site.acl"***
>
> ***http_access deny bad_urls***
>
> \# systemctl restart squid
>
> \- Thực hiện block download file
>
> \# vi /etc/squid/squid.conf
>
> ***acl blockfiles urlpath_regex "/etc/squid/blockfiles.acl"***
>
> ***http_access deny blockfiles***
>
> \# touch /etc/squid/blockfiles.acl
>
> \# vi /etc/squid/blockfiles.acl

- Kiểm tra bằng cách cấu hình proxy trên web browser, truy vấn đến các
  trang web bị chặn

<img src="/media/imageb.png" style="width:5in;height:3.96875in" />

- Kiểm tra log truy cập

\# tail -f /var/log/squid/access.log
