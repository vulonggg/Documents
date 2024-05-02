**Capacity Planning**

1.  **<u>Giám sát CPU</u>**

> <img src="media/image1.png" style="width:5.02067in;height:3.13583in" />

- Khái niệm **load average**: giá trị này được thiết kế để mô tả CPU
  load.

> **\#uptime**

- Với một hệ thống single CPU (đơn CPU). Ví dụ:

  - load average=0.50⇒ 50% CPU được sử dụng trong khoảng thời gian đó.

  - load average=1.50⇒ CPU bị overtasked, các process requests bị kẹt ở
    queue vì CPU đang bận handling process khác.

- Với một hệ thống từ 2 CPUs (đa CPUs). Ví dụ:

  - load average=0.50⇒ 25% CPUs được sử dụng trong khoảng thời gian đó.

  - load average=1.50⇒ 75% CPUs được sử dụng trong khoảng thời gian đó.

- Công thức để tính tải trung bình của CPU:

> <img src="media/image2.png" style="width:3.32568in;height:0.67641in" />

- Công cụ để monitor CPU: **iostat**, **top**, **/proc/cpuinfo**..

<!-- -->

- Sử dụng câu lệnh **iostat** với **-c** option, sẽ cho ta kết quả thống
  kê liên quan tới việc sử dụng CPU từ thời điểm system boot.

- Phần đầu **output** của lệnh **iostat** cho biết một số thông tin:

<img src="media/image3.png" style="width:4.74178in;height:1.31532in" />

- Phần thứ hai cho biết thêm một số thông tin:

  - **%user** -- Giá trị này biểu diễn phần trăm CPU được sử dụng khi
    ứng dụng được chạy ở mức user-level (các processes chạy bởi tài
    khoản user bình thường)

  - **%nice** — Các câu lệnh thường xuyên được người dùng chạy bằng
    **nice**

> command để thay đổi ưu tiên proccess CPU

- **%system** — Giá trị này biểu diễn phần trăm CPU được sử dụng bởi các

> processes của kernel.

- **%iowait** — Giá trị này biểu diễn phần trăm CPU được sử dụng khi CPU
  đang chờ hoạt động disk I/O hoàn thành trước khi chuyển qua hành động
  kế tiếp.

- **%steal** — Giá trị này chỉ gắn liền với virtual CPUs. Trong một vài
  trường hợp, virtual CPU phải chờ hypervisor xử lý các requests từ
  virtual CPUs khác. Giá trị này chỉ ra phần trăm thời gian chờ
  hypervisor xử lý virtual CPU’s request.

- **%idle** — Giá trị này biểu diễn phần trăm thời gian CPU không xử lý
  bất kỳ request nào?

<!-- -->

- Ví dụ output của lệnh **iostat** với iowait cao:

<img src="media/image4.png" style="width:5.4271in;height:1.03288in" />

- **iostat** có 2 options thường rất hay được dùng là:

  - **interval**: Thời gian chờ (đơn vị: giây (s)) giữa những lần chạy
    lệnh **iostat**.

  - **count**: Số lần cần report.

<!-- -->

- Ngoài ra còn một số công cụ có thể dùng để giám sát CPU: **sar**,
  **mpstat**

2.  **<u>GIÁM SÁT MEMORY</u>**

- Một hệ thống được trang bị CPU tốc độ cao vẫn có thể trở nên trì trệ
  nếu như gặp vấn đề về bộ nhớ.

- Khi giám sát lượng bộ nhớ sử dụng, cần nhìn vào cả RAM và Swap space.

<img src="media/image5.png" style="width:5.68888in;height:0.79847in" />

- **Mem**: Dòng này mô tả về RAM

- **Swap**: Dòng này mô tả về Virtual Memory

<!-- -->

- Khi cần thông tin chi tiết hơn dung lệnh **vmstat**, **cat
  /proc/meminfo**

