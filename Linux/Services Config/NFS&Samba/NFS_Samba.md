**NFS & SAMBA**

1.  **NFS server**

<!-- -->

1.  **GIỚI THIỆU DỊCH VỤ NFS**

- **NFS** – Network File System là dịch vụ chia sẻ file trong môi trường
  network giữa các server Linux.

- Dịch vụ NFS cho phép các NFS client mount một phân vùng của NFS server
  như phân vùng cục bộ của nó.

- Dịch vụ NFS không được security nhiều, vì vậy cần thiết phải tin tưởng
  các client được permit mount các phân vùng của NFS server.

- Ưu điểm:

  - NFS là 1 giải pháp chi phí thấp để chia sẻ tệp mạng.

  - Dễ cài đặt vì nó sử dụng cơ sở hạ tầng IP hiện có

  - Cho phép quản lý trung tâm, giảm nhu cầu thêm phần mềm cũ và dụng
    lượng đĩa trên các hệ thống người dùng cá nhân

- Nhược điểm :

  - NFS vốn không an toàn, chỉ nên sử dụng trên 1 mạng đáng tin cậy sau
    Firewall

  - NFS bị chậm trong khi lưu lượng mạng lớn

  - Client và server tin tưởng lần nhau vô điều kiện

  - Tên máy chủ có thể là giả mạo (tự xưng là máy khác)

2.  **KIẾN TRÚC CỦA NFS**

> <img src="media/image1.png" style="width:4.52334in;height:2.94691in" />

3.  **CẤU HÌNH NFS**

- Các tiến trình của **NFS server:**

  - **Portmap:** tiến trình này không làm viêc trực tiếp với dịch vụ NFS
    mà tham gia quản lý các yêu càu RPC từ máy trạm gửi đến.

  - **rpc.nfsd**: là tiến trình chính, thực thi nhiêm vụ của giao thức
    NFS, có nhiêm vụ cung cáp cho máy trạm các tap tin hoac thư mục được
    yêu cầu

  - **rpc.statd** và **rpc.lockd**

  - **rpc.rpquotad**: kiểm soát quota mà NFS users có thể sử dụng.

  - **rpc.mountd**: kiểm soát quyền được mount partition của NFS users.

- File cấu hình của NFS server: **\#/etc/exports**

> <img src="/media/image5.png" style="width:4.43077in;height:1.93472in" />
>
> /etc/exports.d/\*exports: directory of share definitions
>
> /var/lib/nfs/etab: list of available shares
>
> /etc/mtab: mounted drives

- Quyền truy cập có các giá trị sau:

  - secure: Port từ client requests phải nhỏ hơn 1024

  - ro : Read only

  - rw : read – write

  - noaccess : Denied access

  - root_squash : Ngăn remote root users

  - no_root_squash : Cho phép remote root users

<!-- -->

- NFS & SELinux:

\# getsebool –a \| grep nfs

- Lệnh của **NFS client**:

  - **mount**: dùng để mount một phân vùng của NFS server thành phân
    vùng cục bộ. Có thể đưa vào file **/etc/fstab** để mount tự động lúc
    khởi động.

    - Nfsvers

    - Noacl

    - Noexec

    - Nosuid

    - Port

    - Rsize and wsize

    - Hard/soft

    - Ac

    - Fg/bg

    - Retry

    - Sec=mode

    - Async/sync

    - Remount

    - Rw/ro

    - Suid/nosuid

    - User/nouser

    - Auto/nonauto

    - Defaults

    - \_netdev

  - **Nfsstat:** provides NFS & RPC statistics

  - **Nfsiostat:** provides statistics on NFS mounts

  - **Mountstats:** shows per mount statistics

  - **Rpcinfo**

  - **showmount:** hiển thị thông tin client nào sử dụng phân vùng nào
    của NFS server.

  - **Exportfs:** provides filesystems for export

- Để đảm bảo NFS security, sử dụng dựa vào 2 file **/etc/hosts.allow**
  và **/etc/hosts.deny**.

- File /etc/hosts.deny

> *portmap,lockd,mountd,rquotad,statd: ALL*

