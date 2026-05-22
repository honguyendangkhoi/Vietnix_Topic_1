# Xây Dựng Mô Hình Reverse Proxy Với Nginx Và Apache

## Yêu Cầu

Kết hợp giữa 2 webserver là **nginx** và **apache**.

Xây dựng 2 website sử dụng Virtual Host:

- 1 website chạy WordPress
- 1 website chạy Laravel

Sử dụng SSL đã tạo cho cả 2 domain.

Bất kỳ domain khác hoặc truy cập trực tiếp bằng IP VPS đều phải đi qua default vhost.

Hệ thống cần hỗ trợ:

- HTTP → HTTP
- HTTPS → HTTPS

---

# Vì Sao Nginx Đứng Trước Apache?

Mô hình hoạt động:

```text
Client -> Nginx -> Apache -> PHP Application
```

Lý do sử dụng Nginx phía trước Apache:

- Nginx xử lý concurrent connection tốt hơn
- Nginx tối ưu cho reverse proxy và static file
- Apache hỗ trợ `.htaccess` và rewrite mạnh
- SSL xử lý tại Nginx giúp giảm tải backend
- Apache chỉ chạy nội bộ qua port `8080`

Kết quả:

- Tăng hiệu năng
- Dễ mở rộng
- Dễ quản lý SSL
- Giữ được khả năng tương thích của Apache

---

# Bước 1: Cài Đặt Apache

<img width="461" height="76" alt="image" src="https://github.com/user-attachments/assets/b340b248-45dc-4515-a0e4-e122688a2a9b" />

```bash
apt install apache2 -y
a2enmod proxy_fcgi setenvif rewrite
a2enconf php8.1-fpm
```

## Cấu Hình Apache Chạy Port 8080

```bash
sed -i 's/Listen 80/Listen 8080/' /etc/apache2/ports.conf
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8080>/' /etc/apache2/sites-available/000-default.conf
```

---

# Bước 2: Tạo Virtual Host Trên Apache

```bash
cat > /etc/apache2/sites-available/all-vhosts.conf << 'EOF'
```

## 1. DEFAULT VHOST (IP Và phpMyAdmin)

<img width="342" height="98" alt="image" src="https://github.com/user-attachments/assets/9c0005f9-e62c-4ef8-a9e3-5096a6f771c6" />

```apache
<VirtualHost *:8080>
    ServerName localhost
    DocumentRoot /var/www/html
</VirtualHost>
```

---

## 2. WORDPRESS VHOST

<img width="463" height="176" alt="image" src="https://github.com/user-attachments/assets/af2f0bbb-6c30-4846-b9a5-da4552c4a695" />

```apache
<VirtualHost *:8080>
    ServerName wp.dangkhoi.vietnix.tech
    DocumentRoot /var/www/wp.dangkhoi.vietnix.tech

    <Directory /var/www/wp.dangkhoi.vietnix.tech>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

---

## 3. LARAVEL VHOST

<img width="574" height="110" alt="image" src="https://github.com/user-attachments/assets/bc87e9d7-6f6e-4b42-ba9a-239ef7d887f1" />

```apache
<VirtualHost *:8080>
    ServerName laravel.dangkhoi.vietnix.tech
    DocumentRoot /var/www/laravel.dangkhoi.vietnix.tech/public

    <Directory /var/www/laravel.dangkhoi.vietnix.tech/public>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
