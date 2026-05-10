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
