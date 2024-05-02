**PAM & NIS**

1.  **Pluggable Authentication Modules (PAM).**

<!-- -->

1.  **GIỚI THIỆU DỊCH VỤ PAM**

- Mỗi ứng dụng có một kiểu xác thực =\> phức tạp hệ thống.

- Cung cấp một phương thức xác thực tập trung.

- Ứng dụng không trực tiếp xác thực, mà chuyển request cho PAM, yêu cầu
  xác thực.

- PAM làm việc và trả về kết quả xác thực cho ứng dụng.

- Ứng dụng quyết định cho phép user login hay không.

- Theo cách hiểu của Windows, PAM đóng vai trò như DLL (dynamic link
  library) đối với các ứng dụng khác.

- Theo cách hiểu của Linux, PAM là một thư viện.

- PAM cung cấp nhiều module xác thực **/lib/security** từ đơn giản đến
  phức tạp.

- Khi ứng dụng cần xác thực theo phương thức nào thì gọi phương thức đó
  của trong thư viện của PAM.

- Thông tin về các module xác thực của PAM: **man \[pam_module\]**

2.  **KIẾN TRÚC PAM**

> <img src="media/image1.png" style="width:4.03505in;height:3.39067in" />
>
> <img src="media/image2.png" style="width:4.60924in;height:3.29278in" />

3.  **CẤU HÌNH PAM**

- **/lib/security:** những module xác thực của PAM.

- **/etc/security**: file cấu hình tương ứng của từng module xác thực
  của PAM.

- **/etc/pam.d**: file cấu hình của những ứng dụng sử dụng PAM xác thực.

=\> mỗi ứng dụng xác thực bằng PAM có một file cấu hình trong
**/etc/pam.d**

**module_type control_flag module_path arguments**

- **module_type:** nhận một trong 4 giá trị: auth, account, session,
  password.

- **control_flag:** cấu hình cách xử lí của ứng dụng với kết quả xác
  thực do PAM trả về.

- **module_path**: đường dẫn cụ thể của module xác thực.

- **arguments**: các tham số khác.

<!-- -->

- MODULE_TYPE:

<!-- -->

- **Auth**: Là module chịu trách nhiệm cho mục đích xác thực. Nó xác
  minh mật khẩu.

- **Account**: Sau khi người dùng đã xác thực bằng thông tin chính xác,
  phần account sẽ kiểm tra tính hợp lệ của tài khoản như hạn chế đăng
  nhập hoặc thời gian đăng nhập,...

- **Password**: Được sử dụng để thay đổi mật khẩu.

- **Session**: Quản lý các session, chứa tài khoản hoạt động của người
  dùng, tạo hộp thư, tạo thư mục chính của người dùng,...

<!-- -->

- CONTROL_FLAG:

<!-- -->

- **Required**: Module phải chứng thực thành công, nếu không kết quả
  fail sẽ được gởi về..

- **Requisite**: Nếu module này fail, kết quả sẽ được trả về ngay lập
  tức, không sử dụng đến các module sau..

- **Sufficient**: Nếu module này thành công, và không có module required
  nào nữa, kết quả thành công sẽ được trả về.

- **Optional**: Cho phép tiếp tục kiểm tra module khác, dù module này bị
  fail.

<!-- -->

- ARGUMENT:

<!-- -->

- **Debug**: Log lại thông tin debug.

- **no_warn**: Không gởi msg waring đến ứng dụng

- **use_first_pass**: Lưu lại password, để sử dụng cho lần xác thực sau.

- **try_first_pass**: Giống option trên, tuy nhiên nếu password fail,
  yêu cầu user nhập lại.

> Dùng lệnh man \[pam_module\] để tìm hiểu về từng module xác thực:  
> • Vd: man pam_nologin
>
> \# more /etc/pam.d/password-auth
>
> <img src="media/image3.png" style="width:5.45525in;height:1.93804in" />
>
> **Installation & Configuration**

1.  **Kiểm tra ứng dụng có hỗ trợ PAM**:

Để có thể sử dụng được PAM thì một ứng dụng hoặc một chương trình cần
phải được chương trình hỗ trợ PAM, nó cần được viết và biên dịch cụ thể
để sử dụng PAM, kiểm tra xem đã được biên dịch với thư viện PAM bằng
lệnh **ldd**

> **\# ldd /usr/sbin/sshd \| grep libpam.so**

Nếu chương trình có hỗ trợ PAM thì trong đầu ra tồn tại tệp
**lipbpam.so** xác nhận truy vấn.

2.  **Kiểm tra cấu hình PAM**

