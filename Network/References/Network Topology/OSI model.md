![image](https://github.com/vulonggg/Documents/assets/167597317/4189cfd8-30b7-4db4-be95-015bafb30849)

![OSI_Model](https://github.com/vulonggg/Documents/assets/167597317/0408e2ab-6541-492f-b691-07372edc5fbf)



Host Layers

	Tầng Ứng dụng (Application): giao thức chủ yếu HTTP, ứng dụng với các trình duyệt như Chrome, Firefox, skype, outlook cung cấp các chức năng cho các ứng dụng có sẵn cho người dùng, giúp truy cập dịch vụ mạng.

	Tầng Trình diễn (Presentation): xử lý cú pháp, ngữ nghĩa của dữ liệu giữa 2 hệ thống. Dữ liệu sẽ được chuyển sang một dạng cụ thể (.txt, .jpeg, .mp4, ….) trên một đường truyền an toàn, sau đó dữ liệu được mã hóa được chuyển tới tầng presentation. Lớp này xử lý việc dịch dữ liệu ra, thông tin sau đó sẽ được chuyển tới lớp App or Ses tùy thuộc vào dữ liệu.

	Tầng phiên (Session): Bộ điều khiển hội thoại mạng, thiết lập duy trì và đồng bộ hóa các hệ thống cho phép giao tiếp từ hai quy trình trên các hệ thống khác nhau. Lớp này hỗ trợ nhiều loại kết nối, chịu trách nhiệm xác thực và kết nối lại nếu xảy ra gián đoạn mạng.

	Tầng giao vận (Transport): truyền dữ liệu qua các kết nối mạng. Điều phối dữ liệu cần gửi, tốc độ, vị trí, đảm bảo dữ liệu toàn vẹn, đúng thứ tự. Truyền dẫn dữ liệu qua 2 giao thức TCP & UDP.








Media Layers

	Tầng Mạng (Network): Xác định đường đi cho dữ liệu. Tạo kết nối giữa các mạng khác nhau. Router hoạt động ở tầng này. Quản lý ánh xạ giữa các địa chỉ IP, thông qua giao thức phân giải ARP (address resolution protocol) 

	Tầng Liên kết dữ liệu (Data Link): Xác định cách dữ liệu được định dạng để truyền qua đường vật lý. Tạo kết nối giữa các thiết bị trong 1 mạng. Switch hoạt động ở tầng này
Được chia thành 2 tầng con: LLC (logical link control), MAC (media access control). Khi lớp này nhận đc dữ liệu từ lớp physical, nó sẽ kiểm tra lỗi đường truyền, đóng gói các bit thành các khung dữ liệu. Từ đó, lớp này quản lý các phương tiện địa chỉ vật lý cho các lớp MAC & LLC 

	Tầng Vật lý (Physical): Lớp thấp nhất. Cung cấp các công cụ cơ khí và điện để kích hoạt /hủy kích hoạt kết nối vật lý (hub, network adapter, dây cáp, anten, socket, công tắc, ….) là lớp bắt đầu tìm nguyên nhân




![image](https://github.com/vulonggg/Documents/assets/167597317/e33d3d99-b7df-452e-94f1-3ddf82e84606)


