**Active Directory**

1.  Định nghĩa

- Quản lý tập trung, lưu trữ thông tin tài nguyên hệ thống mạng trên
  toàn bộ domain.

- Lưu trữ data dưới dạng Object. Mỗi Object sẽ là một thành phần đơn lẻ,
  như user, group, ứng dụng hoặc thiết bị

2.  AD DS

- Service chính trong Active Directory là Domain Service (AD DS), lưu
  trữ các thông tin thư mục và xử lý tương tác giữa user và domain.

- Xác thực truy cập khi một user đăng nhập thiệt bị hoặc tìm cách kết
  nối với server thông qua 1 network.

- Kiểm soát user nào được truy cập vào tài nguyên nào

3.  **Domain Controllers**

- Server lưu trữ AD DS chính là domain controller

- Có nhiệm vụ lưu trữ và phân phối dung lượng lưu trữ cho tất cả user
  trong hệ thống

4.  **Thành phần đơn vị**

    1.  Forests

    - Nhóm các đối tượng, các thuộc tính và cú pháp thuộc tính trong
      Active Directory

    - Một forest có thể gồm nhiều miền, mỗi miền lại chia sẻ một lược đồ
      chung.

    2.  Domain

    - Nhóm các máy tính chia sẻ một tập chính sách chung, tên và một cơ
      sở dữ liệu của các thành viên của chúng.

    - Phục vụ như các mục trong chính sách bảo mật và các nhiệm vụ quản
      trị

- Admin có thể quản lý tất cả các đối tượng bên trong một Domain

  - AD yêu cầu một hoặc nhiều domain để hoạt động. Một miền phải có một
    hoặc nhiều máy domain controller (DC)

    - lưu cơ sở dữ liệu

    - duy trì các chính sách

    - cung cấp sự thẩm định cho các đăng nhập vào domain

  1.  Organizational unit (OU)

  - Nhóm các mục trong miền nào đó, tạo nên một kiến trúc thứ bậc cho
    miền

    - linh hoạt hơn và cho phép quản lý dễ dàng hơn so với các miền

    - có thể chuyển, xóa và tạo các OU mới

  2.  Sites

  - Nhóm vật lý những thành phần độc lập của miền và cấu trúc OU, định
    nghĩa bởi một hoặc nhiều IP subnet

    - chứa các IP subnet có các liên kết truyền thông tin cậy và nhanh
      giữa các host

    - kiểm soát và giảm số lượng lưu lượng truyền tải trên các liên kết
      WAN chậm

5.  **Thành phần**

    1.  Attribute (thuộc tính)

    - thuộc tính mô tả một đối tượng

      - mật khẩu và tên là thuộc tính của đối tượng người dùng mạng

      - một máy in và một máy trạm, cả hai đều có một thuộc tính là địa
        chỉ IP

    - Các đối tượng khác nhau có danh sách thuộc tính khác nhau, tuy
      nhiên các đối tượng khác nhau cũng có thể có một số thuộc tính
      giống nhau

    2.  Schema (cấu trúc tổ chức)

    - Định nghĩa danh sách các thuộc tính dùng để mô tả một loại đối
      tượng

    - các thuộc tính dùng để định nghĩa một lớp đối tượng có thể sửa đổi
      được

    3.  Container (vật chứa)

    - Chứa các đối tượng và các vật chứa khác

    - Vật chứa cũng có các thuộc tính như đối tượng mặc dù vật chứa
      không thể hiện một thực thể thật sự nào đó như đối tượng

    - 3 loại container

      - Domain

      - Site

      - OU (Organizational Unit)

    4.  Global catalog (GC)

    - GC lưu trữ tất cả các object của miền chứa GC & một phần các
      object thường được user tìm kiếm của các domain khác trong forest

    - Global catalog lưu trữ

      - thuộc tính thường dùng trong việc truy vấn như user’s first
        name, last name, logon name

      - thông tin cần thiết để xác định vị trí của bất kỳ object nào
        trong AD

      - Tập hợp các thuộc tính mặc định cho mỗi loại object

      - Quyền truy cập đến mỗi object

    - Global catalog server

      - một Domain Controller lưu trữ tất các AD object trong một forest

      - Global catalog nằm trên DC đầu tiên khi triển khai Domain

6.  **Triển Khai**

    1.  Add roles & features:

    - AD DS

    2.  Promote to DC

    - Add a domain controller to an existing domain

    - Add a new domain to an existing forest

    - Add new forest

    3.  Đăng nhập với quyền Administrator trong môi trường Domain
        Controller

    4.  DNS

    - Forward Lookup Zone

      - Server Manager \> Mục Tools \> Chọn DNS

      - Forward Lookup Zones

      - kiểm tra và đảm bảo có đầy đủ 06 Folder

    - Reverse Lookup Zones

      - New Zone

      - Zone Type giữ nguyên mặc định chọn Next (3 lần)

      - khai báo đường mạng Network ID

7.  **Additional Domain Controller**

> Nếu trong hệ thống mạng chỉ có một Domain Controller thì thiết bị
> Server này có thể bị quá tải khi số lượng người dùng yêu cầu chứng
> thực tăng cao
>
> Bên cạnh đó trường hợp khi Domain Controller này bị lỗi thì toàn bộ hệ
> thống sẽ bị ngưng hoạt động, người dùng sẽ không thể chứng thực trong
> hệ thống mạng Domain.
>
> Dịch vụ Additional Domain Controller được triển khai đáp ứng một số
> nhu cầu sau:

- Trong hệ thống mạng doanh nghiệp có nhiều Site. Tại từng Site khác
  nhau có thể triển khai dịch vụ Additional Domain Controller để chứng
  thực cho người dùng tại từng Site khác nhau. Thay vì phải chứng thực
  thông qua đường truyền VPN kết nối các Site.

- Load Balancing: Giảm tải việc chứng thực trong hệ thống.

Trong hệ thống có 2 Domain Controller trở lên sẽ giúp cho việc chứng
thực diễn ra nhanh hơn. Không phụ thuộc quá nhiều vào PDC. Tránh tình
trạng nghẽn mạng.

- Failover: Trong hệ thống mạng việc chứng thực được diễn ra trên Domain
  Controller vì vậy khi thiết bị giữ vai trò DC gặp sự cố dẫn đến hệ
  thống hoạt động không ổn định.

Việc chứng thực diễn ra thất bại. Việc xây dựng ADC giúp đề phòng rủi ro
cho dịch vụ AD trong hệ thống.
