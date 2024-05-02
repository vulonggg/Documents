**SSH SERVER**

1.  **GIỚI THIỆU DỊCH VỤ SSH**

- **SSH (Secure Shell)** được hiểu là giao thức kết nối giữa máy khách
  và máy chủ điều khiển từ xa cho phép người sử dụng chỉnh sửa và kiểm
  soát server từ xa nhưng vẫn đảm bảo được an toàn.

- Người dùng có khả năng sử dụng để chuyển tập tin, chạy chương trình,
  chuyển tiếp khác kết nối TCP / IP bằng đường truyền đã được bảo mật.

1.  **CHỨC NĂNG CỦA DỊCH VỤ SSH**

- Truy cập từ xa an toàn vào các hệ thống hay thiết bị mạng có hỗ trợ
  SSH cho người dùng và các quá trình tự động khác.

- Hỗ trợ phiên chuyển file an toàn

- Tự động truyền file an toàn.

- Thực thi lệnh an toàn trên các máy hay hệ thống từ xa.

- Quản lý an toàn các thành phần cơ sở hạ tầng mạng.

2.  **Chứng thực**

- Giao thức SSH hỗ trợ 2 loại hình chứng thực cho người dùng, đó là:

  - Chứng thực người dùng bằng mật khẩu.

  - Cách thứ hai chính là dùng cặp khóa bất đối xứng để chứng thực.
    Người dùng sẽ khởi tạo một cặp khóa public key – private key với độ
    bảo mật cao.

3.  **MÃ HÓA**

- Giao thức SSH sử dụng 03 thuật toán mã hóa khác nhau:

  - **Symmetric Encryption**: Thường được gọi là **shared key** hoặc
    **shared secret encryption**

> <img src="media/image1.png" style="width:4.71318in;height:2.19903in" />

- **Asymmetric Encryption**: sử dụng 2 khóa khác nhau để mã hóa và giải
  mã. 2 khóa này được gọi là **public key** và **private key**. Cả 2
  hình thành nên một cặp khóa là **public-private key pair**.

> <img src="media/image2.png" style="width:5.07956in;height:2.30077in" />

- **Hashing**: Hashing một chiều là một dạng mã hóa khác sử dụng trong
  Secure Shell Connections.

> <img src="media/image3.png" style="width:3.92659in;height:2.56577in" />

4.  **THUẬT TOÁN TẠO KHÓA**

- Để chứng thực bằng SSH key, người dùng cần phải tạo ra cặp Private –
  Public key bằng các thuật toán RSA, DSA, ECDSA, trong đó RSA là thuật
  toán thường hay được dùng nhất với độ dài khóa từ 2048 – 4096:

  - **RSA**: đây là thuật toán khóa bất đối xứng cổ điển và được dùng
    phổ biến nhất hiện nay. Keysize giao động từ 1024 – 4096 bit (nên
    chọn keysize từ 2048 trở đi vì lý do an toàn).

  - **DSA**: một thuật toán mã hóa bất đối xứng lâu đời của chính phủ mỹ
    với keysize thường dùng là 1024 bit.

  - **ECDSA**: thuật toán chữ ký điện tử mới được tiêu chuẩn hóa bởi
    chính phủ Mỹ, thuật toán được dựa trên cách tính đường cong elip.

  - **ED25519**: đây là thuật toán mới được thêm vào OpenSSH

2.  **MÔ HÌNH HOẠT ĐỘNG**

- SSH hoạt động bằng mô hình client-server cho phép chứng thực an toàn
  giữa 2 máy từ xa và mã hóa dữ liệu được truyền giữa chúng.

- SSH vận hành trên TCP port 22 mặc định.

- Có hai giai đoạn để thiết lập kết nối và cấp quyền cho users:

  - Session Encryption Negotiation: Hai bên xác định và đồng ý chuẩn mã
    hóa.

  - Authentication: Xác thực users

> <img src="media/image4.png" style="width:5.37484in;height:2.48314in" />

3.  **CÀI ĐẶT VÀ CẤU HÌNH DỊCH VỤ SSH**

