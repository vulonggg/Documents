**NTP SERVER**

1.  **GIỚI THIỆU VỀ DỊCH VỤ** **NTP**

- NTP (Network Time Protocol - Giao thức đồng bộ thời gian mạng) là một
  giao thức để đồng bộ đồng hồ của các hệ thống máy tính thông qua mạng
  dữ liệu chuyển mạch gói với độ trễ biến đổi.

- NTP (Network Time Protocol) là một giao thức chạy trên cổng 123 UDP
  tại Transport Layer nó giúp cho các máy tính trên hệ thống đồng bộ hóa
  thời gian qua mạng trong một thời gian chính xác.

- NTP cũng là tên gọi của phần mềm được triển khai trong dự án Dịch vụ
  NTP Công cộng (NTP Public Services Project).

> <img src="media/image1.png" style="width:4.58071in;height:0.58255in" />
>
> <img src="/media/image9.png" style="width:5.5848in;height:1.98958in" />
>
> <img src="/media/imagea.png" style="width:5.63584in;height:2.03125in" />
>
> <img src="/media/imageb.png" style="width:5.41667in;height:1.21875in" />
>
> <img src="/media/imagec.png" style="width:5.42708in;height:1.78642in" />
>
> <img src="/media/imaged.png" style="width:5.47917in;height:1.78073in" />
>
> <img src="/media/imagee.png" style="width:5.59242in;height:2.45833in" />
>
> <img src="/media/imagef.png" style="width:5.71111in;height:2.67708in" />

2.  **KIẾN TRÚC CỦA HỆ THỐNG** **NTP**

> <img src="media/image2.png" style="width:4.23915in;height:3.50976in" />

- NTP sử dụng kiến trúc phân cấp, phân lớp cho các cấp nguồn đồng bộ,
  mỗi một cấp trong phân cấp này được gọi là một "**statum**' và được
  gán một số của cấp bắt đầu từ 0 là cấp cao nhất.

- Stratum **0**: Bao gồm những thiết bị như đồng hồ nguyên tử (atomic
  clock), đồng hồ GPS hay các đồng hồ vo tuyến khác. Thiết bị Stratum-0
  thường không được kết nối trực tiếp vào mạng mà được kết nối với máy
  tính (ví dụ thông qua cổng RS-232 sử dụng tín hiệu xung.

- Stratum **1**: Đây là các máy tính kết nối với thiết bị Stratum 0. Đây
  là nguồn đồng hồ tham chiếu cho các server Stratum 2.

- Stratum **2**: Là các máy tính gửi các yêu cầu NTP đến cho server
  Stratum 1.

- Stratum **3**: Các máy tính mày cũng thực hiện các chức năng như
  Stratum 2, có thể có tối đa 16 cấp, NTP có thể hỗ trợ đến 256 Stratum.

<img src="/media/image10.png"
style="width:5.35565in;height:2.66667in" />

<img src="/media/image11.png" style="width:5.75343in;height:2.625in" />

<img src="/media/image12.png"
style="width:5.70313in;height:1.52083in" />

3.  **HOẠT ĐỘNG CỦA NTP SERVER**

> <img src="media/image3.png" style="width:4.50212in;height:3.43366in" />

4.  **CÀI ĐẶT NTP SERVER**

- Có thể cài đặt gói NTP hoặc gói Chronyc bằng yum hoặc rpm

  - Rpm –ivh ntp \[version\].rpm, Rpm –ivh Chronyc \[version\].rpm

  - Yum –y install ntp, Yum –y install ntp, Chronyc

- có thể cài đặt NTP bằng gói source

  - ntp\[version\].tar.gz

  - Chronyc\[version\].tar.gz

- NTP server gồm những file sau trong hệ thống

  - /etc/ntp.conf

  - /etc/chrony.conf

- NTP Client cũng cài đặt và cấu hình gói ntp tương tự như NTP server

<img src="/media/image5.png" style="width:4.34001in;height:2.17023in" />

<img src="/media/image13.png"
style="width:5.63775in;height:2.30208in" />

5.  **Installation & Configuration**

\- **Cài đặt NTP server**

\# yum install -y chrony

\# systemctl enable chronyd

\# systemctl start chronyd

\- **Cấu hình cấu hình NTP Server và kiểm tra dịch vụ**

\# vi /etc/chrony.conf

<img src="/media/image6.png" style="width:5.95833in;height:0.96528in" />

<img src="/media/image7.png" style="width:6.06283in;height:6.51042in" />

\# tail -20f /var/log/messages

\# systemctl restart chronyd

\# systemctl status chronyd

<img src="/media/image14.png"
style="width:6.48958in;height:2.39562in" />

\# firewall-cmd --permanent --add-service=ntp

\# firewall-cmd –reload

\# firewall-cmd –list-all

\# systemctl restart chronyd

- **Thực hiện cấu hình NTP Client**

**\#** yum install chrony

\# systemctl start chronyd

\# systemctl enable chronyd

\# vi /etc/chrony.conf

<img src="/media/image15.png"
style="width:5.51938in;height:6.32292in" />

Comment 3 line of server/pool

Server/pool \<Server’s IP address\> iburst

\# systemctl restart chronyd

\# timedatectl set-ntp true

- **Kiểm tra dịch vụ trên NTP Server sau khi khai báo**

\# chronyc sources -v

\# chronyc clients

- **Kiểm tra dịch vụ trên NTP Client sau khi khai báo**

> **\#** chronyd -q 'server 0.europe.pool.ntp.org iburst'
>
> \# date
>
> \# chronyc tracking
>
> \# chronyc sourcestats –v
>
> \# chronyc sources -v

- Configure time & date

> \# timedatectl
>
> \# timedatectl list-timezones
>
> \# timedatectl list-timezones \| grep Asia
>
> \# timedatectl set-timezone Asia/Hong Kong
>
> \# timedatectl
>
> \# timedatectl set-time 23:26:00
>
> \# timedatectl set-time 2019-09-20
>
> \# timedatectl set-time ‘2019-09-20 23:26:00’
>
> \# timedatectl set-ntp true
>
> \# systemctl restart systemd-timedated
>
> \# timedatectl

- Cryonyc

https://adroittechnologiesautomation.com/t/setting-up-a-ntp-server-and-client/1470

https://vitux.com/how-to-install-ntp-server-and-client-on-ubuntu/
