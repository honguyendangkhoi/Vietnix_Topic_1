
# Bổ sung

## 1. Cấu hình HTTPS Nginx → HTTPS Apache

### Apache — port 8443 (SSL)

Thêm `Listen 8443` vào `/etc/apache2/ports.conf`:

<img width="729" height="96" alt="image" src="https://github.com/user-attachments/assets/6d5eb49f-7b82-4daf-9d37-0cec3cb1b59c" />

```bash
Listen 8080
Listen 8443
```

Thêm vhost SSL vào `/etc/apache2/sites-enabled/all-vhosts.conf`:

**WordPress:**

<img width="725" height="245" alt="image" src="https://github.com/user-attachments/assets/e92c0960-deb7-4d5f-bbc9-28c379203fb1" />

**Laravel:**

<img width="725" height="245" alt="image" src="https://github.com/user-attachments/assets/7f629261-b09c-4309-9926-1d38be790c16" />

### Nginx — proxy_pass theo đúng protocol

<img width="725" height="97" alt="image" src="https://github.com/user-attachments/assets/26b8727f-60a5-417b-8ea6-e6a9f422bd72" />

---

## 2. Nginx tối ưu Static File
**Ngnix tự xử lý static file không foward sang Apache:**

<img width="667" height="116" alt="image" src="https://github.com/user-attachments/assets/0bd82d8e-e43d-4c64-b0c1-1cdfef57128d" />

trong đó:
- location ~* \.(css|js|jpg|...)$ — Nginx bắt tất cả request có đuôi file tĩnh. ~* nghĩa là không phân biệt hoa thường (.CSS hay .css đều khớp)
- root /var/www/wp.dangkhoi.vietnix.tech — Nginx tự tìm file trong thư mục này và trả về, không forward sang Apache
- expires 30d — báo cho browser cache file này 30 ngày, lần sau không cần request lại
- access_log off — không ghi log cho static file
- add_header Cache-Control "public, immutable" — báo browser và CDN file này không đổi, khi user vào lần 2 trở đi, CSS/JS/ảnh load từ cache máy — không tốn băng thông, không tốn request lên server

---

**WordPress:**

<img width="725" height="168" alt="image" src="https://github.com/user-attachments/assets/b2f13c0a-318c-407e-8fc8-12f9aa56d5e3" />

**Laravel:**

<img width="725" height="168" alt="image" src="https://github.com/user-attachments/assets/796f4358-bd15-4bee-9603-8cc89bfb0f03" />

---

## 3. Kiểm tra lại toàn bộ

### 3.1. Static file

**WordPress:**

<img width="725" height="168" alt="image" src="https://github.com/user-attachments/assets/b2f13c0a-318c-407e-8fc8-12f9aa56d5e3" />

```bash
curl -I https://wp.dangkhoi.vietnix.tech/wp-content/themes/flatsome/rtl.css | grep -E "HTTP|Cache-Control|Server"
```

**Laravel:**

<img width="725" height="168" alt="image" src="https://github.com/user-attachments/assets/796f4358-bd15-4bee-9603-8cc89bfb0f03" />

```bash
curl -I https://laravel.dangkhoi.vietnix.tech/themes/cozastore/css/main.css | grep -E "HTTP|Cache-Control|Server"
```

### 3.2. HTTPS Nginx → HTTPS Apache

```bash
curl -I https://127.0.0.1:8443/ -k -H "Host: wp.dangkhoi.vietnix.tech"
```

<img width="725" height="209" alt="image" src="https://github.com/user-attachments/assets/d3f2b4f6-eb5e-455c-bbdc-bae2150b6889" />

### 3.3. HTTP Nginx → HTTP Apache

```bash
curl -I http://127.0.0.1:8080/ -H "Host: wp.dangkhoi.vietnix.tech"
```

<img width="725" height="175" alt="image" src="https://github.com/user-attachments/assets/bd460379-a558-4e39-adb6-acc30ed1c4e7" />

### 3.4. proxy_pass đúng protocol

```bash
grep "proxy_pass" /etc/nginx/sites-enabled/proxy.conf
```

<img width="725" height="96" alt="image" src="https://github.com/user-attachments/assets/b5d56021-836f-4ca7-884b-36c417b6d703" />