- Có thể cài đặt gói OpenSSH bằng RPM hoặc source, Yum

- File cấu hình chính của gói SSH:

  - **/etc/ssh/sshd_config** : file cấu hình dịch vụ OpenSSH Server.

  - **/etc/ssh/ssh_config** : file cấu hình OpenSSH client.

  - **~/.ssh/** : thư mục chứa nội dung cấu hình ssh của user client
    trên Linux.

  - **~/.ssh/authorized_keys** : thư mục chứa thông tin các public key
    (RSA hoặc DSA) được user sử dụng để đăng nhập vào hệ thống Linux

  - **/etc/nologin** : nếu file này tồn tại, thì dịch vụ SSH Server trên
    Linux sẽ từ chối kết nối đăng nhập từ các user khác trên hệ thống
    ngoại trừ user root. File này thường dùng trong trường hợp khẩn cấp
    cần cách ly sớm hệ thống

4.  **Installation & Configuration**

<!-- -->

1.  **Cài đặt SSH**

- Kiểm tra và cài đặt và cấu hình gói **openssh** trên server

> \#rpm –qa \| grep openssh

- Kiểm tra và cài đặt và cấu hình gói openssh trên client

> \# yum install openssh-server
>
> \# yum install openssh-clients
>
> \# systemctl enable sshd
>
> \# systemctl start sshd
>
> \# systemctl restart sshd

2.  **Cấu hình bảo mật cho SSH Server**

- Chỉ sử dụng giao thức SSH phiên bản 2, hiện tại mặc định dịch vụ SSH
  đã kích hoạt phiên bản “2“, nhưng trên 1 số OS cũ thì vẫn còn hỗ trợ
  cả 1 và 2.

> **\#** vi /etc/ssh/sshd_config **-- Protocol 2**

- Không sử dụng mật khẩu rỗng

> **\#** vi /etc/ssh/sshd_config **-- PermitEmptyPasswords no**

- Thay đổi cổng (port) SSH và giới hạn IP lắng nghe dịch vụ SSH, và chỉ
  cho lắng nghe trên một IP duy nhất nếu máy chủ có nhiều hơn 1 IP.

> \#Port 2233
>
> \#ListenAddress 192.168.0.0 \#restrict user & network
>
> …..
>
> AllowUsers user1@192.168.0.0/24

- Không cho đăng nhập bằng user **root**

> **\#**vi /etc/ssh/sshd_config **-- PermitRootLogin no**

- Tắt chức năng đăng nhập của file **~/.rhosts**

> \#IgnoreRhosts yes
>
> \#RhostsRSAAuthentication no

- Cấu hình thời gian ngắt kết nối SSH nếu user không hoạt động

> \#ClientAliveInterval 300
>
> \#ClientAliveCountMax 0

- Cấu hình thời gian timeout khi user không đăng nhập thành công

> \#LoginGraceTime 120

- Chỉ ra đường dẫn lưu Public key

> \#AuthorizedKeysFile .ssh/authorized_keys

- Sử dụng chứng thực SSH Key, tắt chứng thực mật khẩu

> \#PubkeyAuthentication yes
>
> \#PasswordAuthentication no

- Cho phép/từ chối kết nối SSH từ 1 user hoặc 1 group

> \#AllowUsers pnh1 pnh2
>
> \#AllowGroups admin
>
> \#DenyUsers lpi1 lpi2
>
> \#DenyGroups fpt

- Chế độ “StrictModes”: kiểm tra quyền thư mục \$HOME thư mục **“.ssh”**
  và file  
  **“authorized_keys”** chứa key SSH

> \#StrictModes yes

- Số lần tối đa đăng nhập sai

> \#MaxAuthTries 3

3.  Cài đặt và sử dụng **SSH Key**

- **Public Key** : Bạn sẽ copy ký tự key này sẽ bỏ vào file
  **~/.ssh/authorized_keys** trên server của bạn.

- **Private Key** : Bạn sẽ lưu file này vào máy tính, sau đó sẽ thiết
  lập phiên ssh sử dụng key này để có thể login.

