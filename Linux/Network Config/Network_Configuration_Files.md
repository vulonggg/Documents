1.  **File /etc/hosts**

- Là bản map giữa địa chỉ IP và tên máy tính trong network.

- Tương tự file lmhosts của Windows.

- Cú pháp của file:

<img src="media/image1.png" style="width:6.5in;height:1.44236in"
alt="image" />

- Các ứng dụng trước tiên sẽ sử dụng file này khi cần truy vấn một máy
  tính bằng tên.

- Lệnh hostname: xem tên và đổi tên. Lưu ý: Sau khi cấu hình thực hiện
  reboot để hệ thống nhận hostname mới

2.  **File /etc/sysconfig/network**

- File /etc/sysconfig/network định nghĩa các cấu hình network cơ bản cho
  máy tính.

<img src="media/image2.png" style="width:6.5in;height:2.37986in"
alt="image" />

3.  **File /etc/sysconfig/network-scripts/ifcfg-eth\[n\]**

- Mỗi card mạng có một file cấu hình

- n: có giá trị bắt đầu từ 0.

- Card loopback có file cấu hình ifcfg-lo

<img src="media/image3.png" style="width:6.22917in;height:3.98958in"
alt="image" />

<img src="media/image4.png" style="width:6.26042in;height:2.59375in"
alt="image" />

4.  **File /etc/resolv.conf**

- File /etc/resolv.conf dùng để định nghĩa name server mà máy tính sẽ sử
  dụng để thực hiện các truy vấn phân giải tên miền.

- Một số cú pháp thông dụng: o domain: Queries short name sẽ ghép với
  domain này. o nameserver: IP hoặc tên của name server mà máy tính sẽ
  sử dụng. Có tối đa 3 giá trị. o search: default sẽ tìm trên domain nào

5.  **File /etc/services**

- File /etc/services gồm một danh sách network port và các service sử
  dụng những port này.

- Khi định nghĩa một service mới, người quản trị phải định nghĩa một cặp
  service name và port number vào file /etc/services. o Port 0 – 1024:
  là những port đã được dành riêng. o Port \> 1024: port được định nghĩa
  thêm vào tùy theo nhu cầu của ứng dụng.

<img src="media/image5.png" style="width:6.5in;height:1.17222in"
alt="image" />

6.  **File /etc/netplan/00-installer-config.yaml (ubuntu)**

network:

version: 2

renderer: networkd

ethernets:

en01:

addresses:

\- 192.168.1.25/24

\- "2001:1::1/64"

gateway4: 192.168.1.1

gateway6: "2001:1::2"

nameservers:

addresses:

\- 8.8.8.8

\- 8.8.4.4

sudo netplan apply

network:

version: 2

renderer: networkd

ethernets:

en01:

dhcp4: true

dhcp6: true

\*\*\*\*\*\*\*\*\*\*\*\*\* 2 network interfaces for 2 seperate netwoprks
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

network:

ethernets:

ens33:

dhcp4: true

ens34:

\#dhcp4: true

addresses:

\- 192.168.1.5/24

nameservers:

addresses:

\- 192.168.1.2

routes:

\- to: 192.168.1.0/24

via: 192.168.1.1

ens38:

\#dhcp4: true

addresses:

\- 192.168.50.5/24

routes:

\- to: 192.168.50.0/24

via: 192.168.50.1

version: 2
