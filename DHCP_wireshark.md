#Bắt goi tin DHCP với wireshark

##Bước 1:Giải phóng IP
<img src="http://image.prntscr.com/image/158b96fabda846d1837b9624de354a8b.png">

<img src="http://image.prntscr.com/image/59b178bb434f40cb9655bb51f9c47063.png">

##Bước 2:Bật wireshark để bắt đầu bắt gói tin
Chọn card wifi:

<img src="http://i.imgur.com/Ii6shWV.png">

##Bước 3:Cấp mới IP
<img src="http://i.imgur.com/VqchKJz.png">

<img src="http://i.imgur.com/HAPpkTa.png">

##Bước 4:Lọc các gói tin DHCP
    Gõ "bootp" vào ô filter
<img src="http://i.imgur.com/D0RSwPA.png">

##Bước 5:Phân tích các gói tin DHCP vừa bắt được

**a.DHCP Discover:**

<img src="http://i.imgur.com/LMulzGx.png">
Đây là gói tin Broadcast từ client đến các server,chúng ta có thể thấy Dst:Broadcast(ff:ff:ff:ff:ff:ff).Chúng ta quan tâm đến một số trường sau:
* Source port=68(client) và Des port=67(server)
* Message Type với Op code=1 tương ứng với Boot Request(1).
* Hardware type là 0x01 tương ứng với code=1 tức là Ethernet.
* Hardware address length là 6.
* Hop=0.
* Bootflag có dạng 0x8000,với bit 0 ở đầu tương ứng là Broadcast

**b.DHCP Offer:**

<img src="http://i.imgur.com/cBGy750.png">
Đây là gói tin Broadcast từ server đến các client,ngoài một số trường giống gói Discover,ta thấy có một số trường quan trọng sau:
* Message Type với Op code=2 tương ứng với Boot Reply(2)
* Your client ip address:Địa chỉ ip mà server cấp phát cho client
* DHCP server Identifier:Địa chỉ ip của server
* IP address lease time:Thời gian cho thuê IP server dành cho client

**c.DHCP Request:**

<img src="http://i.imgur.com/7U5APEa.png">
Đây cũng là một gói tin Broadcast từ client hồi đáp lại cho 1 trong những gói tin Offer từ server.Chúng ta chú ý đến các trường sau:
* Src:Vì client chưa có IP nên mặc định nó sẽ là 0.0.0.0.
* Client Identifier:Ở đây định danh client bằng địa chỉ vật lý của máy(MAC).
* Host name:Tên của client.
* Ngoài ra còn có trường Client Fully Qualified Domain Name.

**d.DHCP Ack:**

<img src="http://i.imgur.com/ter9X2G.png">
Gói tin hồi đáp lại cho client,bao gồm địa chỉ IP,subnet mask,ngoài ra còn có địa chỉ Ip của gateway,máy chủ DNS.
