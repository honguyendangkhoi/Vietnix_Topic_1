# Triển Khai Wordpress và Laravel Trên cPanel

## Giới thiệu

cPanel là một control panel quản trị hosting phổ biến, cung cấp giao diện web giúp quản lý website, domain, database, SSL, file source và nhiều dịch vụ khác mà không cần thao tác hoàn toàn bằng command line.

---

# Giao Diện cPanel Sau Khi Đăng Nhập

<img width="1127" height="921" alt="image" src="https://github.com/user-attachments/assets/e14c9648-adce-497a-a8fa-33830439414a" />

---

# Upload Source Code và Database

# File Manager

## Giao diện File Manager

<img width="1122" height="921" alt="image" src="https://github.com/user-attachments/assets/0cecd45b-2ba2-4633-9fff-b92a931925c7" />

## Giao diện upload file

<img width="1122" height="589" alt="image" src="https://github.com/user-attachments/assets/3338e088-05dc-4b01-ba2f-718ae8aa1630" />

## Sau khi upload source code

<img width="793" height="65" alt="image" src="https://github.com/user-attachments/assets/ceb861d0-3277-4123-b978-f927fae09679" />

---

# Giải Nén Source Code Laravel

## Thực hiện giải nén file Laravel

<img width="1509" height="115" alt="image" src="https://github.com/user-attachments/assets/21d43dd3-c74e-4ccf-a6ad-16c15c0935be" />

## Kết quả sau khi giải nén

<img width="691" height="442" alt="image" src="https://github.com/user-attachments/assets/f6f392eb-74d2-4170-a97b-eae8b0f27e1c" />

## Tạo thư mục lưu source Laravel

Tạo thư mục `source_code_laravel` và chuyển toàn bộ source code đã giải nén vào thư mục:

```bash
/public_html/source_code_laravel
```

<img width="263" height="323" alt="image" src="https://github.com/user-attachments/assets/ca26a34f-62ca-4dee-8874-a5b15f6d8f95" />

---

# Upload Source Wordpress

Thực hiện upload và giải nén tương tự đối với Wordpress.

<img width="690" height="448" alt="image" src="https://github.com/user-attachments/assets/549a0430-a29d-4070-8205-93d87a5a3091" />

<img width="805" height="772" alt="image" src="https://github.com/user-attachments/assets/c23e239b-ae85-4bc4-bf38-3ac894ea6a3c" />

---

# Tạo Database

## Giao diện Database trên cPanel

<img width="1122" height="445" alt="image" src="https://github.com/user-attachments/assets/5db436c5-7d7a-4f65-8765-424f2057124f" />

---

# Tạo Database Wordpress

## Bước 1: Tạo database

<img width="926" height="484" alt="image" src="https://github.com/user-attachments/assets/4ce1d35b-d869-44b3-a2e9-22485f41702c" />

## Bước 2: Tạo database user

<img width="1111" height="608" alt="image" src="https://github.com/user-attachments/assets/f5f969d7-427d-46e2-9945-554cef98341d" />

## Bước 3: Gán user vào database

<img width="1118" height="842" alt="image" src="https://github.com/user-attachments/assets/846b322a-c817-4115-8b2a-aaad12023fb8" />

## Bước 4: Hoàn tất tạo database Wordpress

<img width="1107" height="437" alt="image" src="https://github.com/user-attachments/assets/f9ba2645-6af6-4e72-9b7d-9d00099d63b2" />

---

# Import Database Wordpress

Sau khi tạo database, truy cập vào phpMyAdmin:

- Chọn database vừa tạo
- Chọn tab `Import`
- Upload file `.sql`

<img width="1119" height="893" alt="image" src="https://github.com/user-attachments/assets/ecc1b052-0207-42fe-896b-b977512c27ff" />

## Kết quả sau khi import thành công

<img width="1507" height="885" alt="image" src="https://github.com/user-attachments/assets/232e57d2-a464-46a7-a64d-281b55d94c59" />

---

# Cấu Hình Database Wordpress

## Chỉnh sửa thông tin database trong file cấu hình

```bash
define( 'DB_NAME', 'linhlt_wp_lodoz' );
define( 'DB_USER', 'root' );
define( 'DB_PASSWORD', '@FLs%K@LUaC^6F(.Wp)tRB' );
define( 'DB_HOST', 'localhost' );
define( 'DB_CHARSET', 'utf8' );
define( 'DB_COLLATE', '' );
```

<img width="297" height="137" alt="image" src="https://github.com/user-attachments/assets/92cdcaaf-54d2-4180-8c14-bcc1341f5988" />

## Backup database Wordpress

```bash
mysqldump -u root -p linhlt_wp_lodoz > wordpress.sql
```

## Sau khi thêm user vào database

<img width="1015" height="138" alt="image" src="https://github.com/user-attachments/assets/72566090-3fbf-43a4-855d-fea98f134e92" />

---

# Tạo Database Laravel

## File cấu hình `.env`

```bash
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:Gzem+2f5UCw7N2/RSaa6aKfnC8j6mhhcbP4+DipayeI=
APP_DEBUG=true
APP_URL=https://laravel.dangkhoi.vietnix.tech

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=linhlt_db
DB_USERNAME=root
DB_PASSWORD=@FLs%K@LUaC^6F(.Wp)tRB
```

## Tạo database Laravel

<img width="430" height="162" alt="image" src="https://github.com/user-attachments/assets/50291134-5b9a-4d2d-a3e9-ac60beee2f20" />

