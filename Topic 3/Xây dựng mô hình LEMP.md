# Hướng Dẫn Cài Đặt VPS — LEMP Stack + WordPress + Laravel

**Yêu cầu:**
- Xây dựng mô hình LEMP (PHP 8.1)
- phpMyAdmin truy cập dạng `IP/phpmyadmin`
- Website WordPress + Laravel mặc định
- Cài SSL cho 2 domain (Certbot)
- Tạo tài khoản FTP
- MySQL: bật remote từ xa với user root

---

## Mục Lục

### **Bước 1 — Setting VPS**

### **Bước 2 — SSH vào VPS**

### **Bước 3 — Cài đặt LEMP Stack**

### **Bước 4 — Cấu hình MySQL Remote với user root**

### **Bước 5 — Cài đặt phpMyAdmin**

### **Bước 6 — Truy cập phpMyAdmin qua IP**

### **Bước 7 — Tạo tài khoản FTP**

### **Bước 8 — Cài đặt WordPress & Laravel**

### **Bước 9 — Cấu hình Nginx & Cài SSL bằng Certbot**

---

## Bước 1 — Setting VPS

Khởi tạo VPS:

<img width="726" height="115" alt="image" src="https://github.com/user-attachments/assets/e6bd06e7-3ec6-412c-88a8-154e2a598458" />

---

## Bước 2 — SSH vào VPS

Kết nối vào VPS qua SSH từ máy local:

<img width="726" height="324" alt="image" src="https://github.com/user-attachments/assets/99973e83-4d2a-4fc0-803e-356e4257bd9c" />

```bash
ssh root@<YOUR_VPS_IP>
```

---

## Bước 3 — Cài đặt LEMP Stack

### 3.1 Cập nhật hệ thống

<img width="726" height="246" alt="image" src="https://github.com/user-attachments/assets/dd4ab619-9d9a-46d4-aa57-8da77dc30045" />

```bash
apt update -y
```

### 3.2 Cài đặt Nginx

<img width="726" height="192" alt="image" src="https://github.com/user-attachments/assets/37ab6e8f-7df9-4d54-ada4-b5984fa61c08" />

```bash
apt install nginx -y
```

### 3.3 Cài đặt MySQL Server

<img width="726" height="78" alt="image" src="https://github.com/user-attachments/assets/ff4fee9c-ca43-4e5f-bab3-a5c5da6cb57a" />

```bash
apt install mysql-server -y
```

### 3.4 Cài đặt PHP 8.1 và các thư viện cần thiết

<img width="726" height="115" alt="image" src="https://github.com/user-attachments/assets/4182993b-3d06-4d73-bf72-7aa7e944320c" />

```bash
apt install php8.1-fpm php8.1-mysql php8.1-curl php8.1-gd \
  php8.1-mbstring php8.1-xml php8.1-xmlrpc php8.1-soap \
  php8.1-intl php8.1-zip php8.1-bcmath unzip -y
```

### 3.5 Khởi động các dịch vụ

**Nginx:**

<img width="726" height="100" alt="image" src="https://github.com/user-attachments/assets/ce4e0d80-7789-4e9b-a99a-719c5dc7aa7b" />

```bash
systemctl enable nginx
systemctl start nginx
```

**MySQL:**

<img width="726" height="101" alt="image" src="https://github.com/user-attachments/assets/7b1fe42f-847e-483c-a2da-8cbc3871f828" />

```bash
systemctl enable mysql
systemctl start mysql
```

---

## Bước 4 — Cấu hình MySQL Remote với user root

### 4.1 Đổi IP lắng nghe của MySQL thành `0.0.0.0`

<img width="730" height="65" alt="image" src="https://github.com/user-attachments/assets/d0bcab32-e228-4e13-b62b-e209fdfa234e" />

```bash
sed -i 's/bind-address.*/bind-address = 0.0.0.0/' /etc/mysql/mysql.conf.d/mysqld.cnf
systemctl restart mysql
```

