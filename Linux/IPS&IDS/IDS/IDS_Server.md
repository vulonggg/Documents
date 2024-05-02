**IDS Server**

1.  **Giới thiệu về IDS và SNORT**

- IDS là hệ thống phát hiện xâm nhập (Intrusion Detection System) là một
  thiết bị hoặc ứng dụng phần mềm giám sát mạng hoặc hệ thống máy tính
  về những hoạt động ác ý hoặc các vi phạm chính sách.

- Các tính năng quan trọng nhất của IDS bao gồm: giám sát traffic mạng
  và các hoạt động khả nghi; đưa ra các cảnh báo về những điểm bất
  thường cho hệ thống và đơn vị quản trị mạng; kết hợp với tường lửa,
  phần mềm diệt virus tạo nên một hệ thống bảo mật hoàn chỉnh.

- Snort là một kiểu IDS/IPS, thực hiện giám sát các gói tin ra vào hệ
  thống với nhiều tính năng trong việc bảo vệ hệ thống bên trong, phát
  hiện sự tấn công từ bên ngoài vào hệ thống.

2.  **KIẾN TRÚC CỦA SNORT**

<img src="media/image1.png" style="width:6.82913in;height:3.55115in"
alt="Diagram Description automatically generated" />

- **Module Decoder**: Snort sử dụng thư viện pcap để bắt mọi gói tin
  trên mạng lưu thông qua hệ thống. Gói tin sau khi được giải mã sẽ đưa
  vào Module tiền xử lý.

- **Module Preprocessors**: Chuẩn bị dữ liệu cho hệ thống phân tích →
  phát hiện dữ liệu bất thường dựa vào header của gói tin → chống phân
  mảnh gói tin → giải mã HTTP URI → lắp ráp lại các gói (TCP, UDP ..)

  - Kết hợp lại các gói tin

  - Giải mã và chuẩn hóa giao thức (decode/normalize)

  - Phát hiện các xâm nhập bất thường (nonrule/anormal)

- **Module Detection Engine**: Đây là module quan trọng nhất của Snort.
  Nó chịu trách nhiệm phát hiện các dấu hiệu xâm nhập. Module sử dụng
  các luật (rule) được định nghĩa từ trước để so sánh với dữ liệu thu
  thập được, từ đó xác định xem có xâm nhập xảy ra hay không

- **Module log** và **cảnh báo**: Tùy thuộc vào module phát hiện
  (detection engine) có nhận dạng được xâm nhập hay ko mà gói tin có thể
  bị ghi log hay đưa ra cảnh báo. Các file log là các file dữ liệu có
  thể ghi dưới nhiều định dạng khác nhau như tcpdump, xml, syslog, log
  file.

3.  **HOẠT ĐỘNG CỦA SNORT**

- **Sniffer mode**: Ở chế độ này snort sẽ lắng nghe và đọc các gói tin
  trên mạng sau đó sẽ trình bày kết quả trên giao diện hiển thị.

- **Packet Logger mode**: lưu trữ các gói tin trong các tập tin log

- **Network instruction detect system (NIDS)**: Đây là chế dộ họat động
  mạnh mẽ và được áp dụng nhiều nhất, khi họat động ở NIDS mode, Snort
  sẽ phân tích các gói tin luân chuyển trên mạng và so sánh với các
  thông tin được định nghĩa của người dùng để từ đó có những hành động
  tương ứng như thông báo cho quản trị mạng khi xảy ra tình huống quét
  lỗi do các hacker attacker tiến hành hay cảnh báo virus…

- **Inline mode**: Khi triển khai snort trên linux thì chúng ta có thể
  cấu hình snort để phân tích các gói tin từ iptables thay vì libpcap do
  đó iptable có thể drop hoặc pass các gói tin theo snort rule.

<!-- -->

- Sniffer mode

  - Hiển thị thông tin header của packet: \#snort -v

  - Hiển thị thông tin ứng dụng đang phát sinh packet: \#snort –v -d

  - Header của tầng datalink: \#snort –vde

