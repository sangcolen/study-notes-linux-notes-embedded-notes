tao moi truong tftp host
Setting up a TFTP server on Ubuntu host
Step 1:  First on your Ubuntu host run the below command using your terminal program.

$ sudo apt-get update

$ sudo apt-get isntall

$ sudo apt upgrade 
----------------------------------------------------------

Step 2: install TFTP server

$ sudo apt-get install tftpd-hpa

This command installs the tftpd deamon. tftpd is a server for the Trivial File Transfer Protocol.    
----------------------------------------------------------
Step 3 : Create/Open the file “tftpd-hpa” in the below directory    

$ sudo vim /etc/default/tftpd-hpa  and put the below entry in to this file  and save it   
----------------------------------------------------------
Step 4: Add the Following Entries: Inside the file, add the following entries:

TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/var/lib/tftpboot"
TFTP_ADDRESS=":69"
TFTP_OPTIONS="--create --secure"
-----------------------------------------------------------
Step 5:   

Create a folder /var/lib/tftpboot and execute below commands    

$ sudo mkdir -p /var/lib/tftpboot

$ sudo chown tftp:tftp /var/lib/tftpboot

$ sudo chmod -R 777 /var/lib/tftpboot
------------------------------------------------------------
Step 6:Now we can start the TFTP daemon.  

$ sudo systemctl start tftpd-hpa
-------------------------------------------------------------
=> setenv serverip 192.168.1.29                                                 
=> setenv ipaddr 192.168.1.100 

tftpboot 0x82000000 uImage
tftpboot 0x88000000 am335x-boneblack.dtb
tftpboot 0x88080000 initramfs


sau khi kết nối có thể share file qua thủ mục /var/lib/tftp-boot
tftp -r helloworld -g 192.168.1.29
nếu có lỗi không kết nối thì
ifconfig eth0 192.168.1.100 setup lại ip đã cấp cho board ở trên
sau khi chạy lại tftp -r helloworld -g 192.168.1.29 file đã dung được file đã chia sẻ qua thư mục
có thể cat để xem nội dung
-------------------------------------------
root@am335x-evm:~# tftp -r helloworld -g 192.168.1.29                           
root@am335x-evm:~# ls                                                           
helloworld
root@am335x-evm:~# cat helloworld                                               
hello Sang        
-------------------------------------------