- **Keypharse** : Mật khẩu để mở private key, khi đăng nhập vào server
  nó sẽ hỏi cái này (Nếu không đặt pass cho private key thì có thể bỏ
  qua)

> a.1. Cài đặt và sử dụng SSH Key
>
> \- Đối với **windows**: Người dùng có thể sử dụng phần mềm
> **PuTTY-Gen**
>
> **-** Sau khi click vào genarate bạn di chuyển chuột quanh màn hình để
> tạo key, sau đó Save private key như hình bên dưới để lưu lại private
> key được tạo ra
>
> **-** Sau đó ta lưu lại đoạn public key ra một file với nội dung copy
> đoạn mã như ảnh bên dưới
>
> **-** Khởi động Putty Client và load Private key đã tạo để thiết lập
> kết nối bằng key với server

- Đối với **Linux Client**: Chạy lệnh **ssh-keygen -t rsa**

> \#mkdir ~/.ssh
>
> \#chmod 700 ~/.ssh
>
> \# ssh-keygen –b 4096 –t rsa

- Check lại cặp key vừa tạo:

> \# ssh-keygen –l

- Tiếp theo, ta sẽ upload cặp key này lên thư mục HOME của người dùng mà
  ta muốn đăng nhập trên Remote Server

> \# ssh-copy-id root@\<ip_address\>

Or \# scp \$HOME/id_rsa.pub RemoteServer :~/.ssh/authorized_keys.

- Trên SSH server cấu hình file **/etc/ssh/sshd_config** không cho phép
  đăng nhập với quyền root và đăng nhập bằng mật khẩu

> \# PermitRootLogin no \#restrict root login with SSH
>
> \# PasswordAuthentication no
>
> \# PermitEmptyPasswords no

- Cấu hình file **/etc/ssh/sshd_config** dùng cặp key RSA để chứng thực
  người dùng

> \# RSAAuthentication yes
>
> \# PubkeyAuthentication yes
>
> \# AuthorizedKeysFile .ssh/authorized_keys

- Thiết lập có xác thực SSH Key đến host tương ứng, ví dụ, kết nối đến
  192.168.16.10 thì dùng Private key lưu tại /home/lpi/.ssh/id_rsa, thì
  file config đó như sau:

> \# Host 192.168.1.52
>
> \# PreferredAuthentications publickey
>
> \# IdentityFile "/home/lpi/.ssh/id_rsa"

- Kiểm tra đăng nhập không cần dùng password: **ssh
  <lpi@192.168.16.10>**

a.2. Copy file sử dụng **SCP** (Secure Copy) từ ssh client lên server và
ngược lại

\# touch lab-scp.txt

\# scp lab-scp.txt root@\<server\>

\# scp lab-scp.txt root@\<server\> :/directory/

\# scp \[options\] \<source file\> \<destination file\>

\# scp /etc/hosts 192.168.1.147:/tmp

\# scp –P 1022 192.168.1.147: /etc/hosts /tmp (nondefault port number)

\# scp –r 192.168.1.147: /etc/hosts /tmp (recursive secure copy)

\# cat ~/.ssh/id_rsa.pub \| ssh 192.168.1.147 “cat - \>\>
~/.ssh/authorized_keys”(piping)

\# dd if=/dev/sdb \| ssh 192.168.1.147 “dd of=/dev/sdb” (duplicate a
disk through ssh)

\# ssh –t <user1@192.168.1.147> “sudo tail /var/log/messages”

<img src="/media/image5.png" style="width:5in;height:2.04167in" />

\# vi ~/.ssh/config

Host host1

User user1

Hostname 192.168.1.2

Port 1022

IdentifyFile ~/.ssh/rhhost2.key

\# chmod 600 ~/.ssh/config

\# ssh host1

id_rsa: private key

id_rsa.pub: public key

authorized_keys

known-hosts

\# ssh-copy-id <user1@192.168.1.2>

\# ssh-add

id_rsa.pub is stored in ~/.ssh/authorized_keys

Fingerprint of remote server is stored in the local users known-hosts
file

<https://www.cyberciti.biz/faq/how-to-install-ssh-on-ubuntu-linux-using-apt-get/>

https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-20-04/
