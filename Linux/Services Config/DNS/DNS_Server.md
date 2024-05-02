**DNS Server**

1.  **Giới thiệu về DNS (Domain Name Server)**

> <img src="media/image1.png" style="width:3.40023in;height:3.21571in" />

1.  **KHÁI NIỆM VỀ DNS**

- DNS là viết tắt của từ Domain Name System (hệ thống tên miền).

- DNS có chức năng dịch một tên sang địa chỉ IP để các máy tính sử dụng
  nhận dạng trên hệ thống mạng và định vị và xác định các dịch vụ và
  thiết bị máy tính và ngược lại.

  1.  **PHÂN LOẠI DNS**

- **Primary DNS Server (PDS):** là nguồn xác thực thông tin chính thức
  cho các tên miền mà nó được phép quản lý. Thông tin về một tên miền do
  PDS được phân cấp quản lý thì được lưu trữ tại đây và sau đó có thể
  được chuyển sang các Secondary DNS Server (SDS).

- **Secondary DNS Server (SDS)**: quản lý các zone và SDS được sử dụng
  để lưu trữ dự phòng cho zone. SDS được phép quản lý tên miền nhưng dữ
  liệu về tên miền không phải được tạo ra từ SDS mà được lấy về từ PDS.

- **Caching DNS (CDS)** : là một server đệm. Khi một quá trình phân giả
  itên miền được truy vấn một lần nó sẽ lưu lại vào server này và khi
  truy vấn lần thứ 2 thì server này sẽ có chức năng tăng tốc độ truy vấn
  giảm độ trễ trên mạng và giảm đi công việc của SDS.

- **Forwarding DNS** : Là server chuyển tiếp nhiệm vụ cho server khác
  làm việc rồi lưu kết quả về bộ nhớ local.

  1.  **CẤU TRÚC DNS**

> <img src="media/image2.png" style="width:4.58723in;height:2.28726in" />

- Cấu trúc DNS là mô hình cấu trúc phân cấp hình cây:

  - **root DNS**: là đỉnh của cấu trúc này và sau đó các miền (domain)
    được phân nhánh dần xuống dưới và phân quyền quản lý. Mọi tên miền
    đều phải thông qua root DNS.

  - Các máy chủ **TLD** (ccTLD và gTLD): được vận hành bởi nhiều cơ quan
    và tổ chức (theo một bộ thỏa thuận khá phức tạp) được gọi là Nhà
    đăng ký tên miền. Có hai loại TLD được điều hành bởi Internet
    Corporation for Assigned Names and Numbers (ICANN)

    - ccTLD : Là tên miền thuộc quyền quản lý của một quốc gia. Mỗi quốc
      gia sẽ có một tên miền khác nhau

    - gTLD : là tên miền chung không thuộc bất kì một quốc gia nào.

  - **DNS user** là DNS local: do người dùng tạo ra và sử dụng cho local

> <img src="media/image3.png" style="width:5.17583in;height:2.31317in" />

- Cấu trúc **URL**:

> <img src="media/image4.png" style="width:3.95398in;height:1.62954in" />

1.  **ZONE VÀ ZONE FILE**

- **Zone** là nơi chứa các bản ghi tài nguyên mô tả domain hoặc
  subdomain. Được dùng để ánh xạ một tên miền thành một địa chỉ IP Zone
  được chia nhỏ ra và phân quyền cho các DNS server khác khi quản lý

> <img src="media/image5.png" style="width:5.47587in;height:2.69517in" />

- **Zone file**: Là một khu tập tin được lưu trữ trên một máy chủ tên
  miền và cung cấp thông tin về một hoặc nhiều tên miền. Mỗi khu tập tin
  chứa một danh sách các bản ghi DNS với ánh xạ giữa tên miền và địa chỉ
  IP:

> <img src="media/image6.png" style="width:5.06024in;height:2.50405in" />

- Bản ghi **SOA**: Trong mỗi tập tin cơ sở dữ liệu DNS phải có một và
  chỉ một record SOA (Start of Authority). Bao gồm các thông tin về
  domain trên DNS Server, thông tin về zone transfer.

> <img src="media/image7.png" style="width:4.51114in;height:1.17189in" />

- Bản ghi **NS**: Mỗi name server cho zone sẽ có một NS record. Chứa địa
  chỉ IP của DNS Server cùng với các thông tin về domain đó.

> <img src="media/image8.png" style="width:4.84892in;height:0.34754in" />

- Bản ghi **A**: Dùng để ánh xạ từ một domain thành địa chỉ IP cho phép
  có thể truy cập website. Record A có dạng như sau.

- Bản ghi **AAAA**: Có nhiệm vụ tương tự như bản ghi A, nhưng thay vì
  địa chỉ IPv4 sẽ là địa chỉ IPv6.

> <img src="media/image9.png" style="width:4.48985in;height:1.06887in" />

- Bản ghi **CNAME**: Cho phép tên miền có nhiều bí danh khác nhau, khi
  truy cập các bí danh sẽ cũng về một địa chỉ tên miền. Để sử dụng bản
  ghi CNAME cần khai báo bản ghi A trước.

> <img src="media/image10.png" style="width:4.57144in;height:0.6072in" />

