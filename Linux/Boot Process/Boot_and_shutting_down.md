**Boot and shutting down**

Booting Linux

> <img src="media/image1.png" style="width:3.93656in;height:3.43005in"
> alt="Diagram Description automatically generated" />
>
> <img src="media/image2.png" style="width:5.06853in;height:4.30652in" />

1.  **QUÁ TRÌNH KHỞI ĐỘNG LINUX**

    1.  **<u>BIOS</u>**

- BIOS là chương trình chạy đầu tiên khi nhấn nút nguồn hoặc nút reset
  trên máy tính của bạn.

- BIOS thực hiện một công việc gọi là POST ( Power-on Self-test) kiểm
  tra các thông số của các phần cứng của máy tính.

- BIOS được lưu trữ trên ROM của bo mạch chủ.

- Quá trình POST kết thúc thành công, BIOS sẽ tìm kiếm và khởi chạy một
  hệ điều hành được chứa trong các thiết bị lưu trữ như ổ cứng…

- Hệ điều hành Linux được cài trên ổ cứng thì BIOS sẽ tìm đến MBR
  (Master Boot Record)

  1.  **<u>MBR</u>**

- **MBR (Master Boot Record)** được lưu trự tại Sector đầu tiên của một
  thiết bị lưu trữ dữ liệu, ví dụ **/dev/hda** hoặc**/dev/dsa**/. MBR
  rất nhỏ chỉ 512 byte.

- **MBR** chứa thông tin:

  - Primary boot loader code (446 Bytes): Cung cấp thông tin boot loader
    và vị trí boot loader trên ổ cứng

  - Partition table information (64 Bytes): Lưu trữ thông tin của các
    partition

  - Magic number (2 Bytes): được sử dụng để kiểm tra MBR, nếu MBR bị lỗi
    thì nó sẽ phục hồi lại.

  1.  **<u>BOOT LOADER</u>**

- Trong giai đoạn này GRUB (Grand Unified Bootloader) nằm trong 30
  kilobyte đĩa cứng đầu tiên ngay sau MBR được nạp vào RAM để đọc cấu
  hình của nó và hiển thị menu khởi động GRUB.

- GRUB có nghiệm vụ sẽ tải kernel do người dùng chọn vào bộ nhớ và
  chuyển điều khiển sang kernel. Nếu người dùng không chọn HĐH, sau khi
  hết thời gian xác định, GRUB sẽ tải kernel mặc định trong bộ nhớ để
  khởi động nó.

- File cấu hình **grub.conf**:

> <img src="media/image3.png" style="width:5.06109in;height:3.53079in"
> alt="Table Description automatically generated" />

1.  **<u>INIT</u>**

- Đây là giai đoạn chính của quá trình BOOT.

- Quá trình này bắt đầu bằng việc đọc file **/etc/inittab** để xác định
  runlevel. Sau đó sẽ thực thi các script tương ứng với runlevel.

  1.  **<u>USER PROMT, RUN LEVEL</u>**

- User prompt: người dùng đăng nhập để sử dụng

- Run levels là chế độ sử dụng của Server. Mỗi chế độ có những module,
  chức năng hoạt động riêng:

> <img src="media/image4.png" style="width:5.48933in;height:3.4749in"
> alt="Text Description automatically generated" />

2.  **KERNEL, IMAGE VÀ INITRD**

- Kernel image là hình ảnh nhỏ nhất của kernel được nén thành file
  **vmlinuz-version.tar.gz.**

- Kernel image chứa những thành phần quan trọng cần thiết đầu tiên để
  boot máy tính.

- **initrd** – initial ram disk: được sử dụng để detect phần cứng và
  load driver.

- Đồng thời mount file systems dưới dạng read only để tiến hành kiểm
  tra.

3.  **TIẾN TRÌNH SYSTEMD**

- Đối với các bản Linux hiện đại như CentOS 7, RHEL 7 gần đây thì init
  và runlevel được thay thế bởi systemd và cũng thực hiện nhiệm vụ tương
  ứng.

