# Linux Command Line

# PING

<img width="696" height="173" alt="image" src="https://github.com/user-attachments/assets/a5693056-4ef1-4f84-bb33-b273713bf5cc" />

## Giải thích:
`ping`: sử dụng giao thức ICMP để gửi gói tin, chủ yếu để kiểm tra độ trễ và khả năng kết nối mạng cơ bản nhanh chóng

### Trong đó:
- `ttl`: là số hop tối đa gói tin được phép đi qua trước khi bị hủy
- `time`: là thời gian trễ (latency) từ lúc máy tính gửi gói tin đến lúc gói tin được phản hồi về

---

# Hping3

<img width="734" height="171" alt="image" src="https://github.com/user-attachments/assets/322ef77d-af23-4529-9731-3afacaa3af63" />

## Giải thích:
`hping3`: là một công cụ phân tích và lắp ráp gói tin mạng TCP/IP thông qua command line

### hping3 được gửi theo cú pháp:
```bash
hping3 + loại gói tin + target + port + cách gửi
```

### Ví dụ:
```bash
hping3 -1 google.com -p 80 -c 3
```

### Trong đó:
- `-1`: là loại gói tin được gửi, ở đây là ICMP
- `target`: là ip hoặc domain, ở đây là google.com
- `-p`: là port, ở đây là 80
- `-c`: là số lượng gói tin, ở đây là gửi 3 gói tin

---

# SSH

## Kết nối bằng Mật khẩu

```bash
ssh username@IP_Address
```

<img width="669" height="447" alt="image" src="https://github.com/user-attachments/assets/88c682a1-c3b5-4d9d-a938-3489bc035d01" />

```bash
ssh ubuntu@localhost
```

---

## Kết nối bằng key

```bash
ssh -i /path/to/private_key username@IP_Address
```

<img width="683" height="407" alt="image" src="https://github.com/user-attachments/assets/5e73f77c-06a2-445b-b4a7-256104bae0f8" />

### Trong đó:
- `-i (Identity file)`: là private key, dùng private key để xác nhận thay vì password
- `~/.ssh/id_rsa`: là đường dẫn đến nơi chứa private key trên máy tính

---

## Kết nối bằng Port Custom

```bash
ssh -p custom_port username@IP_Address
```

<img width="683" height="407" alt="image" src="https://github.com/user-attachments/assets/d6d69a4f-5629-439a-b771-836c8d5263a2" />

### Trong đó:
- `-p`: là port kết nối
- `custom_port`: vì ssh mặc định sử dụng port 22 nên khi đổi sang port 2222 thì 2222 được gọi là custom port

---

# SCP

## Copy 1 file

<img width="733" height="96" alt="image" src="https://github.com/user-attachments/assets/149155c9-07bb-40c1-bf30-4ac3862d49fb" />

---

## Copy 1 folder

<img width="733" height="206" alt="image" src="https://github.com/user-attachments/assets/9a5abd44-4440-4055-b5e3-809646380db0" />

---

# Rsync

## Copy file

<img width="741" height="130" alt="image" src="https://github.com/user-attachments/assets/e0c43c8a-2316-4c05-93f7-22d2c2690727" />

---

## Copy folder

<img width="741" height="184" alt="image" src="https://github.com/user-attachments/assets/87339dab-1bfc-48fe-8b73-8ec0d2b79c65" />

---

## Rsync Incremental

<img width="741" height="284" alt="image" src="https://github.com/user-attachments/assets/babf90d3-b36f-4d44-a42b-85adac6ed16e" />

- Lần đầu: copy toàn bộ dữ liệu
- Lần sau: chỉ sync file/phần thay đổi

---

# CAT

## Xem nội dung 1 file

<img width="676" height="119" alt="image" src="https://github.com/user-attachments/assets/3254291f-b512-4270-9541-032a02789a0f" />

---

## Xem dòng thứ `<n>` trong file

<img width="731" height="67" alt="image" src="https://github.com/user-attachments/assets/1566459a-60a7-4aaf-bd95-8c9f2621206f" />

---

## Ghi nhiều dòng vào 1 file sử bằng EOF

<img width="731" height="155" alt="image" src="https://github.com/user-attachments/assets/2356f8d1-f22d-41bd-87e0-33c9113fc546" />

---

# ECHO

## Chèn thêm 1 dòng vào cuối file

<img width="728" height="169" alt="image" src="https://github.com/user-attachments/assets/41a643c2-69a3-4184-9922-3886d1f52283" />

---

## Overwrite nội dung

<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/48b0ce6f-41cc-44aa-90be-99ecfc48ee28" />

---

# HEAD

## In ra 3 dòng đầu của file

<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/2e895f02-fd7c-451d-8e4b-2cd2b792822b" />

---

# TAIL

## In ra 3 dòng cuối của file

