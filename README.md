#Tổng quan về giao thức DHCP

##1.Khái niệm
* DHCP là một giao thức được sử dụng để phân phối động các tham số cấu hình TCP/IP cho các máy tính.
* Làm việc theo mô hình Client/Server.

##2.Thành phần
**a.Server**
* Là một máy chủ có cài đặt dịch vụ DHCP.
* Cung cấp cho client một số thiết lập TCP/IP, như là địa chỉ IP,subnet mask, và máy chủ DNS một cách tự động.

**b.Client**
* Là dịch vụ có sẵn trên các máy trạm(hay có thể coi Client là một máy trạm).
* Dùng để đăng ký, cập nhật thông tin về địa chỉ IP và các bản ghi DNS cho chính máy trạm đó.

##3.Cơ chế hoạt động
**a.DHCPDISCOVER**
* DHCP Client khởi tạo tiến trình bằng cách gửi một gói tin Broadcast(DHCP Discover) tới cổng UDP 68 (sử dụng cho máy chủ BOOTP và DHCP),yêu cầu bất cứ DHCP server nào nhận được gói thực hiện việc cấu hình.
* Gói tin này chứa địa chỉ Mac của Client.

    <img src="http://i.imgur.com/6CTRt1Y.png">

**b.DHCPOFFER**
* Một DHCP Server sẽ đáp ứng lại một gói tin Broadcast tên là DHCP offer tới máy đưa ra DHCP discover.
* Thông điệp quảng bá này được gửi tới cổng UDP 67 và bao gồm địa chỉ Mac của client, địa chỉ Mac và địa chỉ IP của DHCP Server, cũng như địa chỉ IP và subnet mask cung cấp cho DHCP Client.
    <img src="http://i.imgur.com/6swRJCv.png">

**c.DHCPREQUEST**
* Máy Client sẽ lựa chọn một trong những lời đề nghị (DHCPOFFER) và gửi broadcast lại gói tin DHCPREQUEST chấp nhận lời đề nghị đó.
* Điều này cho phép các lời đề nghị không được chấp nhận sẽ được các Server rút lại và dùng đề cấp phát cho Client khác.
    <img src="http://i.imgur.com/z49IVAU.png">

**d.DHCPACK**
* Khi DHCP server được chọn nhận được DHCP request, nó sẽ trả lời bắng gói DHCP ACK
* DHCP ACK bao gồm địa chỉ IP và subnetmask cho DHCP client. Ngoài các thông tin về địa chỉ IP, DHCP client có thể nhận thêm các thông tin cấu hình như địa chỉ IP của gateway,máy chủ DNS, ...
    <img src="http://i.imgur.com/SEBK1Mg.png">

##4.Đánh giá chung
**a.Ưu điểm:**
* Quản lý TCP/IP tập trung
* Giảm gánh nặng cho các nhà quản trị hệ thống
* Giúp hệ thống mạng luôn được duy trì ổn định
* Linh hoạt và khả năng mở rộng

**b.Nhược điểm:**
Không có sự xác thực hay kiểm soát truy cập trong quá trình trao đổi thông điệp
