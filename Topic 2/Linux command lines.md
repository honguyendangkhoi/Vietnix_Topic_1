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
*lấy thứ tự thứ 3

- Lấy từ ký tự `<n>` trở về sau:
<img width="735" height="49" alt="image" src="https://github.com/user-attachments/assets/7b93ba65-494d-49af-aa83-17615fb67344" />
*lấy từ thứ tự thứ 3 trở về sau

- Lấy đến ký tự thứ `<n>`:
<img width="735" height="49" alt="image" src="https://github.com/user-attachments/assets/8f3f2b91-4e26-41b9-a3b2-6b24f92b96ae" />
*lấy tới thứ tự thứ 4

# DIG COMMAND:
- Kiểm tra record A, MX, NS:

- Kiểm tra record A, MX, NS với custom DNS:

# Tar/Zip/Unzip Command:
- Nén/giải nén `tar.gz`:
<img width="735" height="136" alt="image" src="https://github.com/user-attachments/assets/585c9d80-3233-4768-b48f-6967d32584f6" />
*nén tar.gz

<img width="735" height="136" alt="image" src="https://github.com/user-attachments/assets/f815579b-0d31-4003-9185-d4f6416a90a7" />
*giải nén tar.gz

- Nén/giải nén `.zip`:
<img width="735" height="136" alt="image" src="https://github.com/user-attachments/assets/f42b3674-23cd-44e5-b2ea-75b93c066482" />
*nén zip

<img width="735" height="189" alt="image" src="https://github.com/user-attachments/assets/64dd6e84-b008-47d7-9bfc-515a7b65a86d" />
*giải nén zip

# LS
- Liệt kê file/thư mục:
<img width="735" height="44" alt="image" src="https://github.com/user-attachments/assets/32b83fe1-7665-4ad0-a031-6532f1068413" />

- Liệt kê file/thư mục và thuộc tính:
<img width="735" height="85" alt="image" src="https://github.com/user-attachments/assets/c17f36de-e398-4fc3-8794-9a9c6933e616" />

- Show file ẩn:
<img width="735" height="131" alt="image" src="https://github.com/user-attachments/assets/92f96506-f7dc-4d14-aecc-6979a0343f1b" />


# PS
- Show tiến trình:
<img width="735" height="131" alt="image" src="https://github.com/user-attachments/assets/1641ab45-be7c-4bc1-ad52-e2bece4d7ca7" />

- Kill tiến trình:
<img width="735" height="117" alt="image" src="https://github.com/user-attachments/assets/4ecd66c5-8aa1-4df9-b764-b505a7196141" />
<img width="735" height="31" alt="image" src="https://github.com/user-attachments/assets/aa59105a-64be-4288-9375-afb79beb87d6" />


# TOP COMMAND
- Kiểm tra tài nguyên CPU:
<img width="739" height="316" alt="image" src="https://github.com/user-attachments/assets/9dce91c4-00de-4781-986a-a2ac805e0924" />

- Giải thích các thông số:
load average: Tải trung bình của hệ thống trong 1, 5 và 15 phút vừa qua, trong hình là 0,55, 0,56, 0,58. Với con số 0,55, máy bạn đang tải rất nhẹ


# FREE COMMAND
- Giải thích các thông số về RAM:
<img width="735" height="81" alt="image" src="https://github.com/user-attachments/assets/6b8484ac-b7e9-42c6-902e-27cb540d6f97" />
trong đó:
Total (11Gi): Là tổng dung lượng RAM vật lý của máy
Used (4,1Gi): Dung lượng RAM đang được sử dụng
Free (1,7Gi): Dung lượng RAM hoàn toàn trống
Shared (45Mi): Dung lượng RAM được chia sẻ giữa các tiến trình
Buff/cache (5,2Gi): Là bộ nhớ đệm, cache
Available (6,5Gi): Là tổng lượng RAM thực sự có thể sử dụng cho các ứng dụng mới mà không cần phải dùng đến ổ cứng

