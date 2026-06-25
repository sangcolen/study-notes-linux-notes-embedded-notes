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
cp: Sao chép tệp/thư mục (cp -r cho thư mục). cp -r * /thuMucCanCopy (-r * copy tat ca trong thu muc hien tai) khi nhieu file nang no se copy len RAM sau do bam "sync"
nếu ko cho ghi mà chỉ đọc thì sudo mount -o remount,rw /media/sang/ROOTFS
mv: Di chuyển hoặc đổi tên tệp/thư mục. 

3. Xem và Chỉnh sửa Tệp tin
cat: Xem nội dung file.
less / more: Xem file dài từng trang.
nano / vi: Trình soạn thảo văn bản ngay trong terminal. 

4. Quản lý Hệ thống và Quyền
sudo: Thực hiện lệnh với quyền root (cao nhất).
chmod: Thay đổi quyền truy cập file/thư mục (vd: chmod 755 file).
sudo chmod 755 chương_trình (chi tiết hơn ở dưới)
Số 7 (Chủ sở hữu - Người tạo ra file): Có toàn quyền tối cao. Được phép Đọc (4) + Ghi/Sửa (2) + Chạy file (1).
Số 6 trong lệnh chmod đại diện cho quyền Đọc và Ghi (Read & Write)
Số 5 (Nhóm sở hữu - Group): Chỉ được phép Đọc (4) + Chạy file (1). Nhóm này không có quyền chỉnh sửa hoặc xóa nội dung file.
Số 4 (Người ngoài hệ thống - Others): Chỉ được phép Đọc (4). Người ngoài không thể chỉnh sửa và cũng không thể chạy file này như một chương trình.
chown: Thay đổi chủ sở hữu file/thư mục.
top / htop: Xem tài nguyên hệ thống (CPU, RAM) đang chạy.
ps: Hiển thị danh sách các tiến trình (process) đang chạy.
kill: Dừng một tiến trình (vd: kill -9 PID). 

6. Mạng và Tìm kiếm
ping: Kiểm tra kết nối mạng.
ifconfig / ip a: Xem địa chỉ IP và thông tin mạng.
grep: Tìm kiếm văn bản trong file hoặc kết quả lệnh.
find: Tìm kiếm tệp tin trong hệ thống. 

7. Lệnh Khác
history: Xem lại lịch sử các câu lệnh đã nhập.
man: Xem hướng dẫn sử dụng của một lệnh (vd: man ls).
clear: Làm sạch màn hình terminal.

giải nén file: sudo tar -xvf Name.xz -C  /media/sang/ROOTFS/
 unxz nameFile.img.xz
-------------------------------------------------------------------------------------------------------------------------------------------------------
✨ 3 NHÓM QUYỀN TRÊN LINUX
Linux chia quyền truy cập file thành 3 nhóm chính:
Owner (u) – Người sở hữu file, thường là người tạo ra nó
Group (g) – Nhóm người dùng được gán cho file (ví dụ: team dev, team ops)
Others (o) – Tất cả những người còn lại trên hệ thống
Và 3 loại quyền:
r (read = 4) – Đọc file / liệt kê nội dung thư mục
w (write = 2) – Ghi, sửa, xóa nội dung
x (execute = 1) – Thực thi file hoặc truy cập vào thư mục
VD ĐỌC OUTPUT CỦA LỆNH ls -l
-rwxr-xr-- 1 alice devteam 4096 Jun 25 script.sh
Giải mã từng phần:
Ký tự đầu (-/d/l): loại file (file thường / thư mục / symlink)
rwx : Owner có full quyền (read + write + execute)
r-x : Group chỉ được đọc và thực thi
r-- : Others chỉ được đọc
⚡ CÁC TOOL PHÂN QUYỀN QUAN TRỌNG
chmod – Thay đổi quyền truy cập:
Symbolic: chmod u+x script.sh (thêm execute cho owner)
Octal: chmod 755 script.sh (tương đương rwxr-xr-x)
Recursive: chmod -R 644 /var/www/
chown – Đổi chủ sở hữu file:
chown alice script.sh → đổi owner thành alice
chown alice:devteam script.sh → đổi cả owner lẫn group
chgrp – Đổi nhóm sở hữu:
chgrp devteam script.sh
umask – Quyền mặc định khi tạo file mới:
umask 022 → file mới tạo ra sẽ có quyền 644, thư mục có 755
💡 TẠI SAO QUAN TRỌNG VỚI DEV & SYSADMIN?
Sai phân quyền là nguyên nhân phổ biến của nhiều sự cố thực tế:
Web server lỗi 403 Forbidden → thường do file thiếu quyền r hoặc thư mục thiếu x
Script không chạy được → thiếu quyền x
Lỗ hổng bảo mật nghiêm trọng → file config bị để 777 (mọi người đều ghi được!)
Quy tắc vàng: Principle of Least Privilege – chỉ cấp quyền tối thiểu cần thiết.
Một số giá trị octal phổ biến cần nhớ:
755 → Thư mục public, script có thể chạy
644 → File văn bản, config thông thường
600 → File nhạy cảm (SSH key, .env)
700 → Script chỉ owner mới chạy được
