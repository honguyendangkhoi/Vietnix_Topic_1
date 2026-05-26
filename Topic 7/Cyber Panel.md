# CyberPanel — Triển khai Website, SSL, Proxy & Python App

## Tổng quan về CyberPanel

**CyberPanel** là một control panel hosting mã nguồn mở, được xây dựng trên nền tảng **OpenLiteSpeed** (hoặc LiteSpeed Enterprise) — một trong những web server hiệu năng cao nhất hiện nay. CyberPanel cung cấp giao diện quản trị trực quan, hỗ trợ triển khai nhanh các ứng dụng web phổ biến như **WordPress**, **Laravel**, và nhiều nền tảng khác chỉ trong vài bước.

Một số điểm nổi bật của CyberPanel:
- Tích hợp sẵn **OpenLiteSpeed**, hiệu năng vượt trội so với Apache/Nginx truyền thống
- Hỗ trợ **Let's Encrypt SSL** tích hợp trực tiếp
- Quản lý **DNS, FTP, Email, Database** tập trung trên một giao diện
- Hỗ trợ triển khai **Python App, Node.js App** và cấu hình **ProxyPass**
- Hoàn toàn miễn phí với bản OpenLiteSpeed

---

## Mục lục

1. Chuẩn bị VPS
2. Cài đặt CyberPanel
3. Truy cập CyberPanel
4. Tạo Website
5. Cấu hình SSL
6. Upload Source Code
7. Tạo Database
8. Tạo Python App trên Port 5000
9. Cấu hình ProxyPass trong OpenLiteSpeed
10. Kiểm tra toàn bộ hệ thống

---

## 1. Chuẩn bị VPS

Sau khi reset VPS, tiến hành cập nhật hệ thống và cài đặt các gói cần thiết:

<img width="580" height="164" alt="image" src="https://github.com/user-attachments/assets/2e2921a7-716d-44aa-9b17-616233424a3e" />

```bash
apt update && apt upgrade -y
apt install -y curl wget unzip git ufw
```

---

## 2. Cài đặt CyberPanel

Chạy lệnh cài đặt CyberPanel:

<img width="733" height="47" alt="image" src="https://github.com/user-attachments/assets/23220d67-e4ca-495c-b770-cbb845e017e0" />

```bash
sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)
```

Chọn các tùy chọn cài đặt như sau:

<img width="453" height="163" alt="image" src="https://github.com/user-attachments/assets/87623f26-2161-493b-8eca-040956a24268" />

<img width="1032" height="943" alt="image" src="https://github.com/user-attachments/assets/9dad3f96-5783-4e58-9d44-76a5e9e210eb" />

```
Install CyberPanel?             -> 1
Install with OpenLiteSpeed      -> 1
Full service                    -> Y
Remote MySQL                    -> N
Password                        -> default (1234567)  # sẽ đổi lại sau
Memcached                       -> Y
Redis                           -> Y
WatchDog                        -> no
```

Sau khi cài đặt hoàn tất, tiến hành **reboot VPS**:

<img width="1032" height="943" alt="image" src="https://github.com/user-attachments/assets/1e619c74-2a55-486c-96df-771ec9b1ea02" />

---

## 3. Truy cập CyberPanel

SSH lại vào VPS sau khi reboot:

<img width="661" height="440" alt="image" src="https://github.com/user-attachments/assets/7e010a4d-7d3b-44f8-9e6c-3f94c4ebcb1f" />

<img width="661" height="440" alt="image" src="https://github.com/user-attachments/assets/48a62e9c-03fb-4ee2-bf1b-bc6daf5649c8" />

Truy cập giao diện CyberPanel qua trình duyệt:

```
https://<IP_VPS>:8090
```

> Trình duyệt sẽ cảnh báo **"Your connection is not private"** — chọn **Advanced** → **Proceed anyway** để tiếp tục.

<img width="1366" height="885" alt="image" src="https://github.com/user-attachments/assets/b708e0eb-5454-494a-828b-56d6645a48bc" />

Giao diện đăng nhập CyberPanel:

<img width="1835" height="1045" alt="image" src="https://github.com/user-attachments/assets/93d79156-adf1-402f-be85-50d5ee559565" />

Sau khi đăng nhập thành công:

<img width="1835" height="1045" alt="image" src="https://github.com/user-attachments/assets/f40dd063-c8fc-48b2-9728-3c8b4cb5f0b6" />

---

## 4. Tạo Website

### Laravel

Vào **Websites** → **Create Website** → Điền thông tin website:

<img width="1824" height="956" alt="image" src="https://github.com/user-attachments/assets/69c07b48-b533-4e64-9fec-b1421793bcbc" />

Tạo thành công:

<img width="1414" height="707" alt="image" src="https://github.com/user-attachments/assets/2594cee4-0c32-4e1c-9d98-c6b31e8e6903" />

### WordPress

<img width="1434" height="779" alt="image" src="https://github.com/user-attachments/assets/365a5ef3-9fb8-4c67-915c-768c5aab5369" />

Tạo thành công:

<img width="1434" height="779" alt="image" src="https://github.com/user-attachments/assets/5048ea83-734f-49ab-9f64-ab69616b1b77" />

Kiểm tra danh sách website đã tạo:

<img width="1516" height="552" alt="image" src="https://github.com/user-attachments/assets/74aa741d-51ae-4e80-bdd2-60aa5820e4d2" />

Kiểm tra domain đã trỏ về VPS:

<img width="572" height="409" alt="image" src="https://github.com/user-attachments/assets/b4581ffb-e8bd-4f9c-9a44-76f3145ad9c7" />

---

## 5. Cấu hình SSL

Sử dụng lại chứng chỉ SSL đã tạo bằng **Certbot** trước đó. Cấu hình trực tiếp trong file virtual host của OpenLiteSpeed.

### Laravel

<img width="725" height="252" alt="image" src="https://github.com/user-attachments/assets/2d4b9577-90f3-4a1c-a819-c6923471a877" />

```nginx
vhssl  {
  keyFile                 /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/privkey.pem
  certFile                /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/fullchain.pem
  certChain               1
  sslProtocol             24
  enableECDHE             1
  renegProtection         1
  sslSessionCache         1
  enableSpdy              15
  enableStapling          1
  ocspRespMaxAge          86400
}
```

Kiểm tra SSL hoạt động:

<img width="492" height="395" alt="image" src="https://github.com/user-attachments/assets/3becae3f-7464-4a99-806a-7eed8fc092a6" />

---

## 6. Upload Source Code

### Laravel

Upload source code lên VPS qua File Manager của CyberPanel:

<img width="1172" height="897" alt="image" src="https://github.com/user-attachments/assets/a9eab30e-8cc3-4507-80e4-27c0021169f5" />

Kết quả sau khi upload và giải nén:

<img width="1172" height="897" alt="image" src="https://github.com/user-attachments/assets/a3fb63c2-5933-40a3-ad06-25b1973d2a61" />

Xóa file `index.html` mặc định:

<img width="1172" height="897" alt="image" src="https://github.com/user-attachments/assets/cc34f1d1-296d-43b8-a36b-0f11fdadeaf8" />

Chỉnh sửa `docRoot` trong virtual host để trỏ đến thư mục `/public` của Laravel:

<img width="720" height="481" alt="image" src="https://github.com/user-attachments/assets/5df26cd4-9184-4613-bea2-790b1151a678" />

### WordPress

Upload source code WordPress:

<img width="827" height="823" alt="image" src="https://github.com/user-attachments/assets/6c59af23-119d-4511-b3af-e863861a31f1" />

Giải nén:

<img width="1360" height="941" alt="image" src="https://github.com/user-attachments/assets/c82b933c-096d-4b8f-9e9a-1c65102342da" />

<img width="1360" height="941" alt="image" src="https://github.com/user-attachments/assets/9e25ecdd-55c7-4b7d-8abf-e03318dad0c1" />

---

## 7. Tạo Database

### Laravel

Vào **Database** → **Create Database** → Chọn website → Nhập thông tin:

<img width="884" height="883" alt="image" src="https://github.com/user-attachments/assets/a1b5687f-6ef0-47b0-96c2-71dc03d4f6d9" />

Kiểm tra danh sách database:

<img width="1504" height="867" alt="image" src="https://github.com/user-attachments/assets/926163bd-4094-4a63-a1c7-9ed4503bfea7" />

Upload file `.sql` lên phpMyAdmin:

<img width="1492" height="949" alt="image" src="https://github.com/user-attachments/assets/94914b08-1a52-4610-83d1-6b71b43385a8" />

Chỉnh sửa file `.env` để kết nối database:

<img width="673" height="949" alt="image" src="https://github.com/user-attachments/assets/dbfda1f6-347e-4380-a2d0-bbc5a13758ed" />

Kết nối thành công:

<img width="1855" height="949" alt="image" src="https://github.com/user-attachments/assets/f9442a67-7637-4fe6-a061-c26ec4d4a197" />

<img width="723" height="189" alt="image" src="https://github.com/user-attachments/assets/39f1d974-2137-4eef-bf8f-0161af9a2064" />