<img width="865" height="132" alt="image" src="https://github.com/user-attachments/assets/358c8f5a-a5f0-427f-8d9d-349c764b33a0" />

## Backup database Laravel

```bash
mysqldump -u root -p linhlt_db > laravel.sql
```

---

# Import Database Laravel

## Import file `.sql` của Laravel

<img width="1125" height="884" alt="image" src="https://github.com/user-attachments/assets/d2008aef-bbdb-4aae-b394-4e5da502af18" />

---

# Backup Source Code Từ VPS

## Backup Laravel

```bash
scp -r root@14.225.204.109:/var/www/laravel.dangkhoi.vietnix.tech ~/Desktop/
```

## Backup Wordpress

```bash
scp -r root@14.225.204.109:/var/www/wp.dangkhoi.vietnix.tech ~/Desktop/
```

## Backup file SQL Wordpress

```bash
scp root@14.225.204.109:/var/www/wordpress.sql ~/Desktop/
```

## Backup file SQL Laravel

```bash
scp root@14.225.204.109:/var/www/laravel.sql ~/Desktop/
```

---

# Thêm Domain Vào cPanel

## Giao diện quản lý Domains

<img width="1127" height="921" alt="image" src="https://github.com/user-attachments/assets/68cf86c9-7056-480f-b46f-4bb67adbd716" />

## Thêm domain mới

<img width="1132" height="923" alt="image" src="https://github.com/user-attachments/assets/f9d9c7bd-1af8-4bc3-a8e2-b9bfd9c99744" />

## Nhập domain cần tạo

<img width="886" height="891" alt="image" src="https://github.com/user-attachments/assets/5e9fab6f-aca5-46f0-af6d-7a7af4de7d14" />

## Kết quả thêm domain thành công

<img width="511" height="90" alt="image" src="https://github.com/user-attachments/assets/79bb1c9c-be73-4a27-b128-a30fb8cd5915" />

<img width="1375" height="243" alt="image" src="https://github.com/user-attachments/assets/fc740e49-1129-4d24-8b0e-4a2cb8d57d50" />

---

# Upload SSL Từ VPS

## Lấy nội dung SSL từ VPS

Sử dụng lệnh `cat` để lấy nội dung certificate:

```bash
sudo cat /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/cert.pem
sudo cat /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/privkey.pem
sudo cat /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/chain.pem
```

---

# Cấu Hình SSL Trên cPanel

## Truy cập giao diện SSL

<img width="1257" height="826" alt="image" src="https://github.com/user-attachments/assets/6dd0e8a9-37e7-46a9-98a4-b5e33d1d9f08" />

---

# SSL Wordpress

## Tạo SSL bằng certificate đã lấy từ VPS

<img width="1257" height="826" alt="image" src="https://github.com/user-attachments/assets/2c747697-5bc1-4af4-baa1-8f09d01ca418" />

<img width="1257" height="269" alt="image" src="https://github.com/user-attachments/assets/ccd99736-84c6-45f7-a40c-d1b5c699a13a" />

---

# SSL Laravel

<img width="1257" height="434" alt="image" src="https://github.com/user-attachments/assets/171c01e0-2da2-4502-8b86-e69fdf383d47" />

---

# Kiểm Tra SSL

Sau khi cài đặt SSL, quay lại trang chủ để kiểm tra trạng thái HTTPS.

<img width="283" height="243" alt="image" src="https://github.com/user-attachments/assets/19b6acf5-71d6-45db-9d47-5f6b73270919" />

---

# Trỏ IP Về Domain

## Kiểm tra IP hosting trên cPanel

<img width="295" height="629" alt="image" src="https://github.com/user-attachments/assets/a4af9e9e-8843-4d92-aabf-159755ee2067" />

## Bật domain Wordpress

<img width="1202" height="63" alt="image" src="https://github.com/user-attachments/assets/013cd303-8445-44fd-89b7-016854e3592a" />

---

# Chỉnh Sửa File Hosts Trên Ubuntu Local

## Truy cập file hosts

```bash
sudo nano /etc/hosts
```

<img width="729" height="19" alt="image" src="https://github.com/user-attachments/assets/aa9a0280-0bdd-48c2-8874-a31c1b97c926" />

## Thêm domain và IP hosting vào file hosts

<img width="545" height="254" alt="image" src="https://github.com/user-attachments/assets/82e1e13c-ce6a-48f8-8c0d-0a81d937a0b7" />

Ví dụ:

```bash
103.xxx.xxx.xxx wp.dangkhoi.vietnix.tech
103.xxx.xxx.xxx laravel.dangkhoi.vietnix.tech
```

---

# Kiểm Tra Kết Nối

Sử dụng lệnh `ping` để kiểm tra domain đã trỏ đúng IP hay chưa.

```bash
ping wp.dangkhoi.vietnix.tech
ping laravel.dangkhoi.vietnix.tech
```

<img width="731" height="220" alt="image" src="https://github.com/user-attachments/assets/19f073e2-8537-4f6c-bc98-f689ce28cba8" />

<img width="742" height="332" alt="image" src="https://github.com/user-attachments/assets/3cf070f6-97c2-469e-9bfc-be139373b8d8" />

---

# Kết Quả Cuối Cùng

# Wordpress

<img width="1851" height="956" alt="image" src="https://github.com/user-attachments/assets/ce49c027-7190-474e-b2c6-c494ddb2031b" />

# Laravel

<img width="1851" height="956" alt="image" src="https://github.com/user-attachments/assets/482e5cc1-b75e-4343-86c3-a99d6795245c" />