### 4.2 Cấp quyền remote cho user root

<img width="730" height="23" alt="image" src="https://github.com/user-attachments/assets/00e38a2e-701e-4009-92d8-9784fc3cce85" />

```sql
CREATE USER 'root'@'%' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

> Thay `your_password` bằng mật khẩu thật.

---

## Bước 5 — Cài đặt phpMyAdmin

Tải và đặt phpMyAdmin vào webroot để truy cập theo dạng `IP/phpmyadmin`:

<img width="730" height="131" alt="image" src="https://github.com/user-attachments/assets/2d800569-e860-4218-8198-3b724598cf5d" />

```bash
cd /usr/share
wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.zip
unzip phpMyAdmin-latest-all-languages.zip
mv phpMyAdmin-*-all-languages phpmyadmin
rm phpMyAdmin-latest-all-languages.zip
chown -R www-data:www-data /usr/share/phpmyadmin
ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
```

---

## Bước 6 — Truy cập phpMyAdmin qua IP

Mở trình duyệt và truy cập:

```
http://<YOUR_VPS_IP>/phpmyadmin
```

Đăng nhập bằng tài khoản `root` và mật khẩu đã thiết lập ở Bước 4.

<img width="460" height="488" alt="image" src="https://github.com/user-attachments/assets/517d9706-cffe-46b1-b425-9e3286ee682c" />

Giao diện sau khi đăng nhập thành công:

<img width="1266" height="888" alt="image" src="https://github.com/user-attachments/assets/fb76e47c-3525-465a-b74c-7af991c0ee2b" />

---

## Bước 7 — Tạo tài khoản FTP

### 7.1 Cài đặt vsftpd

<img width="525" height="79" alt="image" src="https://github.com/user-attachments/assets/6433b37f-15a3-4293-8c62-ec0e81556087" />

```bash
apt install vsftpd -y
```

### 7.2 Cấu hình FTP

<img width="727" height="133" alt="image" src="https://github.com/user-attachments/assets/a3a7c8d9-ac6e-4c8f-888c-daa9116575bc" />

```bash
sed -i 's/#write_enable=YES/write_enable=YES/g' /etc/vsftpd.conf
sed -i 's/#chroot_local_user=YES/chroot_local_user=YES/g' /etc/vsftpd.conf
grep -q "allow_writeable_chroot=YES" /etc/vsftpd.conf || echo "allow_writeable_chroot=YES" >> /etc/vsftpd.conf
```

Thêm hoặc chỉnh sửa các dòng sau để cho phép upload:

```ini
listen=YES
listen_ipv6=NO
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
```

Khởi động lại vsftpd:

```bash
systemctl restart vsftpd
```

### 7.3 Tạo user FTP và đặt mật khẩu

<img width="727" height="319" alt="image" src="https://github.com/user-attachments/assets/18b62718-0c11-419e-bb42-d93912f60dd6" />

```bash
adduser ftpuser
passwd ftpuser
```

### 7.4 Phân quyền thư mục code cho user FTP

<img width="727" height="42" alt="image" src="https://github.com/user-attachments/assets/c73805c5-8f16-4198-b1ac-a05e892c4d39" />

```bash
usermod -d /var/www webadmin
chown -R webadmin:webadmin /var/www
```

---

## Bước 8 — Cài đặt WordPress & Laravel

### 8.1 WordPress

Tải và thiết lập thư mục WordPress:

<img width="586" height="151" alt="image" src="https://github.com/user-attachments/assets/c4eeeba4-efbc-4e46-a200-344e780f4552" />

```bash
cd /var/www
wget https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
rm latest.tar.gz
mv wordpress wp.dangkhoi.vietnix.tech
chown -R www-data:www-data /var/www/wp.dangkhoi.vietnix.tech
```

### 8.2 Laravel

Cài Composer và tạo project Laravel mặc định:

<img width="730" height="161" alt="image" src="https://github.com/user-attachments/assets/ad95836f-c9ec-47eb-b067-bcb97c3917bc" />

```bash
cd /var/www
curl -sS https://getcomposer.org/installer -o composer-setup.php
php composer-setup.php --install-dir=/usr/local/bin --filename=composer
rm composer-setup.php