<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/18fdf963-e01e-464c-8734-b2ddae9a2ef7" />

### Sự khác nhau giữa `head` và `tail`

- `head`: xem đầu file
- `tail`: xem cuối file

---

# TAILF

<img width="1039" height="213" alt="image" src="https://github.com/user-attachments/assets/653fb7d0-9e70-4744-abe1-de6779757ccf" />

## Sự khác nhau của `tailf` và `tail`

- `tailf`: theo dõi file liên tục có thêm dòng mới không
- `tail`: xem cuối file

---

# SED

<img width="741" height="152" alt="image" src="https://github.com/user-attachments/assets/8c8e37b1-06a4-45ae-a4e7-df476dfa4bc9" />

---

# SORT

## Thứ tự tăng dần

<img width="741" height="171" alt="image" src="https://github.com/user-attachments/assets/46c994d9-f1b2-4302-ade2-9fc7a863c6f7" />

---

## Thứ tự giảm dần

<img width="741" height="106" alt="image" src="https://github.com/user-attachments/assets/c26f1be2-dc70-421f-990c-4648009eb194" />

---

## Sắp xếp theo cột

### Bước 1

<img width="734" height="151" alt="image" src="https://github.com/user-attachments/assets/ab5bc275-5339-407e-b50e-17f0286af651" />

*Tạo dữ liệu*

### Bước 2

<img width="734" height="107" alt="image" src="https://github.com/user-attachments/assets/d91aae23-c409-4443-b27a-6bd41acb441d" />

*Sắp xếp theo column 2*

---

# UNIQ

## Lọc dòng trùng

### Bước 1

<img width="748" height="351" alt="image" src="https://github.com/user-attachments/assets/7cc30e98-3022-4479-ac22-544dc4cb0392" />

*Tạo dữ liệu*

### Bước 2

<img width="748" height="98" alt="image" src="https://github.com/user-attachments/assets/cddf76c4-3fb5-42ae-aadb-9f2aa4901deb" />

*Lọc dữ liệu trùng*

<img width="748" height="98" alt="image" src="https://github.com/user-attachments/assets/5f1cd814-bffe-4a8b-b177-e4738cf9a420" />

*Đếm dữ liệu trùng*

---

# WC

## Đếm số dòng

<img width="748" height="46" alt="image" src="https://github.com/user-attachments/assets/4c173a44-7652-48d6-9677-0af2f843ce32" />

---

## Đếm số ký tự

<img width="748" height="46" alt="image" src="https://github.com/user-attachments/assets/44039cdf-7708-441b-888c-6f3ad135cbb3" />

---

# CP

## Copy file

<img width="735" height="46" alt="image" src="https://github.com/user-attachments/assets/513f6aa8-e813-4242-9b0f-9071018b60da" />

<img width="301" height="46" alt="image" src="https://github.com/user-attachments/assets/ed9af079-252d-4d47-81e2-519aaf1fcfea" />

---

## Copy folder

<img width="735" height="46" alt="image" src="https://github.com/user-attachments/assets/97f2f7b9-7a21-4aa5-9795-d73185957329" />

<img width="735" height="46" alt="image" src="https://github.com/user-attachments/assets/d244e263-afda-4040-b045-e38eb8d4db2b" />

---

# MV

## Đổi tên file

<img width="735" height="85" alt="image" src="https://github.com/user-attachments/assets/2b990acc-8915-478e-93f8-1453363fb31a" />

---

## Di chuyển folder

<img width="735" height="169" alt="image" src="https://github.com/user-attachments/assets/14d99b32-fb0f-499b-933b-03c4f6e74571" />

---

# CUT

## Lấy ký tự thứ `<n>`

<img width="735" height="49" alt="image" src="https://github.com/user-attachments/assets/848b9aa9-466e-4843-ad9f-ca1184c6f15b" />

*Lấy ký tự thứ 3*

---

## Lấy từ ký tự `<n>` trở về sau

<img width="735" height="49" alt="image" src="https://github.com/user-attachments/assets/7b93ba65-494d-49af-aa83-17615fb67344" />

*Lấy từ ký tự thứ 3 trở về sau*

---

## Lấy đến ký tự thứ `<n>`

<img width="735" height="49" alt="image" src="https://github.com/user-attachments/assets/8f3f2b91-4e26-41b9-a3b2-6b24f92b96ae" />

*Lấy tới ký tự thứ 4*

---

# DIG COMMAND

## Kiểm tra record A, MX, NS

### Record A

<img width="710" height="444" alt="image" src="https://github.com/user-attachments/assets/963c8117-8f24-499c-af7e-981c1dde29fe" />

### Record MX

<img width="710" height="416" alt="image" src="https://github.com/user-attachments/assets/712f603f-93a4-40db-8179-878476011876" />

### Record NS

