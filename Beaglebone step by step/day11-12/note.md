Khi m đang làm việc ở tầng thấp (OS Development), mỗi lần m chỉnh sửa code U-Boot 
hoặc build xong một file kernel mới trên máy tính, m phải tìm cách chuyển cái file đó từ máy tính sang con BeagleBone Black để chạy thử.

Thầy đang bảo là thay vì mỗi lần sửa code m lại phải rút thẻ nhớ ra, cắm vào máy tính, copy file, 
rồi lại cắm ngược vào bo (cực kỳ thủ công và dễ hư khe thẻ), 
thì thầy sẽ dạy m cách dùng các giao thức truyền file trực tiếp qua dây cáp kết nối giữa Máy tính và Bo mạch:

X-Modem / Y-Modem: Là các giao thức truyền file đời đầu, cực kỳ quen thuộc khi m kết nối qua cổng Serial (UART/Minicom). 
U-Boot nó có sẵn lệnh để hứng file truyền từ máy tính qua đường Serial này luôn.

TFTP (Trivial File Transfer Protocol): Cái này là "vũ khí hạng nặng" nè. Khi con BBB của m kết nối mạng LAN với máy tính, 
m biến máy tính thành một TFTP Server. Con U-Boot trên BBB chỉ cần chạy một lệnh là nó tự kéo file kernel từ máy tính qua dây mạng trong vòng 1 giây.
------------------------------------------------------------------------------------------
zImage: Đây là file nén của Linux Kernel sau khi m compile (biên dịch) xong. Nó ở định dạng ELF binary format. Tuy nhiên, một mình con zImage này thì con bootloader U-Boot nó không hiểu. Nó giống như một cuốn sách hay nhưng không có bìa và mục lục, U-Boot nhìn vào sẽ không biết phải đọc từ đâu.

64 bytes of u-boot image header: Đây chính là cái "bìa sách". 64 byte này chứa các thông tin metadata cực kỳ quan trọng như: loại CPU (ARM), hệ điều hành (Linux), địa chỉ sẽ load vào RAM, checksum để kiểm tra file có lỗi không, thời gian tạo file....

mkimage: Đây là một công cụ (command tool) đi kèm của U-Boot. Nhiệm vụ của nó là làm thợ đóng sách: lấy 64 byte header dán vào đầu file zImage.

uImage: Là thành phẩm cuối cùng sau khi dán header. Đúng như sub trong hình ghi: "uImage is nothing but zImage plus u-boot header" (uImage không có gì khác ngoài zImage cộng thêm u-boot header).
-------------------------------------------------------------------------------------------
1. Bài toán tính dung lượng (Structure Size)
   Dựa vào các kiểu dữ liệu trong hình, m cộng nhẩm với t nè:
uint32_t nặng 4 bytes. Có 7 biến đầu tiên (ih_magic tới ih_dcrc) 7 * 4 = 4 bytes.
uint8_t nặng 1 byte. Có 4 biến tiếp theo (ih_os, ih_arch, ih_type, ih_comp) 4 * 1 = 4 bytes.
uint8_t ih_name[IH_NMLEN];: Đây là một mảng ký tự để đặt tên cho Image.
Trong mã nguồn của U-Boot, cái hằng số IH_NMLEN này được #define cố định là 32.Vậy mảng này nặng 32 * 1 = 32 bytes.
=> Tổng cộng = 28 + 4 + 32 = 64 bytes
Quá chuẩn chỉnh! Không có một byte nào bị thừa hay dính structure padding ở đây hết.

2. Ý nghĩa của từng thanh ghi (Trường dữ liệu) m đang nhìn:
Mấy cái comment tiếng Anh bên cạnh giải thích rất rõ, t tóm gọn lại bản chất cho m dễ nuốt:

ih_magic (Magic Number): Một con số đặc biệt (thường là 0x27051956 cho U-Boot). Khi U-Boot đọc file,
việc đầu tiên là nó check xem 4 byte đầu có đúng con số này không. Nếu không đúng,
nó biết ngay đây không phải file uImage hợp lệ và từ chối boot.

ih_hcrc & ih_dcrc (Checksum): Mã CRC32 dùng để kiểm tra xem file của m có bị lỗi trong quá trình truyền file (qua TFTP/X-Modem) 
hoặc bị bad sector trên thẻ nhớ không. Một bit bị sai là nó báo lỗi liền.ih_time: Thời gian m gõ lệnh mkimage để build ra file này.

ih_size: Kích thước thực tế của phần file zImage (phần ruột) nằm phía sau.

ih_load (Load Address): Địa chỉ đích trên RAM mà U-Boot phải copy toàn bộ file Kernel vào đó.

ih_ep (Entry Point Address): Địa chỉ của dòng lệnh đầu tiên trong Kernel. Khi nạp xong vào RAM, CPU sẽ nhảy thẳng tới địa chỉ này để bắt đầu chạy Linux.

ih_os, ih_arch, ih_type, ih_comp: Khai báo hệ điều hành (Linux), kiến trúc chip (ARM), kiểu image (Kernel), và kiểu nén (gzip hay bzip2 để U-Boot biết đường mà giải nén).

