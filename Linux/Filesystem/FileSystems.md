**File Systems**

1.  **<u>DISK VÀ PARTITION</u>**

- Mọi đĩa cứng (disk) đều cần được phân chia partition, partition là
  những phân vùng nhỏ (phân vùng logic) được chia ra từ 1 ổ cứng vật lý.

- Sau đó, dùng một một trình quản lý **bootloader** để quản lý quá trình
  boot.

3 loại partition chính là: *primary, extended và logical*.

- **Primary partition**: đây là những phân vùng có thể được dùng để boot
  hệ điều hành

- **Extended partition**: là vùng dữ liệu còn lại khi ta đã phân chia ra
  các primary partition, extended partition chứa các logical partition
  trong đó. Mỗi một ổ đĩa chỉ có thể chứa 1 extended edition.

- **Logical partition**: các phân vùng nhỏ nằm trong extended partition,
  thường dùng để chứa dữ liệu.

Mục đích:

- Cải thiện sai phạm hệ thống. Khi dữ liệu đầy, partition này không thể
  “overflow” (lấn chiếm) kích thước của partition khác do mỗi partition
  được xem như một phân vùng độc lập, mọi thao tác trên partition này sẽ
  không ảnh hưởng đến partition kia.

- Có thể cài các hệ điều hành khác nhau lên các partition khác nhau =\>
  có thể cài nhiều HĐH trên cùng một ổ cứng

- Hỗ trợ quản lý tập tin: có riêng một partition chỉ dành riêng cho mục
  đích cá nhân

2.  **<u>MBR vs GPT</u>**

<img src="media/image1.png" style="width:5.02725in;height:3.07118in" />

Thông tin về các partition của ổ cứng sẽ được lưu trữ trên **MBR**
(Master Boot Record) hoặc **GPT** (GUID Partition Table) tùy loại ổ cứng
hỗ trợ.

Đây là 2 chuẩn cấu hình và quản lý các partition trên ổ cứng. Thông tin
được lưu trữ trên đây gồm vị trí và dung lượng của các partition.

**MBR**

MBR là chuẩn phân chia ổ đĩa truyền thống, một ổ đĩa sẽ được chia thành
các vùng nhỏ (sector) với dung lượng bằng nhau là 512 bytes.

Trên Linux, một ổ đĩa cứng được chia thành nhiều partition với số hiệu
như
sau: */dev/hda1*, */dev/hda2*, */dev/sda1*, */dev/sda2*, */dev/sdb1*,…

Ta có thể dùng lệnh ***fdisk*** hoặc ***parted ***để hiển thị thông tin
về ổ đĩa dùng MBR trên Linux.

**GPT**

GPT là chuẩn mới hơn, hỗ trợ đến 128 phân vùng trên 1 ổ đĩa vật lý.
Thông tin về các partition sẽ được ghi thành nhiều bản rải rác khắp ổ
vật lý. GPT hỗ trợ cơ chế kiểm tra và chỉnh sửa dữ liệu dựa trên CRC
(cyclic redundancy check).

Nhờ 2 cơ chế này, chuẩn GPT làm giảm tỷ lệ mất mát dữ liệu. Ngoài ra,
nếu ta cần khởi tạo một phân vùng với dung lượng lớn hơn 2TB, ta sẽ phải
dùng GPT vì MBR không trợ dung lượng lớn hơn 2 TB. Dùng
lệnh ***gdisk*** hoặc ***parted*** để kiểm tra các ổ đĩa dùng GPT.

> **parted /dev/sdb mklabel gpt**

3.  **<u>Hard Disk</u>**

- Những ổ đĩa IDE sẽ có tên là **hdX.**

**X** có giá trị từ \[a-z\] đại diện cho một ổ đĩa vật lý. Vd**: hda,
hdb…**

- Khi được chia partition, partition sẽ có dạng: **hdXY**

  - **X** là kí tự ổ đĩa.

  - **Y** là số thứ tự.

  - Vd: hda1, hda2, hdb1, hdb2…

- CDROM cũng được hiểu như một ổ đĩa IDE.

- Ổ đĩa SCSI sẽ có tên là **sdX.**

