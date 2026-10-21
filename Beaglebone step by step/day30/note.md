Compilation of U-boot Source Tree
+ Method1: Execute the script

sudo chmod +x build-am335x.sh

sudo ./build-am335x.sh

+ Method2: Execute Commands Manually

ls configs/ | grep am335x    tim file co chu am335x o dau

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- am335x_boneblack_vboot_defconfig     kiem xong thay vao cuoi
