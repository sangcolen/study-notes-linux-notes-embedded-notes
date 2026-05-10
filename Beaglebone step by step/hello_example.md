Mở terminal trên con BBB lên và gõ:

make (để biên dịch ra file hello.ko).

sudo insmod hello.ko (để nạp driver vào nhân).

dmesg | tail (để xem kết quả).

Gõ: nano hello.c (hoặc vi hello.c nếu mày muốn khổ dâm).

Dán đoạn code tao đưa lúc nãy vào.

Nhấn Ctrl + O rồi Enter để lưu, Ctrl + X để thoát.

Làm tương tự với file Makefile.
1. Nano: Người bạn quốc dân (Dễ như Notepad)
Cách dùng: Mày nhìn thấy gì là mày gõ đó. Muốn lưu hay thoát thì nhìn xuống dưới cùng màn hình, nó có hướng dẫn sẵn (ví dụ ^O là Ctrl + O để lưu).

Ưu điểm: Cực kỳ trực quan, không cần học cũng dùng được ngay.

Nhược điểm: Làm mấy việc phức tạp như tìm kiếm, thay thế hàng loạt thì hơi chậm.

Dành cho ai: Những người đang bị nóng 34°C hành hạ và chỉ muốn gõ xong cái code hello.c nhanh nhất có thể. Mày nên dùng cái này ngay lúc này!

2. Vi (hoặc Vim): "Quái vật" của dân Pro
Cách dùng: Nó cực kỳ dị. Mới vào mày không thể gõ chữ ngay được.

Mày phải nhấn phím i để vào chế độ "Insert" thì mới gõ code được.

Gõ xong muốn lưu thì phải nhấn Esc, rồi gõ :wq (write and quit).
----------------------------------------------------------------------
#include <linux/module.h>
#include <linux/init.h>

/* Hàm này chạy khi mày nạp driver (insmod) */
static int __init sang_init(void) {
    printk(KERN_INFO "Sang dep trai: Kernel xin chao!\n");
    return 0;
}

/* Hàm này chạy khi mày gỡ driver (rmmod) */
static void __exit sang_exit(void) {
    printk(KERN_INFO "Sang dep trai: Tam biet, hen gap lai.\n");
}

module_init(sang_init);
module_exit(sang_exit);

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Sang");
MODULE_DESCRIPTION("Driver dau tay cua Sang dep trai");
----------------------------------------------------------------------
tao MakeFile
obj-m := hello.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
----------------------------------------------------------------------
kiem tra
drwx------ 3 debian debian 4096 Apr  6 13:43 .gnupg
-rw-r--r-- 1 debian debian  525 Apr  6 16:58 hello.c
-rw-r--r-- 1 debian debian  155 Apr  6 17:02 MakeFile.c
-rw-r--r-- 1 debian debian  807 Apr 18  2019 .profile
-rw------- 1 debian debian 1185 Apr  6 17:02 .viminfo
-rw-r--r-- 1 debian debian   64 Apr  6 13:33 .xsessionrc
debian@beaglebone:~$ pwd
/home/debian
debian@beaglebone:~$ mv MakeFile.c Makefile
debian@beaglebone:~$ ls-la
-bash: ls-la: command not found
debian@beaglebone:~$ ls -la
total 52
drwxr-xr-x 5 debian debian 4096 Apr  6 17:05 .
drwxr-xr-x 3 root   root   4096 Apr  6 13:33 ..
-rw------- 1 debian debian  265 Apr  6 16:51 .bash_history
-rw-r--r-- 1 debian debian  220 Apr 18  2019 .bash_logout
-rw-r--r-- 1 debian debian 3526 Apr 18  2019 .bashrc
drwxr-xr-x 2 debian debian 4096 Apr  6 13:33 bin
lrwxrwxrwx 1 debian debian   16 Apr  6 17:03 .c9 -> /opt/cloud9/.c9/
drwx------ 4 debian debian 4096 Apr  6 14:05 .config
-rw-r--r-- 1 debian debian    0 Apr  6 13:34 .gitconfig
drwx------ 3 debian debian 4096 Apr  6 13:43 .gnupg
-rw-r--r-- 1 debian debian  525 Apr  6 16:58 hello.c
-rw-r--r-- 1 debian debian  155 Apr  6 17:02 Makefile
-rw-r--r-- 1 debian debian  807 Apr 18  2019 .profile
-rw------- 1 debian debian 1185 Apr  6 17:02 .viminfo
-rw-r--r-- 1 debian debian   64 Apr  6 13:33 .xsessionrc
debian@beaglebone:~$

