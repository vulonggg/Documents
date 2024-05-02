**LDAP**

1.  **LDAP là gì**

- **LDAP** (Lightweight Directory Access Protocol) là  là một giao thức
  ứng dụng truy cập các cấu trúc thư mục. LDAP được dùng để tìm thông
  tin liên hệ từ 1 server. Được thiết kế trên giao thức
  Internet [TCP/IP](https://vietnix.vn/tcp-ip-la-gi/) và là chuẩn cho
  dịch vụ thư mục (Directory Service – DS) chạy trên nền tảng OSI.

- LDAP sử dụng gói tin overhead thấp, được xác định chính xác trên lớp
  TCP của danh sách giao thức TCP/IP còn X500 là hạng nặng vì thuộc lớp
  giao thức ứng dụng, chứa nhiều header hơn (các header của các layer
  tầng thấp hơn).

- LDAP chủ là một giao thức chứ không hỗ trợ xử lý như database. Nhưng
  nó cần một nơi để lưu
  trữ [backend](https://vietnix.vn/backend-va-frontend/) và xử lý dữ
  liệu. LDAP là một giao thức truy cập dạng client/server.

- LDAP là giao thức truy cập vì vậy nó theo mô hình dạng cây (Directory
  Information Tree).

> <img src="media/image1.png" style="width:4.96906in;height:3.43169in" />

2.  **Phương thức hoạt động của LDAP**

- LDAP hoạt động theo mô hình client-server. Một hoặc nhiều LDAP server
  chứa thông tin về cây thư mục (Directory Information Tree – DIT).

- Client kết nối đến server và gửi yêu cầu. Server phản hồi bằng chính
  nó hoặc trỏ tới LDAP server khác để client lấy thông tin.

- Trình tự khi có kết nối với LDAP:

  - **Connect** (Kết nối với LDAP): Client sẽ mở kết nối tới LDAP
    server.

  - **Bind** (kiểu kết nối – ẩn danh hoặc đăng nhập): Client gửi đi các
    thông tin xác thực.

  - **Search** (Tìm kiếm): Client gửi đi yêu cầu tìm kiếm.

  - **Interpert search** (xử lý tìm kiếm): Server thực hiện việc xử lý
    tìm kiếm.

  - **Result** (kết quả): Máy chủ phản hồi lại kết quả với Client.

  - **Unbind**: Client gửi đi yêu cầu đóng kết nối với server.

  - **Close connection** (đóng kết nối): Đóng kết nối từ server.

> <img src="media/image2.png" style="width:5.9811in;height:2.70535in" />

3.  **Database backend của LDAP**

- **Slapd** là một “LDAP directory server” có thể chạy trên nhiều
  platform khác nhau. Bạn có thể sử dụng nó để cung cấp những dịch vụ
  của riêng mình. Những tính năng mà slapd cung cấp:

  - LDAPv3: slapd hỗ trợ LDAP cả IPv4, IPv6 và Unix IPC.

  - Simple Authentication and Security Layer: Slapd hỗ trợ mạnh mẽ chứng
    thực và bảo mật dữ liệu dịch vụ bằng SASL.

  - Transport Layer Security: Slapd có hỗ trợ TLS và SSL.

- Hiện tại, SLAPD sử dụng BDB và HDB để lưu trữ các dữ liệu. Với BDB sử
  dụng Oracle Berkeley DB để lưu trữ các dữ liệu. Nó được đề nghị sử
  dụng làm database backend chính cho các SLAPD thông thường.

- HDB cũng giống với BDB, tuy nhiên nó sử dụng database phân cấp nên sẽ
  hỗ trợ cơ sở dữ liệu dạng cây. Với hiện nay thì HDB được mặc định cấu
  hình trong SLAPD.

4.  **Mô hình của LDAP**

LDAP được chia làm 4 mô hình sau:

- LDAP information: Xác định cấu trúc và đặc điểm của các thông tin
  trong thư mục.

- LDAP Naming: Xác định cách các thông tin được tham chiều và tổ chức.

- LDAP Functional: Định nghĩa cách mà các bạn truy cập và cập nhật thông
  tin trong thư mục của bạn.

- LDAP Security: Định nghĩa ra cách thông tin trong thư mục của bạn được
  bảo vệ để tránh các truy cập không được cho phép.

5.  **Lưu trữ thông tin của LDAP**

- LDIF (LDAP Data Interchange Format) là một chuẩn định dang file text
  lưu trữ thông tin cấu hình LDAP và nội dung thư mục. File LDIF thường
  dùng để import dữ liệu mới vào trong directory hoặc thay đổi dữ liệu
  đã có. Dữ liệu trong file LDIF phải tuân theo quy luật có trong schema
  của LDAP.

- Schema là loại dữ liệu được định nghĩa từ trước. Mọi thành phần được
  thêm vào hoặc thay đổi trong directory của bạn sẽ được kiểm tra lại
  trong schema để đảm bảo chính xác.

  1.  **Cấu trúc tập tin LDIF**

- Thông thường file LDIF sẽ có mẫu sau:

  - Mỗi tập entry khác nhau được phân cách bởi dòng trắng

  - “tên thuộc tính: giá trị”

  - Một tập chỉ dẫn cú pháp để làm sao xử lý thông tin

- Những yêu cầu khi khai báo LDIF:

  - Lời chú thích được gõ sau dấu \# trong 1 dòng

  - Thuộc tính được liệt kê bên trái dấu “:” và giá trị được biểu diễn
    bên phải.

  - Thuộc tính dn định nghĩa duy nhất cho một DN xác định trong entry
    đó.

  1.  **Entry**

- Một entry là tập hợp của các thuộc tính, từng thuộc tính này mô tả một
  nét đặt trưng tiêu biểu của một đối tượng. Một entry bao gồm nhiều
  dòng

  - **DN**: distinguished name - là tên của entry thư mục, tất cả được
    viết trên một dòng.

  - Sau đó lần lượt là các thuộc tính của entry, thuộc tính dùng để lưu
    giữ dữ liệu. Mỗi thuộc tính trên một dòng theo định dạng là “kiểu
    thuộc tính : giá trị thuộc tính”.

> <img src="media/image3.png" style="width:5.45427in;height:4.16968in" />
>
> <img src="media/image4.png" style="width:5.46812in;height:3.54844in" />
>
> <img src="media/image5.png" style="width:5.43493in;height:1.78928in" />

6.  **Cài đặt LDAP trên CentOS 7**

<!-- -->

1.  **<u>Chuẩn bị</u>**

- Cài đặt epel-release và cập nhật các gói phần mềm

> \# yum install epel-release –y
>
> \# yum update –y

- Tắt firewalld

> \# systemctl stop firewalld
>
> \# systemctl disable firewalld

- Tắt Selinux

\# setenforce 0

\# sed -i 's/SELINUX=enforcing/SELINUX=disabled/g'
/etc/sysconfig/selinux

\# sed -i 's/SELINUX=permissive/SELINUX=disabled/g'
/etc/sysconfig/selinux

\# sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config

\# sed -i 's/SELINUX=permissive/SELINUX=disabled/g' /etc/selinux/config

- Reboot

2.  **<u>Cài đặt OpenLDAP</u>**

- Cài gói

\# yum -y install openldap compat-openldap openldap-clients
openldap-servers openldap-servers-sql openldap-devel

- Sao chép file cấu hình và phân quyền

\# cp /usr/share/openldap-servers/DB_CONFIG.example
/var/lib/ldap/DB_CONFIG

\# chown ldap. /var/lib/ldap/DB_CONFIG

- Khởi động **slapd**

> \# systemctl start slapd
>
> \# systemctl enable slapd

- Verify the LDAP.

> \# netstat -antup \| grep -i 389

- Thiết lập LDAP admin password, tạo mật khẩu

> \# slappasswd -h {SSHA} -s ldppassword

- Thêm mới file **chroot.ldif**

cat \> chrootpw.ldif \<\< EOF

\# Chỉ định mật khẩu được tạo ở trên cho phần "olcRootPW"

dn: olcDatabase={0}config,cn=config

changetype: modify

add: olcRootPW

olcRootPW: {SSHA}xxxxxxxxxxxxxxxxxxxxxLDAPPASS1

EOF

- Chạy lệnh sau để update thông tin từ file **chroot.ldif**

> \# ldapadd -Y EXTERNAL -H ldapi:/// -f chrootpw.ldif

- Import các schemas:

> \# ldapadd -Y EXTERNAL -H ldapi:/// -f
> /etc/openldap/schema/cosine.ldif
>
> \# ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/nis.ldif
>
> \# ldapadd -Y EXTERNAL -H ldapi:/// -f
> /etc/openldap/schema/inetorgperson.ldif

- Thiết lập Manager Password, tạo mật khẩu:

> \# slappasswd

- Thêm mới file **chdomain.ldif**: \# vi chdomain.ldif

dn: olcDatabase={2}hdb,cn=config

changetype: modify

replace: olcSuffix

olcSuffix: dc=itzgeek,dc=local

dn: olcDatabase={2}hdb,cn=config

changetype: modify

replace: olcRootDN

olcRootDN: cn=ldapadm,dc=itzgeek,dc=local

dn: olcDatabase={2}hdb,cn=config

changetype: modify

replace: olcRootPW

olcRootPW: {SSHA}d/thexcQUuSfe3rx3gRaEhHpNJ52N8D3

The above entries need to be updated in 

**/etc/openldap/slapd.d/cn=config/olcDatabase={2}hdb.ldif** file.

Manual editor of LDAP configuration is not recommended as you will lose
changes whenever you run **ldapmodify** command.

- Chạy lệnh sau để update thông tin:

> \# ldapmodify -Y EXTERNAL -H ldapi:/// -f chdomain.ldif

Make a changes
to **/etc/openldap/slapd.d/cn=config/olcDatabase={1}monitor.ldif (Do not
edit manually) **file to restrict the monitor access only to ldap root
(**ldapadm**) user not to others.

\# **vi monitor.ldif**

dn: olcDatabase={1}monitor,cn=config

changetype: modify

replace: olcAccess

olcAccess: {0}to \* by
dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external, cn=auth" read
by dn.base="cn=ldapadm,dc=itzgeek,dc=local" read by \* none

\# ldapmodify -Y EXTERNAL -H ldapi:/// -f monitor.ldif

\# ldapmodify -Y EXTERNAL -H ldapi:/// -f monitor.ldif

3.  **<u>Set up LDAP database</u>**

> \# cp /usr/share/openldap-servers/DB_CONFIG.example
> /var/lib/ldap/DB_CONFIG
>
> \# chown ldap:ldap /var/lib/ldap/\*

- Add the **cosine and nis** LDAP schemas.

> \# ldapadd -Y EXTERNAL -H ldapi:/// -f
> /etc/openldap/schema/cosine.ldif
>
> \#ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/nis.ldif
>
> \#ldapadd -Y EXTERNAL -H ldapi:/// -f
> /etc/openldap/schema/inetorgperson.ldif

\# **vi** **base.ldif**

dn: dc=itzgeek,dc=local

dc: itzgeek

objectClass: top

objectClass: domain

dn: cn=ldapadm ,dc=itzgeek,dc=local

objectClass: organizationalRole

cn: ldapadm

description: LDAP Manager

dn: ou=People,dc=itzgeek,dc=local

objectClass: organizationalUnit

ou: People

dn: ou=Group,dc=itzgeek,dc=local

objectClass: organizationalUnit

ou: Group

> \# ldapadd -x -W -D "cn=ldapadm,dc=itzgeek,dc=local" -f base.ldif
>
> \# ldapsearch -x cn= ldapadm -b dc= itzgeek,dc=local

4.  **<u>Cài đặt PHP LDAP Admin để quản trị LDAP trên giao diện</u>**

- Cài đặt httpd

> \# yum -y install httpd

- Mở file **/etc/httpd/conf/httpd.conf** và sửa đổi các thông tin sau:

\# Tại dòng 151 sửa như sau :

AllowOverride All

\# Tại dòng 164, sửa thông tin như sau:

DirectoryIndex index.html index.cgi index.php

\# Thêm vào cuối file những cấu hình sau:

ServerTokens Prod

KeepAlive On

- Khởi động lại httpd

> \# systemctl restart httpd
>
> \# systemctl enable httpd

- Khởi tạo biến

> \# rpm -ivh
> <https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm>
>
> \# yum -y install epel-release

- Cài đặt PHP

> \# yum -y install php php-mbstring php-pear

- Mở file **/etc/php.ini**:

> \# Tại dòng 878 sửa lại timezone:
>
> date.timezone = "Asia/Ho_Chi_Minh"

- Cài đặt phpLdapadmin

> \# yum --enablerepo=epel -y install phpldapadmin
>
> \# sudo apt-get update
>
> \$ sudo apt-get install -y phpldapadmin

- Mở file **/etc/httpd/conf.d/phpldapadmin.conf** và thêm thông tin sau

> \# Tại dòng 11 sửa lại như
>
> Require all granted

- Khởi động lại httpd

> \# systemctl restart httpd
>
> \# firewall-cmd --permanent --zone=public --add-service=http
>
> \# firewall-cmd --reload

5.  **<u>Configure phpLDAPAdmin</u>**

> \# vi /etc/phpldapadmin/config.php
>
> \$ sudo nano /etc/phpldapadmin/config.php

- Mở file **/etc/phpldapadmin/config.php** và sửa các thông tin như sau:

> \# Tại dòng 397&398:
>
> \$servers-\>setValue('login','attr','dn');
>
> // \$servers-\>setValue('login','attr','uid');
>
> \$servers-\>setValue('server','name','ITzGeek Local LDAP Server');
>
> \$servers-\>setValue('server','host','127.0.0.1'); (Optional)
>
> \$servers-\>setValue('server','port',389); (Optional)
>
> \$servers-\>setValue('server','base',array('dc=itzgeek,dc=local'));
> (Ubuntu)

- If you have SELinux enabled on CentOS 7 / RHEL 7 then run this
  command.

> \# setsebool -P httpd_can_connect_ldap on

- Truy cập vào trang quản trị theo đường dẫn

> <http://IP_Server/phpldapadmin/>

6.  **Kết nối client tới server (login ssh bằng account LDAP)**

- Trên client, cài đặt các gói package sau: **apt-get install
  libpam-ldap nscd** và thiết lập các thành phần:

  - LDAP server Uniform Resource Identifier:
    ldap://LDAP-server-IP-Address

  - Distinguished name of the search base: "dc=test,dc=com"

  - LDAP version to use: 3

  - Make local root Database admin: Yes

  - Does the LDAP database require login? No

  - LDAP account for root: "cn=admin,dc=test,dc=com"

  - LDAP root account password: Your-LDAP-root-password

- Cấu hình file **/etc/nsswitch.conf**: thay đổi các dòng:

  - passwd: ldap compat

  - group: ldap compat

  - shadow: ldap compat

- Sửa lại file PAM config. PAM là module xác thực để hệ thống kết nối
  tới các ứng dụng yêu cầu xác thực.

- Ta sửa các file: **/etc/pam.d/common-session, common-account,
  common-auth** và **common-password**

> <img src="media/image6.png" style="width:4.80811in;height:1.34869in" />
>
> <img src="media/image7.png" style="width:5.56042in;height:1.77029in" />
>
> <img src="media/image8.png" style="width:4.89281in;height:1.6311in" />
>
> <img src="/media/imagea.png" style="width:5.13846in;height:2.5725in" />
>
> **Cài đặt PHPAdmin**

- Cài đặt gói php

> \#yum install php

- Cài đặt gói phpmyadmin

> \#yum install phpMyAdmin

- Cấu hình file /etc/httpd/conf.d/phpMyAdmin.conf

> \# vi /etc/httpd/conf.d/phpMyAdmin.conf
>
> require ip \<client's IP\>
>
> vim config.inc.php