<img src="media/image6.png" style="width:5.68475in;height:1.7371in" />

3.  **<u>GIÁM SÁT DISK I/O</u>**

- Để monitoring disk I/O ta có thể sử dụng command **iostat**, với
  **-d** option

<img src="media/image7.png" style="width:5.2422in;height:1.29825in" />

- Ngoài ra còn có thể sử dụng lệnh: **lsblk**, **lsof** (Listing Open
  Files)

<img src="media/image8.png" style="width:5.69681in;height:2.36531in" />

4.  **<u>GIÁM SÁT NETWORK I/O</u>**

- Để hiển thị chi tiết thông tin về network I/O hơn ta lại dùng câu lệnh
  **netstat**

<img src="media/image9.png" style="width:5.22417in;height:1.87739in" />

- Dùng option **–s** để có thêm nhiều thông tin về network dựa trên
  protocol

5.  **<u>CÁC CÔNG CỤ GIÁM SÁT KHÁC</u>**

- Hiển thị các process đang chạy: **ps –ef, ps -aux**

- Để hiện thị mối liên hệ của processes theo cấu trúc cây, dùng lệnh
  **pstree**

- Để hiển thị các thông tin cơ bản của hệ thống như running time,
  average system load, số lượng process đang chạy, CPU statistics, thông
  tin memory, … Ta dùng lệnh **top**

**<u>LAB</u>**

1.  **<u>Giám sát CPU</u>**

    1.  Giám sát với lệnh **iostat \#iostat -c**

    2.  Giám sát với lệnh **sar \#sar \| head**

    3.  Giám sát với lệnh **mpstat \#mpstat -P ALL**

2.  **<u>Giám sát Mem</u>**

> **2.1** Giám sát với lệnh **free \#free**

<img src="media/image10.png" style="width:5.71119in;height:0.87399in" />

- **Mem:** Dòng này mô tả về RAM

- **Swap:** Dòng này mô tả về Virtual Memory

Các cột:

- **total** — Giá trị này biểu diễn tổng dung lượng bộ nhớ của hệ thống.

- **used** — Dung lượng bộ nhớ hiện đang được sử dụng

- **free** — Dung lượng bộ nhớ còn trống.

- **shared** — Giá trị này biểu diễn dung lượng bộ nhớ được sử dụng bởi
  <u>tmpfs</u>. <u>tmpfs</u> là một filesystem thường xuyên hiện hữu
  trên hard disk, nhưng thực sự lưu trữ dữ liệu trong memory.

- **buff/cache** — Buffer hoặc Cache là các vị trí lưu trữ tạm thời.

- **available** — Giá trị này biểu diễn bao nhiêu dung lượng bộ nhớ
  trống cho một tiến trình mới (new processes).

Mặc định, các giá trị hiển thị với đơn vị là **kilobytes**. Tuy nhiên có
thể hiển thị chính xác giá trị hơn với option **-b**/–bytes, hoặc hiển
thị theo megabytes **-m**/–mega, hoặc gigabytes **-g**/–giga.

**2.2** Giám sát với lệnh **vmstat \#vmstat**

<img src="media/image11.png" style="width:4.545in;height:1.28206in" />

- Procs --

  - **r**: Số process đang chạy hoặc chờ chạy.

  - **b**: Số process trong trạng thái uninterruptible sleep.

- Memory —

  - **swpd**: Dung lượng virtual memory đã sử dụng.

  - **free**: Dung lượng memory trống.

  - **buff**: Dung lượng memory được sử dụng làm buffer.

  - **cache**: Dung lượng memory được sử dụng làm cache.

  - **inact**: Dung lượng memory inactive (-a option).

  - **active**: Dung lượng memory active (-a option).

- Swap —

  - **si**: Số lượng memory đổi chỗ từ disk (/ s). - so: Số lượng memory
    đã được

> hoán đổi sang disk (/ s).

