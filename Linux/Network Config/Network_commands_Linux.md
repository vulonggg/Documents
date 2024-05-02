1.  **Lệnh ifconfig, ifup, ifdown**

- Lệnh ifconfig dùng để Xem IP của card mạng cụ thể, tham số -a để xem
  thông tin của toàn bộ các card mạng. Tương tự, ip a

- Lệnh ifconfig dùng để cấu hình địa chỉ IP, netmask, địa chỉ broadcast
  và các tham số cấu hình khác. Ifconfig eth\[n\] netmask 

- Systemctl restart network

\# Yum install network-scripts \#cài đặt gói quản lí network

\# Yum install net-tools

- Lệnh ifup dùng để enable một interface. ifup

- Lệnh ifdown dùng để disable một interface. ifdown

**sudo ip link set dev eth1 up/dơn**

**ip -s link**

**ip route list**

<img src="media/image1.png" style="width:6.04598in;height:3.88403in"
alt="image" />

2.  **LệnhIP **<img src="media/image2.png" style="width:6.5in;height:1.54028in"
    alt="image" />

> **sudo ip link set dev eth1 up/down**
>
> **ip –s link**
>
> **ip route list**
>
> **ip addr list = ip a**
>
> **ip a add 192.168.1.150/255.255.255.0 dev eth1**

**ip route add \<IP/netmask\> dev**

3.  **Lệnh Route**

- Routing:

> o If source and destination hosts are on the same physical network,
> the trafic is forwarded to the destinantion directly.
>
> o If source and destination hosts are not on the same physical
> network, then all defined routes in the routing tables are tried.
>
> o If a proper route is not found, then the packet is sent to the
> default gateway.

- Routing Table: Show thông tin của

> o Destination hosts
>
> o Device
>
> o Protocol
>
> o Scope
>
> o Source address
>
> o Metric

- Lệnh route dùng để hiển thị, chỉnh sửa, quản lý bảng routing table.

- Lệnh route cho phép định nghĩa các static route theo ý của người quản
  trị.

- Static route là những routing ít thay đổi, không phải cập nhật thường
  xuyên, được định nghĩa vì một mục đích nào đó.

- Lệnh route cũng cho phép người quản trị điều chỉnh default gateway
  theo ý muốn.

> \#Xem routing table
>
> route -n  
> netstat -rn
>
> Ip route list

Thêm/Xóa route

> \#route add/del -net netmask gw dev

Thêm/Xóa default gateway cho một địa chỉ

> \#route add/del default gw

4.  **Lệnh Troubleshoot**

- Lệnh **ping**: kiểm tra kêt nối giữa 2 máy tính \#ping -c n ping n lần
  \#ping -t ping nonstop

- Lệnh **netstat**: để liệt kê các port đang lắng nghe, các kết nối đang
  mở đến máy tính, và tình trạng của các kết nối này.

> \#netstat -rn xem routing table
>
> \#netstat -ano kiểm tra các port đang mở
>
> \#netstat -i kiểm tra card mạng
>
> \#netstat -l \| grep 
>
> \#netstat -s
>
> \#netstat -

- Lệnh **traceroute**: để theo dõi đường đi của gói tin trong hệ thống
  mạng. Lệnh traceroute thường dùng để debug, xác định vì sao gói tin
  không di chuyển đến một network được. \#traceroute

- Lệnh **tcpdump**: để bắt gói tin di chuyển trong network. Có thể lưu
  lại thành file, dùng ethereal để phân tích gói tin, xác định loại
  traffic, hoặc tìm kiếm các dấu hiệu mong muốn.

Ping

Putty: \#tcpdump -i -n icmp(protocol)

- Lệnh **ss**: same as netstat but faster o ss –lp o ss –t -a

- Lệnh **telnet**: remote access vào terminal của 1 máy tính thông qua 1
  port nào đó

- Lệnh **arp**: resolving IP address to MAC address, to see ARP cache.
  Each network device contains a cache of known MAC and IP address
  mappings. This cache is called ARP cache.

<img src="media/image3.png" style="width:6.73958in;height:4.09349in"
alt="image" />

<img src="media/image4.png" style="width:6.89885in;height:3.84375in"
alt="image" />

**Arp** là viết tắt của “Giao thức phân giải địa chỉ”, giao tiếp với
mạng IPv4 và phân giải địa chỉ IP của bất kỳ máy nào khác thành địa chỉ
vật lý được gọi là địa chỉ MAC (Kiểm soát truy cập phương tiện). Lệnh
arp là một trong những công cụ mạng chuyển đổi địa chỉ IP của bất kỳ máy
nào thành địa chỉ MAC của nó

- Lệnh nmap Scanning
  opening <https://linuxhint.com/scan-all-ports-nmap/>

- Lệnh ethtool - check network transmitting speed ethtool \| grep speed

<https://www.baeldung.com/linux/using-ethtool>