- File /etc/hosts.allow

> *portmap,lockd,mountd,rquotad,statd: 192.168.0.0/255.255.0.0*

<img src="/media/image6.png" style="width:5.57522in;height:2.625in" />

2.  **<u>Samba server</u>**

<!-- -->

1.  **Giới thiệu dịch vụ Samba.**

- **Samba** là dịch vụ chia sẻ file và dịch vụ in trong môi trường
  network giữa các máy tính Linux và máy tính Windows.

- Từ Linux:

  - Mount thư mục chia sẻ của Windows.

  - Truy cập máy in của Windows.

  - Chứng thực với các máy tính Windows.

- Từ Windows:

  - Thấy những thư mục chia sẻ của Linux.

  - Chứng thực với các máy tính Linux.

  - Truy cấp máy in của Linux.

<img src="/media/image7.png" style="width:5in;height:2.08333in" />

<img src="/media/image8.png" style="width:5in;height:0.6875in" />

- Dịch vụ Samba gồm những tiến trình sau:

<!-- -->

- Tiến trình **smbd**:

  - Lắng nghe trên port **139**, trực tiếp xử lí các request truy cập
    đến thư mục chia sẻ trên Linux.

  - Khi một client kết nối, smbd sẽ tạo ra một tiến trình mới, phục vụ
    cho kết nối này.

- Tiến trình **nmdb**:

  - Lắng nghe trên port **137**, chịu trách nhiệm cung cấp tên NetBIOS
    của samba server cho các request kết nối.

<!-- -->

- Tiến trình windbinđ:

  - Interface to NSS

  - Allows domain users to authenticate services on local hosts.

<!-- -->

- Windows và Linux đều sử dụng mã hóa khi cần chứng thực users.

- Khi users cần chứng thực, password do user nhập vào sẽ được mã hóa,
  đêm so sánh với password mã hóa đã được lưu sẵn. Nếu giống nhau thì
  chứng thực thành công.

- Kiểu mã hóa mà Windows và Linux sử dụng là khác nhau.

- Để một user trên windows chứng thực thành công trên linux, tạo lại
  user đó trên linux, dùng lệnh **smbpasswd**.

2.  **CẤU HÌNH DỊCH VỤ SAMBA**

- Dịch vụ Samba có thể được cài đặt từ RPM:

  - samba-client-\[version\]

  - samba-common-\[version\]

  - samba-\[version\]

  - system-config-samba-\[version\]

- Hoặc có thể cài đặt dịch vụ Samba từ gói **yum**.

- File cấu hình chính của dịch vụ Samba: **/etc/samba/smb.conf**

  - **/etc/samba/smbusers:** maintains Samba to Linux user mappings

  - **/etc/sysconfig/samba:** stores samba startup config

  - **/var/lib/samba/private/smbpasswd:** holds samba passwords

  - **/var/log/samba:** location of samba logs

- Dùng lệnh **testparm** để test file cấu hình Samba.

- File cấu hình dịch vụ Samba có thể được chỉnh sửa trực tiếp, hoặc
  chỉnh sửa qua giao diện web sử dụng **SWAT**.

- Định nghĩa các option chung của Samba trong section \[global\]:

> <img src="media/image3.png" style="width:3.87559in;height:0.70961in" />

- Những thư mục share của Samba được định nghĩa thành từng section.

- Thư mục share của Samba:

> <img src="media/image4.png" style="width:3.75881in;height:1.20384in" />

- SWAT là giao diện web-based cho phép chỉnh sửa các cấu hình của Samba
  trên giao diện web.

- Lệnh của **Samba client**:

  - Smbclient

  - Smbmount

