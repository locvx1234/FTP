# FTP
Ghi chép về giao thức FTP

## 1. FTP là gì ?
FTP (File Transfer Protocol) là giao thức trao đổi tập tin qua mạng lưới truyền thông, được định nghĩa trong [RFC-959](https://tools.ietf.org/html/rfc959). FTP được xây dựng trên kiến trúc client-server và sử dụng kết nối riêng biệt giữa hai luồng điểu khiển và dữ liệu. Người dụng có thể xác thực bằng cách sử dụng username và password, cũng có thể sử dụng kết nối nặc danh nếu máy chủ cấu hình cho phép điều đó.

## 2. Hoạt động 

<img src="http://i.imgur.com/V0yYH2j.png">

Khác với nhiều giao thức trong mô hình TCP/IP thông thường sử dụng 1 đường kết nối, FTP sử dụng 2 đường kết nối riêng biệt:
- Cổng 21 cho kết nối điều khiển
- Cổng 20 cho truyền tập tin
Việc sử dụng 2 đường truyền tạo sự linh hoạt nhưng cũng tạo nên sự phức tạp nhất định.

##### Mô hình hoạt động 

<img src="http://users.skynet.be/spouseele/FTP/FTP-overview.gif" alt="FTP Model">

Protocol Interpreter (PI) là thành phần quản lý kênh điều khiển, nhiệm vụ của nó là phát và nhận lệnh

Data Transfer Process (DTP) có chức năng gửi và nhận dữ liệu giữa client và server

Bên cạnh đó, phía Client còn có thêm giao diện người dùng (user interface)

##### Thứ tự tiến trình 

- FTP Client liên lạc với FTP server ở cổng 21, sử dụng giao thức TCP 
- Client xác thực trên kết nối điều khiển sử dụng username và password
- Client gửi lệnh qua kết nối điều khiển 
- Khi server nhận được lệnh, nó mở cổng 20 để truyền file
- Khi truyền xong một file, server đóng kết nối dữ liệu


## 3. Cài đặt và cấu hình 

Để sử dụng dịch vụ FTP, Linux sử dụng gói phần mềm có tên : **vsftpd**

#####Cài đặt trên Ubuntu : 

	sudo apt-get install vsftpd
	
#####Cấu hình vsftpd :

	sudo vi /etc/vsftpd.conf

#####Một số thông số cần lưu ý : 

- Tắt truy cập ẩn danh :

	anonymous_enable=NO 

- Bỏ ghi chú ở tùy chọn `local_enable` và cho phép người dùng ghi vào thư mục :

	local_enable=YES
	
	write_enable=YES
	
- Bỏ ghi chú ở `chroot_local_user` , tất cả user sẽ hoạt động trong `chroot` của họ và sẽ không được quyền truy cập vào các phần khác của server.

	chroot_local_user=YES

#####Cấp quyền truy cập 

- Tạo một thư mục mới bên trong `home`:

	mkdir /home/username/files
	
- Thay đổi quyền truy cập file như `root`: 
	
	chown root:root /home/username
	
- Tạo những thay đổi cần thiết trong thư mục con

##### Sau tất cả, chúng ta cần restart dịch vụ để những thay đổi có hiệu lực :

	 sudo service vsftpd restart

### Truy cập vào FTP server

Do firewall trên máy chủ không cho phép dịch vụ FTP nên ta tắt firewall bằng lệnh :

	$ sudo ufw disable
	
##### Sử dụng giao diện console
Dùng Command Line ftp tới một máy chủ :

	> ftp host

<img src="http://i.imgur.com/3JlrouO.png">

Sử dụng `help` để xem các lệnh hỗ trợ

##### Browser

Nhập ftp://host để thiết lập kết nối ftp đến server 

<img src="http://i.imgur.com/LdjW5J2.png">

##### File zilla


## 4. Tham khảo

Book : Computer Networking A Top-Down Approach 6th-edition - Kurose Ross.

http://sinhvienit.net/forum/tim-hieu-ve-giao-thuc-ftp.28754.html

http://thachpham.com/hosting-domain/ftp-la-gi.html