- Bản ghi **PTR**: Hệ thống tên miền thông thường cho phép chuyển đổi từ
  tên miền sang địa chỉ IP. Trong thực tế, một số dịch vụ Internet đòi
  hỏi hệ thống máy chủ DNS phải có chức năng chuyển đổi từ địa chỉ IP
  sang tên miền.

> <img src="media/image11.png" style="width:4.45109in;height:0.58924in" />

- Bản ghi **MX**: Bản ghi MX dùng để khai báo trạm chuyển tiếp thư điện
  tử của một tên miền.

> <img src="media/image12.png" style="width:4.45459in;height:0.5272in" />

- Bản ghi **TXT**: Bản ghi TXT(text) được sử dụng để cung cấp khả năng
  liên kết văn bản tùy ý với máy chủ. Chủ yếu dùng trong mục đích xác
  thực máy chủ với tên miền.

2.  **HOẠT ĐỘNG CỦA DỊCH VỤ DNS**

- xử lí request của DNS không hỗ trợ mode **interactive**:

> <img src="media/image13.png" style="width:4.52367in;height:1.75194in" />

- Chi tiết xử lí request của DNS hỗ trợ mode **recursive**:

> <img src="media/image14.png" style="width:4.63518in;height:2.15097in" />
>
> <img src="/media/image1c.png" style="width:5in;height:2.69792in" />
>
> <img src="/media/image1d.png" style="width:5in;height:2.21875in" />
>
> <img src="/media/image1e.png" style="width:5in;height:1.70833in" />
>
> <img src="/media/image1f.png" style="width:5in;height:1.70833in" />
>
> <img src="/media/image20.png" style="width:5in;height:1.27083in" />

3.  **CÀI ĐẶT DNS SERVER**

> Cài đặt gói **BIND9** bằng RPM hoặc source, Yum:

- **bind-9.x:** là package chính của DNS Server, cung cấp file cấu hình
  dịch vụ, file script để cài đặt hệ thống DNS.

- **bind-libs-x:** cung cấp các thư viện trợ giúp cho DNS Server.

- **bind-utils-x:** cung cấp các tiện ích tích hợp cho DNS Server.

- **bind-chroot-x:** là package cung cấp một số tính năng bảo mật mới để
  giới hạn truy xuất file cấu hình của dịch vụ DNS.

> **File cấu hình** chính của DNS:

<img src="media/image15.png" style="width:5.66191in;height:1.81392in" />

4.  **ZONE TRANSFER**

- Để đề phòng rủi do khi DNS Primary gặp sự cố người ta dùng hơn một DNS
  Server để quản lý Zone. Do vậy phải có cơ chế đồng bộ, chuyển giao dữ
  liệu các Zone giữa các DNS server với nhau, có hai cách đồng bộ:

  - Truyền toàn bộ Zone (All zone transfer)

  - Truyền phần thay đổi (Incremental zone transfer).

- Việc DNS secondary server duy trì dữ liệu của server chính trên nó
  được gọi là **zone maintainance** và Quá trình sao chép dữ liệu này
  được gọi là **zone transfer**.

- Zone transfer xảy ra khi:

  - Khi quá trình làm mới của một Zone kết thúc (refresh expire)

  - Khi secondary được thông báo zone đã thay đổi tại nguồn quản lý của
    zone.

  - Khi thêm mới DNS Secondary

  - Tại DNS Secondary yêu cầu chuyển zone

- PHƯƠNG PHÁP **ĐỒNG BỘ** DNS SERVER

> <img src="media/image16.png" style="width:4.72764in;height:2.86943in" />

- Full zone transfer (**AXFR**):

  - Là sẽ transfer toàn bộ thông tin cơ sở dữ liệu của dns server chính
    về cho server phụ.

  - Được thực hiện thông qua việc kiểm tra serial number của SOA
    Resource Record, nếu serial number của server chính lớn hơn (mới
    hơn) thì server phụ sẽ yêu cầu server chính gửi toàn bộ thông tin về
    zone cho nó.

  - Thời gian các server phụ kiểm tra xem đã có sự thay đổi hay chưa đc
    định nghĩa bởi giá trị refresh của SOA RR.

  - AFXR hoạt động trên TCP port 53.

- Incremental zone transfer (**IXFR**):

  - Full zone transfer bộc lộ một điểm yếu là nếu chỉ có 1 RR thay đổi
    thì việc full zone transfer là gây lãng phí cả về băng thông mạng và
    tốn nhiều thời gian.

  - RFC 1995 đã đưa ra một giao thức cho phép chỉ transhfer những RR có
    sự thay đổi.

  - Slave dns server gửi request đến master dns server mỗi lần hết giá
    trị refresh. Nếu serial number của SOA RR là mới hơn thì nó sẽ gửi
    yêu cầu xem có thể sử dụng IXFR hay không.

  - Nếu cả slave và master server đều hỗ trợ IXFR thì sẽ sử dụng cách
    này để transfer zones. Nếu thất bại sẽ sử dụng AXFR.

  - IXFR hoạt động trên TCP port 53.

