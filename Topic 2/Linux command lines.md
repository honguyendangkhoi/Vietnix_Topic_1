# PING
<img width="696" height="173" alt="image" src="https://github.com/user-attachments/assets/a5693056-4ef1-4f84-bb33-b273713bf5cc" />

- Giải thích:
ping: sử dụng giao thức ICMP để gửi gói tin, chủ yếu để kiểm tra độ trễ và khả năng kết nối mạng cơ bản nhanh chóng
-trong đó:
ttl: là số bước nhảy (hop) qua các router
time: là thời gian trễ (latency) từ lúc máy tính gửi gói tin đến lúc gói tin được phản hồi về

# Hping3
<img width="734" height="171" alt="image" src="https://github.com/user-attachments/assets/322ef77d-af23-4529-9731-3afacaa3af63" />

- Giải thích:
hping3: là một công cụ phân tích và lắp ráp gói tin mạng TCP/IP thông qua command line

hping3 được gửi theo cú pháp:
hping 3 + loại gói tin + target + port + cách gửi
ví dụ:
hping 3 -1 google.com -p 80 -c 3
trong đó:
-1: là loại gói tin được gửi, ở đây là ICMP 
-target: là ip hoặc domain, ở đây là google.com
-p: là port, ở đây là 80
-c: là cách gửi, ở đây là gửi 3 gói tin

# SSH
- Kết nối bằng Mật khẩu:

```bash
ssh username@IP_Address
```
<img width="669" height="447" alt="image" src="https://github.com/user-attachments/assets/88c682a1-c3b5-4d9d-a938-3489bc035d01" />
ssh ubuntu@localhost

- Kết nối bằng key:
- ```bash
  ssh -i /path/to/private_key username@IP_Address
  ```
<img width="683" height="407" alt="image" src="https://github.com/user-attachments/assets/5e73f77c-06a2-445b-b4a7-256104bae0f8" />
trong đó:
-i (Identity file): là private key, dùng private key để xác nhận thay vì password
/.ssh/id_rsa: là đường dẫn đến nơi chứa private key trên máy tính

- Kết nối bằng Port Custom:
```bash
ssh -p custom_port username@IP_Address
```
<img width="683" height="407" alt="image" src="https://github.com/user-attachments/assets/d6d69a4f-5629-439a-b771-836c8d5263a2" />
trong đó:
-p: là port kết nối
custom_port: vì ssh mặc định sử dụng port 22 nên khi đổi sang port 2222 thì 2222 được gọi là custom 

# SCP
- copy 1 file:
<img width="733" height="96" alt="image" src="https://github.com/user-attachments/assets/149155c9-07bb-40c1-bf30-4ac3862d49fb" />

- copy 1 folder:
<img width="733" height="206" alt="image" src="https://github.com/user-attachments/assets/9a5abd44-4440-4055-b5e3-809646380db0" />

# Rsync:
- Copy file:
<img width="741" height="130" alt="image" src="https://github.com/user-attachments/assets/e0c43c8a-2316-4c05-93f7-22d2c2690727" />

- Copy folder:
<img width="741" height="184" alt="image" src="https://github.com/user-attachments/assets/87339dab-1bfc-48fe-8b73-8ec0d2b79c65" />

- Rsync Incremental:
<img width="741" height="284" alt="image" src="https://github.com/user-attachments/assets/babf90d3-b36f-4d44-a42b-85adac6ed16e" />
- lần đầu: copy toàn bộ dữ liệu
- lần sau: chỉ sync file/phần thay đổi

# CAT
<img width="676" height="119" alt="image" src="https://github.com/user-attachments/assets/3254291f-b512-4270-9541-032a02789a0f" />
xem nội dung 1 file

<img width="731" height="67" alt="image" src="https://github.com/user-attachments/assets/1566459a-60a7-4aaf-bd95-8c9f2621206f" />
xem dòng thứ '<n>' trong file

<img width="731" height="155" alt="image" src="https://github.com/user-attachments/assets/2356f8d1-f22d-41bd-87e0-33c9113fc546" />
ghi nhiều dòng vào 1 file sử bằng EOF

# ECHO
<img width="728" height="169" alt="image" src="https://github.com/user-attachments/assets/41a643c2-69a3-4184-9922-3886d1f52283" />
chèn thêm 1 dòng vào cuối file

<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/48b0ce6f-41cc-44aa-90be-99ecfc48ee28" />
overwrite nội dung

# HEAD
<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/2e895f02-fd7c-451d-8e4b-2cd2b792822b" />
in ra 3 dòng đầu của file