\` <img src="/media/image9.png" style="width:5in;height:2.41667in" />

- **Samba Server**

<!-- -->

- File format: **/etc/samba/smb.conf**

<img src="/media/image16.png"
style="width:5.29166in;height:2.20486in" />

<img src="/media/image17.png" style="width:2.1875in;height:1.18766in" />

<img src="/media/imagec.png" style="width:5in;height:2.36458in" />

<img src="/media/imaged.png" style="width:5in;height:2.1875in" />

<img src="/media/imagee.png" style="width:5in;height:1.52083in" />

<img src="/media/imagef.png" style="width:5in;height:2.35417in" />

<img src="/media/image10.png" style="width:5in;height:1.91667in" />

\# getsebool –a \| egrep ‘smb\|samba\|cifs’

- **Create a simple public share**

> \# mkdir /home/sambapublic
>
> \# setsebool –P samba_export_all_ro on
>
> \# setsebool –P samba_export_all_rw on
>
> \# chown nobody:nobody /home/sambapublic/
>
> \# chmod 775 /home/sambapublic/
>
> \# semanage fcontext –at public_content_rw_t
> “/home/sambapublic(/.\*)?”
>
> \# restorecon /home/sambapublic

\# firewall-cmd –permanent –add-service samba

> \# firewall-cmd –reload
>
> \# vi /etc/samba/smb.conf
>
> \[sambapublic\]
>
> Comment = public samba share
>
> Path = /home/sambapublic
>
> Writable = yes
>
> Public = yes
>
> \# testparm
>
> \# systemctl restart smb
>
> \# systemctl enable smb
>
> \# smbclient –L //localhost
>
> \# smbclient //localhost/sambapublic

**Installation & Configuration**

1.  **NFS Server**

<!-- -->

1.  **Cài đặt NFS Server**

> \# rpm –ql nfs-utils
>
> \# yum install nfs-utils
>
> \# systemctl start nfs-server.service
>
> \# systemctl enable nfs-server.service
>
> \# sudo systemctl enable --now nfs-server rpcbind

- Các file cấu hình của NFS server là:

  - **/etc/nfs.conf**: File cấu hình chính cho trình nền và công cụ NFS.

  - **/etc/nfsmount.conf**: File cấu hình NFS mount.

    - Mount

    - Server

    - Global

  - **/etc/exports**: File config chính của NFS, chứa thông tin danh
    sách các file và thư mục chia sẻ trên NFS Server.

  - **/etc/fstab**: Để tự động mount một thư mục NFS trên hệ thống

  - **/etc/sysconfig/nfs**: File config của NFS để quản lý port đang
    lắng nghe của rpc và các service.

- cấu hình NFS server **/etc/exports** để xác định các máy client nào có
  thể truy cập được file được chia sẽ trên NFS server

  - **vi\|cat /etc/exports**

- Trong đó:

  - /root/test-nfs-server: Là thư mục chia sẽ dữ liệu.

  - \<IP address range\>: Dãy địa chỉ có thể truy cập.

  - (rw,sync): Quyền truy cập.

- Các quyền trong NFS:

  - ro: Read only.

  - rw: Read – write.

  - noaccess: Denied access.

  - root_squash: Ngăn remote root users

  - no_root_squash: Cho phép remote root users.

- Để load file cấu hình chúng ta chạy lệnh **exportfs**: **exportfs
  –arv**

exportfs -s

- **Create a simple NFS share**

\# mkdir /home/usershare

\# setsebool –P nfs_export_all_ro on

\# setsebool –P nfs_export_all_rw on

\# getsebool –a \| grep nfs_export

\# firewall-cmd –permanent –add-service nfs

\# firewall-cmd –reload

\# vi /etc/exports

/home/usershare rhhost2(rw)

\# exports –avr

\# cat /var/lib/nfs/etab

\# chown user1:user1 /home/usershare

2.  **Cài đặt dịch vụ NFS client**

> \# yum install nfs4-acl-tools
>
> \# showmount –e \<Server’s IP\> -- kiểm tra mount point on server

- Tạo thư mục trên client để test. \# mkdir /home/usermount

<!-- -->

- Mount NFS file thực thi

***mount –t nfs \<server’s IP\>:\<server‘s test_file\> \<client’s
test_file\>***

- confirm file từ NFS: \#mount \| grep nfs

\# vi /etc/fstab hoặc

\# echo “ \<server’s IP\>:\<server‘s test_file\> \<client’s test_file\>
nfs defaults 0 0” \>\> /etc/fstab

<https://linux.101hacks.com/unix/rpc-port-mapper-failure/>

<https://forum.proxmox.com/threads/storage-nfs-rpc-remote-system-error-no-route-to-host.116719/>

- Delayed mounting with autofs

\# yum –y install autofs

\# vi /etc/auto.master

Add **/-** **/etc/auto.direct**

\# vi /etc/auto.direct

Add /home/usermount rhhost1:/home/usershare

\# systemctl stop autofs

\# umount /home/usermount

\# df

\# ls –lZ /home

\# systemctl start autofs

3.  **Check hoạt động NFS**

\- Trên server NFS kiểm tra bằng lệnh: **touch \<file_name\>**

\- Qua client, kiểm tra xem có thấy file mới tạo bên NFS server không:

\- Thực hiện ngược lại

\# tail –f /var/log/audit/audit.log

\# nfsstat

\# rpcinfo

\# nfsiostat

**NFS Share Exercises**

- **<u>Create an NFS share with root access</u>**

\# mkdir /home/rootshare

\# setsebool –P nfs_export_all_ro on

\# setsebool –P nfs_export_all_rw on

\# firewall-cmd –permanent –add-service nfs

\# firewall-cmd –reload

\# systemctl start nfs-server

\# systemctl enable nfs-server

\# vi /etc/exports

/home/usershare rhhost2(rw)

/home/rootshare rhhost2(rw,no_root_squash)

\# exportfs –avr

\# mkdir /home/rootmount

\# mount –t nfs rhhost1:/home/rootshare /home/rootmount

\# touch /home/rootmount/testfile.txt

\# touch /home/usermount/testfile.txt

- **<u>Create an NFS share for group collaboration</u>**

\# mkdir /home/groupshare

\# useradd user2

\# groupadd –g 6000 groupcollab

\# usermod –a –G groupcollab user1

\# usermod –a –G groupcollab user2

\# cat /etc/group

\# chown nfsnobody:groupcollab /home/groupshare

\# chmod 2770 /home/groupshare

\# setsebool –P nfs_export_all_ro on

\# setsebool –P nfs_export_all_rw on

\# firewall-cmd –permanent –add-service nfs

\# firewall-cmd –reload

\# systemctl start nfs-server

\# systemctl enable nfs-server

\# vi /etc/exports

/home/groupshare rhhost2(rw,no_root_squash)

\# exportfs –avr

- **<u>Mount a NFS share for group collaboration</u>**

\# mkdir /home/groupmount

\# useradd user2

\# passwd user2

\# groupadd –g 6000 groupcollab

\# usermod –a –G groupcollab user1

\# usermod –a –G groupcollab user2

\# mount –t nfs rhhost1:/home/groupshare /home/groupmount

\# touch /home/groupmount/user1.txt

\# touch /home/groupmount/user2.txt

2.  **SAMBA**

<!-- -->

1.  **Cài đặt SAMBA**

- Cài đặt các gói cài đặt của SAMBA

> \#yum install samba samba-client samba-common

- Khởi động dịch vụ

> \#systemctl enable smb
>
> \#systemctl start smb

2.  **Cấu hình SAMBA**

- \*\*\*\* Backup File trước khi làm \*\*\*\*

- Thực hiện cấu hình:

\[comment\]

comment = common Directory

path = /var/common

valid users = users root

browseable = yes

writable = yes

read only = no

create mask = 0755

directory mask = yes

- Thực hiện **restart** lại dịch vụ samba

- tạo user và group và biến user đó thành thành viên của nhóm đó để họ
  có thể sử dụng dịch vụ

> \#useradd \<user\>
>
> \#passwd \<user\>
>
> \#smbpasswd –a \<user\>
>
> \#more /etc/passwd -- check list of users
>
> \# groupadd \<group\>

- vào Run trên Windows: \\\<server’s IP\>

- Nhập thông tin đăng nhập của bạn và nhấn OK

3.  **Samba Client Tools**

<img src="/media/image11.png" style="width:5.48958in;height:2.6533in" />

<img src="/media/image12.png" style="width:5in;height:1.38542in" />

\# smbclient //localhost/sambapublic

<img src="/media/image13.png" style="width:5in;height:2.29167in" />

<img src="/media/image14.png" style="width:5in;height:1.27083in" />

- Mount a simple public share

\# smbclient //rhhost1/sambapublic

\> mkdir testdir2

\> ls

\# mkdir /home/sambapublic

\# mount –t cifs -o guest, noperm //rhhost1/sambapublic
/home/sambapublic/

\# cd /home/sambapublic/

\# touch file1

\# ls

4.  Samba share Exercises

\# mkdir /home/sambaprivate

\# chown user1:user1 /home/sambaprivate

\# chmod 775 /home/sambaprivate/

\# semanage fcontext –at public_content_rw_t “/home/sambaprivate(/.\*)?”

\# restorecon /home/sambaprivate/

\# vi /etc/samba/smb.conf

\[sambaprivate\]

comment = Private Samba Share available to user1

path = /home/sambaprivate

writable = yes

valid users = user1

write list = user1

public = yes

\# testparm

\# smbpasswd –a user1

\# pdbedit –Lv

\# systemctl restart smb

\# smbclient –NL //localhost

\# smbclient //rhhost1/sambaprivate -U user1

\# mkdir /home/sambaprivate

\# mount –t cifs –o username=user1 //rhhost1/sambaprivate
/home/sambaprivate

\# touch /home/sambaprivate/file.txt

- Automount using a credentials file

\# vi /root/sambaprivate.cred

Username=user1

Password=password

\# vi /etc/fstab

//rhhost1/sambaprivate /home/sambaprivate cifs
credentials=/root/sambaprivate.cred 0 0

\# umount /home/sambaprivate

\# mount –a

- Create a Samba share for group collaboration

\# mkdir /home/sambagroup

\# groupadd –g 6001 sambacollab

\# usermod –a –G sambacollab user1

\# usermod –a –G sambacollab user2

\# chown :sambacollab /home/sambagroup/

\# chmod 770 /home/sambagroup/

\# semanage fcontext –at public_content_rw_t “/home/sambagroup(/.\*)?”

\# restorecon /home/sambagroup/

\# ls –dZ /home/sambagroup

\# vi /etc/samba/smb.conf

\[sambagroup\]

comment = Samba Share for group collaboration

path = /home/sambagroup

browsable = no

force group = sambacollab

writable = yes

valid users = @sambacollab

write list = @sambacollab

public = no

create mask = 0770

\# testparm

\# smpasswd –a user2

\# pdbedit –Lv

\# systemctl restart smb

\# systemctl status smb

\# smbclient –L //localhost -U user1

- Mount a share for group collaboration

\# groupadd –g 6001 sambacollab

\# usermod –a –G sambacollab user1

\# usermod –a –G sambacollab user2

\# smbclient –L //rhhost1/sambagroup -U user1

\# smbclient –L //rhhost1/sambagroup -U user2

\# mkdir /home/sambagroup/

\# mount –t cifs –o username=user1 //rhhost1/sambagroup /home/sambagroup

\# mount \| grep sambagroup

- Create a secure share using Keberos

<img src="/media/image18.png" style="width:5in;height:2.32292in" />

<https://ubuntu.com/tutorials/install-and-configure-samba#2-installing-samba>

<https://ubuntu.com/server/docs/samba-file-server>

<https://phoenixnap.com/kb/ubuntu-samba>

<https://linuxize.com/post/how-to-install-and-configure-samba-on-centos-7/>

<https://www.linuxtechi.com/install-configure-samba-centos-8/>

<https://poweradm.com/configure-nfs-client-windows/>

<https://www.tecmint.com/install-nfs-server-on-centos-8/>

<https://computingforgeeks.com/configure-nfs-client-on-centos-rhel/?expand_article=1>

<https://computingforgeeks.com/install-and-configure-nfs-server-on-centos-rhel/?expand_article=1>

LINUX Storage

https://computingforgeeks.com/configure-iscsi-target-and-initiator-on-centos-rhel/?expand_article=1

https://computingforgeeks.com/how-to-configure-iscsi-initiator-on-centos-rhel/?expand_article=1
