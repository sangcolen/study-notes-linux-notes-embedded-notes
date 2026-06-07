neu chua co file cau hinh
vi /etc/resolv.conf
namesever 8.8.8.8
namesever 8.8.4.4

Để chắc chắn mọi thứ hoạt động ngon lành, bạn chạy tuần tự các lệnh này trên máy Ubuntu (nếu lệnh nào chạy rồi thì chạy lại cũng không sao):

Bật chuyển tiếp gói tin:
Bash
sudo sysctl -w net.ipv4.ip_forward=1

Cấu hình NAT qua card ens33 (Lệnh vừa sửa ở trên):
Bash
sudo iptables -t nat -A POSTROUTING -o ens33 -j MASQUERADE
