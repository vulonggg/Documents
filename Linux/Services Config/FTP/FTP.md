**FTP & FTPS SERVER**

1.  **GIỚI THIỆU FTP**

- **FTP** là từ viết tắt của File Transfer Protocol, giao thức này được
  xây dựng dựa trên chuẩn TCP/IP và là giao thức truyền tệp tin khá phổ
  biến hiện nay.

- **FTP** là một dịch vụ đặc biệt vì nó dùng đến 02 cổng:

  - Cổng **20** dùng để truyền dữ liệu (data port)

  - Cổng **21** dùng để truyền lệnh (command port).

> <img src="media/image1.png" style="width:4.22003in;height:1.32678in" />

2.  **MÔ HÌNH HOẠT ĐỘNG**

> <img src="media/image2.png" style="width:5.17295in;height:3.5111in" />

- Do chức năng điều khiển và dữ liệu được truyền tải bằng cách sử dụng
  các kênh riêng biệt nên mô hình FTP chia mỗi thiết bị thành 2 phần
  giao thức logic chịu trách nhiệm cho mỗi kết nối ở trên:

  - Protocol interpreter (PI): Là thành phần quản lý kênh điều khiển,
    phát và nhận lệnh và trả lời.

  - Data transfer process (DTP): chịu trách nhiệm gửi và nhận dữ liệu
    giữa client và server.

- ACTIVE MODE

> <img src="media/image3.png" style="width:4.97591in;height:3.24837in" />

- PASSIVE MODE

> <img src="media/image4.png" style="width:4.78293in;height:2.96396in" />

3.  **CÀI ĐẶT VÀ CẤU HÌNH DỊCH VỤ FTP**

- Có nhiều gói để cài đặt dịch vụ FTP như: **vsftpd**, **wuftpd**,
  **pureFTPd**, **proFTPD**.

- Gói **vsftpd** được đánh giá là security tốt.

- Có thể cài đặt bằng **RPM** hoặc **source**.

- File cấu hình chính của gói vsftpd:

  - **vsftpd.conf**: kiểm soát hoạt động của dịch vụ FTP.

  - **vsftpd.ftpusers**: ds những users không được phép log vào FTP.

  - **vsftpd.user_list**: tùy theo cấu hình file vsftpd.conf, dịch vụ
    FTP sẽ deny hoặc allow ds những users này.

4.  **CÁC LỆNH CỦA FTP**

> <img src="media/image5.png" style="width:5.52235in;height:3.76095in" />

5.  **GIỚI THIỆU FTPS VÀ MÔ HÌNH**

- FTPS được viết tắt bởi File Transfer Protocol Secure. Là giao thức
  được sử dụng cùng loại trao đổi dữ liệu với FTP.

- FTPS bổ sung thêm ứng dụng hỗ trợ bảo mật lớp vận chuyển ( Transfer
  Layer Security - TLS) và tiền thân (Secure Socket Layer - SSL) của nó,
  mục đích của việc bổ sung này là tăng tính bảo mật, hạn chế nhược điểm
  của FTP

- FTPS có thể được gọi qua 2 phương thức:

  - Giao thức FTPS ẩn: kết nối qua cổng 990

  - Giao thức FTPS hiện: kết nối trên cổng 21

> <img src="media/image6.png" style="width:4.68942in;height:1.37462in" />

6.  **CÀI ĐẶT VÀ CẤU HÌNH DỊCH VỤ FTPS**

- Cài đặt gói vsftpd, openssl và bật tính năng ssl/tls.

- Tạo key cert trong thư mục:/etc/pki/tls/certs

  - vsftpd.conf:

    - Cấu hình enable ssl/tls.

    - Cấu hình allow passive ports.

7.  **Installation & Configuration**

> <img src="media/image7.png" style="width:5.41727in;height:2.16043in" />

1.  Cài đặt **FTP SERVER**

- Cài đặt và cấu hình gói **vsftpd** **\#yum install vsftpd -y**

- Cấu hình file **vsftpd.conf**

> <img src="/media/image9.png" style="width:5.80694in;height:6.71101in" />

- Nếu **Selinux** đang **enable** thì thực hiện cấu hình cho phép dịch
  vụ vsftp chạy **\#setsebool –P ftpd_full_access on**