- Thông điệp **NOTIFY**:

  - Giá trị refresh được định nghĩa trong SOA RR thường là vài giờ đồng
    hồ, nếu như có bất kỳ sự thay đổi nào từ master server thì slave
    server vẫn sẽ không biết được cho đến khi hết giá trị refresh đó.

  - RFC 1996 định nghĩa một cơ chế cho phép master server gửi một thông
    điệp NOTIFY đến các slave servers mỗi khi nó đc load hoặc đc cập
    nhật mới.

  - Thông điệp NOTIFY này sẽ chỉ ra rằng, đã có một sự thay đổi nào đó
    đối với các RR.

  - Các slave nhận đc thông điệp NOTIFY sẽ gửi đến master server yêu cầu
    kiểm tra SOA RR. Nếu serial number lớn hơn so với serial hiện tại,
    slave server sẽ đưa ra yêu cầu là AXFR hoặc IXFR.

> <img src="media/image17.png" style="width:4.45054in;height:3.03527in" />

5.  **DNS Secondary**

<img src="media/image18.png" style="width:4.70586in;height:3.12454in" />

- Cài đặt tương tự như DNS Server

- Cấu hình trong file **/etc/named.conf** và các zone files.

- DNS Secondary cũng có thể trở thành DNS Primary của một DNS khác.

<!-- -->

- Để DNS có thể hoạt động được ta cần thực hiện một số bước sau:

<!-- -->

- Cấu hình cho phép zone transfer trong file **/etc/named.conf** của DNS
  Primary \# allow-transfer {localhost; \<Secondary IP\>;}

- Cấu hình **zone file** bổ sung bản ghi NS của DNS Secondary trên
  server của DNS Primary.

- Cấu hình **zone** trong file **/etc/named.conf** của DNS Secondary
  (Slave)

- Thực hiện khởi động dịch vụ named hoặc dùng công cụ **rndc** để đồng
  bộ manual.

<!-- -->

- DNS Caching

> Cấu hình trong file **/etc/named.conf** và không có tạo bất cứ **zone
> files** nào.

6.  **Installation & Configuration**

> <img src="/media/image5b.png" style="width:5.18403in;height:1.4415in" />

1.  **Cài đặt BIND9**

- Trên server cài đặt gói **bind bind-utils**

> **\# yum install bind bind-utils**

- Khai báo zone trong tập tin /etc/named.conf. **\# vi /etc/named.conf**