4.  **<u>FILE SYSTEMS</u>**

> <img src="/media/image4.png" style="width:6.50769in;height:4.33803in" />
>
> <img src="/media/image5.png" style="width:5in;height:3.07292in" />
>
> <img src="/media/image7.png" style="width:5.45833in;height:3.31406in" />
>
> **A, cấu trúc thư mục**

**1. / – Root – Thư mục gốc**

- Mỗi tập tin đơn và thư mục được bắt đầu thư mục gốc.

- Chỉ người dùng root mới có quyền ghi trong thư mục này.

- Lưu ý: rằng thư mục /root là thư mục của người dùng root chứ không
  phải là thư mục **/**.

**2. /bin – Các tập tin thực thi của người dùng**

- Chứa các tập tin thực thi.

- Các lệnh thường dùng của Linux mà bạn cần để dùng trong chế độ người
  dùng đơn được lưu ở đây.

- Các lệnh được sử dụng bởi tất cả người dùng trong hệ thống được lưu ở
  đây.

- *<u>Ví dụ:</u>* ps, ls, ping, grep, cp.

**3. /sbin – Các tập tin thực thi của hệ thống**

- Giống như */bin*, */sbin* cũng chứa các tập tin thực thi.

- Nhưng, các lệnh được lưu trong thư mục này về cơ bản được dùng cho
  người quản trị và được dùng để bảo trì hệ thống.

- *<u>Ví dụ:</u>* iptables, reboot, fdisk, ifconfig, swapon

**4. /etc – Các tập tin cấu hình**

- Chứa các tập tin cấu hình cần thiết cho tất cả các chương trình.

- Nó cũng chứa các đoạn mã khởi động và tắt mà được dùng để khởi
  động/dừng các chương trình đơn lẻ.

- *<u>Ví dụ:</u>* /etc/resolv.conf, /etc/logrotate.conf

**5. /dev – Các tập tin thiết bị**

- Chứa các tập tin thiết bị.

- Nó chứa các tập tin thiết bị đầu cuối như là USB hay bất kỳ thiết bị
  nào gắn vào hệ thống.

- *<u>Ví dụ:</u>* /dev/tty1, /dev/usbmon0

**6. /proc – Thông tin tiến trình**

- Chứa thông tin về các tiến trình của hệ thống.

- Như các tập tin chứa thông tin về các tiến trình đang chạy. *<u>Ví
  dụ:</u>* /proc/{pid} directory \>\>\> lưu thông tin về tiến trình với
  pid bạn chọn.

- Hay các tập tin hệ thống ảo với nội dung về tài nguyên hệ
  thống. *<u>Ví dụ:</u>* /proc/uptime

**7. /var – Các tập tin biến đổi**

- **var** là viết tắt của các tập tin biến đổi.

- Gồm những tập tin mà dung lượng lớn dần theo thời gian sử dụng.

- Chẳng hạn — các tập tin ghi chú hệ thống (/**var/log**); các gói và
  các tập tin cơ sở dữ liệu (/**var/lib**); thư điện tử (/**var/mail**);
  hàng đợi – in queues (/**var/spool**); các tập tin khóa
  (/**var/lock**); các tập tin tạm được dùng khi khởi động lại
  (**/var/tmp**).

**8. /tmp – Thư mục chứa các tập tin tạm**

- Thư mục chứa các tập tin tạm được tạo bởi hệ thống và người dùng.

- Các tập tin trong thư mục này bị xóa khi hệ thống khởi động lại.

**9. /usr – Các chương trình của người dùng**

- Tập trung các tập tin thực thi, thư viện, tài liệu, và mã nguồn cho
  các chương trình mức độ thứ hai.

- ***/usr/bin*** chứa các tập tin thực thi cho các chương trình của
  người dùng. Nếu bạn không thể tìm thấy trong thư mục /bin thì tìm
  trong */usr/bin*. *<u>Ví dụ:</u>* at, awk, cc, less, scp

- ***/usr/sbin*** chứa các tập tin thực thi cho quản trị hệ thống. Nếu
  bạn không thể tìm thấy trong ***/sbin*** thì tìm
  trong ***/usr/sbin***. *<u>Ví dụ:</u>* atd, cron, sshd, useradd,
  userdel

