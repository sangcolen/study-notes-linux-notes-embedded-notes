booting serial uart port

ctrl + a, s
có thể dung các loại modem (hiện tại dung xmodem) các bước chọn file đều dung xmodem
load spl -> u-boot.img (sau đó canh bấm dấu cách để vào setting environmental variable) --> chọn uimage

thứ tự file load
u-boot-spl.bin -> u-boot.img -> uImage -> dtb -> initramfs

recommended load address
Linux kernel image 0x82000000
FDT & DTB 0x88000000
RAMDISK or Initramfs 0x88080000

initramfs laf file nén các driver phần cứng cần thiết, thay vì để chung vào kernel sẽ rất nặng nếu nhiều loại board. nên thay vào đó file nén này sẽ để riêng sẽ được chạy cùng bước load kernel, 
sao đó file này được giải nén trên ram load driver cần thiết để đọc phân vùng ổ cứng chứa hệ điều hành chính root (có /) sau đó switch_root nhường quyền cho OS Linux và giải phóng ram

sau khi load xong 5 file thì set biến bootargs

setenv bootargs console=ttyO0,115200 root=/dev/ram0 rw initrd=0x88080000

bootm 0x82000000 0x88080000 0x88000000

dang nhap la root