EOF
```

---

# Bước 3: Kích Hoạt Cấu Hình Apache

<img width="473" height="74" alt="image" src="https://github.com/user-attachments/assets/dd8470fa-fd8c-425a-b1ba-14a9f64328a3" />

```bash
a2dissite 000-default.conf
a2ensite all-vhosts.conf
systemctl restart apache2
```

---

# Bước 4: Cấu Hình Nginx Reverse Proxy

## Dọn Dẹp Cấu Hình Cũ

<img width="587" height="56" alt="image" src="https://github.com/user-attachments/assets/473cbccb-96c1-44fe-a06d-7366dd0dbdb2" />

```bash
rm -f /etc/nginx/sites-enabled/default
rm -f /etc/nginx/sites-enabled/wp
rm -f /etc/nginx/sites-enabled/laravel
```

---

## Tạo File Proxy Config

<img width="712" height="23" alt="image" src="https://github.com/user-attachments/assets/173dc6d6-d24d-424b-92b9-4a415a2acce5" />

```bash
cat > /etc/nginx/sites-available/proxy.conf << 'EOF'
```

---

## 1. DEFAULT VHOST

<img width="625" height="205" alt="image" src="https://github.com/user-attachments/assets/beefa092-5e39-41e0-8aef-b4851eaa5d6d" />

```nginx
server {
    listen 80 default_server;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

---

## 2. WORDPRESS

### HTTP

<img width="625" height="205" alt="image" src="https://github.com/user-attachments/assets/7636a3f4-19cc-42ec-984d-d08688cd0576" />

```nginx
server {
    listen 80;
    server_name wp.dangkhoi.vietnix.tech;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### HTTPS

<img width="735" height="295" alt="image" src="https://github.com/user-attachments/assets/f73e0fe1-5d31-4506-9eca-833d0dffaffc" />

```nginx
server {
    listen 443 ssl;
    server_name wp.dangkhoi.vietnix.tech;

    ssl_certificate /etc/letsencrypt/live/wp.dangkhoi.vietnix.tech/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/wp.dangkhoi.vietnix.tech/privkey.pem;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

## 3. LARAVEL

### HTTP

<img width="735" height="206" alt="image" src="https://github.com/user-attachments/assets/def8323a-399a-4515-a1b0-f8562b5d3b69" />

```nginx
server {
    listen 80;
    server_name laravel.dangkhoi.vietnix.tech;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### HTTPS

<img width="729" height="302" alt="image" src="https://github.com/user-attachments/assets/8a761cee-4468-4d0e-b0ed-841deb75c3e1" />

```nginx
server {
    listen 443 ssl;
    server_name laravel.dangkhoi.vietnix.tech;

    ssl_certificate /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/privkey.pem;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
EOF
```

---

## Kích Hoạt Và Kiểm Tra Nginx

<img width="728" height="119" alt="image" src="https://github.com/user-attachments/assets/cbdfeeae-ab80-4cad-b0ff-0aef185c3dc2" />

```bash
ln -s /etc/nginx/sites-available/proxy.conf /etc/nginx/sites-enabled/

nginx -t

systemctl restart nginx
```

---

# Kiểm Tra Reverse Proxy

## Kiểm Tra Apache Port 8080

<img width="728" height="154" alt="image" src="https://github.com/user-attachments/assets/1a91acb2-0a26-49db-907e-68b5233d6c38" />

```bash
curl -I http://127.0.0.1:8080 -H "Host: wp.dangkhoi.vietnix.tech"
```

---

## Kiểm Tra WordPress

<img width="727" height="154" alt="image" src="https://github.com/user-attachments/assets/cf70c6d2-2add-4a5e-937e-a95227db551a" />

```bash
curl -I https://wp.dangkhoi.vietnix.tech
```

---

## Kiểm Tra Default Vhost

<img width="727" height="211" alt="image" src="https://github.com/user-attachments/assets/ac6c4320-f188-49de-9c9b-dcc515a6daa1" />

```bash
curl -I http://IP_VPS
```

---

# Upload Source Code Và Database

## Upload Database

<img width="730" height="149" alt="image" src="https://github.com/user-attachments/assets/23755475-9a50-41bf-b497-a97bbb4d3820" />

---

## Kiểm Tra Database

<img width="734" height="220" alt="image" src="https://github.com/user-attachments/assets/993e5a9b-7182-4b65-bdbd-721eeadf9014" />

---

## Upload Source Code

<img width="727" height="152" alt="image" src="https://github.com/user-attachments/assets/7fb08c33-ffdf-4b70-8fe0-51eb31c846e7" />

```bash
scp /home/ubuntu/Desktop/lavarel_source/laravel_source.zip root@14.225.204.109:/tmp/

scp /home/ubuntu/Desktop/wordpress_source/source_wp.zip root@14.225.204.109:/tmp/
```

---

## Kiểm Tra File Upload

<img width="726" height="60" alt="image" src="https://github.com/user-attachments/assets/f3c4b11d-acde-49bb-b4db-ef28c1626597" />

```bash
ls -lh /tmp/*.zip
```

---

# Cấu Hình WordPress

<img width="727" height="93" alt="image" src="https://github.com/user-attachments/assets/5f1d4f68-002c-486b-8744-8a70233d6f7d" />

```bash
cp /var/www/wp.dangkhoi.vietnix.tech/wp-config-sample.php \
   /var/www/wp.dangkhoi.vietnix.tech/wp-config.php

nano /var/www/wp.dangkhoi.vietnix.tech/wp-config.php
```

## Cấu Hình Database

<img width="724" height="350" alt="image" src="https://github.com/user-attachments/assets/5cd7b5fa-ebd4-4491-9d10-af5ccc160363" />

<img width="253" height="29" alt="image" src="https://github.com/user-attachments/assets/22efb098-e070-4037-9b6f-f379167c6d8d" />

```php
define( 'DB_NAME',     'linhlt_wp_lodoz' );
define( 'DB_USER',     'root' );
define( 'DB_PASSWORD', '@FLs%K@LUaC^6F(.Wp)tRB' );
define( 'DB_HOST',     'localhost' );
define( 'DB_CHARSET',  'utf8mb4' );

$table_prefix = 'Sa3QIZ_';
```

---

## Cấp Quyền WordPress

<img width="724" height="41" alt="image" src="https://github.com/user-attachments/assets/64e54c4e-007f-4f90-b438-4f0a62f8d012" />

```bash
chown -R www-data:www-data /var/www/wp.dangkhoi.vietnix.tech
```

---

# Cấu Hình Laravel

<img width="726" height="93" alt="image" src="https://github.com/user-attachments/assets/190d4776-6170-4605-a357-cc4b59ca6b09" />

```bash
cp /var/www/laravel.dangkhoi.vietnix.tech/.env.example \
   /var/www/laravel.dangkhoi.vietnix.tech/.env

nano /var/www/laravel.dangkhoi.vietnix.tech/.env
```

## Cấu Hình Database

<img width="421" height="308" alt="image" src="https://github.com/user-attachments/assets/3ea392f5-8457-4f53-9b16-e3d21d5468be" />

```env
APP_URL=

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=
DB_USERNAME=root
DB_PASSWORD=
```

---

# Chỉnh Sửa Source WordPress

<img width="726" height="43" alt="image" src="https://github.com/user-attachments/assets/26f654ef-b9a1-4bec-88b3-529202d52251" />

```bash
nano /var/www/wp.dangkhoi.vietnix.tech/wp-config.php
```

<img width="726" height="334" alt="image" src="https://github.com/user-attachments/assets/324d9886-a9f2-4630-8d5e-3c09b4f0c38a" />

```php
define( 'DB_USER',     'root' );
define( 'DB_PASSWORD', '@FLs%K@LUaC^6F(.Wp)tRB' );
define( 'DB_HOST',     'localhost' );
```

---

# Kiểm Tra WordPress

## HTTP

<img width="729" height="187" alt="image" src="https://github.com/user-attachments/assets/7dc9d8d8-382c-4889-89c8-ac1cad063f1b" />

```bash
curl -I http://wp.dangkhoi.vietnix.tech/
```

---

## HTTPS

<img width="729" height="226" alt="image" src="https://github.com/user-attachments/assets/0c761209-9472-4df9-93a6-f2eee55b1fda" />

```bash
curl -I https://wp.dangkhoi.vietnix.tech/
```

---

# Kết Quả WordPress

<img width="1271" height="927" alt="image" src="https://github.com/user-attachments/assets/193b0d60-e23d-419b-b72a-42d2730ec93d" />

---

# Cấu Hình Laravel HTTPS

## Chỉnh Sửa File `.env`

<img width="156" height="34" alt="image" src="https://github.com/user-attachments/assets/8f43e815-af57-4d1e-a408-62428d1e9e24" />

---

## Sửa Hàm boot

<img width="697" height="143" alt="image" src="https://github.com/user-attachments/assets/71822408-9dc2-4378-bef6-4a470f13cdfd" />

---

## Clear Cache Và Test

<img width="729" height="217" alt="image" src="https://github.com/user-attachments/assets/cfc54ef2-80c4-4165-ab5f-2eaef809fe2f" />

---

# Tạo File `.htaccess`

## WordPress

<img width="729" height="239" alt="image" src="https://github.com/user-attachments/assets/9ee7afb7-611b-41f0-b2dc-c292dc75335f" />

```bash
cat > /var/www/wp.dangkhoi.vietnix.tech/.htaccess << 'EOF'
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule . /index.php [L]
</IfModule>
# END WordPress
EOF
```

---

## Laravel

<img width="729" height="220" alt="image" src="https://github.com/user-attachments/assets/fede0fd8-4a49-4fb7-adb0-3ac297294b93" />

```bash
cat > /var/www/laravel.dangkhoi.vietnix.tech/public/.htaccess << 'EOF'
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews -Indexes
    </IfModule>

    RewriteEngine On

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f

    RewriteRule ^ index.php [L]
</IfModule>
EOF
```

---

## Cấp Quyền Và Reload Apache

<img width="729" height="62" alt="image" src="https://github.com/user-attachments/assets/e81f02f9-cd0d-479e-b613-59296b2b60c3" />

```bash
chown www-data:www-data /var/www/wp.dangkhoi.vietnix.tech/.htaccess

systemctl reload apache2
```

---

# Kết Quả Laravel

<img width="1259" height="924" alt="image" src="https://github.com/user-attachments/assets/55d85b5a-1a38-4541-bd33-064fdbd8cd4f" />

---

# Kiểm Tra Toàn Bộ Hệ Thống

## 1. Kiểm Tra Nginx Và Apache

<img width="716" height="98" alt="image" src="https://github.com/user-attachments/assets/38955209-1bd9-434b-9428-847342e41cb9" />

```bash
systemctl status nginx | grep "Active:"
systemctl status apache2 | grep "Active:"
```

---

## 2. Kiểm Tra Port

<img width="716" height="191" alt="image" src="https://github.com/user-attachments/assets/d467a638-8f77-4f00-acb6-f6af17ba06fa" />

```bash
ss -tlnp | grep -E "80|443|8080"
```

---

## 3. Kiểm Tra PHP 8.1

<img width="716" height="101" alt="image" src="https://github.com/user-attachments/assets/9c180614-9d22-4728-914a-a3105d1433de" />

```bash
php -v
```

---

## 4. Kiểm Tra MySQL

<img width="716" height="182" alt="image" src="https://github.com/user-attachments/assets/28227538-efb3-4fcd-87da-31cc1684a394" />

```bash
systemctl status mysql | grep "Active:"

mysql -u root -p'@FLs%K@LUaC^6F(.Wp)tRB' \
-e "SELECT VERSION();"
```

---

## 5. Kiểm Tra phpMyAdmin

<img width="725" height="164" alt="image" src="https://github.com/user-attachments/assets/ffa9fb70-9736-4136-b670-0ac29ee92d7a" />

```bash
curl -I http://14.225.204.109/phpmyadmin
```

---

## 6. Kiểm Tra WordPress HTTP → HTTP

<img width="730" height="226" alt="image" src="https://github.com/user-attachments/assets/88c28391-5745-4acf-8029-37a6411683c6" />

```bash
curl -I http://wp.dangkhoi.vietnix.tech/ | grep -E "HTTP|Location"
```

---

## 7. Kiểm Tra WordPress HTTPS → HTTPS

<img width="730" height="115" alt="image" src="https://github.com/user-attachments/assets/7e6cfe1b-6c65-4d4f-8531-2315aa2124c1" />

```bash
curl -I https://wp.dangkhoi.vietnix.tech/ | grep -E "HTTP|Location"
```

---

## 8. Kiểm Tra Laravel HTTP → HTTP

<img width="730" height="115" alt="image" src="https://github.com/user-attachments/assets/b9fd3f72-a965-409e-b89c-fe4fe8933138" />

```bash
curl -I http://laravel.dangkhoi.vietnix.tech/ | grep -E "HTTP|Location"
```

---

## 9. Kiểm Tra Laravel HTTPS → HTTPS

<img width="730" height="115" alt="image" src="https://github.com/user-attachments/assets/7672ec40-7c91-46c7-9b27-9ec76b7a7814" />

```bash
curl -I https://laravel.dangkhoi.vietnix.tech/ | grep -E "HTTP|Location"
```

---

## 10. Kiểm Tra Default Vhost

<img width="730" height="116" alt="image" src="https://github.com/user-attachments/assets/2a760e9b-08f1-4782-be9b-ebb33c561d59" />

```bash
curl -I http://14.225.204.109/

curl -I https://14.225.204.109/ -k
```

---

## 11. Kiểm Tra SSL WordPress

<img width="730" height="116" alt="image" src="https://github.com/user-attachments/assets/c7547f59-7554-4c13-9751-860d881f4afd" />

```bash
echo | openssl s_client \
-connect wp.dangkhoi.vietnix.tech:443 2>/dev/null \
| openssl x509 -noout -dates -subject
```

---

## 12. Kiểm Tra SSL Laravel

<img width="730" height="116" alt="image" src="https://github.com/user-attachments/assets/3c6a93b1-7303-4fef-8815-73991306fcef" />

```bash
echo | openssl s_client \
-connect laravel.dangkhoi.vietnix.tech:443 2>/dev/null \
| openssl x509 -noout -dates -subject
```

---

# Kết Luận

Hệ thống Reverse Proxy sử dụng:

- Nginx
- Apache
- PHP 8.1
- MySQL 8
- WordPress
- Laravel
- SSL HTTPS

đã được cấu hình thành công.

Kết quả đạt được:

- Chạy đồng thời WordPress và Laravel
- Hỗ trợ HTTP và HTTPS
- Reverse Proxy hoạt động ổn định
- SSL hợp lệ
- Default vhost xử lý domain/IP lạ
- Apache backend được ẩn phía sau Nginx

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
