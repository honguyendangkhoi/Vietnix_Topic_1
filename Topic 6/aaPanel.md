# Báo Cáo Triển Khai aaPanel — WordPress & Laravel

---

## Mục Lục

1. Tổng quan về aaPanel
2. So sánh Plugin Cache: WP-Optimize vs LiteSpeed Cache
3. Chuẩn bị môi trường VPS
4. Cài đặt aaPanel
5. Triển khai Source Code
6. Liên kết Domain & Cấu hình Website
7. Cấu hình Database
8. Cấu hình WordPress & Laravel
9. Cài đặt WordPress Plugins
10. Plugin All-in-One WP Migration & Backup
11. Các Tính Năng Quản Trị của aaPanel

---

## 1. Tổng quan về aaPanel

**aaPanel** là một Web Hosting Control Panel miễn phí dành cho hệ điều hành Linux, được thiết kế để đơn giản hóa việc quản trị máy chủ.

### Ưu điểm cốt lõi

| # | Tính năng | Mô tả |
|---|-----------|-------|
| 1 | **Triển khai "1 chạm"** | Cài đặt toàn bộ bộ khung LNMP/LAMP (Nginx, Apache, MySQL, PHP) cực nhanh chỉ với một nút bấm |
| 2 | **Quản lý đa nền tảng** | Chạy song song nhiều website, nhiều phiên bản PHP; hỗ trợ đồng thời WordPress và Laravel trên cùng một VPS |
| 3 | **Trực quan & Tối ưu** | Tích hợp File Manager, App Store phong phú, biểu đồ CPU/RAM thời gian thực; tốn ít tài nguyên hơn cPanel và DirectAdmin |

---

## 2. So sánh Plugin Cache: WP-Optimize vs LiteSpeed Cache

### WP-Optimize — Caching cấp độ Ứng dụng (Application-Level)

- **Cơ chế hoạt động:** Hoạt động dựa trên PHP, sử dụng Output Buffering để biên dịch trang web thành các tệp HTML tĩnh lưu trên ổ cứng.
- **Luồng xử lý:** Thông qua Rewrite Rules, Web Server trả trực tiếp tệp HTML tĩnh cho người dùng, bỏ qua tiến trình PHP-FPM.
- **Điều kiện triển khai:** Tương thích với **mọi** nền tảng Web Server tiêu chuẩn (Apache, Nginx, hoặc mô hình Proxy kết hợp), vì caching được xử lý hoàn toàn ở tầng ứng dụng.

### LiteSpeed Cache — Caching cấp độ Máy chủ (Server-Level)

- **Cơ chế hoạt động:** Engine caching tích hợp trực tiếp vào nhân (kernel) của Web Server. Plugin WordPress chỉ đóng vai trò API, gửi chỉ thị qua HTTP Headers để máy chủ tự lưu/xóa cache.
- **Luồng xử lý:** Web Server kiểm tra và trả dữ liệu từ bộ nhớ đệm trước khi yêu cầu chạm đến tầng ứng dụng — triệt tiêu hoàn toàn thời gian khởi chạy PHP.
- **Điều kiện triển khai:** Hoạt động **độc quyền** trên **OpenLiteSpeed** hoặc **LiteSpeed Enterprise**. Mất hoàn toàn tính năng Page Cache khi triển khai trên Nginx hoặc Apache do thiếu `mod_litespeed`.

> **Kết luận:** Chỉ cài LiteSpeed Cache khi web server đang chạy OpenLiteSpeed/LiteSpeed Enterprise. Với Nginx/Apache, sử dụng WP-Optimize.

---

## 3. Chuẩn bị môi trường VPS

### 3.1. Reset SSH Key

<img width="1016" height="113" alt="image" src="https://github.com/user-attachments/assets/ee7a7511-ae30-4495-aa61-eab7bacde9f1" />

### 3.2. Cập nhật hệ thống

<img width="606" height="119" alt="image" src="https://github.com/user-attachments/assets/918db752-6bb3-4252-a72d-1da4a3247fb6" />

```bash
apt update && apt upgrade -y
```

---

## 4. Cài đặt aaPanel

<img width="1046" height="248" alt="image" src="https://github.com/user-attachments/assets/bcd206d0-b34b-4391-bc22-ab1be735a565" />

```bash
URL=https://www.aapanel.com/script/install_7.0_en.sh && \
if [ -f /usr/bin/curl ];then curl -ksSO "$URL";else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi; \
bash install_7.0_en.sh aapanel
```

**Giao diện sau khi cài đặt hoàn tất:**

<img width="676" height="179" alt="image" src="https://github.com/user-attachments/assets/599a8390-1d76-4005-88a3-f41dfec72fbb" />

**Giao diện chính của aaPanel:**

<img width="1843" height="1054" alt="image" src="https://github.com/user-attachments/assets/df82056d-23ce-40bb-a99a-b5890dadccec" />

