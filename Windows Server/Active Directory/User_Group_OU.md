**User, Group, OU**

1.  **Mô Hình**

    1.  Workgroup

- Peer to Peer, các máy tính có vai trò như nhau được kết nối thông qua
  mạng LAN

- Các dữ liệu tài nguyên của user được lưu & tự chứng thực ngay trên máy
  cục bộ

- không có máy tính đảm nhiệm cài đặt các dịch vụ và quản lý hệ thống
  mạng

- bảo mật sẽ không được cao và tin cậy

<!-- -->

- Phù hợp doanh nghiệp nhỏ, phòng NET, hệ thống mạng gia đình

  1.  Domain

<!-- -->

- Client-Server, có ít nhất một máy tính làm Domain Controller

- điều khiển toàn bộ hoạt động của hệ thống mạng = AD

- Bảo mật & tin cậy cao =\> công ty, doanh nghiệp vừa và lớn

2.  **Tài khoản User**

    1.  User Account

- tài khoản người dung, Admin sẽ tạo ra User và phân quyền, cấp phát cho
  user

- 1 số user được tạo ra mặc định khi cài AD, Administrator là quyền quản
  trị cao nhất trong hệ thống , user này không thể gỡ bỏ

  1.  Local User Account

- tài khoản người dùng được định nghĩa trên máy tính Local

- chỉ được phép Log on trên máy tính đó

  1.  Domain User Account

- tài khoản người dùng được định nghĩa trên AD, được phép Log on trên
  toàn mạng

- được phép truy cập các tài nguyên trong hệ thống mạng dưới sự phân
  quyền của Admin

  1.  Yêu cầu về tài khoản

- từ 1-20 kí tự

- không được phép trùng nhau

