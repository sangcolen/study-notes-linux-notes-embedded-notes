Dùng Diskpart có sẵn trên Windows (Không cần cài app)
Nếu lười tải app, m chơi thẳng bằng dòng lệnh Windows cho chất kĩ sư:

Bấm nút Windows, gõ cmd, chuột phải chọn Run as Administrator.

Gõ diskpart rồi nhấn Enter.

Gõ list disk để xem danh sách ổ cứng. Nhìn xem cái thẻ nhớ của m là Disk mấy (dựa vào dung lượng gốc của nó, ví dụ Disk 1 hoặc Disk 2). (Bước này phải nhìn cho kỹ kẻo chọn nhầm ổ cứng máy tính là bay màu dữ liệu nha Sang!).

Gõ select disk X (Thay X bằng số thứ tự của thẻ nhớ m vừa nhìn thấy).

Gõ clean (Lệnh này sẽ quét sạch toàn bộ các phân vùng ẩn Linux).

Gõ tiếp create partition primary để tạo lại một phân vùng duy nhất.

Cuối cùng gõ format fs=ntfs quick (hoặc fs=fat32) để định dạng lại là xong.