> Kiểm tra cấu hình PAM trong thư mục **/etc/pam.d/\***
>
> **\# cd /etc/pam.d/**
>
> **\# ls**
>
> **\# more sshd**
>
> **Module type control-flag module-path module-arguments**
>
> Trong đó:**  
> Module:** Tên của ứng dụng hoặc dịch vụ.**  
> type:** Loại module type/context/interface.**  
> control-flag:** Cho biết nhiệm vụ của PAM-API nếu module không thành
> công trong việc xác thực.  
> **module-path:** Tên tệp tuyệt đối hoặc tên đường dẫn tương đối của
> PAM.**  
> module-arguments:** Danh sách mã được phân tách bằng dấu cách để kiểm
> soát module.
>
> Các phần trong mã được phân tách với nhau bằng dấu **Tab**

3.  **Tìm hiểu các module PAM**

    1.  **pam_succeed_if Module**

- Module này cho phép truy cập cho các nhóm được chỉ định. Chúng ta có
  thể xác thực tài khoản người dùng như bên dưới:

> ***auth required pam_succeed_if.so gid=1000,2000*** -- chỉ những người
> dùng trong nhóm có ID 1000 hoặc 2000 mới được phép đăng nhập.

- Chúng ta cũng có thể sử dụng **uid** thay thế **id** người dùng:

> ***auth requisite pam_succeed_if.so uid \>= 1000*** -- chỉ cho người
> dùng có uid \>1000 mới đc phép đăng nhập

- Chúng ta cũng có thể kết hợp **pam_succeed_if** cùng với tham số
  **ingroup** như sau:

> ***auth required pam_succeed_if.so user ingroup \<group\>*** -- Chỉ
> những người dùng có trong nhóm **\<group\>** mới có thể đăng nhập.

2.  **pam_access Module**

- Module này hoạt động giống như **pam_succeed_if module** ngoại trừ
  **pam_access module** kiểm tra việc ghi nhật ký từ các máy chủ được
  nối mạng

> \#account required pam_access.so accessfile=/etc/security/access.conf

- Chúng ta có thể thiết lập quy tắc bằng trình soạn thảo **vi** tại:

> \#vi /etc/security/access.conf

- Chỉnh sửa tập tin như sau:

  - **+**:pnh

  - **-**:ALL:ALL

  - Các thiết lập trên chỉ cho những user thuộc **pnh** mới được phép
    đăng nhập.

- Trong đó:

  - **+**: Cho phép đăng nhập.

  - -: Không cho phép đăng nhập.

  2.  **pam_unix Module**

- Module này được sử dụng để kiểm tra thông tin đăng nhập của người dùng
  đối với file **/etc/shadow.**

  - auth required pam_unix.so

  2.  **pam_localuser Module**

- Module này dùng để kiểm tra xem user có được liệt kê trong
  **/etc/shadow**

  - account sufficient pam_localuser.so

  2.  **pam_cracklib Module**

- Module này đảm bảo rằng chúng ta sẽ sử dụng mật khẩu mạnh.

  - password required pam_cracklib.so retry=4 minlen=12 difok=6

- Các thông số trên có ý nghĩa như sau:

  - Độ dài mật khẩu tối thiểu = 12

  - Bốn lần để chọn một mật khẩu mạnh, nếu không nó sẽ thoát.

  - Mật khẩu mới của chúng ta phải có 6 ký tự mới từ mật khẩu cũ.

  2.  **pam_cracklib Module**

- Module được sử dụng để đặt giới hạn cho tài nguyên hệ thống, user
  **root** cũng bị ảnh hưởng bởi các giới hạn này.

- Các cấu hình giới hạn là trong: \#vi /etc/security/limits.conf

  - Có dạng như sau: session required pam_limits.so

- Chúng ta có thể sử dụng để bảo vệ tài nguyên hệ thống.

- Các giới hạn trong tệp **/etc/security/limits.conf** có thể hard hoặc
  mềm.

  - **Hard**: Người dùng không thể thay đổi giá trị của nó, nhưng
    **root** có thể.

  - **Soft**: Người dùng bình thường có thể thay đổi nó.

- Ví dụ thay đổi **max-open-file** của một user **pnh**:

> \#vi /etc/security/limits.conf
>
> \## Example hard limit for max opened files  
> ***pnh hard nofile 4096***  
> \## Example soft limit for max opened files  
> ***pnh soft nofile 1024***
>
> Kiểm tra sau khi khai báo:
>
> su pnh
>
> su –Hn
>
> ulimit –Sn

2.  **Cách hạn chế quyền truy cập root vào dịch vụ SSH qua PAM**

- Chúng ta sẽ định cấu hình bằng cách sử dụng PAM để vô hiệu hóa quyền
  truy cập của người dùng root vào hệ thống thông qua SSH và các chương
  trình đăng nhập.