- ***/usr/lib*** chứa các tập tin thư
  viện ***/usr/bin*** và ***/usr/sbin***

- ***/usr/local*** chứa các chương trình của người dùng mà bạn cài từ mã
  nguồn. Ví dụ, khi bạn cài Apache từ mã nguồn, nó được đưa vào thư mục
  /usr/local/apache2

**10. /home – Thư mục người dùng**

- Chứa các tập tin của các người dùng trong hệ thống.

- *<u>Ví dụ:</u>* /home/john, /home/nikita

**11. /boot – Các tập tin của chương trình khởi động máy**

- Chứa những tập tin liên quan tới chương trình quản lý khởi động máy.

- Các tập tin *initrd*, *vmlinux*, *grub* được lưu trong thư
  mục ***/boot***

- *<u>Ví dụ:</u>* initrd.img-2.6.32-24-generic,
  vmlinuz-2.6.32-24-generic

**12. /lib – Các tập tin thư viện của hệ thống**

- Chứa các tập tin thư viện để hỗ trợ các tập tin thực thi được lưu
  trong ***/bin*** và ***/sbin***

- Tên của các tập tin này là ***ld\**** hay ***lib\*.so.\****

- *<u>Ví dụ:</u>* ld-2.11.1.so, libncurses.so.5.7

**13. /opt – Các ứng dụng tùy chọn hay thêm**

- **opt** là viết tắt của optional.

- Chứa các ứng dụng thêm của các hãng khác nhau.

- Các ứng dụng thêm nên được cài trong thư mục con của thư
  mục ***/opt/***.

**14. /mnt – Thư mục Mount**

- Thư mục mount tạm thời nơi mà người quản trị hệ thống có thể mount các
  tập tin hệ thống.

**15. /media – Các thiết bị tháo lắp**

- Thư mục chưa các mount tạm thời cho các thiết bị tháo lắp.

- *<u>Ví dụ:</u>* /media/cdrom cho CD-ROM; /media/floppy cho ổ đĩa mềm;
  /media/cdrecorder cho ổ đĩa ghi CD.

**16. /srv – Dữ liệu dịch vụ**

- **srv** là viết tắt của service.

- Chứa dữ liệu liên quan tới các dịch vụ trên máy chủ.

- *<u>Ví dụ:</u>* /srv/cvs chứa dữ liệu liên quan tới CVS.

> **B, Mount & filesystem**

- Mỗi một partition sẽ cần có một filesystem riêng. Filesystem là cách
  thức lưu trữ và tìm kiếm dữ liệu trên một partition. Một số file
  system thông dụng được hỗ trợ trên Linux gồm:

  - File system trên đĩa cứng: ext2, ext3, ext4, Btrfs, JFS, NTFS, xfs…

  - File system trên thẻ nhớ flash: ubifs, JFFS2, YAFFS,…

  - File system của các loại database.

  - File system đặc biệt: procfs, sysfs, tmpfs, debugfs,…

- Partition,ổ đĩa CD-ROM, floopy, usb… cần được mount, nhờ thế nội dung
  của nó mới có thể đọc được.

- Mount là biến một partition, một thiết bị (CDROM, USB…) thành một thư
  mục trên cây thư mục. Thư mục này được gọi là mount-point.

- Xem nội dung của partition vừa được mount bằng xem nội dung của thư
  mục mount-point.

- Tạo một thư mục /mnt/cdrom. Thư mục này dùng làm mount-point cho ổ đĩa
  CD-ROM

> **mount /dev/cdrom /mnt/cdrom**

- Thêm ổ cứng vào Server với các bước và sử dụng các lệnh sau:

  - **fdisk**: để phân chia partition của ổ cứng

  - **mkfs**: để format

  - **mount**: để gắn một partition đã format vào một mount point.

  - Chỉnh sửa **/etc/fstab** để Linux có thể tự động mount khi boot.

- Mọi partition đều phải được mount để sử dụng =\> những partition hệ
  thống được mount lúc nào =\> **vi /etc/fstab**

**\##### Cơ bản về Fstab**