composer create-project laravel/laravel laravel.dangkhoi.vietnix.tech
chown -R www-data:www-data /var/www/laravel.dangkhoi.vietnix.tech
chmod -R 775 /var/www/laravel.dangkhoi.vietnix.tech/storage /var/www/laravel.dangkhoi.vietnix.tech/bootstrap/cache
```

---

## Bước 9 — Cấu hình Nginx & Cài SSL bằng Certbot

### 9.1 Cấu hình Nginx

**File cấu hình cho WordPress:**

<img width="730" height="314" alt="image" src="https://github.com/user-attachments/assets/857cb20f-dc20-411e-8e0c-fc3e7c4c9d70" />

```bash
cat > /etc/nginx/sites-available/wp << 'EOF'
server {
    listen 80;
    server_name wp.dangkhoi.vietnix.tech;
    root /var/www/wp.dangkhoi.vietnix.tech;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}
EOF
```

**File cấu hình cho Laravel:**

<img width="734" height="328" alt="image" src="https://github.com/user-attachments/assets/493d4e7a-c1a5-444e-994b-dc911f049776" />

```bash
cat > /etc/nginx/sites-available/laravel << 'EOF'
server {
    listen 80;
    server_name laravel.dangkhoi.vietnix.tech;
    root /var/www/laravel.dangkhoi.vietnix.tech/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}
EOF
```

**Kích hoạt 2 website và khởi động lại Nginx:**

<img width="734" height="133" alt="image" src="https://github.com/user-attachments/assets/7ca1efeb-c9d3-4ba4-a64e-10b731b6c312" />

```bash
ln -s /etc/nginx/sites-available/wp /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
nginx -t
systemctl restart nginx
```

---

### 9.2 Cài SSL bằng Certbot

**Cài đặt Certbot:**

<img width="708" height="76" alt="image" src="https://github.com/user-attachments/assets/2e6a0463-b1fc-4237-8c54-a896601af73f" />

```bash
apt install certbot python3-certbot-nginx -y
```

**Cài SSL cho WordPress:**

<img width="708" height="44" alt="image" src="https://github.com/user-attachments/assets/858932b4-6424-4ba4-8a50-cb3603afa287" />

```bash
certbot --nginx -d wp.dangkhoi.vietnix.tech
```

Kết quả:

<img width="1262" height="886" alt="image" src="https://github.com/user-attachments/assets/b1cf569b-dbd7-4975-964c-82b0f07932d7" />

**Cài SSL cho Laravel:**

<img width="728" height="57" alt="image" src="https://github.com/user-attachments/assets/ff5a5e07-d59f-45d8-9c52-3b50c1eac8a9" />

```bash
certbot --nginx -d laravel.dangkhoi.vietnix.tech
```

Kết quả:

<img width="1262" height="886" alt="image" src="https://github.com/user-attachments/assets/c0feb6c9-ead0-4d77-ad3b-034b15ad80f8" />

---

## Tổng kết

| Thành phần | Mô tả |
|---|---|
| Nginx | Web server, reverse proxy cho PHP-FPM |
| MySQL | Database server, bật remote với user root |
| PHP 8.1-FPM | PHP runtime với đầy đủ extension |
| phpMyAdmin | Quản trị DB qua `IP/phpmyadmin` |
| FTP (vsftpd) | Tài khoản FTP với quyền truy cập webroot |
| WordPress | Triển khai tại `/var/www/wp.dangkhoi.vietnix.tech` |
| Laravel | Triển khai tại `/var/www/laravel.dangkhoi.vietnix.tech` |
| SSL (Certbot) | HTTPS cho cả 2 domain |