- Chúng ta có thể sử dụng module **/lib/security/pam_listfile.so** để
  giới hạn các đặc quyền của các tài khoản cụ thể

- vi /etc/pam.d/sshd

- Trong đó

  - **auth**: Là loại module.

  - **required**: Điều kiện cần thiết, nhưng nếu module không tải được
    vì bất kỳ lý do gì, nó tiếp tục tải các module khác và trả về thất
    bại khi kết thúc thực thi.

  - **pam_listfile.so**: Module cung cấp cách từ chối hoặc cho phép các
    dịch vụ dựa trên một tệp tùy ý.

  - **onerr=succeed**: Đối số Module

  - **item = user**: Đối số module chỉ định nội dung được liệt kê trong
    tệp và cần được kiểm tra.

  - **sense=deny**: Đối số module chỉ định hành động sẽ thực hiện nếu
    được tìm thấy trong tệp.

  - **file=/etc/ssh/deniedusers**: Đối số module chỉ định tệp chứa một
    item trên mỗi dòng

- Thực hiện tạo tập tin **/etc/ssh/deniedusers** và thêm user **root**
  vào:

> \# vi /etc/ssh/deniedusers
>
> \# chmod 600 /etc/ssh/deniedusers

- Các quy tắc trên sẽ yêu cầu **PAM** tham khảo tệp
  **/etc/ssh/deniedusers** và từ chối quyền truy cập vào **SSH** và các
  dịch vụ đăng nhập cho bất kỳ người dùng được liệt kê trong file này.

- Thử đăng nhập bằng user root đã được denied: ssh@\<localhost\>

  2.  Cấu hình chính sách an toàn cho mật khẩu:

- Tất cả các thiết lập về mật khẩu an toàn trên Linux đều được lưu tại
  **/etc/login.defs**, mở file **/etc/login.defs** và thực hiện các
  chính sách về mật khẩu

  - vi /etc/login.defs

- Với thiết lập này thì các users phải thay đổi mật khẩu của họ khi mật
  khẩu dùng tới giới hạn **60 ngày** mà chúng ta đã thiết lập.
  PASS_MAX_DAYS 60

- Với thiết lập này thì khi bạn thay đổi mật khẩu hay đặt mật khẩu cho
  user, mật khẩu đó sẽ tồn tại trong khoảng thời gian **2 ngày**, mà
  chúng ta quy định sau đó mới có thể đổi mật khẩu: PASS_MIN_DAYS 2

- Giới hạn mật khẩu đã được đặt trước đó: \# **vi
  /etc/pam.d/password-auth**

*pam_unix.so sha512 shadow nullok try_first_pass use_authtok remember=5*

- Thiết lập độ dài ngắn nhất của mật khẩu:

  - **authconfig --passminlen=8 –update**

- Thiết lập độ phức tạp của mật khẩu theo lớp:

  - **authconfig --passminclass=2 –update**

- Thiết lập số ký tự lặp lại:

  - **authconfig --passmaxrepeat=2 –update**

- Thiết lập có ít nhất một ký tự thường:

  - **authconfig --enablereqlower –update**

- Thiết lập có ít nhất một ký tự hoa:

  - **authconfig --enablerequpper –update**

- Thiết lập có ít nhất 1 ký tự số:

  - **authconfig --enablereqdigit –update**

2.  **NIS Server**

<!-- -->

1.  **Giới thiệu NIS**

- **Network Information Services (NIS):** Cho phép tạo tài khoản và quản
  lý chứng thực người dùng tập trung

- NIS được xây dựng trên mô hình **client-server**. Một server NIS là
  một host mà chứa các file dữ liệu NIS, gọi là maps. Client là những
  host truy vấn thông tin từ các maps này.

- Một lợi thế của NIS là người sử dụng cần phải thay đổi mật khẩu của
  mình duy nhất trên máy chủ của NIS, thay vì mỗi hệ thống trên mạng

- NIS không mã hóa các thông tin tên người dùng và mật khẩu khi các máy
  client đăng nhập và tất cả người dùng có thể truy cập các mật khẩu mã
  hóa được lưu trữ trên máy chủ của NIS

- Dữ liệu có thể lưu trữ trong NIS là những dữ liệu text.

  - /etc/passwd, /etc/hosts, /etc/services, /etc/protocol…

  - Những dữ liệu text này cách nhau bằng “tab”, và có ít nhất một cột
    có giá trị duy nhất trên mỗi dòng.

<img src="media/image4.png" style="width:5.59329in;height:3.87314in" />

2.  **KIẾN TRÚC HỆ THỐNG NIS**

<img src="media/image5.png" style="width:5.33221in;height:3.24705in" />

3.  **CÀI ĐẶT DỊCH VỤ NIS**