> **Lưu ý:** Nếu không truy cập được panel, tiến hành mở port tương ứng trên firewall của VPS.

<img width="412" height="88" alt="image" src="https://github.com/user-attachments/assets/3cbc1566-22cd-400e-85c5-0b0d063b529a" />

---

## 5. Triển khai Source Code

### 5.1. Upload file lên server

<img width="1843" height="1054" alt="image" src="https://github.com/user-attachments/assets/4d4cd862-f098-4676-9748-c1eed729a32b" />

**Sau khi upload thành công:**

<img width="1843" height="1054" alt="image" src="https://github.com/user-attachments/assets/5a443b4f-4114-4a71-b38f-8da3514d6302" />

### 5.2. Giải nén

<img width="759" height="604" alt="image" src="https://github.com/user-attachments/assets/d4f2cd10-f176-49a8-93d9-4501fb97d40b" />

---

## 6. Liên kết Domain & Cấu hình Website

Trong aaPanel → **Website** → Cài đặt package theo yêu cầu.

### 6.1. Cài đặt Nginx

<img width="838" height="483" alt="image" src="https://github.com/user-attachments/assets/33b45502-5798-41ab-8146-1330956dd3c9" />

### 6.2. Thêm Domain

<img width="825" height="619" alt="image" src="https://github.com/user-attachments/assets/fdcf8f2d-75b2-48ea-8978-a765ff04ee25" />

<img width="825" height="619" alt="image" src="https://github.com/user-attachments/assets/9ede34d0-05cb-423f-a48f-693bb2571e9f" />

**Kết quả sau khi liên kết 2 domain thành công:**

<img width="1611" height="276" alt="image" src="https://github.com/user-attachments/assets/5fb9dd7b-4653-4abf-b61b-810fdc3cf9a0" />

---

## 7. Cấu hình Database

### 7.1. Cài đặt package MySQL

<img width="1818" height="917" alt="image" src="https://github.com/user-attachments/assets/0040384d-d08e-4174-b049-4dd085804119" />

### 7.2. Tạo Database

<img width="1818" height="917" alt="image" src="https://github.com/user-attachments/assets/7bf18e76-2e45-4fc7-85cc-918f4fd51ec3" />

### 7.3. Import Database

**WordPress:**

<img width="901" height="345" alt="image" src="https://github.com/user-attachments/assets/5a99ab00-dffd-4f36-aeb1-7dcce73d7286" />

**Laravel:**

<img width="901" height="345" alt="image" src="https://github.com/user-attachments/assets/4be301ac-2612-4565-8c0e-99c2c1f0812b" />

### 7.4. Bật Auto Backup Database

<img width="357" height="68" alt="image" src="https://github.com/user-attachments/assets/87bbc86d-8b29-4b69-93cc-64afb2c21aa0" />

---

## 8. Cấu hình WordPress & Laravel

### 8.1. Chỉnh sửa file cấu hình kết nối Database

Cập nhật thông tin database vừa tạo vào file `wp-config.php` (WordPress) và file `.env` (Laravel):

<img width="759" height="604" alt="image" src="https://github.com/user-attachments/assets/a267977a-f563-48d5-bbc9-3defc5412bd7" />

<img width="310" height="117" alt="image" src="https://github.com/user-attachments/assets/1263647c-32a5-4861-9702-e88ca60f2d71" />

### 8.2. Trỏ Document Root về thư mục `public` của Laravel

<img width="871" height="736" alt="image" src="https://github.com/user-attachments/assets/8ba201b6-a7cb-4d4c-a23f-c6324dd0a723" />

### 8.3. Xóa Cache Laravel

<img width="908" height="95" alt="image" src="https://github.com/user-attachments/assets/44c0649b-de02-4b05-b010-3a028e9d3ddd" />

```bash
/www/server/php/82/bin/php artisan config:clear
/www/server/php/82/bin/php artisan cache:clear
```

### 8.4. Phân quyền thư mục WordPress

<img width="864" height="113" alt="image" src="https://github.com/user-attachments/assets/819cfe7e-25b8-4bbb-9808-b9d042499165" />

```bash
chown -R www:www /www/wwwroot/wp.dangkhoi.vietnix.tech

find /www/wwwroot/wp.dangkhoi.vietnix.tech -type d -exec chmod 755 {} \;
find /www/wwwroot/wp.dangkhoi.vietnix.tech -type f -exec chmod 644 {} \;
```

### 8.5. Kiểm tra kết quả

**Truy cập website Laravel:**

<img width="1854" height="1005" alt="image" src="https://github.com/user-attachments/assets/1ead0ec4-65f7-4d9a-add1-35010b7d245e" />

<img width="738" height="221" alt="image" src="https://github.com/user-attachments/assets/05c3867d-ba0d-46dc-ad59-e07f60df3e26" />

**Truy cập website Vietnix.vn:**

