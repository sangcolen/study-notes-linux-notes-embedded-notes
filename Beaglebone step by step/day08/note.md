PCB :Printed Circuit Board 
MPU : micro processor Unit

AM355x (arm cortex a8) gom: cache L1 (32KB cho Instruction (lệnh) và 32KB cho Data (dữ liệu)) có SED (Stack Error Detection) check
                            cache L2 (256KB) (như L1 nhưng để chung Instruction và Data) có ECC (Error Correction Code) check và sửa lôĩ
                            Rom, Ram

• GPMC: Chơi với NAND, NOR, SRAM (Bộ nhớ tĩnh/chậm).
GPMC (General-Purpose Memory Controller)
• EMIF: Chỉ chuyên trị DDR (RAM động/tốc độ cao).
EMIF (External Memory Interface.) Đây là bộ điều khiển phần cứng được thiết kế riêng để giao tiếp với các loại RAM động như DDR2, DDR3, hoặc mDDR

tinh RAM 
  4Gb (Gigabit): Đây là dung lượng tính theo từng bit nhị phân đơn lẻ.
  512MB (Megabyte): Đây là dung lượng tính theo Byte (1 Byte = 8 bit).

AM335x:
• Cortex-A8: Có.
• PRU: Có (2 nhân).(Programmable Real-Time Unit Chuyên xử lý các tác vụ thời gian thực (Real-time) cực nhanh mà không làm phiền đến nhân Cortex-A8 chính.).
• DSP: Không có (nhân DSP (Digital Signal Processor) chuyên dụng để tính toán số thực dấu phẩy động phức tạp).

Tại sao EEPROM lại luôn nằm ở I2C0?
Trong thiết kế phần cứng của BeagleBone Black:
• I2C0 (Internal/System): Đây là nhánh I2C "nội bộ" và quan quan trọng nhất. Nó kết nối với con chip quản lý nguồn (PMIC) và con EEPROM chứa thông tin định danh của board (tên board, số serial, revision).
• Tại sao lại là I2C0? Vì khi vừa cấp nguồn, CPU cần đọc thông tin từ EEPROM ngay lập tức để biết nó đang chạy trên phần cứng nào nhằm cấu hình các chân (Pinmux) và điện áp cho đúng. I2C0 là nhánh mặc định mà Bootloader (như U-Boot) sẽ quét đầu tiên.
• I2C1 và I2C2: Thường được đưa ra các chân cắm (header) P8 và P9 để mày kết nối với các cảm biến bên ngoài (LCD, cảm biến nhiệt độ, v.v.).
--> Lưu ý cực quan trọng cho dân làm OS
Khi viết code trong khóa của thầy Kiran:
• Mỗi bộ I2C (0, 1, 2) sẽ có một địa chỉ cơ sở (Base Address) khác nhau trong bộ nhớ.
• Nếu mày muốn đọc dữ liệu từ EEPROM, bắt buộc phải trỏ con trỏ C vào các thanh ghi của I2C0. Nếu trỏ sang I2C1 hay I2C2 thì sẽ chẳng thấy con EEPROM nào trả lời đâu.

cach tra tai lieu so do connect la tra ten chip tren board co ki hieu roi tra so do tra chan noi chan nao cha ten chip len mang tim