### WordPress

<img width="1185" height="927" alt="image" src="https://github.com/user-attachments/assets/85b81a66-4076-48ad-b7ac-643554186739" />

Kiểm tra danh sách database:

<img width="1504" height="867" alt="image" src="https://github.com/user-attachments/assets/2b32dcb3-23ea-4cc5-9ea3-a26e579b9515" />

Upload file `sql.zip` lên phpMyAdmin (nén thành `.zip` do giới hạn dung lượng của CyberPanel):

<img width="1839" height="967" alt="image" src="https://github.com/user-attachments/assets/396eeadf-dfdb-4972-8ed8-0cc6c6a72615" />

Chỉnh sửa file `wp-config.php`:

<img width="1846" height="1018" alt="image" src="https://github.com/user-attachments/assets/976f357a-85c9-4c50-a559-4724e05b299d" />

Khai báo đường dẫn SSL trong `wp-config.php`:

<img width="723" height="243" alt="image" src="https://github.com/user-attachments/assets/45879574-0884-48e4-a79b-3a596944ce07" />

Khởi động lại OpenLiteSpeed:

<img width="723" height="37" alt="image" src="https://github.com/user-attachments/assets/de92058a-0860-4419-8cb7-71ada22cebe3" />

Kiểm tra:

<img width="432" height="445" alt="image" src="https://github.com/user-attachments/assets/aa56026d-0558-454b-a005-445208bd81bf" />

Truy cập website WordPress thành công:

<img width="1846" height="1018" alt="image" src="https://github.com/user-attachments/assets/4d40d3c1-c4c0-4d0f-9f47-97396aeaa6e0" />

---

## 8. Tạo Python App trên Port 5000

Tạo một ứng dụng Python chạy trên port 5000 thông qua CyberPanel:

<img width="648" height="345" alt="image" src="https://github.com/user-attachments/assets/37f4a94d-9c7d-429a-9ee8-94d14b7f489a" />

Kiểm tra ứng dụng đang lắng nghe đúng port:

<img width="728" height="99" alt="image" src="https://github.com/user-attachments/assets/c15893bf-7fec-4f20-847c-475075108fac" />

---

## 9. Cấu hình ProxyPass trong OpenLiteSpeed

Cấu hình **ProxyPass** để chuyển tiếp request từ `domain/api` đến ứng dụng đang chạy trên port **5000**.

### WordPress

Chỉnh sửa file cấu hình virtual host:

```bash
nano /usr/local/lsws/conf/vhosts/wp.dangkhoi.vietnix.tech/vhost.conf
```

<img width="372" height="291" alt="image" src="https://github.com/user-attachments/assets/6dc1468c-72ff-4a79-9502-4cd93687a83b" />

### Laravel

```bash
nano /usr/local/lsws/conf/vhosts/laravel.dangkhoi.vietnix.tech/vhost.conf
```

<img width="381" height="284" alt="image" src="https://github.com/user-attachments/assets/09bad1cd-b512-46cc-9a23-a75b2e28d29f" />

---

## Kết quả truy cập ứng dụng Python:

### Laravel

<img width="1843" height="1006" alt="image" src="https://github.com/user-attachments/assets/2c29c287-e94b-4154-82cc-6af8ce2bd279" />

### Wordpress

<img width="711" height="397" alt="image" src="https://github.com/user-attachments/assets/3d49eb96-0640-406f-b4b7-93c9bbf30dbe" />

---

## 10. Kiểm tra toàn bộ hệ thống

### 1. Kiểm tra trạng thái Web Server

<img width="345" height="43" alt="image" src="https://github.com/user-attachments/assets/8019ff06-bd97-4d6e-accb-e6a85f1718a2" />

```bash
/usr/local/lsws/bin/lswsctrl status
```

### 2. Kiểm tra Python App đang chạy trên port 5000

<img width="732" height="73" alt="image" src="https://github.com/user-attachments/assets/2a3df953-ad8f-4a6f-ab9d-1954f2cdeab4" />

```bash
lsof -i :5000
```

### 3. Kiểm tra log Python App

<img width="732" height="73" alt="image" src="https://github.com/user-attachments/assets/3ffb36e2-5370-47dc-9023-55299606681f" />

```bash
cat /root/app.log
```
### 4. Kiểm ProxyPass:

<img width="732" height="73" alt="image" src="https://github.com/user-attachments/assets/57cfc87e-7af5-4ecf-b52a-9fb1133fa3b1" />

```bash
curl https://laravel.dangkhoi.vietnix.tech/api/
```
