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


## 4. 