<img width="1832" height="876" alt="image" src="https://github.com/user-attachments/assets/879fa97f-f396-4672-90b6-4cacc5e66898" />

---

## 9. Cài đặt WordPress Plugins

### 9.1. Tải Plugin từ Portal Vietnix

Tải toàn bộ plugin tại: [https://portal.vietnix.vn/index.php?rp=/download](https://portal.vietnix.vn/index.php?rp=/download)

**File sau khi tải về:**

<img width="694" height="223" alt="image" src="https://github.com/user-attachments/assets/7e4363a6-ed1e-4466-a851-188524b6cc8f" />

### 9.2. Truy cập WP Admin & Cài đặt Plugin

<img width="1852" height="1051" alt="image" src="https://github.com/user-attachments/assets/3a00d4eb-6840-4a77-9da5-9d635269a279" />

**Giao diện danh sách Plugin:**

<img width="1852" height="1051" alt="image" src="https://github.com/user-attachments/assets/b538dd5d-19fc-473b-977a-7106f63ea722" />

### 9.3. Kết quả từng Plugin

**Rank Math Seo**

<img width="1456" height="782" alt="image" src="https://github.com/user-attachments/assets/5bd256b6-5015-4688-9c56-d0ac9582a7f9" />


**MyThemeShop:**

<img width="1854" height="1045" alt="image" src="https://github.com/user-attachments/assets/c0bbe989-aa18-4a28-b4a0-41f2dfd519f8" />

**Elementor:**

<img width="1676" height="927" alt="image" src="https://github.com/user-attachments/assets/c842264b-c36a-42b4-9144-c558bcaf684f" />

**Divi Theme:**

<img width="1448" height="645" alt="image" src="https://github.com/user-attachments/assets/ff043e44-16f2-4625-a5e4-64ff42e83417" />

**Giao diện WordPress sử dụng Divi Theme:**

<img width="1845" height="1007" alt="image" src="https://github.com/user-attachments/assets/9f988d0f-5dc3-412b-bf06-df6703e21c85" />

<img width="707" height="183" alt="image" src="https://github.com/user-attachments/assets/6aab0d3d-3177-4c5d-8550-a9f0ffe572b7" />

### 9.4. Bật Cache với WP-Optimize

<img width="1672" height="766" alt="image" src="https://github.com/user-attachments/assets/d7d65458-e161-4628-8ff8-2305184881ec" />

---

## 10. Plugin All-in-One WP Migration & Backup

### 10.1. Giao diện chính

<img width="1272" height="431" alt="image" src="https://github.com/user-attachments/assets/93572097-46e5-4c84-a5c9-526f8b287d77" />

### 10.2. Xuất (Export) toàn bộ Website

<img width="1345" height="807" alt="image" src="https://github.com/user-attachments/assets/ecff1a2a-f431-481f-9b6b-ef30f413991b" />

<img width="1345" height="807" alt="image" src="https://github.com/user-attachments/assets/309c42f1-a6de-4868-8d22-a8ec0f460eea" />

> **Lưu ý:** Các tính năng nâng cao như Backup theo lịch, Import từ Google Drive, Dropbox, v.v. yêu cầu bản **Pro**.

<img width="1830" height="1007" alt="image" src="https://github.com/user-attachments/assets/9fcfd94a-48e0-441a-85de-635113ac08e9" />

---

## 11. Các Tính Năng Quản Trị của aaPanel

### 11.1. Vị trí file Access Log & Error Log

**Đường dẫn:**
```
/www/wwwlogs/
```

<img width="1830" height="1007" alt="image" src="https://github.com/user-attachments/assets/22ca9ed4-ce62-431b-879a-68f66ec70748" />

### 11.2. File Config PHP-FPM

**Đường dẫn:**
```
/www/server/php/82/etc
```

<img width="1830" height="1007" alt="image" src="https://github.com/user-attachments/assets/14abb14a-dabf-4f8e-93ad-2ae39baaf0c5" />

### 11.3. Cài đặt PHP Extension

**Đường dẫn thao tác:** `App Store → PHP → Settings → Install Extensions`

<img width="841" height="738" alt="image" src="https://github.com/user-attachments/assets/1cdf34d4-a045-4a57-8790-777cca3f0a28" />

### 11.4. Tắt MySQL Binary Log

**Đường dẫn thao tác:** `App Store → MySQL → Setting → Binary Log`

<img width="1830" height="1007" alt="image" src="https://github.com/user-attachments/assets/55750607-f1ac-4160-8d23-52f10d116fa7" />

**Xóa các file Binary Log cũ:**

<img width="535" height="378" alt="image" src="https://github.com/user-attachments/assets/7e6cf6d2-6f4a-4d7d-9b07-c599e912913f" />

> **Lưu ý:** Chuyển toggle Binary Log sang **OFF** trước, sau đó nhấn **Delete** để xóa toàn bộ file `mysql-bin.*` cũ đang chiếm dụng dung lượng.

---
