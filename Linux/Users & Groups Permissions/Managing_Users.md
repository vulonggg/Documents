**Managing Users**

1.  **ĐỊNH NGHĨA USERS**

- Users được định nghĩa trong một hệ thống để xác định “ai? được quyền
  dùng cái gì?” trong hệ thống đó.

- Loai user:

  - Nonlogin

    - Run system devices

  - Login

    - Super user (root)

    - Regular user (unprivileged)

- Với Linux, mỗi user có một định danh duy nhất, gọi là **UID** (User
  ID).

  - **0 – 99**: user có quyền quản trị.

  - **\> 99**: user khác.

  - **\>= 500**: không phải user hệ thống.

- Mỗi user thuộc ít nhất một group. Mỗi group cũng có một định danh duy
  nhất là **GID**.

- Mỗi users cần có những thông tin: tên user, UID, tên group, GID, home
  directory…

- Windows quản lý thông tin bằng LDAP, Kerberos. Linux quản lý thông tin
  bằng file text.

- Có thể chỉnh sửa thông tin của users bằng công cụ, hoặc sửa trực tiếp
  bằng text file.

<!-- -->

- Những file định nghĩa thông tin users:

<!-- -->

- **/etc/passwd**: chứa thông tin user login, password mã hóa, UID, GID,
  home directory, và login shell. Mỗi dòng là thông tin của một user.

> <img src="media/image1.png" style="width:4.51906in;height:2.23008in"
> alt="Timeline Description automatically generated" />

- **/etc/shadow**: chứa thông tin password mã hóa, thời gian sử dụng
  password, thời gian phải thay đổi password…

> <img src="media/image2.png" style="width:5.15226in;height:2.53594in"
> alt="Timeline Description automatically generated with low confidence" />

- **/etc/group**: chứa thông tin group.

> <img src="media/image3.png" style="width:3.64109in;height:1.82531in"
> alt="Diagram Description automatically generated" />

- **/etc/gshadow**: contains the shadowed information for group
  accounts.

<!-- -->

- Secure group account information.

2.  **CẤU HÌNH MẶC ĐỊNH**

- Khi dùng lệnh **useradd** không có option kèm theo để tạo user, các
  thuộc tính của user sẽ được tạo theo các cấu hình mặc định.

- Những file định nghĩa cấu hình mặc định:

  - /etc/default/useradd

  - /etc/login.defs

  - /etc/skel

- Nếu muốn thay đổi cấu hình mặc định, thay đổi trực tiếp trong những
  file này.

  - **/etc/default/useradd**: những giá trị mặc định cho việc tạo
    acount.

  - **/etc/login.defs**: những cấu hình mặc định cho shadow password.

  - **/etc/skel**: thư mục chứa nội dung mặc định sẽ tạo trong home
    directory của users.

- Edit password policies:

> **\#vi /etc/security/pwquality.conf**

- **Passwd:** *Thay đổi password cho người dùng*

> Passwd -l**:** *Khóa tài khoản người dùng*
>
> cat /etc/shadow \|grep \<user\>
>
> passwd -u: *unlock*
>
> passwd -S: *cài đặt password*

- Account aging – **chage**

> Options:
>
> **-d:** days since last pasword change
>
> **-E:** days from January 1,1970 until expiration
>
> **-l:** Inactivity after expiration before
>
> **-m:** minimum days between password changes
>
> **-M:** Maximum days of password validity
>
> **-W:** days of warning before password change

<img src="/media/image7.png" style="width:5.5in;height:3.875in" />

3.  **Công cụ quản lý users.**

- **User:**

<!-- -->

- **useradd**: tạo user & cấu hình, điều kiện user.

Options (typical):

- -d: user’s home directory

- -u: user ID

- -g: primary group ID

- -G: supplementary group

- -s: default shell

<!-- -->

- **userdel**: xóa user. (-r)

- **usermod**: chỉnh sửa thông tin user; khóa & mở khóa user; thêm users
  vào supplemental groups; move user’s home directory.

  - User options

    - -s: change shell

    - -l: change user’s name

    - -u: change user ID

    - -d: change user’s home directory

  - Group options

    - -g: change primary group ID

    - -G: add to supplementary group

    - -a: append to existing list

  - Admin options

    - -m: move home directory

    - -L: lock account

    - -U: unlock account

<!-- -->

- Group:

<!-- -->

- groupadd: tạo group.

- groupdel: xóa group.

- groupmod: chỉnh sửa thông tin group.

  - -n: Đổi tên nhóm

  - -G: Add users vào trong nhóm

4.  **Elevating Privileges**

    1.  **Become super user**

- -c \<command\> \<user\>: run a command as a user

- -g \<primary group\>: run a command as the group

- \- / -l: start a login shell

- -s: run the command in a different shell

<!-- -->

- whoami: tells me who I currently am

- logname: tells me who I logged in as initially

- Difference between logging as root and switching to the root user, the
  environment – the variables & system configuration that comes with a
  logged in user.

<!-- -->

- su root \| echo \$PATH =\> environment of initial user.

- su – root \| echo \$PATH =\> environment of root user.

  1.  **Sudo**

- SUID/SGID: no password needed

- su: enter root password

- sudo: enter user password

<!-- -->

- **Privileges**

<!-- -->

- Root: all commands

- DBA: mysql, pgsql, mysqldump, mysqladmin,psql

- Web Admin: httpd, apachectl, apache, nginx

<!-- -->

- **Sudo Aliases**

<!-- -->

- User_Alias - Group users

- Runas_Alias – Groups run-as users

