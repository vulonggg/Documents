**NGINX**

1.  **GIỚI THIỆU VỀ NGINX**

- NGINX là một web server mạnh mẽ mã nguồn mở. Nginx sử dụng kiến trúc
  đơn luồng, hướng sự kiện vì thế nó hiệu quả hơn Apache server.

- NGINX cũng được thiết kế để làm những hệ thống khác như load
  balancing, HTTP caching, hay sử dụng như một reverse proxy.

- NGINX hiện là ứng dụng web server phổ biến nhất hiện nay, có hàng chục
  triệu trang web sử dụng NGINX, bao gồm top 100.000 trang web lớn nhất
  thế giới: Airbnb, Google, Dropbox, Netflix, Tumblr, WordPress.com…

> <img src="media/image1.png" style="width:4.76222in;height:2.04849in" />

2.  **KIẾN TRÚC CỦA NGINX**

> <img src="media/image2.png" style="width:5.89466in;height:3.78739in" />

- **Master process**: thực thi những tác vụ như đọc config, binding
  ports, tạo một số lượng các process con.

- **Cache loader process**: process này chạy lúc khởi động để nạp bộ nhớ
  disk cache vào memory sau đó nó sẽ exit. Process này được lên kế hoạch
  trước, sử dụng ít tài nguyên hệ thống.

- **Cache manager process**: process chạy định kỳ, để giữ cho bộ nhớ
  disk cache luôn đúng kích thước như trong config.

- **Worker process**: là những process làm việc với connections, nó đọc
  và ghi nội dung vào disk, và giao tiếp với app server, handle request
  từ clients.

3.  **HOẠT ĐỘNG CỦA NGINX**

> <img src="media/image3.png" style="width:6.09514in;height:3.64653in" />

4.  **CÀI ĐẶT NGINX**

- Có thể cài đặt NGINX bằng gói yum, rpm

  - nginx\[version\].rpm

- Hoặc có thể cài đặt NGINX bằng gói source

  - nginx\[version\].tar.gz

- Khi cài đặt bằng gói source có thể cần cài đặt thêm các gói
  dependencies khác như:

  - zlib

  - openssl

  - Pcre

5.  **CẤU HÌNH NGINX**

> **Cấu trúc:**

- Tất cả file cấu hình của nginx nằm trong thư mục - **/etc/nginx**

- File cấu hình chính của nginx là **– /etc/nginx/nginx.conf**

- Document root directory **– /usr/share/nginx/html**

- File config **/etc/nginx/nginx.conf** sẽ bao gồm:

  - **directive:** là chỉ thị lệnh bao gồm tên và tham số truyền vào, và
    kết thúc bởi dấu ;. Ví dụ : gzip on;

  - **context:** tương tự như là một scope trong ngôn ngữ lập trình, hay
    có thể hiểu là một block bao gồm nhiều directive.

> <img src="media/image4.png" style="width:3.94083in;height:1.55503in" />

- File bắt đầu cùng với 4 directives: **user, worker_processes,
  error_log, và pid.**

- NGINX không có Virtual host, thay vào đó là Server Blocks sử dụng
  **server_name** và nghe các chỉ thị để liên kết với các **tcp
  sockets**. Tất cả các file server block phải có định dạng là **.conf**
  và được lưu trong thư mục **/etc/nginx/conf.d** hoặc
  **/etx/nginx/conf.**

- **worker_processes:** Thiết lập này định nghĩa số worker processes mà
  NGINX sẽ sử dụng. Bởi vì NGINX là đơn luồng (single threaded), nó
  thường bằng với số lõi CPU.

- **worker_connection**: Đây là số lượng tối đa của các kết nối đồng
  thời cho mỗi worker process và nói cho các worker process của chúng ta
  có bao nhiêu người có thể được phục vụ đồng thời bởi NGINX.

- **access_log & error_log**: Đây là những tệp tin mà NGINX sẽ sử dụng
  để log bất kỳ lỗi và số lần truy cập. Các bản ghi này thường được sử
  dụng để gỡ lỗi hoặc sửa chữa.