- Packet Logger Mode:

  - Hiển thị thông tin header của packet: \#snort -v

  - Lưu thông tin xuống file: \#snort –dev –l \[filename\]

  - Lưu thông tin ở dạng binary: \#snort –l \[filename\] -b

  - Đọc ngược thông tin từ file binary:

    - \#snort –dv –r \[filename\]

    - \#snort –dv –r \[filename\] icmp

- Network instruction detect system (NIDS): đây là chế dộ họat động mạnh
  mẽ và được áp dụng nhiều nhất

  - Bắt buộc phải chỉ ra file luật dùng để hoạt động (option -c)

> \#snort –u snort –g snort –D –c /etc/snort

- Mặc định của mode này là cảnh báo full alert và log lại packet theo
  dạng ASCII

<!-- -->

- Inline Mode

  - Biên dịch hỗ trợ inline mode:

    - ./configure –enable-inline

  - Có 3 loại luật được sử dụng ở mode inline:

    - **drop**: iptables sẽ bỏ qua packet và log lại sự kiện này.

    - **reject**: iptables sẽ bỏ qua packet, log lại sự kiện, và thông
      báo đến máy tính rằng packet này sẽ không đến nơi.

    - **sdrop**: iptables sẽ bỏ qua packet, không thông báo đến máy đích
      và cũng không log lại sự kiện.

> \# snort_inline –QDc ../etc/drop.conf –l /var/log/snort

4.  **CÀI ĐẶT SNORT SERVER**

- Có thể cài đặt gói Snort bằng yum hoặc rpm

> \# rpm –ivh snort \[version\].rpm
>
> \# yum –y install snort

- Hoặc có thể cài đặt NTP bằng gói source

> \# snort\[version\].tar.gz

- Snort server gồm những file sau trong hệ thống:

  - /etc/snort/snort.conf

  - classification.config, magic.conf, reference.config, threshold.conf

- **CẤU TRÚC BỘ LUẬT CỦA SNORT**

> <img src="media/image2.png" style="width:6.23958in;height:4.36458in"
> alt="Graphical user interface, text Description automatically generated with medium confidence" />

<img src="media/image3.png" style="width:6.5in;height:2.67569in"
alt="Text Description automatically generated" />

<img src="media/image4.png" style="width:6.17767in;height:3.07101in"
alt="Text Description automatically generated" />

<img src="media/image5.png" style="width:6.2536in;height:2.41325in"
alt="Text Description automatically generated" />

<img src="media/image6.png" style="width:5.99117in;height:2.95462in"
alt="Text, letter Description automatically generated" />

<img src="media/image7.png" style="width:6.5in;height:2.15972in" />

5.  **Install & Configure**

> <img src="media/image8.png" style="width:5.87182in;height:3.48106in"
> alt="Diagram Description automatically generated" />

- **Cài đặt các gói phần mềm bổ trợ**

<!-- -->

- pcap (libpcap-dev)

- PCRE (libpcre3-dev)

- Libdnet (libdumbnet-dev)

- DAQ (Data AcQuisition library) - \[root@lpi-pnh ~\]

\# rpm -qa \| grep gcc

\# yum install gcc

\# rpm -qa \| grep flex

\# yum install flex

\# rpm -qa \| grep bison

\# yum install bison

\# rpm -qa \| grep zlib

\# yum install zlib\*

\# rpm -qa \| grep libpcap

\# rpm -qa \| grep tcpdump

\# rpm -qa \| grep libdnet-devel

\# yum install libdnet-devel

\# yum install libpcap-devel

\# yum install libtirpc-devel

\# yum install pcre\*

\# yum install openssl\*

- **Tạo thư mục chứa mã nguồn Snort, DAQ và tải về các rules**

> \# mkdir -p /sources/snort
>
> \# cd /sources/snort
>
> \# wget -c <https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz> \#
> cài DAQ
>
> \# wget -c https://www.snort.org/downloads \# cài snort

- **Cài đặt Snort DAQ (Data AcQuisition library)**