Là một tập tin cấu hình chứa các thông tin về các phân vùng trên ổ cứng
cũng như các thiết bị lưu trữ khác trong máy tính

> **\<Device\> \<Mount Point\> \<File System Type\> \<Options\> \<Dump\>
> \<Pass\>**
>
> **Cấu trúc: gồm 6 cột**
>
> **Cột 1** và **cột 2:** Thiết bị cần mount và nơi mặc định để mount.
>
> **Cột 3:** loại file system (ext3,ext4, swap, vfat, xfs …)
>
> **Cột 4:** Các tùy chọn mount (auto, noauto, user, …)
>
> **Cột 5:** Các tùy chọn cho lệnh **dump** và **fsck**

- Lệnh **fdisk**: xem, tạo, xóa partition.

- Lệnh **fsck**: chẩn đoán và sửa lỗi file systems.

5.  **Phân vùng boot, root, swap**

<!-- -->

1.  Phân vùng **boot**

- phân vùng Boot chứa những gì cơ bản cần thiết để khởi động một hệ điều
  hành

- Khi máy bạn khởi động lên, nó sẽ truy cập vào phân vùng boot để tìm
  những files cần thiết để khởi động hệ thống.

2.  Phân vùng **root**

- Phân vùng nút gốc (root) là nơi chứa tất cả các file và thư mục. Chỉ
  có root user mới có quyền ghi trong thư mục này.

3.  Phân vùng **SWAP**

- một vùng trên ổ đĩa mà nó có thể được sử dụng để lưu trữ các dữ liệu
  mà không được sử dụng trên bộ nhớ vật lý (RAM). Đây là nơi tạm thời
  chứa các tài nguyên đang không hoạt động trong bộ nhớ.

- Swap được sử dụng khi hệ thống của bạn quyết định rằng nó cần thêm bộ
  nhớ RAM cho quá trình hoạt động và bộ nhớ RAM không còn dư để sử
  dụng. 

- Nếu điều đó xãy ra, các tài nguyên và dữ liệu tạm thời không hoạt động
  trên bộ nhớ RAM sẽ được di chuyển để lưu trữ vào không gian Swap để
  giải phóng bộ nhớ RAM và sử dụng cho việc khác.

- thời gian truy cập vào vùng Swap là chậm hơn rất nhiều, do đó bạn
  không nên coi việc sử dụng Swap là một phương pháp thay thế hoàn hảo
  cho bộ nhớ vật lý (RAM).

> ***<u>LAB</u>***

1.  **Cấu hình tạo thêm ổ cứng mới**

> Các lệnh sử dụng:
>
> \- **fdisk**: để phân chia partition của ổ cứng
>
> \- **mkfs**: để format
>
> \- **mount**: để gắn một partition đã format vào một mount point.
>
> \- Chỉnh sửa **fstab** để Linux có thể tự động mount khi boot.
>
> Quy trình cấu hình cho một ổ cứng mới:

1.  Gắn một ổ cứng mới vào server, kiểm tra với lệnh: **fdisk –l** và
    lệnh **lsblk**

2.  Định dạnh ổ cứng HDD sdb với lệnh:

- \#fdisk /dev/sdb

- Chọn **n** để add partition mới

- Chọn **p** để tạo primary partition

- Chọn **1** để tạo partition số 1

- Chọn **default** cho cylinder

- Chọn **w** để write tables to disk

- Kiểm tra partition vừa tạo: **fdisk -l**

- Định dạng phân vùng: **mkfs.ext4 /dev/sdb1**

- Tạo thư mục gắn kết với **hdd** mới **mkdir /mnt/sdb1**

- Chỉnh sửa file **fstab** (Thêm vào dòng sau)

> ***/dev/sdb1 /mnt/sdb1 ext4 defaults 0 0***

- Restart Server sau đó kiểm tra bằng lệnh **df -h**.

https://www.linode.com/docs/guides/mount-file-system-on-linux/

6.  **<u>LVM</u>**

<img src="media/image3.png" style="width:6.79112in;height:2.80461in" />

- Linh hoạt trong việc phân chia partition.

- Dễ dàng mở rộng kích thước của volume.