# TAIL
<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/18fdf963-e01e-464c-8734-b2ddae9a2ef7" />
in ra 3 dòng cuối của file

=> Head là lệnh xem đầu file, tail là lệnh xem cuối file

# TAILF
<img width="1039" height="213" alt="image" src="https://github.com/user-attachments/assets/653fb7d0-9e70-4744-abe1-de6779757ccf" />

## SỰ KHÁC NHAU CỦA TAILF VÀ TAIL:
TAILF: theo dõi file liên tục có thêm dòng mới không
TAIL: xem cuối file

# SED
<img width="741" height="152" alt="image" src="https://github.com/user-attachments/assets/8c8e37b1-06a4-45ae-a4e7-df476dfa4bc9" />

# SORT
- thứ tự tăng dần:
<img width="741" height="171" alt="image" src="https://github.com/user-attachments/assets/46c994d9-f1b2-4302-ade2-9fc7a863c6f7" />

- thứ tự giảm dần:
<img width="741" height="106" alt="image" src="https://github.com/user-attachments/assets/c26f1be2-dc70-421f-990c-4648009eb194" />

- sắp xếp theo cột:
bước 1:
<img width="734" height="151" alt="image" src="https://github.com/user-attachments/assets/ab5bc275-5339-407e-b50e-17f0286af651" />
 *tạo dữ liệu

bước 2:
<img width="734" height="107" alt="image" src="https://github.com/user-attachments/assets/d91aae23-c409-4443-b27a-6bd41acb441d" />
 *sắp xếp theo column 2

# UNIQ
- lọc dòng trùng:
bước 1:
<img width="748" height="351" alt="image" src="https://github.com/user-attachments/assets/7cc30e98-3022-4479-ac22-544dc4cb0392" />
*tạo dữ liệu

bước 2:
<img width="748" height="98" alt="image" src="https://github.com/user-attachments/assets/cddf76c4-3fb5-42ae-aadb-9f2aa4901deb" />
*lọc dữ liệu trùng

<img width="748" height="98" alt="image" src="https://github.com/user-attachments/assets/5f1cd814-bffe-4a8b-b177-e4738cf9a420" />
*đếm dữ liệu trùng

# WC
- đếm số dòng:
<img width="748" height="46" alt="image" src="https://github.com/user-attachments/assets/4c173a44-7652-48d6-9677-0af2f843ce32" />

- đếm số ký tự:
<img width="748" height="46" alt="image" src="https://github.com/user-attachments/assets/44039cdf-7708-441b-888c-6f3ad135cbb3" />

# CP
- copy file:
<img width="735" height="46" alt="image" src="https://github.com/user-attachments/assets/513f6aa8-e813-4242-9b0f-9071018b60da" />
<img width="301" height="46" alt="image" src="https://github.com/user-attachments/assets/ed9af079-252d-4d47-81e2-519aaf1fcfea" />

- copy folder:
<img width="735" height="46" alt="image" src="https://github.com/user-attachments/assets/97f2f7b9-7a21-4aa5-9795-d73185957329" />
<img width="735" height="46" alt="image" src="https://github.com/user-attachments/assets/d244e263-afda-4040-b045-e38eb8d4db2b" />

# MV
- Đổi tên file:
<img width="735" height="85" alt="image" src="https://github.com/user-attachments/assets/2b990acc-8915-478e-93f8-1453363fb31a" />

- Di chuyển folder:
<img width="735" height="169" alt="image" src="https://github.com/user-attachments/assets/14d99b32-fb0f-499b-933b-03c4f6e74571" />

# CUT
- Lấy thứ tự thứ '<n>':
<img width="735" height="49" alt="image" src="https://github.com/user-attachments/assets/848b9aa9-466e-4843-ad9f-ca1184c6f15b" />

- Lấy từ ký tự `<n>` trở về sau:

- Lấy đến ký tự thứ `<n>`:

# DIG COMMAND:
- Kiểm tra record A, MX, NS:

- Kiểm tra record A, MX, NS với custom DNS:

# Tar/Zip/Unzip Command:
- Nén/giải nén `tar.gz`:

- Nén/giải nén `.zip`:

# LS
- Liệt kê file/thư mục:

- Liệt kê file/thư mục và thuộc tính:

- Show file ẩn

# PS
- Show tiến trình

- Kill tiến trình

# Top Command
- Kiểm tra tài nguyên CPU

- Giải thích các thông số

# Free Command
- Giải thích các thông số về RAM:

# Df Command
- Xem dung lượng disk:

- Phân vùng `/` là gì:
