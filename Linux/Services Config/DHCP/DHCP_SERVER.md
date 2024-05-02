**DHCP SERVER**

1.  **Giới thiệu dịch vụ DHCP**

    1.  **Chức năng**

- DHCP (Dynamic Host Configuration Protocol) là một giao thức mạng cho
  phép server tự động cấp phát IP và các tham số cấu hình mạng liên quan
  cho các client.

- Các IP được cấp cho Client sẽ nằm trong nhóm IP đã được chúng ta cấu
  hình trước.

- Khi một client khởi động thì nó sẽ nhận được một địa chỉ IP động

- Địa chỉ IP được DHCP server gán cho DHCP client, thời gian được thay
  đổi IP có thể tùy thuộc vào thời gian hiệu lực cấp phát (hay
  leasetime)

- DHCP cũng cung cấp động các tham số khác: DNS, gateway…, cấp IP tĩnh.

  1.  **Cách hoạt động**

> <img src="media/image1.png" style="width:4.42296in;height:2.40968in" />

- **DHCP Discover:** Đây là một gói tin được gửi đến DHCP server khi có
  một thiết bị yêu cầu cung cấp địa chỉ IP để truy cập vào mạng.

- **DHCP Offer**: Được máy chủ DHCP gửi phản hồi cho Client sau khi nhận
  DHCP Discover. Đây là gói chứa địa chỉ IP, cấu hình TCP/IP bổ sung.

- **DHCP Request**: Đây là gói tin được DHCP Client phản hồi với server
  về sự chấp nhận địa chỉ IP sau khi nhận DHCP Offer.

- **DHCP Acknowleadge**: Đây là gói tin mà máy chủ DHCP phản hồi lại với
  Client nhằm xác minh rằng đã chấp nhận địa chỉ IP DHCP Request đồng
  thời định hướng các tham số tùy chọn để thực hiện việc cho phép Client
  truy cập mạng TCP/IP cũng như hoàn tất quá trình khởi động.

- **DHCP Nak**: Nếu Client không còn sử dụng địa chỉ IP do nó đã hết hạn
  hoặc đã chuyển sang một người dùng mới. Thì lúc này DHCP sẽ gửi một
  gói tin DHCP Nak.

Và nó chính là gói tin được gửi từ DHCP server đến Client khi nó nhận
được yêu cầu từ một địa chỉ IP không có giá trị theo các Scope mà nó
được định cấu hình.

- **DHCP Decline**: Trường hợp DHCP Client quyết định tham số thông tin
  được đề nghị nào không có giá trị nó sẽ gửi một gói DHCP Decline đến
  các server và client phải bắt đầu quá trình thuê bao lại.

- **DHCP Release**: Đây là một gói tin được DHCP Client gửi đến một
  server để giải phóng địa chỉ IP và có thể xóa bất kỳ IP đang còn tồn
  tại

  1.  **GÓI CÀI ĐẶT**

- Ứng dụng **isc dhcp server.**

- Ứng dụng **dnsmasq**.

- DHCP được cài đặt bằng hai gói:

  - dhcp-\[version\].rpm.

  - dhcp-devel-\[version\].rpm.

- Cài đặt từ yum: **yum install dhcp -y**

- Hoặc cài đặt từ gói source.

- File cấu hình chính: **/etc/dhcpd.conf**

> <img src="media/image2.png" style="width:3.42874in;height:2.51071in" />

- File cài đặt: **/var/lib/DHCP/DHCPD.LEASE**

<!-- -->

- theo dõi tình trạng cấp phát IP động

> <img src="media/image3.png" style="width:3.06574in;height:2.25837in" />

- Có thể get IP động bằng cách điều chỉnh file:

***/etc/sysconfig/network-scripts/ifcfg-eth\[n\]***

- Lệnh **dhclient**: Dùng để get IP động từ DHCP server.

> ***dhclient –s \<IP address\>***

2.  **<u>LAB</u>**

<!-- -->

1.  <u>Cấu hình **dhcp server**</u>

