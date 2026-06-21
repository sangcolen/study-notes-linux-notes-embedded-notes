&#x20;loaded the Linux kernel image to the DDR memory from MMC 0 (SD card) interfaceD

&#x20;load zImage 

load mmc 0:3 0x82000000 /boot/vmlinuz-6.18.32-bone35



&#x20;loaded the dtb image to the DDR memory from MMC 0 (SD card) interface

&#x20;load dtb

load mmc 0:3 0x88000000 /boot/dtbs/6.18.32-bone35/am335x-boneblack.dtb



&#x20;Boot from memory comand

&#x20;Kích hoạt Boot hệ thống (load file **zImage** thi dung bootz, load **uImage** thì dùng bootm)

Gõ lệnh kết hợp cả địa chỉ RAM của Kernel và DTB (dấu gạch ngang ở giữa nghĩa là bỏ qua ramdisk)

bootz 0x82000000 - 0x88000000



send bootargs to the Linux kernel from u-boot (ls mmc 0:3 hoac thay 0:2 de tim rootfs)

setenv bootargs console=ttyO0,115200 root=/dev/mmcblk0p3 rw 

&#x20;Nếu vẫn lỗi trên thẻ nhớ của ông đã có sẵn file Ramdisk chuẩn đi kèm với bản Kernel này rồi! Tên file là: initrd.img-6.18.32-bone35.

setenv bootargs "console=ttyO0,115200n8 root=/dev/mmcblk0p3 rw rootwait"

&#x20;Nếu bị reboot liên tục sau khi khắc phục lỗi trên thì chặn watchdog để khởi động

setenv bootargs "console=ttyO0,115200n8 root=/dev/mmcblk0p3 rw rootwait watchdog.watchdog\_thresh=0 omap\_wdt.nowayout=1"



Nếu KHÔNG có rootwait: Kernel lao đến chỗ thẻ nhớ, thấy driver chưa kịp dựng xong phân vùng mmcblk1p3 -> Nó tưởng phân vùng này bị xóa hoặc không tồn tại -> Nó quẳng ra lỗi Kernel panic ngay lập tức ở giây thứ 4.



Nếu CÓ rootwait: Kernel lao đến, thấy thẻ nhớ chưa sẵn sàng, nó sẽ block (tạm dừng) tiến trình mount lại, kiên nhẫn đợi thêm vài mili-giây nữa. Ngay khi thẻ SD khởi động xong và báo cáo "Tôi có phân vùng 3 rồi đây!", Kernel sẽ bốc lấy và đi tiếp mà không bị Panic giữa đường.

\--------------------------------------------------------------------------

loadx send/receive file using xmodem protocal

loady send/receive file using ymodem protocal

loady send/receive file using zmodem protocal



ctrl + a, s

hiện giao diện x,y,zmodem,kermit,ascii hiển thị những cái minicom có hỗ trợ chọn ymodem

dùng mũi tên lên xuống để navigate, press space two times in order to selected



=> đã tới bước load file uEnv