- Thực hiện khai báo cho phép các port của ftp nếu hệ thống đang chạy
  firewall

> \#firewall-cmd --add-service=ftp --permanent
>
> \#firewall-cmd --reload

- Khởi động dịch vụ **vsftpd**

> **\#systemctl enable -now vsftpd**

- Cấu hình cho phép user pnh, root được quyền truy cập

> \#vi /etc/vsftpd/chroot_list

2.  Cài đặt FTP CLIENT

- Cấu hình **lftp** và cấu hình ftp Client

> **\#yum install lftp**

- Thực hiện đăng nhập vào từ **ftp client** và thực hiện các lệnh cơ bản
  của **ftp**

- Thực hiện đăng nhập: **\#lftp -u pnh 58.186.205.148**

- Kiểm tra thu mục hiện tại trên ftp server:

> \#**lftp pnh@58.186.205.148:~\> pwd**
>
> \#**ftp://pnh@58.186.205.148**

- Kiểm tra thu mục hiện tại trên ftp client:

> **\#lftp pnh@58.186.205.148:~\> !pwd**
>
> **\#/root**

- Liệt kê các file đang có trong thu mục hiện tại trên ftp server:

> \#**lftp pnh@58.186.205.148:~\> ls**

- Liệt kê các file đang có trong thu mục hiện tại trên ftp client:

> \#**lftp pnh@58.186.205.148:~\> !ls –l**

- Thực hiện tạo file test-ftp từ ftp client lên trên ftp server:

> \#**lftp pnh@58.186.205.148:~\> put test-ftp.txt // ls -l**

- Thực hiện đẩy nhiều file từ ftp client lên trên ftp server:

> \#**mput -a \*.cfg**

- Xóa file test-ftp trên thư mục của ftp client và tải lại từ ftp
  server:

> \#lftp pnh@58.186.205.148:~\> !rm test-ftp.txt
>
> \#lftp pnh@58.186.205.148:~\> !ls –l
>
> \#lftp pnh@58.186.205.148:~\> get -a test-ftp.txt
>
> \#lftp pnh@58.186.205.148:~\> !ls –l

- Thực hiện chế độ overwirte file khi dùng lệnh **mput/mget**

> **\#lftp pnh@58.186.205.148:~\> !ls –l**

- Thực hiện tạo và xóa thư mục trên ftp server

> \#lftp pnh@58.186.205.148:~\> mkdir lpi-pnh
>
> \#lftp pnh@58.186.205.148:~\> rm lpi-pnh/

- Thực hiện xóa nhiều file cùng lúc

> \#lftp pnh@58.186.205.148:~\> mrm anaconda-ks.cfg original-ks.cfg

- Thực hiện logout ra khỏi phiên ftp

> \#ftp pnh@58.186.205.148:~\> quit

3.  Cài đặt FTPS sử dụng SSL/TLS

- Cài đặt gói **openssl \#yum install openssl**

- Tạo thư mục chứa SSL Certificate tự generate và tự signed

> \# cd ../../private
>
> \# openssl req –x509 –nodes –newkey rsa:2048 –keyout
> /etc/pki/tls/certs/vsftpd.pem –out /etc/pki/tls/certs/vsftpd.pem

- Thực hiện phân quyền cho file:

> \# cd /etc/pki/tls/certs
>
> \# chmod 600 vsftpd.pem

- Cấu hình các tham số vào cuối file **/etc/vsftpd/vsftpd.conf** cho
  phép hỗ trợ **ssl/tls**  
  và cho phép chạy các port **passive** mode, sau đó khởi động lại dịch
  vụ **vsftpd**

> \<enable SSL/TLS\>
>
> \# rsa_cert_file=/etc/pki/tls/certs/vsftpd.pem
>
> \# ssl_enable=YES
>
> \# force_local_data_ssl=YES
>
> \# force_local_logins_ssl=YES
>
> \<fix passive ports\>
>
> \#pasv_enable=YES
>
> \#pasv_min_port=60000
>
> \#pasv_max_port=60100
>
> \# systemctl restart vsftpd

- Thực hiện cấu hình hỗ trợ **ssl/tls** trên ftp client.

> \# vi ~/.lftprc