- Cài đặt package \# yum install dhcp-server

- Xem file \# cat /etc/dhcp/dhcpd.conf

- Copy cấu hình theo mẫu có sẵn

\#cp /usr/share/doc/dhcp-server/dhcpd.conf.example /etc/dhcp/dhcpd.conf

\#more /usr/share/doc/dhcp-4.2.5/dhcpd.conf.example

\#cp /usr/share/doc/dhcp-4.2.5/dhcpd.conf.example /etc/dhcp/dhcpd.conf

- Cấu hình file \#vi /etc/dhcp/dhcpd.conf

> \#Cấu hình DHCP

subnet \<IP address\> netmask \<netmask\> {

interface eth\[n\];

range \<first_IP\> \<last_IP\>;

option domain-name-servers \<DNS_IP\>;

option domain-name "\<name\>";

option routers \<gateway\>;

option broadcast-address \<broadcast address\>;

default-lease-time \<time\>;

max-lease-time \<max_time\>;

}

- Khởi động dịch vụ dhcpd

> \#systemctl start dhcpd
>
> \#systemctl enable dhcpd

- Cấu hình gán IP động và cố định cho một địa chỉ MAC

host testclient {

Hardware ethernet \<MAC address\>

Fixed-address \<IP address\>

}

Ý nghĩa một số options:

- **ddns-update-style interim**: Không cho phép DHCP cập nhật động DNS

- **ignore client-updates**: Không cho phép DHCP cập nhật động DNS

- **subnet** …. **netmask** : Subnet và netmask

- **option routers** : Default gateway

- **option subnet-mask** : Netmask cấp cho client

- **option nis-domain** : NIS domain

- **option domain-name** : Domain mame

- **option domain-name-servers** : IP DNS server

- **range dynamic-bootp** : Vùng địa chỉ cấp phát cho các clients

- **default-lease-time** : Thời gian mặc định cấp IP cho một client

- **max-lease-time** : Thời gian tối đa cấp IP cho một client

- **host ns** : Khái báo những máy luôn nhận IP cố định

2.  <u>Thiết lập với **client**</u>

- Chỉnh sửa file cấu hình card mạng trên máy Client

> \# vi /etc/sysconfig/network-scripts/ifcfg-eth0

TYPE=Ethernet

BOOTPROTO=dhcp

NAME=eth0

UUID=2da380ad-6733-47d5-aead-e1a28d35faed

DEVICE=eth0

ONBOOT=yes

> \# systemctl restart network

- cài đặt DHCP client \#yum install dhcp-client

- sử dụng lệnh **dhclient** để yêu cầu địa chỉ IP \#dhclient eth0

\#dhclient –s \<IP_address\>

- Kiểm tra **log** quá trình cấp phát trong **/var/log/message**

> \# cat /var/log/message \| grep -i "dhcp"

- Kiểm tra **log** quá trình cấp phát bằng cách lắng nghe port **udp
  67**

> \# tcpdump -i eth0 port 67

- Theo dõi tình hình cấp phát DHCP trên Server

> \# cat /var/lib/dhcpd/dhcpd.leases

**DHCP Relay Agent** là gì?

- Do DHCP sử dụng broadcast, nên DHCP client và DHCP server phải nằm
  trên cũng một mạng vật lý để có thể lắng nghe các bản tin broadcast
  của nhau. Để một client và một server trên các mạng khác nhau có thể
  liên lạc, một thành phần thứ 3 được yêu cầu giải quyết vấn đề chuyển
  tiếp các bản tin broadcast là **DHCP relay agent**.

- Thiết bị này thông thường là router lắng nghe DHCP client và relay
  chúng tới DHCP server. Server gửi bản tin reply lại cho client tới
  DHCP relay agent và nó sẽ gửi bản tin đó lại cho client

<https://reintech.io/blog/configure-dhcp-relay-agent-ubuntu-2004>

https://viblo.asia/p/cau-hinh-dhcp-tren-centos-7-gDVK2a4A5Lj