- không chứa các kí tự ” / \\ \] \[ : : = + ? \> \< ”

- có thể chứa các kí tự đặc biệt như dấu chấm , khoảng trắng , dấu gạch
  ngang , dấu gạch dưới

3.  **Tài khoản Group**

    1.  Security group

- cấp phát các quyền hệ thống và quyền truy cập

- 3 loại:

  - Local: Nhóm trên máy Stand-alone Server, các máy ở dạng workgroup,
    chỉ hoạt động trên các máy cục bộ

  - Global: Nhóm này nằm trên máy DC được tạo ra trong AD, cấp phát
    những quyền quan trọng như quyền hệ thống & quyền truy cập vượt qua
    1 quan hệ Domain

  - Universial: Có chức năng gần giống Global, cấp quyền cho các đối
    tượng trên khắp các domain trên 1 Forest hoặc trong các domain có
    mối liên hệ với nhau

  1.  Distribution group

- nhóm phi bảo mật

- không được dùng bởi Admin, được dùng bởi các Dev

**Group Policy**

- tập hợp các thiết lập cấu hình cho Computer và Users , xác định cách
  thức để các chương trình , tài nguyên mạng và hệ điều hành làm việc
  với người dùng và máy tính trong 1 tổ chức 

- Mục đích sử dụng GPO nhằm triển khai các chính sách từ miền máy chủ
  Domain Controller xuống Users 

- Các Group Policy có thể dùng để triển khai cài đặt phần mềm xuống các
  máy trạm trong miền một cách tự động. Dùng để ấn định các quyền hạn
  cho người dùng trong mạng .

-  Các chính sách nhóm được áp dụng cho các đối tượng như Site , domain,
  OU được gọi là GPO ( Group Policy Objects)

- Các Group Policy Objects được lưu trữ trong cơ sở dữ liệu của Active
  Directory. Chương trình để tạo ra và chỉnh sửa GPO có tên là Group
  Policy Object Editor. Console: gpedit.msc

- Các GPO chỉ có thể hiện hữu trong miền Active Directory , GPO mất tác
  dụng đối với những máy client khi chúng được xóa khỏi miền

1.  **Thành phần**

> Khi cấu hình GPO, ta cấu hình trên máy Domain Controller, vào Server
> Manager / Tools / Group Policy Management.
>
> GPO bao gồm hai thành phần chính:

- Computer Configuration: Các thay đổi trong phần này sẽ áp dụng cho
  toàn bộ máy tính trong mạng

-  User Configuration: Cấu hình chính sách cho các tài khoản trong miền 

Và các thành phần con như: 

- Software Settings: Chính sách triển khai cài đặt phần mềm xuống Client
  tự động 

- Windows Settings: Tại đây chúng ta có thể tinh chỉnh , áp dụng các
  chính sách về vấn đề sử dụng tài khoản , quản lý khởi động và đăng
  nhập trên máy client

- Script ( Logon / Logoff) : Chỉ định cho Windows chạy 1 đoạn mã nào đó

- Name Resolution Policy: Các chính sách phân giải tên 

- Security Settings: Các thiết lập bảo mật cho hệ thống , thiết lập này
  áp dụng cho toàn bộ hệ thống chứ không riêng người nào

- Administrative Template: Các chính sách về hệ thống 

- Account Policies: Các chính sách áp dụng cho tài khoản người dung

- Local Policy**:** Kiểm định chính sách, những tùy chọn quyền lợi và
  chính sách an toàn cho người dùng cục bộ

- Public Key Policies. Các chính sách khóa dùng chung

2.  **Thành phần chi tiết**

    1.  **Account Policies:**

- **Password Policies:** Bao gồm các chính sách liên quan đến mật khẩu
  tài khoản của người sử dụng tài khoản trên máy

- **Enforce password history**

- **Maximum password age:** Thời gian tối đa mật khẩu còn hiệu lực, sau
  thời gian này hệ thống sẽ yêu cầu ta thay đổi mật khẩu

- **Minimum password age:** Xác định thời gian tối thiểu trước khi có
  thể thay đổi mật khẩu

- **Minimum password length:** Độ dài nhỏ tối thiểu của mật khẩu tài
  khoản

- **Password must meet complexity requirements**

- **Store password using reversible encryption fo all user in the
  domain:** Lưu trữ mật khẩu sử dụng mã hóa ngược cho tất cả các người
  sử dụng domain.

  1.  **Account lockout Policy**

- **Account lockout duration:** Xác định số phút còn sau khi tài khoản
  được khóa trước khi mở khóa

- **Account lockout threshold:** Xác định số lần cố gắng đăng nhập nhưng
  không thành công. Trong trường hợp này Account sẽ bị khóa

- **Reset account lockout counter after:** Thiết lập lại số lần cố gắng
  đăng nhập về 0 sau một khoảng thời gian quy định. Thiết lập này chỉ có
  hiệu lực khi *“Account lockout threshold”* được thiết lập

  1.  **Local Policy**

- **User rights Assignments:** Ấn định quyền cho người dùng.

- **Access this computer from the network**

- **Act as part of the operating system:** Chính sách này chỉ định tài
  khoản nào sẽ được phép hoạt động như một phần của hệ thống.

- **Add workstation to domain:** Thêm một tài khoản hoặc nhóm vào miền.
  Chính sách này chỉ hoạt động trên hệ thống sự dụng Domain Controller.

- **Adjust memory quotas for a process**: Chỉ định những ai được phép
  điều chỉnh chi tiêu bộ nhớ dành cho một quá trình xử lý.

- **Allow logon through Terminal Services:** Terminal services là một
  dịch vụ cho phép đăng nhập từ xa đến máy tính.

- **Backup files and directories**

- **Change the system time:** Cho phép người sử dụng nào có quyền thay
  đổi thời gian của hệ thống

- **Create global objects**: Cấp quyền cho ai có thể tạo ra các đối
  tượng dùng chung

- **Force shutdown from a remote system:** Cho phép ai có quyền tắt máy
  qua hệ thống điều khiển từ xa

- **Shutdown the system**

- **Deny access to this computer from the net**

- **Deny logon localy:** Cấm User Logon cục bộ

- **Deny logon through Terminal Services:** Cấm User Remote Desktop

- **Logon localy:** Thiết lập người dùng Logon cục bộ

3.  **Security Options**

- **Account: Administrator account status:** Trạng thái hoạt động của
  Administrator.

- **Account: Guest account status:** Trạng thái hoạt động của User
  Guest.

- **Account: Limit local account use of blank password to
  console:** Đăng nhập không cần password.

- **Account: Rename administrator account:** Đổi tên Administrator.

- **Account: Rename guest account**: Đổi tên Guest.

- **Devices: Prevent users from installing printer drivers:** Không cho
  phép cài Printer

- **Devices: Restrict CD-ROM access to localy logged-on user only:** Cấm
  truy nhập xa từ CD-ROM.

- **Interactive: Do not require CTRL + ALT + DEL:** Bỏ Ctrl + alt + Del

- **Interactive: Message text for users attempting to logon:** Đặt tiêu
  đề khi logon.

- **Interactive:  Message title for users attempting to log on:** Đặt
  tiêu đề khi logon

- **Interactive: Number of previous logons to cache in cache:** Cache
  kho logon

- **Shutdown:** Allow system to be shut down

- **Shutdown: Allow system to be shut down without having to log
  on:** Shutdown không cần logon.

- **Shutdown: Clear virtual memory pagefile.** Xóa bộ nhớ ảo khi
  Shutdown

**Chú ý : để triển khai các GPO xuống Client ta dùng lệnh ” gpupdate
/force ” trong CMD **