> \# ls -l daq-2.0.7.tar.gz snort-2.9.19.tar.gz
>
> \# tar -xzvf daq-2.0.7.tar.gz
>
> \# cd daq-2.0.7
>
> \# autoreconf -f -i
>
> \# ./configure
>
> \# make && make install
>
> \# cd ..

- **Cài đặt libpcap**

> \# wget http://www.tcpdump.org/release/libpcap-1.8.1.tar.gz
>
> \# tar xzvf libpcap-1.8.1.tar.gz
>
> \# cd libpcap-1.8.1
>
> \# ./configure && make && make install
>
> \# yum install libpcap-devel -y
>
> \# cd ..

- **Cài đặt Luajit**

> \# wget http://luajit.org/download/LuaJIT-2.0.5.tar.gz
>
> \# tar xvzf LuaJIT-2.0.5.tar.gz
>
> \# cd LuaJIT-2.0.5/
>
> \# make && make install
>
> cd ..

- **Cài đặt Snort**

> \# tar -xzvf snort-2.9.19.tar.gz
>
> \# cd snort-2.9.19
>
> \# ./configure --enable-sourcefire
>
> \# make && make install
>
> \*\* Tham số **–enable-sourcefire** cho phép chúng ta enable tính năng
> **Packet Performance Monitoring (PPM)** cho phép chúng ta giám sát các
> rules và các pre-processors.

- **Cập nhật lại thư viện và chạy dịch vụ snort**

> \# ldconfig
>
> \# ln -s /usr/local/bin/snort /usr/sbin/snort
>
> \# snort -v
>
> \# groupadd snort
>
> \# useradd snort -r -s /sbin/nologin -c SNORT_IDS -g snort
>
> **\##Tạo thư mục và các file rules của snort**
>
> \# mkdir -p /etc/snort/{rules,preproc_rules}
>
> \# mkdir /var/log/snort
>
> \# mkdir /usr/local/lib/snort_dynamicrules
>
> \# chmod -R 5775 /etc/snort /var/log/snort
> /usr/local/lib/snort_dynamicrules
>
> \# chown -R snort:snort /var/log/snort
>
> \# chown -R snort:snort /usr/local/lib/snort_dynamicrules
>
> \# touch /etc/snort/rules/white_list.rules
>
> \# touch /etc/snort/rules/black_list.rules
>
> \# touch /etc/snort/rules/local.rules
>
> **\##Chép các file cấu hình và file map vào thư mục /etc/snort**
>
> \# cp /sources/snort/snort-2.9.19/etc/\*.conf\* /etc/snort/
>
> \# cp /sources/snort/snort-2.9.19/etc/\*.map /etc/snort/
>
> \# sed -i "s/include \\RULE\\PATH/#include \\RULE\\PATH/ "
> /etc/snort/snort.conf

\# vi /etc/snort/snort.conf

> **\##Khai bao cấu hình dòng 45, ta khai báo Internal network và các
> network được xem là External, các HTTP servers, DNS servers, danh sách
> các port**
>
> ipvar HOME_NET 58.186.205.0/24
>
> ipvar EXTERNAL_NET !\$HOME_NET
>
> **\###Khoảng dòng thứ 104, cấu hình đường dẫn của các file như sau**
>
> var RULE_PATH /etc/snort/rules
>
> var SO_RULE_PATH /etc/snort/so_rules
>
> var PREPROC_RULE_PATH /etc/snort/preproc_rules
>
> var WHITE_LIST_PATH /etc/snort/rules
>
> var BLACK_LIST_PATH /etc/snort/rules
>
> Khoảng dòng 546, bạn sẽ thấy một tập hợp khai báo các file rules, tuy
> nhiên đây là các sensor phải trả tiền để tải các rules này về nên
> trong bài lab này
>
> đánh dấu comment hết tất cả (gồm các dòng include \$RULE_PATH và cả
> \$PREPROC_RULE_PATH) và chỉ để lại dòng “include
> \$RULE_PATH/icmp.rules”.
>
> site specific rules
>
> include \$RULE_PATH/local.rules
>
> \# cp /etc/snort/snort.conf /etc/snort/snort.conf.backup
>
> \# xóa từng dòng include

- **Cấu hình rules icmp và kiểm tra file config**