- IO —

  - **bi**: Block nhận từ block device (blocks/s).

  - **bo**: Block gửi block device (blocks/s).

- System —

  - **in**: Số interupt trên giây. Bao gồm cả clock interrupt.

  - **cs**: Số lượng context switch trên giây.

- CPU —

  - Tỷ lệ phần trăm của tổng thời gian CPU.

  - **us**: Thời gian sử dụng cho việc chạy ngoài Kernel-code (bao gồm
    cả user time

> và nice time).

- **sy**: Thời gian sử dụng để chạy Kernel-code.

- **id**: Idle time.

- **wa**: Thời gian chờ IO.

- **st**: Thời gian bị lấy từ một máy ảo.

3.  **Giám sát Disk I/O**

    1.  Giám sát với lệnh **iostat \#iostat –d**

> <img src="media/image12.png" style="width:5.51736in;height:1.19735in" />

- **sda —** 1st SATA drive.

- **dm-0 —** 1st LVM logical volume.

- **dm-1 —** 2nd LVM logical volume.

- **tps** — Giá trị transfer/s cho mỗi device.

- **kB_read/s** — Số kilobytes/s đọc từ device.

- **kB_wrtn/s** — Số kilobytes/s ghi vào device.

- **kB_read** — Số kilobytes đọc từ device.

- **kB_wrtn** — Số kilobytes ghi vào device.

2.  Giám sát với lệnh **lsof**

> <img src="media/image13.png" style="width:6.26875in;height:2.09444in" />
>
> **\#lsof -u root**
>
> <img src="media/image14.png" style="width:6.26875in;height:1.81458in" />
>
> Thực hiện thêm các command và cho biết ý nghĩa:
>
> **- lsof –i**
>
> **- lsof /usr/bin/bash**
>
> **- lsof +d /usr/bin**
>
> **- lsof -p 100**

- **COMMAND —** Câu lệnh mở file.

- **PID —** Process ID của câu lệnh mở file.

- **USER** — Người dùng chạy câu lệnh.

- **FD** — Các thông tin về việc file được sử dụng như thế nào, …

- **TYPE** — Kiểu của node (file) được mở.

Ví dụ **DIR** là directory, **REG** là regular node, **CHR** là
character special node, **IPv4** là một IPv4 socket node, …

- **DEVICE** — Đây là giá trị device number. Giá trị này liên quan tới
  device vật lý,

ví dụ SATA hard drive hoặc pseudo drive.

1.  Giám sát với lệnh **netstat \#netstat –s**

> <img src="media/image15.png" style="width:3.63796in;height:1.59189in" />

- **-l —** Hiển thị network sockets đang trong trạng thái lắng nghe.

- **-lt —** Hiển thị TCP sockets đang trong trạng thái lắng nghe.

- **-lu** — Hiển thị UDP sockets đang trong trạng thái lắng nghe.

- **-p** — Hiển thị program name và PID trong output.

- **-n** — Tăng tốc câu lệnh netstat, giảm trễ khi DNS chưa respond.

- **-c** — Update output realtime.

4.  **<u>Bổ sung</u>**

> \# yum install sysstat
>
> \# dd if=/dev/zero of=/tmp/test2.img bs=512 count=1000 oflag=dsync
>
> \# yum install sysbench
>
> sysbench cpu --threads=2 run
>
> \#

[How to Check Disk Space Usage in Linux Using df and du Commands
(hostinger.com)](https://www.hostinger.com/tutorials/vps/how-to-check-and-manage-disk-space-via-terminal#:~:text=Check%20Disk%20Usage%20in%20Linux%20Using%20the%20du%20Command,-Another%20important%20command&text=du%20%2Dsh%20%2Fhome%2Fuser,see%20the%20information%20in%20Kilobytes).)

<https://www.cyberciti.biz/faq/check-how-many-cpus-are-there-in-linux-system/>

du: show directory space usage

df: show disk usage