- Cmnd_Alias – Groups commands

- Host_Alias – Groups hosts

> \# sudo visudo \| vi /etc/sudoers
>
> \##User Aliases

User_Alias DRIVEADMINS = user1

Cmnd_Alias DRIVETOOLS = /usr/sbin/gdisk

Host_Alias DRIVEHOSTS = rhhost1.localnet.com

DRIVEADMINS DRIVEHOSTS =(ALL) NOPASSWD: DRIVETOOLS

5.  **Permissions**

- **Files**: users can read, write, and execute

- **Directories**: users list, create files, and traverse

- **Ownership**

  - Files can only belong to one user, one group

  - Directories can only belong to one user, one group

  1.  **File and directory modes**

<!-- -->

- Quyền trong linux được phân chia như sau:

<!-- -->

- **Đọc** **(read):** Cho phép đọc nội dung tập tin và xem nội dung thư
  mục bằng lệnh ls.

- **Ghi** **(write):** Cho phép ghi, thay đổi nội dung hoặc xóa tập tin.
  Đối với thư mục, quyền này cho phép tạo, xóa hoặc đổi tên tập tin mà
  không phụ thuộc vào quyền sở hữu trên tập tin chứa trong thư mục.

- **Thực thi (execute)**: Tải file vào bộ nhớ và chạy trên CPU. Cho phép
  thực thi chương trình, đối với thư mục, quyền này cho phép chuyển vào
  thư mục bằng lệnh cd.

<!-- -->

- Mỗi file trong linux được gán quyền theo ba lớp user sau:

<!-- -->

- owner

- group

- everyone (other)

> <img src="media/image4.png" style="width:5.37293in;height:1.39317in"
> alt="Diagram Description automatically generated" />
>
> <img src="media/image5.png" style="width:3.11199in;height:3.43117in"
> alt="Table Description automatically generated" />

- Quyền của người sở hữu (owner hoặc user) ký hiệu bằng ký tự **u**:
  Người tạo ra thư mục/tập tin hoặc được gán quyền sở hữu.

- Quyền của nhóm (group) ký hiệu bằng ký tự **g**: Nhóm người sử dụng
  được gán quyền

- Quyền của những người dùng khác (others) ký hiệu bằng ký tự **o**: Là
  những người sử dụng khác không thuộc về 2 loại trên.

  1.  **Biểu diễn quyền truy xuất**

<!-- -->

- **Bằng chữ**

Trong cách biểu diễn này, quyền truy xuất được viết bằng các ký tự:

r: read

w: write

x: excute

-: không có quyền

- **Bằng số**

Trong cách biểu diễn này, mỗi quyền được gán cho một giá trị số theo
bảng sau:

**r=4, w=2, x=1**

<img src="media/image6.png" style="width:5.82355in;height:2.43332in"
alt="Table Description automatically generated" />

1.  **Set ownership**

- Lệnh **chmod**: Thay đổi quyền truy xuất trên thư mục/tập tin. Có 2
  cách để sử dụng chmod, đó là dùng chữ hoặc dùng số.

Cấu trúc lệnh:

***chmod \[Options\] Mode file***

Option: -R - Áp dụng đối với thư mục làm cho lệnh chmod có tác dụng trên
cả các thư mục con (đệ quy).

Mode: Quyền truy xuất mới trên tập tin

- Quyền truy xuất mới có thể gán cho từng nhóm quyền bằng cách sử dụng
  ký tự **u** đại diện cho quyền của người sở hữu (owner), **g** đại
  diện cho quyền của nhóm (group) và **o** đại diện cho quyền của mọi
  người dùng khác (others).

- Ký tư “**+**” có ý nghĩa gán thêm quyền, “**-**“ có ý nghĩa rút bớt
  quyền và “**=**” có nghĩa là gán.

Ví dụ:

\#chmod 755 File.txt

\#chmod -R go+rw /var/www

- Lệnh **chown**: thay đổi quyền sở hữu của file hoặc folder

Cấu trúc lệnh:

***chown \[Options\] Owner file***

Option -R

Owner: Người sở hữu mới trên tập tin.

- Thay đổi owner của file (chủ sở hữu của file), lệnh cơ bản sẽ như sau:

> chown user filename(s)

- Thay đổi quyền group owner:

> chown user\[:group\] filename(s)

- Thay đổi owner, group cho toàn bộ thành phần thư mục

> Chown -R user:group \<directory\>

1.  **Umask, SUID, SGID & sticky bit**

- **Umask**

<!-- -->

- Directory: umask value = 777 (max initial dir mode) – quyền truy xuất
  yêu cầu (vd:755)

- File: umask value = 666 (max initial file mode) – quyền truy xuất yêu
  cầu

<!-- -->

- **Special Bits on files**

<!-- -->

- Set user ID (SUID): run as user owner of the file

- Set group ID (SGID): run as group owner of the file

- Sticky Bit: remain on swap, not functional on files

- SUID=4; SGID = 2; sticky =1

  - Set SUID: chmod 4755 /usr/bin/su

> Chmod u+s /usr/bin/su

- Set SGID: chmod 2755 /usr/bin/screen

> Chmod g+s /usr/bin/screen

- **Special Bits on Directories**

<!-- -->

- SGID: providing group inheritance for files and directories created
  inside the directory

- Sticky bit: only owners or root can delete their own files

> \# chmod 1777 stickydir
>
> \# cd stickydir – touch file.txt
>
> \# chmod 777 file.txt
>
> \# su – user
>
> \# rm file.txt – operation not permitted
