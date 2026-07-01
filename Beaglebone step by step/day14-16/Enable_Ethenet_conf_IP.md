neu chua co file cau hinh tren bbb, xong ping 8.8.8.8 de kiem tra
vi /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4

Bước 1: Cho phép Ubuntu chuyển tiếp dữ liệu (IP Forwarding)
Bash
sudo sysctl -w net.ipv4.ip_forward=1

kiem tra da ket noi chua 
route add default gw 192.168.7.2/.6.2 usb0/usb1 nho 


Bước 2: Cấu hình NAT (iptables) để share Internet ubuntu
Bạn cần chỉ định rõ dữ liệu từ BeagleBone đi vào Ubuntu sẽ được "đẩy" ra ngoài mạng internet bằng card mạng nào. Thường trong bài học, lệnh sẽ dạng như thế này:
Bash
sudo iptables -t nat -A POSTROUTING -o <tên_card_mạng_internet> -j MASQUERADE
  Lưu ý: Hãy thay <tên_card_mạng_internet> bằng card mạng đang kết nối dải 192.168.17.0 của bạn (bạn có thể gõ ip a trên Ubuntu để xem tên chính xác của nó, thường là ens33, eth0, hoặc wlan0 nếu dùng wifi).

Thầy viết --table nat  Bạn viết gọn lại là -t nat
Thầy viết --append  Bạn viết gọn lại là -A
Thầy viết --out-interface  Bạn viết gọn lại là -o
Thầy viết --in-interface  Bạn viết gọn lại là -i
sudo iptables -A FORWARD -i <tên_card_mạng> -j ACCEPT

sudo ifconfig enx1cba8ca2ed6a 192.168.7.1 netmask 255.255.255.0 up
sudo ifconfig enx1cba8ca2ed6c 192.168.6.1 netmask 255.255.255.0 up

ping ww.google.com

---------------------sudo nmtui------------------------------- ben ubuntu
1. Cấu hình cho BeaglePlay USB0:
Chọn dòng BeaglePlay USB0 → nhấn Tab chọn <Edit...> ở bên phải → nhấn Enter.
Tìm mục IPv4 CONFIGURATION, đổi từ <Automatic> thành <Manual>.
Chọn <Show> ngay bên cạnh để hiện bảng cài đặt nâng cao.
Tại dòng Addresses, điền vào: 192.168.7.1/24
Di chuyển xuống dưới cùng chọn <OK> để lưu lại.

2. Cấu hình cho BeaglePlay USB1:
Chọn dòng BeaglePlay USB1 → nhấn Tab chọn <Edit...> → nhấn Enter.
Đổi mục IPv4 CONFIGURATION sang <Manual> → chọn <Show>.
Tại dòng Addresses, điền vào dải mạng số 6: 192.168.6.1/24
Di chuyển xuống dưới cùng chọn <OK> để lưu lại.
-------------------------------------------------------------
sudo systemctl restart NetworkManager
xoa may cái route add
sudo ip route flush cache
