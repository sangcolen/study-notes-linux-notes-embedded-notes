1. Giải nén file .zip
  Sử dụng lệnh unzip:
   unzip ten_file.zip
  Để giải nén vào một thư mục chỉ định:
   unzip ten_file.zip -d /duong/dan/den/thu_muc/

2. Giải nén file .tar.gz hoặc .tgz
  Sử dụng lệnh tar với các tùy chọn ( -x để giải nén, -z cho gzip, -v hiển thị tiến trình, -f chỉ định tệp):
   tar -zxvf ten_file.tar.gz

3. Giải nén file .tar.xz
  Tương tự nhưng sử dụng cờ -J cho xz:
    tar -Jxvf ten_file.tar.xz

4. Giải nén file .tar.bz2 hoặc .tbz2
  Sử dụng cờ -j cho bzip2:
   tar -jxvf ten_file.tar.bz2
  Để giải nén vào một thư mục chỉ định:
   tar -jxvf ten_file.tar.bz2 -C /duong/dan/den/thu_muc/

5. Giải nén file .tar (chưa nén)Chỉ cần bỏ qua cờ nén (z, j, hoặc J):
   tar -xvf ten_file.tar

6. Giải nén file .gz (đơn lẻ)Sử dụng lệnh gunzip:
   gunzip ten_file.gz

7. Giải nén file .rar
  Lệnh này cần cài thêm gói (thường là unrar). Để cài đặt, hãy chạy sudo apt install unrar (trên Ubuntu/Debian) hoặc sudo yum install unrar (trên CentOS).
   unrar x ten_file.rar