- NIS được cài đặt gói bằng gói **rpm**, hoặc **source**:

  - **ypserv-\[version\].rpm**

- Server có các daemon sau:

  - **ypserv**: lắng nghe truy vấn từ client, và trả lời cho những truy
    vấn này.

  - **ypxfrd**: transfer những thay đổi từ NIS master sang NIS slave.

- Daemon của client:

  - **ypbind**: tìm kiếm NIS server để gởi truy vấn.

- Để NIS server có thể hoạt động được, đầu tiên cần khởi tạo dữ liệu cho
  NIS server bằng tiến trình **ypinit**.

- File **/var/yp/Makefile**: quyết định những dữ liệu nào NIS server sẽ
  hỗ trợ.

- Khi cần update dữ liệu của NIS server, sử dụng lệnh: **/var/yp/make**

- Client có thể sử dụng những **tools** sau để truy vấn từ NIS server:

  - **ypcat**: dump nội dung một bảng map của NIS server.

    - ***ypcat passwd***

  - **ypwhich**: cho biết NIS server nào đang phục vụ request

    - ***ypwhich***

  - **ypmatch:** truy vấn dữ liệu bảng map của NIS match một từ khóa nào
    đó

    - ***ypmatch test passwd***

**Installation & Configuration**

<img src="media/image6.png" style="width:5.5926in;height:2.60002in" />

1.  **Cài đặt NIS SERVER**

- Cài đặt **Ypserv** và cấu hình NIS server

  - yum –y install ypserv rpcbind

  - ypdomain \<domain_name\>

  - echo “NISDOMAIN=\<domain_name\>”\>\>/etc/sysconfig/network

  - more /etc/sysconfig/network

- Khai báo hostname cho NIS server

  - vi /etc/hosts

- Khai báo dải IP được quyền truy cập đến NIS server

  - vi /var/yp/securenets

- enable service

  - systemctl enable --now rpcbind ypserv ypxfrd yppasswd nis-domainname

  - /usr/lib64/yp/ypinit –m

- Nếu thêm local user hoặc local group, hosts mới trong **/etc/hosts**
  của NIS Server thì  
  thực hiện chạy lệnh sau để cập nhật dữ liệu mới:

  - cd /var/yp/

  - make

- Nếu selinux on thì thực hiện hai cách, một là disable hai là thực hiện
  như sau:

  - setsebool –P nis_enabled_on

  - setsebool –P domain_can_mmap_files on

- Thực hiện **fix port** cho dịch vụ NIS và **mở port** này trên
  firewall, nếu trên server có chạy dịch vụ **firewalld**

  - vi /etc/sysconfig/network

> <img src="media/image7.png" style="width:3.19262in;height:1.58494in" />

- vi /etc/sysconfig/yppasswd

> <img src="media/image8.png" style="width:5.70499in;height:0.48696in" />

- systemctl restart rpcbind ypserv ypxfrd yppasswd

2.  **Cài đặt NIS CLIENT**

- Cấu hình Ybind và cấu hình NIS Client

  - yum –y install ypbind rpcbind oddjob-mkhomedir

  - ypdomainname \<domain_name\>

  - echo “NISDOMAIN=\<domain_name\>” \>\> /etc/sysconfig/network

- config

  - vi /etc/yp.conf

    - domain \<NIS domain\> server \<NIS server\>

- enable NIS service

- see NIS documentation \#authselect select nis --force

- Thực hiện tạo account trên NIS Server

  - useradd \<user\>

  - passwd \<user\>

- update dữ liệu

  - cd /var/yp/

  - Make

- thực hiện đăng nhập account đó trên NIS Client.

  - su \<user_test\>

  - who

  - pwd

  - su \<user\>

  - su \<user_test\>

  - pwd

3.  **Cài đặt NIS SLAVE server**

- Cài đặt **Ypserv** trên NIS Slave Server.

  - yum –y install ypserv rpcbind

- Cấu hình **Ypserv** trên NIS Slave Server.

  - ypdomainname \<domain_name\>

  - echo “NISDOMAIN=\<domain\>” \>\> /etc/sysconfig/network

  - vi /var/yp/securenets

- Khởi tạo service

  - systemctl start rpcbind ypserv ypxfrd yppasswd

  - systemctl enable rpcbind ypserv ypxfrd yppasswd

- Cấu hình thêm Slave server trên NIS Server

  - /usr/lib64/yp/ypinit –m

- Thực hiện cấu hình NIS client truy vấn cả NIS Slave

  - vi /etc/yp.conf

> domain \<name\> server \<slave_name\>

- systemctl restart ypbind

[An introduction to Pluggable Authentication Modules (PAM) in Linux \|
Enable Sysadmin
(redhat.com)](https://www.redhat.com/sysadmin/pluggable-authentication-modules-pam)