> \# cd /sources/snort/snort-2.9.19
>
> \# vi /etc/snort/rules/icmp.rules
>
> alert icmp any any -\> \$HOME_NET any (msg:"ICMP test"; sid:10000001;
> rev:001;)
>
> \# snort -T -c /etc/snort/snort.conf
>
> \# snort -A console -c /etc/snort/snort.conf -i eth0
>
> <img src="media/image9.png" style="width:5.84777in;height:1.7737in" />
>
> \# snort -A console -q -u snort -g snort -c /etc/snort/snort.conf

6.  **Cấu hình tự động khởi động cùng hệ thống**

> \# vi /lib/systemd/system/snort.service
>
> \[Unit\]
>
> Description=Snort NIDS Daemon
>
> After=syslog.target network.target
>
> \[Service\]
>
> Type=simple
>
> ExecStart=/usr/local/bin/snort -q -u snort -g snort -c
> /etc/snort/snort.conf
>
> \[Install\]
>
> WantedBy=multi-user.target
>
> \# systemctl start snort
>
> \# systemctl enable snort

7.  **Cài đặt, cấu hình Barnyard2**

> Barnyard2 hỗ trợ việc xuất dữ liệu đầu ra của snort ra CSDL MySQL như
> vậy sẽ thuận tiện hơn cho việc lưu trữ hoặc xử lý nó
>
> Cài một số gói cần thiết
>
> \# yum install git unzip libtool mariadb-server -y
>
> Sửa dòng **521** trong file **/etc/snort/snort.conf** thành như sau để
> định dạng lại dữ liệu đầu ra của snort để dùng được Barnyard2
>
> output unified2: filename snort.log, limit 1024

- **Bắt đầu cài đặt**

> \# cd /sources/
>
> \# wget https://github.com/firnsy/barnyard2/archive/master.tar.gz -O
> barnyard2-Master.tar.gz
>
> \# tar -xzvf barnyard2-Master.tar.gz
>
> \# cd barnyard2-master/
>
> \# ./autogen.sh && ./configure --with-mysql
> --with-mysql-libraries=/usr/lib64/mysql &&
>
> \# make && make install
>
> \# cp -v etc/barnyard2.conf /etc/snort/

- **vi /etc/snort/barnyard2.conf**

> config logdir: /var/log/barnyard2
>
> config hostname: localhost
>
> config interface: ens33
>
> config waldo_file: /var/log/barnyard2/barnyard2.waldo

- **Tạo folder log cho Barnyard2**

> \# mkdir /var/log/barnyard2
>
> \# chmod 744 /var/log/barnyard2 && chown snort.snort
> /var/log/barnyard2
>
> \# touch /var/log/barnyard2/barnyard2.waldo && chown snort.snort
> /var/log/barnyard2/barnyard2.waldo

- **kiểm tra barnyard**

> \# cd /var/log/snort
>
> \# barnyard2 -c /etc/snort/barnyard2.conf -o snort.log

- **Cấu hình MySQL**

> \# systemctl start mariadb && systemctl enable mariadb
>
> \# mysql_secure_installation
>
> Thực hiện set password cho root và trả lời tất cả câu hỏi là Y

- **Kết nối MySQL và tạo DB**

> \# mysql -u root -p
>
> \# create database snort;
>
> \# grant all privileges on snort.\* to snort@'localhost' identified by
> '123456';
>
> \# grant all privileges on snort.\* to snort@'127.0.0.1' identified by
> '123456';
>
> \# flush privileges;
>
> \# exit

- **Tạo các bảng cho DB vừa tạo**

> \# cd /sources/barnyard2-master/schemas/
>
> mysql -u root -p snort \< create_mysql

- **Cấu hình cho Barnyard2 kết nối đến mysql**

> \# vi /etc/snort/barnyard2.conf
>
> \#Comment lại dòng 227
>
> \#output alert_fast: stdout
>
> \#Bỏ comment dòng 351 và khai báo thông tin mysql
>
> output database: log, mysql, user=snort password=123456 dbname=snort
>
> host=localhost