- **gzip**: Đây là các thiết lập nén GZIP của các NGINX reponse, là một
  phương thức để nén và làm giảm dung lượng các file ở server trước khi
  gửi đến client (ví dụ như trình duyệt). Nó giúp tiết kiệm băng thông,
  tăng tốc độ tải của website.

- Trong các thiết lập phụ của GZIP, cần quan tâm tới
  **gzip_comp_level**, nó là mức nén và nằm trong khoảng từ 1 tới 10.
  Thông thường, giá trị này không nên lớn hơn 6

- NGINX có thể hỗ trợ nhiều hơn một website, và các tệp tin định nghĩa
  các

trang web ở trong thư mục **/etc/nginx/sites-available**.

6.  **Installation & Configuration**

> <img src="media/image5.png" style="width:6.06591in;height:2.33251in" />
>
> Lưu ý: Xài NGINX thì phải stop APACHE

1.  **Cài đặt Nginx**

> \# yum install nginx

2.  **Khởi động và kiểm tra dịch vụ Nginx**

> \# systemctl enable nginx
>
> \# systemctl start nginx
>
> \# systemctl status nginx
>
> \# netstat –nalp \|grep 80

3.  **Cấu hình firewalld cho phép chạy dịch vụ Nginx**

\# firewall-cmd --permanent --zone=public --add-service=http

\# firewall-cmd --permanent --zone=public --add-service=https

\# firewall-cmd --reload

4.  **Truy cập bằng Web Browser để kiểm tra xem Nginx đã hoạt động với
    web default page**

5.  **Tạo một virtual host riêng cho domain \<site.com\>**

> \# vi /etc/nginx/conf.d/site.com.conf

\# create new

server {

listen 80;

server_name www.site.com;

location / {

root /usr/share/nginx/site.com;

index index.html index.html;

}

}

6.  **Tạo một thư mục để lưu trữ dữ liệu cho trang web**

\# mkdir /usr/share/nginx/site.com

\# vi /usr/share/nginx/site.com/index.html

- một trang mặc định index.html

\<html\>

\<body\>

\<div style="width: 100%; font-size: 40px; font-weight: bold;
text-align: center;"\>

Nginx Virtual Host Test Page WWW.SITE.COM

\</div\>

\</body\>

\</html\>

7.  **Kết hợp khai báo bản ghi www.site.com trên DNS server trỏ về Ip
    của WebServer.**

8.  **Kiểm tra và truy vấn từ web browser bằng domain vừa khai báo.**

> \# nslookup

9.  **Cấu hình Nginx hỗ trợ SSL/TSL**

- Tạo thư mục chứa **self-sign key**

> \# mkdir /etc/ssl/private
>
> \# chmod 700 /etc/ssl/private

- Tạo cặp chứng chỉ và khóa với **OpenSSL**

\# cd vào thư mục **named**

\# openssl req -x509 -nodes -days 365 -newkey rsa:2048 –keyout
/etc/ssl/private/nginx-selfsigned.key -out
/etc/ssl/certs/nginx-selfsigned.crt

\# openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048

- Cấu hình Nginx sử dụng **SSL**

\# vi /etc/nginx/conf.d/ssl.conf

server {

listen 443 http2 ssl;

listen \[::\]:443 http2 ssl;

server_name \<server’s IP address\>;

ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;

ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;

ssl_dhparam /etc/ssl/certs/dhparam.pem;

root /usr/share/nginx/html;

location / {

}

error_page 404 /404.html;

location = /404.html {

}

error_page 500 502 503 504 /50x.html;

location = /50x.html {

}

}

- Cấu hình redirect từ **http** sang **https**

> \# vi /etc/nginx/default.d/ssl-redirect.conf
>
> return 301 https://\$host\$request_uri/;

- Thực hiện load lại cấu hình Nginx

> \# nginx –t
>
> \# systemctl restart nginx

- Thực hiện test dịch vụ với https

> <https://server_domain_or_Ip>

<https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04>

<https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04>

[Cấu hình Reverse Proxy trên Nginx
(viblo.asia)](https://viblo.asia/p/cau-hinh-reverse-proxy-tren-nginx-Az45bGxqKxY)

[How To Configure Nginx as a Reverse Proxy on Ubuntu 22.04 \|
DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-as-a-reverse-proxy-on-ubuntu-22-04)
