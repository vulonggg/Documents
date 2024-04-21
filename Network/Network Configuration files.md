1. File /etc/hosts

-	Là bản map giữa địa chỉ IP và tên máy tính trong network.
-	Tương tự file lmhosts của Windows.
-	Cú pháp của file:

![image](https://github.com/vulonggg/Documents/assets/167597317/f7e96f88-d321-457f-a915-c674b69c49a3)

-	Các ứng dụng trước tiên sẽ sử dụng file này khi cần truy vấn một máy tính bằng tên.
-	Lệnh hostname: xem tên và đổi tên. 
Lưu ý: Sau khi cấu hình thực hiện reboot để hệ thống nhận hostname mới



2. File /etc/sysconfig/network

-	File /etc/sysconfig/network định nghĩa các cấu hình network cơ bản cho máy tính.

![image](https://github.com/vulonggg/Documents/assets/167597317/21c380d1-98f2-47d3-bafb-f69c87beb30e)


3. File /etc/sysconfig/network-scripts/ifcfg-eth[n]

-	Mỗi card mạng có một file cấu hình
-	n: có giá trị bắt đầu từ 0.
-	Card loopback có file cấu hình ifcfg-lo

![image](https://github.com/vulonggg/Documents/assets/167597317/5397f9af-67de-4eed-9ea2-2f80182f6255)

![image](https://github.com/vulonggg/Documents/assets/167597317/0714a71b-f05d-453a-ae0c-81bc451d2fdd)



4. File /etc/resolv.conf

-	File /etc/resolv.conf dùng để định nghĩa name server mà máy tính sẽ sử dụng để thực hiện các truy vấn phân giải tên miền.
-	Một số cú pháp thông dụng:
o	domain: Queries short name sẽ ghép với domain này.
o	nameserver: IP hoặc tên của name server mà máy tính sẽ sử dụng. Có tối đa 3 giá trị.
o	search: default sẽ tìm trên domain nào


5. File /etc/services
   
-	File /etc/services gồm một danh sách network port và các service sử dụng những port này.
-	Khi định nghĩa một service mới, người quản trị phải định nghĩa một cặp service name và port number vào file /etc/services.
o	Port 0 – 1024: là những port đã được dành riêng.
o	Port > 1024: port được định nghĩa thêm vào tùy theo nhu cầu của ứng dụng.

![image](https://github.com/vulonggg/Documents/assets/167597317/fd71592b-fb8c-454c-8cbf-2f3d007092ea)