- Để mở rộng dung lượng lưu trữ dữ liệu, đơn giản chỉ cần thêm đĩa mới
  vào.

1.  ***<u>Các thành phần</u>***

**Physical Volume - PV**: Là một cách gọi khác của partition trong kỹ
thuật LVM, nó là những thành phần cơ bản được sử dụng bởi LVM. Một
Physical Volume không thể mở rộng ra ngoài phạm vi một ổ đĩa.

**Logical Volume Group - VG**: Nhiều Physical Volume trên những ổ đĩa
khác nhau được kết hợp lại thành một Logical Volume Group, với LVM
Logical Volume Group được xem như một ổ đĩa ảo.

**Logical Volumes - LV**: Logical **Volume Group** được chia nhỏ thành
nhiều **Logical Volume**, mỗi **Logical Volume** có ý nghĩa tương tự như
partition. Nó được dùng cho các mount point và được format với những
định dạng khác nhau như ext3, ext4 …  
Khi dung lượng của **Logical Volume** được sử dụng hết ta có thể đưa
thêm ổ đĩa mới bổ sung cho Logical Volume Group và do đó tăng được dung
lượng của **Logical Volume**.

**Physical Extent**: là một đại lượng thể hiện một khối dữ liệu dùng làm
đơn vị tính dung lượng của Logical Volume.

2.  ***<u>Các lệnh tạo, xóa, thay đổi kích cỡ</u>***

**pvcreate**: khởi tạo những physical volume để sử dụng trong môi trường
LVM. Physical volume có thể là đĩa cứng, thiết bị lưu trữ khác, hoặc
partition…

**pvdisplay**: hiển thị thông tin của physical volume.

**vgcreate**: khởi tạo một volume group từ những physical devices đã
được khởi tạo bằng pvcreate.

**vgextend**: thêm physical volume vào volume group.

**vgdisplay**: xem không tin của volume group

**lvcreate**: tạo logical volume từ volume group.

**lvdisplay**: xem thông tin của logical volume.

**lvextend:** mở rộng kích thước

***<u>LAB - Cấu hình LVM</u>***

Quy trình này gồm 4 bước:

Bước 1: Khởi tạo **Physical Volume** từ đĩa cứng vật lý.

Bước 2: Gộp các **Physical Volume** lại thành **Volume Group**.

Bước 3: Tạo các **Logical Volume** từ **Volume Group**.

Bước 4: Format và mount các **Logical Volumes** lên hệ thống.

**Bước 1**: Tạo thêm ổ cứng mới

Khởi động lại máy ảo, kiểm tra xem đã nhận 03 ổ cứng mới chưa bằng lệnh
**lsblk**

**Bước 2**: Tạo Logical Volume với lệnh **fdisk /dev/sdb**

Tương tự tạo thêm các Partition từ **sdb, sdc,sdd**

**Bước 3**: Tạo physical volume

**pvcreate /dev/sdb1**

Kiểm tra kết quả bằng lệnh **pvs**, **pvdisplay** xem đã tạo được
physical volume chưa

**Bước 4**: Tạo Volume Group Sau khi tạo các Physical Volume ta gộp các
PV đó thành 1 Volume Group bằng lệnh sau : **vgcreate vg-demo1 /dev/sdb1
/dev/sdc1 /dev/sdd1**

Kiểm tra kết quả bằng lệnh **pvs, pvdisplay**

**Bước 5**: Tạo Logical Volume

Từ một Volume group , ta tạo các **Logical Volume** để sử dụng bằng lệnh
sau:

**lvcreate -L 1G -n lv-demo1 vg-demo1**

Định dạnh lại Logical Volume

**mkfs -t ext4 /dev/vg-demo1/lv-demo1**

**Bước 6**: Mount và sử dụng

swapon -s

> mkswap /dev/sdnx
>
> swapon /dev/sdnx
>
> swapoff /dev/sdnx
>
> swapon -p 10 /dev/sdnx
>
> **--create temp swap files--**
>
> dd if=/dev/zero of=/swapfile count=1 bs=500MiB
>
> mkswap /swapfile
>
> chmod 600 /swapfile
>
> swapon /swapfile
>
> swapon -s
>
> swapoff -a
>
> swapon -a