- Systemd đọc tệp liên kết bởi **/etc/systemd/system/default.target** để
  xác định đích hệ thống mặt định.

- Systemd sẽ bắt đầu mọi thứ trong **/etc/systemd/system/basic.target**
  trước khi bắt đầu multi-user service.

- Systemd sử dụng mục tiêu thay vì runlevel. Systemd có hai mục tiêu
  chính: multi-user.target và graphical.target tương ứng với runlevel 3
  và runlevel 5.

- Để xem các mục tiêu mặc định hiện tại chúng ta chạy lệnh: systemctl
  get-default

- Để đặt mục tiêu mặt định chúng ta chạy lênh: **systemctl set-default
  TARGET.target**

- Tiến trình systemd thực thi những nhiệm vụ sau:

  - Thiết lập **hostname** của máy tính và detect **môi trường
    network**.

  - Mount **/proc** file system.

  - Thiết lập các tham số của kernel.

  - Thiết lập giờ hệ thống, fonts.

  - Khởi tạo phân vùng swap.

  - Check file system và mount lại ở mode read-write.

  - Load những module cần thiết.

4.  **/ETC/RC.D/RC SCRIPTS**

- Thực thi tất cả script liên quan đến run level đó.

- Vd: nếu runlevel là 5, sẽ gọi thực thi các script trong
  /etc/rc.d/rc5.d

- Các script này là file symbolic link, link đến các script thật sự,
  thường chứa trong /etc/init.d.

> <img src="media/image5.png" style="width:3.22395in;height:1.13023in"
> alt="Graphical user interface, text, application, chat or text message Description automatically generated" />

5.  **SHUTTING DOWN LINUX**

> <img src="media/image6.png" style="width:5.20373in;height:4.00002in"
> alt="Diagram Description automatically generated" />

6.  **LAB**

    1.  **<u>Boot Manager với Grub</u>**

        1.  **Xem file cấu hình grub**

> <img src="media/image7.png" style="width:5.87795in;height:2.43059in"
> alt="Text, letter Description automatically generated" />
>
> Ý nghĩa một số tham số:
>
> \- **default**: Chọn hệ điều hành tự động boot vào nếu người dùng
> không chọn từ menu boot.
>
> \- **timeout**: Thời gian chờ người dùng chọn hệ điều hành. Thời gian
> này tính bằng giây.
>
> \- **splashimage**: File image hiển thị tại menu boot.
>
> \- **hiddenmenu**: Ẩn menu boot.
>
> \- **title**: Tiêu đề của HĐH trên menu boot.
>
> \- **root**: Partition và ổ đĩa của HĐH khởi động.
>
> \- **kernel**: Đường dẫn chỉ đến kernel image.
>
> \- **initrd**: Cho phép load kernel modules từ một image.

2.  **Thêm một kernel mới vào boot menu:**

> <img src="media/image8.png" style="width:5.61918in;height:0.97975in"
> alt="Text Description automatically generated" />
>
> <img src="media/image9.png" style="width:5.56051in;height:2.94719in"
> alt="Text Description automatically generated" />

2.  **<u>Kiểm tra các starup service được đặt trong /etc/rc.d</u>**

> <img src="media/image10.png" style="width:5.96923in;height:0.65368in" />

3.  **Quản lý các dịch vụ khi khởi động**

- Kiểm tra danh sách các service được nạp vào khi khởi động

> \#systemctl list-units –type=service

- Kiểm tra các service đang active/running

> \# systemctl list-units –type=service –state=active

- Kiểm tra một service cụ thể

> \# systemctl status \<service\>

- Thực hiện disable/enable một service

> \# systemctl disable \<service\>
>
> \# systemctl enable \<service\>

- Thực hiện bật/tắt/khởi động lại một service

> \# systemctl start \<service\>
>
> \# systemctl stop \<service\>
>
> \# systemctl restart \<service\>
