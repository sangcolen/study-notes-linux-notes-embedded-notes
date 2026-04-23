 USB-to-TTL

Các phần mềm phổ biến theo hệ điều hành:
Cho Windows:

PuTTY: Phổ biến nhất, cực kỳ nhẹ và đa năng, hỗ trợ cả Serial và SSH.
Tera-Term: Rất ổn định, cho phép quản lý các cổng COM (Serial) rất chi tiết và hỗ trợ truyền file qua giao thức XMODEM/YMODEM.
Hyper-Terminal: Một công cụ cũ trên các bản Windows đời đầu, hiện nay ít dùng hơn hai loại trên.

Cho Ubuntu (Linux):

minicom: Chạy trực tiếp trên giao diện dòng lệnh (Terminal) của Linux. 

Tại sao bạn cần chúng ngay lúc này?
Thay thế màn hình HDMI

Debug lỗi hệ điều hành: Khi bạn học khóa "OS Development From Scratch", nếu kernel bị lỗi (kernel panic), nó sẽ không hiện gì trên màn hình HDMI hay SSH được. Chỉ có cổng Serial mới xuất ra được các dòng thông báo lỗi cuối cùng để biết sửa.

1. Khi nào dùng MobaXterm (Tiện cho Windows)
Nếu bạn cắm cáp USB-to-TTL trực tiếp vào máy tính Windows, MobaXterm là "vua". Nó có giao diện đồ họa, dễ copy-paste, quản lý nhiều tab (SSH, Serial, SFTP) rất sướng.

Bạn dùng Windows để đọc tài liệu, xem video, và dùng MobaXterm để gõ lệnh điều khiển BeagleBone.

2. Khi nào dùng Minicom (Chuẩn dân Linux)
Làm việc tập trung: Nếu bạn đang ở trong Ubuntu để biên dịch code (Compile), rồi muốn nạp và chạy thử ngay mà không muốn chuyển qua chuyển lại giữa cửa sổ Linux và Windows, thì mở minicom ngay trong Ubuntu sẽ nhanh hơn.

Tương thích tuyệt đối: Một số lệnh hoặc scripts tự động (automation) trong khóa học OS có thể gọi trực tiếp đến minicom để thực hiện tác vụ nào đó mà MobaXterm không làm được.

Môi trường thuần Linux: Video hướng dẫn dùng Ubuntu vì dân chuyên nghiệp thường muốn "nhốt" toàn bộ công cụ vào một chỗ. Nếu bạn dùng máy ảo (VMware/VirtualBox), bạn phải "Pass-through" thiết bị USB từ Windows vào Ubuntu thì minicom mới thấy cổng để chạy.

Chốt lại là:
Bạn không cần dùng cả hai cùng lúc cho một kết nối. (Vì một cổng COM/ttyUSB chỉ có một phần mềm được chiếm dụng thôi).

Lời khuyên: Nếu bạn cảm thấy dùng MobaXterm trên Windows thoải mái hơn thì cứ dùng MobaXterm. Bạn chỉ cần dùng Ubuntu để biên dịch code (tạo ra file .bin hay .img), còn việc xem log hay gõ lệnh thì MobaXterm xử lý tốt chán.

Nhưng có một điểm cộng cho việc cài minicom: Vì bạn đang học khóa "OS Development From Scratch", sau này sẽ có lúc bạn cần viết script để tự động hóa việc debug.
