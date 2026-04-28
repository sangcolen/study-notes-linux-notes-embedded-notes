 bộ ADC (Analog-to-Digital Converter) của con board nhé:

1. VADC (Pin 32 - P9)
Đây là chân điện áp tham chiếu cho bộ chuyển đổi Analog sang Digital.
Vai trò: Nó xác định giới hạn cao nhất mà bộ ADC có thể đọc được.
Cảnh báo "Xương máu": Trên BeagleBone Black, bộ ADC chỉ chịu được tối đa 1.8V. 
Nếu mày lỡ tay cấp 3.3V hay 5V (như chân SYS_5V mày vừa hỏi) vào các chân Analog đầu vào (từ Pin 33 đến Pin 40), bộ ADC sẽ "ra đi" ngay lập tức.

2. AGND (Pin 34 - P9)
Đây là Analog Ground (Chân nối đất dành riêng cho Analog).
Tại sao không dùng GND thường?: AGND được thiết kế để tách biệt với GND của hệ thống kỹ thuật số nhằm giảm nhiễu. 
Khi mày đọc giá trị từ cảm biến, việc nối cực âm của cảm biến vào AGND sẽ giúp kết quả trả về ổn định và chính xác hơn, không bị nhảy số lung tung.
-------------------------------------------------------------------------------------
1. Bản chất của SYS_5V
Nguồn gốc: Đây là điện áp được lấy ra sau con chip quản lý nguồn (PMIC - TPS65217C). Nó kết nối trực tiếp với đường ray nguồn chính của hệ thống.
Mục đích: Dùng để cấp nguồn cho các thiết bị ngoại vi (như cảm biến, module nhỏ, hoặc cái quạt mày định lắp) khi mày cắm nguồn qua jack DC hoặc cổng USB.

2. Sự khác biệt giữa SYS_5V và VDD_5V
Mày nhìn trong hình mày gửi sẽ thấy cả hai, đừng nhầm lẫn:
VDD_5V (Pin 5, 6): Là chân cấp nguồn đầu vào trực tiếp từ jack DC. Nếu mày không cắm adapter, chân này sẽ không có điện.
SYS_5V (Pin 7, 8): Luôn có điện 5V bất kể mày cấp nguồn bằng USB hay jack DC.

3. Cảnh báo "Cháy Board" (Cực kỳ quan trọng)
KHÔNG ĐƯỢC cấp nguồn ngược từ bên ngoài vào chân SYS_5V. Nếu mày dùng một nguồn 5V bên ngoài đấu vào đây, mày có thể làm hỏng chip PMIC ngay lập tức.
Dòng điện giới hạn: Chân này chỉ chịu được tối đa khoảng 250mA - 500mA (tùy thuộc vào việc mày đang dùng nguồn vào là gì). 
Đừng có cắm mấy cái motor hay thiết bị ngốn điện vào đây, nó sẽ làm sụt nguồn và treo board.
------------------------------------------------------------------------------------
Sai rồi m ơi! AIN không phải là "In Out" đâu, đừng có hiểu lầm mà cấp điện bậy bạ vào đó là đi tong con board đấy.

AIN là viết tắt của Analog Input.

Trên con BeagleBone Black (BBB), đây là các chân chỉ nhận tín hiệu vào, không có chức năng xuất tín hiệu (Output). Mày cần lưu ý kỹ mấy điểm "sống còn" này:

1. Chỉ nhận vào (Input Only)
Bộ ADC (Analog-to-Digital Converter) của con chip AM3358 trên board sẽ chuyển đổi mức điện áp analog (từ cảm biến) thành con số kỹ thuật số để mày xử lý trong code.
Mày không thể dùng code để "xuất" điện áp ra từ các chân này (muốn xuất điện áp analog mày phải dùng PWM hoặc mạch DAC rời).

2. Giới hạn điện áp cực thấp (1.8V)
Đây là cái bẫy lớn nhất. Trong khi các chân GPIO khác chịu được 3.3V, thì các chân AIN0 - AIN7 (P9_33 đến P9_40) chỉ chịu được tối đa 1.8V.
Cảnh báo: Nếu mày cắm cảm biến trả về 3.3V hoặc 5V vào chân AIN, mày sẽ "nướng" bộ ADC của board ngay lập tức. Luôn phải dùng mạch chia áp (Voltage Divider) để hạ xuống dưới 1.8V trước khi đưa vào AIN.