<img width="710" height="409" alt="image" src="https://github.com/user-attachments/assets/43beb1ba-4af4-48db-924b-9810b97e72bf" />

---

## Kiểm tra record với custom DNS

### Record A

<img width="710" height="440" alt="image" src="https://github.com/user-attachments/assets/f135d467-e9ff-4add-8e88-7a7937b1a492" />

### Record MX

<img width="710" height="440" alt="image" src="https://github.com/user-attachments/assets/aeffda89-0826-4f4c-acb8-c86e890c7134" />

### Record NS

<img width="710" height="440" alt="image" src="https://github.com/user-attachments/assets/5cda5cf9-611f-4e58-90d0-512abf0fe33f" />

---

# TRACEROUTE

## Thực hiện và giải thích kết quả

- `Traceroute` dùng để kiểm tra đường đi của gói tin qua các router tới đích
- Mỗi dòng là một hop/router trung gian

<img width="1285" height="465" alt="image" src="https://github.com/user-attachments/assets/4147148e-b239-4638-9bbc-94c8a821c509" />

### Trong đó:
- `Hops`: bước nhảy của gói tin khi đi qua một router hoặc thiết bị mạng trung gian
- `IP/Hostname`: tên thiết bị hoặc địa chỉ IP của router tại chặng đó
- `Thời gian (ms)`: thời gian phản hồi (Round Trip Time - RTT)
- `*`: gói tin gửi đi nhưng không nhận được phản hồi

---

# SYMBOLIC LINK, HARD LINK COMMAND

## Định nghĩa Sym Link

`Symbolic link` là shortcut trỏ tới đường dẫn file khác

---

## Định nghĩa Hard Link

`Hard link` là một tên khác của cùng inode/file dữ liệu

---

## Ví dụ về Sym Link và Hard Link

### Sym Link

<img width="680" height="37" alt="image" src="https://github.com/user-attachments/assets/d453bd44-922d-4bc5-b612-9d4210364eca" />

<img width="680" height="37" alt="image" src="https://github.com/user-attachments/assets/7bbf9bb9-6fe6-4a38-9379-9428e417f279" />

---

### Hard Link

<img width="680" height="40" alt="image" src="https://github.com/user-attachments/assets/7e2c3e0c-5a40-4ecd-929a-29c2bde5d89a" />

<img width="680" height="40" alt="image" src="https://github.com/user-attachments/assets/5c6eae59-6d7f-4934-9bf9-5b2a6ba7a8a8" />

---

# MOUNT/UNMOUNT

## Mô phỏng ổ đĩa 5GB

### Thêm ổ cứng `sdb`

<img width="829" height="22" alt="image" src="https://github.com/user-attachments/assets/851ed4c0-3169-46db-9c2e-60249b3b4f3b" />

---

### Kiểm tra số lượng ổ cứng

<img width="952" height="83" alt="image" src="https://github.com/user-attachments/assets/7c24ef76-6137-46d4-ade7-b8f50548dbd4" />

---

### Mount vào `/mnt/test`

<img width="952" height="83" alt="image" src="https://github.com/user-attachments/assets/cfcdc9de-795f-4fcd-9343-04d894ddbfd3" />

---

### Umount `/mnt/test`

<img width="952" height="83" alt="image" src="https://github.com/user-attachments/assets/68fce5ac-3a9c-4da1-bf8b-68ca9a2eb2e4" />

---

## 1. SSL

* **SSL là gì?**
  SSL (Secure Sockets Layer) là giao thức bảo mật mã hóa liên kết giữa máy chủ web (Web Server) và trình duyệt (Browser), đảm bảo dữ liệu truyền tải được an toàn và riêng tư.

* **Có bao nhiêu cách xác thực SSL?**
  Có 3 mức độ xác thực cấp phát chứng chỉ:
  * **DV (Domain Validation):** Xác thực quyền sở hữu tên miền (nhanh nhất).
  * **OV (Organization Validation):** Xác thực tổ chức, doanh nghiệp.
  * **EV (Extended Validation):** Xác thực doanh nghiệp mở rộng (mức độ tin cậy và bảo mật cao nhất, hiển thị tên công ty).

* **CSR file dùng để làm gì?**
  CSR (Certificate Signing Request) là một tệp văn bản mã hóa chứa thông tin định danh của chủ sở hữu tên miền và Public Key. Tệp này được gửi đến Tổ chức cấp phát (CA) để họ dựa vào đó tạo ra chứng chỉ SSL (CRT) cho máy chủ.

* **Gen file CSR và request SSL bằng OpenSSL:**
  Lệnh tạo đồng thời Private Key và CSR cho domain `tech.training.vietnix.tech`:
  ```bash
  openssl req -new -newkey rsa:2048 -nodes -keyout tech.training.vietnix.tech.key -out tech.training.vietnix.tech.csr
