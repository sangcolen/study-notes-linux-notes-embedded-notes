1. Kiểm tra RAM và CPU đang sử dụng (Thời gian thực)
top: Lệnh mặc định có sẵn trên mọi máy Linux. Nó hiển thị danh sách các tiến trình, tỉ lệ % CPU và RAM đang dùng.
htop: Phiên bản "nâng cấp" của top với giao diện màu sắc, dễ đọc hơn và hỗ trợ thao tác bằng chuột/phím tắt (thường cần cài đặt bằng sudo apt install htop).
vmstat: Báo cáo tóm tắt về bộ nhớ, tiến trình và hoạt động của CPU. 

2. Kiểm tra thông số phần cứng (Cấu hình)
Nếu bạn muốn biết tổng dung lượng RAM hay loại CPU của máy: 

free -h: Kiểm tra nhanh dung lượng RAM tổng, đã dùng và còn trống dưới định dạng dễ đọc (GB, MB).
lscpu: Hiển thị chi tiết thông tin về CPU (tên chip, số nhân, số luồng, tốc độ xung nhịp).
cat /proc/meminfo: Xem chi tiết tất cả các thông số chuyên sâu về bộ nhớ hệ thống.
cat /proc/cpuinfo: Xem thông tin chi tiết của từng nhân CPU. 

3. Các lệnh bổ trợ khác
nproc: Xem nhanh số lượng nhân (core) xử lý hiện có.
iostat: Theo dõi tải của CPU và hiệu suất xuất/nhập dữ liệu của ổ đĩa.

1. Quản lý Thư mục và Tệp tin
ls: Liệt kê nội dung thư mục (ls -la xem chi tiết bao gồm file ẩn).
cd: Thay đổi thư mục (vd: cd /home, cd .. để lên thư mục cha).
pwd: Hiển thị đường dẫn tuyệt đối của thư mục đang đứng.
mkdir: Tạo thư mục mới (vd: mkdir folder_name).
touch: Tạo file trống mới (vd: touch file.txt).
rm: Xóa tệp hoặc thư mục (rm -rf xóa thư mục và nội dung bên trong).
cp: Sao chép tệp/thư mục (cp -r cho thư mục). cp -r * /thuMucCanCopy (-r * copy tat ca trong thu muc hien tai)
mv: Di chuyển hoặc đổi tên tệp/thư mục. 

2. Xem và Chỉnh sửa Tệp tin
cat: Xem nội dung file.
less / more: Xem file dài từng trang.
nano / vi: Trình soạn thảo văn bản ngay trong terminal. 

3. Quản lý Hệ thống và Quyền
sudo: Thực hiện lệnh với quyền root (cao nhất).
chmod: Thay đổi quyền truy cập file/thư mục (vd: chmod 755 file).
chown: Thay đổi chủ sở hữu file/thư mục.
top / htop: Xem tài nguyên hệ thống (CPU, RAM) đang chạy.
ps: Hiển thị danh sách các tiến trình (process) đang chạy.
kill: Dừng một tiến trình (vd: kill -9 PID). 

4. Mạng và Tìm kiếm
ping: Kiểm tra kết nối mạng.
ifconfig / ip a: Xem địa chỉ IP và thông tin mạng.
grep: Tìm kiếm văn bản trong file hoặc kết quả lệnh.
find: Tìm kiếm tệp tin trong hệ thống. 

5. Lệnh Khác
history: Xem lại lịch sử các câu lệnh đã nhập.
man: Xem hướng dẫn sử dụng của một lệnh (vd: man ls).
clear: Làm sạch màn hình terminal.
