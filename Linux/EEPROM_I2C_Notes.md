  240  top
  241  free -h
  242  lsblk
  243  cat /sys/dogtag
  244  history
  245  cat /etc/debian_version
  246  cat /etc/dogtag
  247  cat /sys/class/thermal/thermal_zone0/temp
  248  sudo poweroff
  249  i2cdetect -l
  250  sudo i2cdetect -y -r 2
  251  cat /sys/bus/i2c/devices/2-0054/eeprom
  252  sudo cat /sys/bus/i2c/devices/2-0054/eeprom
  253  sudo -i
  254  sudo cat /sys/bus/i2c/devices/2-0054/eeprom
  255  top
  256  free -h
  257  sudo i2cdump -y 2 0x54
  258  sudo cat /sys/class/i2c-adapter/i2c-2/2-0054/eeprom | hexdump -C
  259  echo 2-0054 | sudo tee /sys/bus/i2c/drivers/at24/unbind
  260  cat /etc/dogtag
  261  cat /etc/debian_version
  262  sudo i2cdump -y 2 0x54
  263  sudo i2cdump -y -f 2 0x54 w
  264  sudo i2cdump -y -f 2 0x54 c
  265  echo 24c32 0x54 | sudo tee /sys/bus/i2c/devices/i2c-2/new_device
  266  cat /sys/bus/i2c/devices/2-0054/eeprom | hexdump -C
  267  cat /etc/debian_version
  268  cat /etc/dogtag
  269  sudo poweroff

Bạn chạy lệnh này để bắt hệ thống thôi không quản lý con chip đó bằng driver mặc định nữa:

echo 2-0054 | sudo tee /sys/bus/i2c/drivers/at24/unbind
Lưu ý: Nếu nó báo lỗi "No such device", có nghĩa là driver đang quản lý nó tên là khác, hoặc nó đã tự nhả ra rồi.

Sau khi đã unbind, bạn hãy thử quét lại bằng i2cdump nhưng với tốc độ chậm hơn một chút để tránh Timed out:

sudo i2cdump -y 2 0x54

debian@beaglebone:~$ sudo i2cdump -y 2 0x54
No size specified (using byte-data access)
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f    0123456789abcdef
00: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
10: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
20: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
30: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
40: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
50: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
60: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
70: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
80: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
90: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
a0: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
b0: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
c0: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
d0: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
e0: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX
f0: XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX    XXXXXXXXXXXXXXXX

