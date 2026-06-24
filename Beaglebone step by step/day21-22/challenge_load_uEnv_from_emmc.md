set up environment code C gcc

load mmc

Ngặt một nỗi, ở các bản Kernel cũ như bản 4.19.94-ti-r42 mày đang chạy, tên định danh của cổng Serial trong Kernel đã bị các nhà phát triển đổi từ ttyO0 (chữ O) sang ttyS0 (chữ S - Standard 8250 serial driver).

setenv bootargs "console=ttyS0,115200n8 root=/dev/mmcblk1p1 rw rootwait"

load  mmc 1:1 0x90000000 /boot/dtbs/4.19.94-ti-r42/am335x-boneblack.dtb

load mmc 1:1 0x82000000 /boot/vmlinuz-4.19.94-ti-r42 

bootz 0x82000000 - 0x90000000 