Options {

Listen-on port 53 { \<DNS IP address\>; }

……..

Allow-query { \<Ip range\>; };

………..

Zone “\<zone_name\>” IN {

Type master;

File “\<forward_file_name\>”;

};

Zone “zone.in-addr.arpa” IN {

Type master;

File “\<reverse_file_name\>”;

};

- Khai báo resource record cho **zone thuận** và **zone ngược.**

> <img src="media/image20.png" style="width:4.52537in;height:2.19047in" />
>
> <img src="media/image21.png" style="width:4.51658in;height:1.86477in" />

- Khởi động dịch vụ named và mở firewall cho phép dịch vụ named

> \# systemctl start named
>
> \# firewall-cmd --add-service=dns --permanent
>
> \# firewall-cmd --reload

- Lệnh **named-checkconf named.conf** kiểm tra lỗi trên tập tin cấu hình
  zone.

> Lệnh **named-checkzone -d “zonename” zonefile.zone** để kiểm tra lỗi
> trong tập tin phân giải thuận.
>
> Lệnh **named-checkzone -d “reversezonename” zonefile.rev** kiểm tra
> lỗi trên file phân giải nghịch

- Cấu hình DNS Client. \# **vi /etc/resolv.conf**

- Kiểm tra hoạt động. \# **nslookup**

> **\# host \<web url\>**

- **DNS Slave**

<img src="media/image22.png" style="width:5.8913in;height:4.3004in" />

- Trên DNS Salve cài đặt gói **bind bind-utils**

> **\# yum install bind bind-utils**

- Khai báo zone trong tập tin **/etc/named.conf**

- Khai báo resource record cho zone **thuận** và zone **ngược** trên DNS
  Slave

> <img src="media/image23.png" style="width:4.45393in;height:2.52731in" />
>
> <img src="media/image24.png" style="width:4.78268in;height:2.27024in" />

- Khai báo cấu hình trong tập tin **/etc/named.conf** của DNS Master cho
  phép transfer xuống DNS Slave.

- Khởi động dịch vụ **named** và mở **firewall** cho phép dịch vụ named
  trên DNS Slave

> \# systemctl start named
>
> \# firewall-cmd --add-service=dns --permanent
>
> \# firewall-cmd --reload
>
> \# check cấu hình zone

- Cấu hình DNS client

- Kiểm tra hoạt động bằng **nslookup / dig / host**.

2.  **Securing DNS**

    1.  **BIND Version**

- Hạn chế hiển thị phiên bản phần mềm cài đặt của Bind trên DNS Server.

\# vi /etc/named.conf

\# dig txt chaos version.bind. @\<server_IP\>

1.  **Access Control List**

- Cấu hình **ACL**: Là danh sách các địa chỉ IP được thiết lập để có thể
  sử dụng trong các cấu hình: allow-notify, allow-query, allow-query-on,
  allow recursion, blackhole, allowtransfer, match-clients.

- ACL giúp cho người quản trị có thể kiểm soát và hạn chế truy cập không
  cần thiết đến DNS Server.

// Cấu hình ACL có tên "Block-ip"— Dùng để chặn các IP không cần thiết

acl block-ip {

0.0.0.0/8; 192.0.2.0/24; 224.0.0.0/3;

10.0.0.0/8; 172.16.0.0/12; 192.168.0.0/16;

};

// Cấu hình ACL nội bộ có tên pnh-nets.

acl pnh-nets { x.x.x.x/24; x.x.x.x/21; };

options {

...

blackhole { block-ip; };

...

};

zone "pnh.com.vn" {

type master;

file "pnh.com.vn.db";

allow-query { any; };

};

1.  **Hạn chế IP được phép query, recursion và transfer**

2.  **Hạn chế IP từng zone cụ thể**

acl "pnh-block-zone" { 10.10.10.20; };

zone "pnh.com.vn" {

type master;

file "pnh.com.vn.db";

masters { 192.169.16.10; };

allow-query { "pnh-block-zone"; };

};

3.  **Giới hạn nội dung truy vấn theo từng view riêng biệt**

acl block-ip {0.0.0.0/8;192.0.2.0/24;224.0.0.0/3;};

acl pnh-nets {10.10.10.0/24;192.168.0.0/16;};

options {

listen-on port 53 { 127.0.0.1;58.186.205.148;};

listen-on-v6 port 53 { ::1; };

directory "/var/named";

dump-file "/var/named/data/cache_dump.db";

statistics-file "/var/named/data/named_stats.txt";

memstatistics-file "/var/named/data/named_mem_stats.txt";

secroots-file "/var/named/data/named.secroots";

recursing-file "/var/named/data/named.recursing";

allow-query { localhost;pnh-nets;};

allow-transfer { 58.186.205.0/24; };

version "Khong biet version";

recursion yes;

dnssec-enable yes;

dnssec-validation yes;

managed-keys-directory "/var/named/dynamic";

pid-file "/run/named/named.pid";

session-keyfile "/run/named/session.key";

/\* https://fedoraproject.org/wiki/Changes/CryptoPolicy \*/

include "/etc/crypto-policies/back-ends/bind.config";

};

logging {

channel default_debug {

file "data/named.run";

severity dynamic;

};

};

view "internal" {

match-clients {

localhost;

10.10.10.0/24;

};

zone "." IN {

type hint;

file "named.ca";

};

zone "pnh.com.vn" IN {

type master;

file "pnh.com.vn.lan";

};

include "/etc/named.rfc1912.zones";

include "/etc/named.root.key";

};

view "external" {

match-clients { any; };

allow-query { any; };

recursion no;

zone "pnh.com.vn" IN {

type master;

file "pnh.com.vn.wan";

};

};

- Khai báo hai zone phục vụ cho hai view khác nhau là:
  **pnh.com.vn.lan** và **pnh.com.vn.wan.**

> <img src="media/image25.png" style="width:4.74561in;height:5.07771in" />

- Truy cập và lookup domain **www.pnh.com.vn** khi client ở view
  internal.

> <img src="media/image26.png" style="width:5.00806in;height:1.92157in" />

- Truy cập và lookup domain www.pnh.com.vn khi client ở view external:

> <img src="media/image27.png" style="width:5.1756in;height:2.13277in" />

1.  **Cấu hình logging**

logging {

channel "default_syslog" {

syslog local2;

severity debug;

};

channel secure_log {

file "bind/named.log";

severity debug;

print-time yes;

};

category default { default_syslog; };

category general { default_syslog; };

category security { secure_log; };

category config { default_syslog; };

category resolver { default_syslog; };

category xfer-in { secure_log; };

category xfer-out { secure_log; };

category client { secure_log; };

category network { secure_log; };

category queries { secure_log; };

category lame-servers { default_syslog; };

}; //Lưu ý cấu hình ngoài option

2.  **Cấu hình rndc key**

> Cấu hình chương trình **rndc** để quản trị máy chủ DNS Server và sử
> dụng phương pháp xác thực chia sẻ khóa bí mật để cấp quyền cho các
> host được phép truy cập và ngăn chặn các máy chủ không được phép.
>
> Thực thi lệnh **rndc-confgen** linux để tạo rndc-key và các bản sao
> cấu hình thích hợp cho các dịch vụ Bind và RNDC.
>
> \# rndc-confgen

\# Start of rndc.conf

key "rndc-key" {

algorithm hmac-sha256;

secret "EhYB+7tIx9qC4jN3OdQ0RRgTf3/KEAVLhtO1cURR3os=";- };

options {

default-key "rndc-key";

default-server 127.0.0.1;

default-port 953;

};

\# End of rndc.conf

\# Use with the following in named.conf, adjusting the allow list as
needed:

\# key "rndc-key" {

\# algorithm hmac-sha256;

\# secret "EhYB+7tIx9qC4jN3OdQ0RRgTf3/KEAVLhtO1cURR3os=";

\# };

\#

\# controls {

\# inet 127.0.0.1 port 953

\# allow { 127.0.0.1; } keys { "rndc-key"; };

\# };

\# End of named.conf

- Chèn đoạn cấu hình RNDC đã tạo trước đó vào tệp **/etc/rndc.key**, mỗi
  máy chủ sẽ có một mã rndc key khác nhau.

key "rndc-key" {

algorithm hmac-sha256;

secret "EhYB+7tIx9qC4jN3OdQ0RRgTf3/KEAVLhtO1cURR3os=";

};

- Cấu hình trong file **/etc/named.conf**

include "/etc/rndc.key";

controls {

inet 127.0.0.1 port 953

allow { 127.0.0.1; } keys { "rndc-key"; };

};

- Khởi động lại dịch vụ **Bind**

  1.  Khởi tạo môi trường **Chroot** cho dịch vụ **Named**

Chroot là một công đoạn thay đổi thư mục root cho các tiến trình đang
chạy hiện tại và các tiến trình con của nó.

Mục đích tách biệt chương trình named ra khỏi hệ thống filesystem để đảm
bảo an toàn khi dịch vụ named bị tấn công.

**\# yum install bind-chroot**

- Thực hiện kiểm tra dịch vụ named xem có lỗi gì không, sau đó tạm thời
  stop và disable.

systemctl status named

systemctl stop named

systemctl disable named

- Khởi tạo môi trường **/var/names/chroot** bằng cách chạy:

/usr/libexec/setup-named-chroot.sh /var/named/chroot on

systemctl stop named

systemctl disable named

systemctl start named-chroot

systemctl enable named-chroot

- Kiểm tra lại môi trường chroot sau khi cài đặt

\# cd /var/named/chroot/

\# cd var/named/

\# cd /var/named/chroot/etc/

> **Configure a caching-only DNS Server**
>
> \# vi /etc/named.conf
>
> listen-on port 53 { any; };
>
> allow-query { any; };
>
> dnssec-enable no;
>
> dnssec-validation no;
>
> \#named-checkconf
>
> \#systemctl restart named
>
> \#firewall-cmd –permanent –add-service dns
>
> \#firewall-cmd –reload
>
> \#vi /etc/resolv.conf
>
> nameserver \<IP address\>

- Type of name servers

1.  Caching NS

- Called resolver, to look things up, remembers answers to queries,
  answers without looking them up again.

- It takes a relatively long time to query remote name servers compared
  to calling up something from a local cache.

- Speed up, when name server handles the DNS queries for an entire LAN,
  the savings can add up to a significant amount of time saved.

- Furthermore, if the DNS queries are being handled by caching NS,
  serving the LAN, then it reduces the amount of outbound network
  traffic as many queries will be answered before leaving the LAN.

- A caching name server is the type of name server that is most often
  put in the /etc/resolv.conf file.

<img src="/media/image21.png" style="width:5in;height:2.67708in" />

<img src="/media/image22.png" style="width:5in;height:1.33333in" />

- Modify the file /etc/named.conf

<img src="/media/image23.png" style="width:5in;height:2.55208in" />

- First item is the line “recursion yes”, this configures the name
  server to do recursive DNS queries as well as enable caching.

- Next item is setting up the .zone file that provides data to Bind on
  where to locate the internet’s root name servers. This will allow the
  resolution of top-level domains, and any query can be handled from
  there.

- If your name server will be accessible via public interface, you may
  employ access control list. First define the ACL at the top of the
  file, we will name this ACL internals and provide 2 networks as being
  allowed to query the NS. Next step is to add allow recursive,
  internals, and you save this file, and you are done.

2.  Forwarding NS

- Also called PROXY server.

<img src="/media/image24.png" style="width:5in;height:2.32292in" />

- Use cases

  - When you have outsourced your DNS service to a third party. Some
    third-party providers are Google Public DNS and OpenDNS.

  - A forwarding name server is set up to provide the benefit of
    caching, while leaving the actual DNS querying to remote name
    servers provided by the third party. Makes the configuration of a
    LAN easier.

  - Set the resolvers for each node on the LAN to the forwarding name
    server, and you set the forwarders on the forwarding name server to
    that of the third party.

  - If one’s DNS provider changes, only the configuration of the
    forwarding name server needs to be changed.

<img src="/media/image26.png" style="width:5in;height:2.38542in" />

- /etc/named.conf

Recursion no;

Forward only;

Forwarders { 8.8.8.8; 8.8.4.4; };

<img src="/media/image27.png" style="width:5in;height:1.09375in" />

<img src="/media/image28.png" style="width:5in;height:2.58333in" />

<img src="/media/image29.png" style="width:5in;height:1.33333in" />

View “external”

<img src="/media/image2a.png" style="width:5in;height:1.25in" />

<img src="/media/image2b.png" style="width:5in;height:2.39583in" />

<img src="/media/image34.png" style="width:5in;height:2.17708in" />

- Biggest downside is that you are exposing everything to the outside
  world, and providing a target for hackers and that is your single DNS
  server inside your firewall.

<img src="/media/image35.png" style="width:5in;height:2.48958in" />

- Internal clients are connected to a DNS named server behind your
  firewall. Everybody in the public Internet get access to that named
  server by port forwarding port 53.

<img src="/media/image36.png" style="width:5in;height:2.33333in" />

- None of the people in the public Internet are going to be interacting
  with anything inside your firewall at any time. If the outside named
  server is hacked, there’s no vulnerability into the internal network

- Have to update both the records in the private DNS and the public DNS
  when things change.

<img src="/media/image2f.png" style="width:5in;height:2.64583in" />

<img src="/media/image30.png" style="width:5in;height:2.05208in" />

<img src="/media/image37.png" style="width:5in;height:2.33333in" />

- A server that serves a single purpose and sits on both the internal
  and external networks. Both internal and external networks are treated
  in the same fashion. If a query comes in from outside, get the same
  result as if a query comes from the inside.

- Popular set up when most of infrastructure is outsourced to third
  parties.

- If you have your website hosted externally, email hosted externally,
  maybe vendors and suppliers are external, using CNAMEs to point to
  them.

- No A records involved, you ‘re not describing your internal network.
  Much safer.

- Have a Bastion setting inside and outside the firewall

<img src="/media/image32.png" style="width:5in;height:2.16667in" />

<img src="/media/image38.png"
style="width:5.63542in;height:2.54768in" />

- Instead of having a single zone file serving up answers to both
  internal and external queries by using Vuse, you are able to have
  separate zone files and provide different answers to external and
  internal queries.

- Reduce hardware cost as you don’t need to have multiple named servers
  hosted both internally and externally.

1.  Which configuration setting enables caching? recursion yes;

2.  Which configuration setting determines which servers the queries are
    forwarded to? forwarders {8.8.8.8, 8.8.4.4};

3.  Authoritative-only servers will cache only one domain. FALSE

- Zone Configuration File

1.  Zone config files

- Zone files are plain text files that describe what is in a DNS zone.

- Zone file uses textual resource records that map domain names to IP
  addresses.

2.  \$TTL

- First entry in zone configuration file is usually the time to live or
  \$TTL record.

<img src="/media/image33.png" style="width:5in;height:2.67708in" />

<img src="/media/image39.png" style="width:5in;height:0.84375in" />

<img src="/media/image3a.png" style="width:5in;height:1.125in" />

- If change the IP address of a host in your zone, it may take a long
  time for your change to propagate.

<img src="/media/image3b.png"
style="width:4.58333in;height:0.67238in" />

- Full propagation of a change take less than one day. We can override
  this default value on any record in the zone.

<img src="/media/image3c.png" style="width:5in;height:2.21875in" />

<img src="/media/image3d.png" style="width:5in;height:1.73958in" />

3.  \$ORIGIN

<img src="/media/image3e.png" style="width:5in;height:0.66667in" />

- To clean up a zone file and make it easier to read.

<img src="/media/image3f.png" style="width:5in;height:2.375in" />

- Entries that end in a dot are called Fully Qualified Domain Names.

<img src="/media/image40.png" style="width:5in;height:0.79167in" />

4.  SOA (Start of Authority)

- Most important and the most complex

- Long and broken up over several lines to be more readable.

- Start with the name of the zone with @ sign, means to substitute the
  current value of \$ sign origin, which is usually given in the line
  before the SOA.

- Next is IN (internet), next is SOA, identify the start of authority
  record. Then the primary master name server for the zone (FQDN). Next
  is the administrative email address for the zone, recommend use
  hostmaster. Place the email address in the SOA line, only use dots, no
  @ signs. Next comes a serial number and several TTO values grouped
  inside a pair of parentheses. Serial number is yyyymmddss (ss is
  sequence number). This number is used during zone transfers to
  determine if a zone has been modified.

- Follow with several durations. First is the refresh value, this is
  duration of time between checks by slave name server to check with the
  master name server to see if a zone has been modified. Typical values
  are 24 hours or less.

- If the slave NS tries contacting a master NS to see if the zone has
  been updated, but it’s unable to contact the zone master server, it
  will wait in intervals of the next value: the retry interval.

- The slave NS will keep attempting to contact the master NS based on
  the entry interval. It will continue to do this until the next value
  is reached, which is the expiry value. This is the maximum duration to
  attempt to make a connection with the master NS.

- If the expiry value is reached, the slave NS will give up and stop
  responding to queries. Timing out and shutting down.

- Last duration is the negative response TTL. When a resolver requests
  to resolve a hostname, and the NS can’t resolve it. Because it doesn’t
  exist in the DB, it will receive an nxdomain error from the NS. The
  resolver will return its value for the duration of the nx value (0-3
  hours).

<img src="/media/image41.png"
style="width:5.47917in;height:2.89939in" />

5.  NS Record

- Defines the authoritative name servers, to state which server acts in
  the zone.

- That zone is a domain, Syntax is name, ttl, class, NS, name.

- First name can be explicitly stated but is most often taken from the
  name in the SOA record. Name of the zone.

- TTL is a standard for that record should chose to override the zone’s
  default.

- Class is almost always to be IN,

- Second name is the name of the name server. Almost always a FQDN with
  the dot at the end.

- No name is given at the front of the line, that is the @ sign, which
  resolves to the value of the \$ORIGIN. No TTL is provided, so default.

- A domain has more than one NS, anything beyond the first, serving as a
  backup server.

<img src="/media/image42.png" style="width:5in;height:0.67708in" />

6.  MX

<img src="/media/image43.png" style="width:5in;height:1.67708in" />

<img src="/media/image44.png" style="width:5in;height:0.66667in" />

- 10, 20 are the priorities. If 2 or more mail servers have the same
  priority, then one will be chosen at random.

- Mail servers need not be in the same zone. These days it is also very
  common for domain name registrars to offer email services when you use
  their domain hosting service.

- Another case when a MS record may point to a mail exchanger in a
  different domain. It’s true if your web hosting provider is your email
  provider.

- Other options are to get a hosted forwarding-only mail server. These 2
  are often offered by DNS service providers, and they will store your
  email if your local email server goes down.

7.  A record (Address Resource Records)

<img src="/media/image45.png" style="width:5in;height:1.61458in" />

<img src="/media/image46.png" style="width:5in;height:1.8125in" />

8.  CNAME

<img src="/media/image47.png" style="width:5in;height:1.71875in" />

- Implement some rudimentary fault talents and load balancing. CNAME
  resource records are also the type of resource records when you want
  hostnames from one domain to point to hostnames on a different domain.

<img src="/media/image48.png" style="width:5in;height:3.03125in" />

<img src="/media/image49.png" style="width:5in;height:2.34375in" />

- Creates a tangled nest of aliases that is difficult to keep track of
  when changes are required. Chaining CNAMEs would also cause avoidable
  delays due to a few issues.

- First of all, each CNAME record must be looked up. That puts
  additional strain on the Name server.

- Secondly, each CNAME record is returned in the answer to the query. If
  there are too many CNAMEs, the answer may be larger than a single 512
  byte transaction causing increased delays and network traffic.

1.  PTR (Pointer) Resource Record

<img src="/media/image4a.png" style="width:5in;height:2.52083in" />

<img src="/media/image4b.png" style="width:5in;height:1.97917in" />

10.9.8.3 =\> ns1.example.com

9.  Other resources

<img src="/media/image4c.png" style="width:5in;height:1.01042in" />

<img src="/media/image4d.png" style="width:5in;height:1.13542in" />

<img src="/media/image4e.png" style="width:5in;height:1.47917in" />

- What does TTL stands for? Time To Live

- \$ORIGIN is always followed by an amount in seconds? FALSE

- Which is true for an SOA record?

  - An SOA record includes a serial number.

  - An SOA record can be spread among several lines in the file.

  - An SOA record includes an email address.

<!-- -->

- Which is true for an NS record? It points to an authoritative name
  server.

- Which is included in an MX record?

  - \$ORIGIN

  - Hostname

  - Priority

- Which is true for an A record?

  - host name

  - TTL

  - IPv4 address

<!-- -->

- What is true about CNAME records?

  - CNAME records are like aliases.

  - Like A records, CNAME records contain a TTL.

  - A zone file can have multiple CNAME records.

<!-- -->

- PTR records will match an IP address with a hostname.

<!-- -->

- Basic Name Server Setup

1.  Get Ready

<img src="/media/image4f.png" style="width:5in;height:2.26042in" />

2.  Create and verify the zone file for the new domain or zone

> \# vi tinjaw.site.internal.zone

\$ORIGIN mysite.com

\$TTL 3M

@ IN SOA ns1.tinjaw.site. hostmaster.tinjaw.site.

> 2016102501 3M 3M 3M 3M
>
> IN NS ns1.tinjaw.site.
>
> ns1 IN A 192.168.0.100
>
> \# vi /etc/named.conf // create Zones
>
> Zone “tinjaw.site” IN {
>
> Type master;
>
> File “tinjaw.site.internal.zone”;
>
> };
>
> \# named-checkconf /etc/named.conf //check if zone config is right or
> not
>
> \# named-checkconf –p /etc/named.conf //print out the standardized
> format of the conf
>
> \# named-checkzone tinjaw.site tinjaw.site.internal.zone

3.  Load and test the zone file

\# cp tịnaw.site.internal.zone /var/named

\# systemctl restart named

\# dig ns1.tinjaw.site

4.  Allow queries from localnets

\# less /etc/named.conf.new

View “localhost_resolver” // match-clients as a keyword, and then we
provide a list of the addresses we want to accept in this view. Only
going to accept from localhost. Continue to have our recursion, have
caching. Got our root zone, got our rfc1912 zones. So, this is serving
up basically what we were serving up before, but only to localhost.

{

match-clients { localhost; };

> Recursion yes;
>
> Zone “.” IN {
>
> Type hint;
>
> File “/var/named/named.ca”;
>
> };
>
> Include “/etc/named.rfc1912.zones”;
>
> };
>
> View “internal” // for internal networks, include all of the local
> networks, including any IP addresses on any network to which the local
> system is connected. Continue to use recursion, because internally,
> still want it to do caching. Not only are we allowing the packets in,
> based on the match.clients, but we’re also allowing queries from
> localnets. Included our root zone.
>
> {
>
> Match-clients { localnets; };
>
> Recursion yes;
>
> Allow-query { localnets; };
>
> Zone “.” IN {
>
> Type hint;
>
> File “/var/named/named.ca”;
>
> };
>
> Include “/etc/named.rfc1912.zones”;
>
> Zone “tinjaw.site” IN {
>
> Type master;
>
> File “tinjaw.site.internal.zone”;
>
> };
>
> \# cp named.conf.new /etc/named.conf
>
> \# systemctl restart named
>
> \# dig @192.168.0.100 ns1.tinjaw.site

5.  Reverse Zone file

\# vi 0.168.192.in-addr.arpa.rev.zone

\$ORIGIN 0.168.192.in-addr.arpa.

\$TTL 3M

@ IN SOA ns1.tinjaw.site. hostmaster.tinjaw.site. 2016102501

> 3M 3M 3M 3M

IN NS ns1.tinjaw.site.

100 IN PTR ns1.tinjaw.site.

2 IN PTR client.tinjaw.site.

\# vi /etc/named.conf

Zone “0.168.192.in-addr.arpa.” IN {

type master;

file “0.168.192.in-addr.arpa.rev.zone”;

};

\# cp 0.168.192.in-addr.arpa.rev.zone /var/named/

\# systemctl restart named

\# dig @192.168.0.100 -x 192.168.0.2

6.  External zone

\# cp tinjaw.site.internal.zone tinjaw.site.external.zone

\# vi tinjaw.site.external.zone

\$ORIGIN tinjaw.site.

\$TTL 3M

@ IN SOA ns1.tinjaw.site. hostmaster.tinjaw.site. 2016102501

> 3M 3M 3M 3M

IN NS ns1.tinjaw.site.

ns1 IN A 72.215.187.245 (external IP address)

- The IP address you’re looking for is the external IP address that will
  be forwarded to your name server.

\# vi /etc/named.conf

View “external”

{

match-clients { any; };

recursion no;

allow-query { any; };

zone “.” IN {

type hint;

file “/var/named/named.ca”

};

> Include “/etc/named.rfc1912.zones”;
>
> Zone “tinjaw.site” IN {
>
> Type master;
>
> File “tinjaw.site.external.zone”;
>
> };
>
> \# cp tinjaw.site.external.zone /var/named
>
> \# systemctl restart named
>
> \# dig @72.215.187.245 ns1.tinjaw.site

- The only way to verify a zone file is by restarting the BIND server.
  FALSE

- Which utility can be used to test a zone file? dig

- What feature allows for various levels of access? Views

- What type of resource records do reverse zone files contain? PTR

<!-- -->

- Advanced Name Server Setup

1.  Configure a Secondary NS

- Being redundant is not only acceptable but expected

- Geographical Redundancy: Operating a system at more than one
  geographical location

<img src="/media/image50.png" style="width:5in;height:1.59375in" />

\# vi /etc/named.conf

Zone “tinjaw.site.” IN {

type master;

file “tinjaw.site.external.zone”;

allow-transfer {

173.244.206.26; \# a.transfer.buddyns.com

88.198.106.11; \# b.transfer.buddyns.com

};

};

\# vi /var/named/tinjaw.site.external.zone

\$ORIGIN tinjaw.site.

\$TTL 3M

@ IN SOA ns1.tinjaw.site. hostmaster.tinjaw.site. 2016102502

> 3M 3M 3M 3M
>
> IN NS ns1.tinjaw.site.
>
> IN NS d.ns.buddyns.com.

\# vi /var/named/tinjaw.site.external.zone

2.  Register a NS

- Commonly known as setting glue records

- Primary, and at least one secondary

<img src="/media/image51.png"
style="width:4.57292in;height:1.67674in" />

3.  Updating a Zone

\# vi /etc/named.conf

Zone “tinjaw.site.” IN {

type master;

file “tinjaw.site.external.zone”;

allow-transfer {

173.244.206.26; \# a.transfer.buddyns.com

88.198.106.11; \# b.transfer.buddyns.com

};

notify explicit;

also-notify { 0.0.0.0;};

};

4.  Serve a website

- Pointing to web servers

\# vi /var/named/tinjaw.site.external.zone

\$ORIGIN tinjaw.site.

\$TTL 3M

@ IN SOA ns1.tinjaw.site. hostmaster.tinjaw.site. 2016102502

> 3M 3M 3M 3M
>
> IN NS ns1.tinjaw.site.
>
> IN NS d.ns.buddyns.com.

ns1 IN A 72.215.187.245

www IN CNAME tinjawtk.000webhostapp.com.

www2 IN CNAME hamburgers.000webhostapp.com.

IN MX 10 mx.zoho.com.

IN MX 20 mx2.zoho.com.

- Which is not true for a secondary name server? It must be hosted on
  the same subnet as the primary master server.

  - It acts as a backup server for one or more primary name servers.

  - It will contain zone files

  - They can be hosted by third-party service providers.

- What is not needed to register a name server? PTR resource record

- Only one webserver can be included in a zone file. FALSE

- What is not needed to configure a third-party email server? a primary
  mail server hosted on-site

  - a registered domain

  - a means to verify that you control the domain

  - an MX record in the zone file

- SPF records are used to reduce spam emails. TRUE

<!-- -->

- Security

<img src="/media/image52.png" style="width:5in;height:1.52083in" />

<img src="/media/image53.png" style="width:5in;height:0.82292in" />

<img src="/media/image54.png" style="width:5in;height:2.02083in" />

\# mkdir /var/named/keys

\# cd /var/named/ keys/

\# dnssec-keygen –a hmac-md5 –b 128 –C –n host tinjaw.site

\# vi tinjaw.site.key

Key “tinjaw.site” {

algorithm hmac-md5;

secret “EUIUts/IPOREwDwFlfIGyw== “:

};

\# chown named:named tinjaw.site.key

\# chmod 0400 tinjaw.site.key

\# vi /etc/named.conf

Include “keys/tinjaw.site.key”;

<img src="/media/image55.png" style="width:5in;height:0.95833in" />

<img src="/media/image56.png" style="width:5in;height:1.98958in" />

<img src="/media/image57.png" style="width:5in;height:2.25in" />

<img src="/media/image58.png" style="width:5in;height:1.61458in" />

<img src="/media/image59.png" style="width:5in;height:1.9375in" />

<img src="/media/image5a.png" style="width:5in;height:1.36458in" />

- What is not true about TSIG? It required a private and a public key.

  - It needs to be securely distributed.

  - It uses a single shared secret.

  - It is used to secure message traffic between name servers.

<!-- -->

- By default, rndc only works on localhost. TRUE

- All domains require DNSSEC. FALSE