# DF COMMAND
- Xem dung lượng disk:
<img width="735" height="169" alt="image" src="https://github.com/user-attachments/assets/4ecb2020-f919-479f-9098-233930934c7c" />

- Phân vùng `/` là gì:
  * Phân vùng `/` là điểm gốc, mọi file, thư mục, thiết bị phần cứng đều được gắn (mount) vào một vị trí bên dưới thư mục /.
  * Trong hình phân vùng /dev/sda2 có nghĩa toàn bộ hệ điều hành, các phần mềm cài đặt, và dữ liệu cá nhân của đều đang được lưu trữ trên phân vùng này.

# FIND
- Tìm file đuôi `.log`:
<img width="727" height="80" alt="image" src="https://github.com/user-attachments/assets/fbb0d376-0f51-49dc-99b5-f34b9fbe4bfb" />

- Tìm folder tên `abc`:
<img width="727" height="62" alt="image" src="https://github.com/user-attachments/assets/3f20a26c-5757-4e07-ae70-0bda96d313ad" />

- Tìm file tên `abc`:
<img width="727" height="78" alt="image" src="https://github.com/user-attachments/assets/e8ff5a7e-864e-44f0-b025-556ce0a3ef1e" />

- Tìm file `abc` và đặt quyền read only:
<img width="739" height="78" alt="image" src="https://github.com/user-attachments/assets/4eddee49-3a0d-4dbe-a9a2-f56dbec0cd89" />


# CHMOD, CHOWN, CHATTR COMMAND
- Phân quyền bằng số và chữ:
<img width="739" height="78" alt="image" src="https://github.com/user-attachments/assets/773b53e5-4b96-43fa-954a-e1775428d1b1" />
*phân quyền bằng số

<img width="739" height="78" alt="image" src="https://github.com/user-attachments/assets/a9b3e79e-f682-4e43-af99-218e4f9a0f00" />
*phân quyền bằng chữ

- Đổi owner user/group:
<img width="739" height="65" alt="image" src="https://github.com/user-attachments/assets/4a5119b3-fa8b-4e27-9742-f035072f585e" />

- Set Immutable Attribute:
<img width="619" height="181" alt="image" src="https://github.com/user-attachments/assets/bfcebbb2-e113-453b-b607-dd49e07ecb94" />


# NETSTAT
- Hiển thị các socket đang listen:
<img width="742" height="366" alt="image" src="https://github.com/user-attachments/assets/2b5df280-298c-4e2d-b382-633c26fda21f" />

- Không resolve hostname:
<img width="749" height="420" alt="image" src="https://github.com/user-attachments/assets/1e8de6b0-13aa-4439-afb2-504f5d2aa8c0" />

- Không resolve portname:
<img width="749" height="420" alt="image" src="https://github.com/user-attachments/assets/37618f39-92a8-486b-a7e7-cf4ff4e1047d" />

- Display process name/PID:
<img width="749" height="420" alt="image" src="https://github.com/user-attachments/assets/6b3443e8-65f5-415d-b33d-2d2acd3c7ba7" />

- Chỉ hiển thị socket TCP:
<img width="749" height="188" alt="image" src="https://github.com/user-attachments/assets/d845e21c-524a-4084-a17b-1737570c7775" />

- Chỉ hiển thị socket UDP:
<img width="716" height="165" alt="image" src="https://github.com/user-attachments/assets/e3c48c53-e4cf-465c-a6eb-100668912428" />

# TRACEROUTE
- Thực hiện và giải thích kết quả:

# SYMBOLIC LINK, HARD LINK COMMAND
- Định nghĩa Sym Link:

- Định nghĩa Hard Link:

- Ví dụ về Sym Link và Hard Link:

# MOUNT/UNMOUNT:
- Thêm ổ cứng `sdb` ~ 5gb:

- Kiểm tra số lượng ổ cứng

- Mount vào `/mnt/test`

- Umount `/mnt/test`
