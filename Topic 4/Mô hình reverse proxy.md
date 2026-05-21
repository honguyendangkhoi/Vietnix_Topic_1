# Từ mô hình LEMP tiếp tục xây dựng mô hình reverse proxy:

- Yêu cầu:
--Kết hợp giữa 2 webserver là **_nginx_** và **_apache_**
--Tìm hiểu vì sao nginx đứng trước apache
--Thao tác xây dựng 2 web với 2 domain trước đó sử dụng vhost:
    + 1 Website chạy wordpress
    + 1 Website chạy laravel
    (chạy bằng 2 source code được cấp)
--SSL sử dụng cert SSL đã tạo
--Bất kỳ domain nào khác khi trỏ về IP VPS hoặc truy cập qua IP phải cần qua 1 default vhost.
--Chạy cả 2 website tại cả http và https:
    + https -> https
    + http -> http

---

# Bước 1:
- Cài đặt Apache
<img width="461" height="76" alt="image" src="https://github.com/user-attachments/assets/b340b248-45dc-4515-a0e4-e122688a2a9b" />
```bash
apt install apache2 -y
a2enmod proxy_fcgi setenvif rewrite
a2enconf php8.1-fpm
```
- Cấu hình port 8080
```bash
sed -i 's/Listen 80/Listen 8080/' /etc/apache2/ports.conf
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8080>/' /etc/apache2/sites-available/000-default.conf
```
---

# Bước 2:
- Tạo Virtual Host trên Apache
```bash
cat > /etc/apache2/sites-available/all-vhosts.conf << 'EOF'
```
## 1. DEFAULT VHOST (IP & phpMyAdmin)

<img width="342" height="98" alt="image" src="https://github.com/user-attachments/assets/9c0005f9-e62c-4ef8-a9e3-5096a6f771c6" />

```bash
<VirtualHost *:8080>
    ServerName localhost
    DocumentRoot /var/www/html
</VirtualHost>
```
## 2. WORDPRESS VHOST

<img width="463" height="176" alt="image" src="https://github.com/user-attachments/assets/af2f0bbb-6c30-4846-b9a5-da4552c4a695" />

```bash
<VirtualHost *:8080>
    ServerName wp.dangkhoi.vietnix.tech
    DocumentRoot /var/www/wp.dangkhoi.vietnix.tech
    <Directory /var/www/wp.dangkhoi.vietnix.tech>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

## 3. LARAVEL VHOST

<img width="574" height="110" alt="image" src="https://github.com/user-attachments/assets/bc87e9d7-6f6e-4b42-ba9a-239ef7d887f1" />

```bash
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

# Bước 3:
Kích hoạt cấu hình và Khởi động lại Apache:

<img width="473" height="74" alt="image" src="https://github.com/user-attachments/assets/dd8470fa-fd8c-425a-b1ba-14a9f64328a3" />

```bash
a2dissite 000-default.conf
a2ensite all-vhosts.conf
systemctl restart apache2
```
---

# Bước 4: Cấu hình Nginx
Dọn dẹp cấu hình Nginx cũ:

<img width="587" height="56" alt="image" src="https://github.com/user-attachments/assets/473cbccb-96c1-44fe-a06d-7366dd0dbdb2" />

```bash
rm -f /etc/nginx/sites-enabled/default
rm -f /etc/nginx/sites-enabled/wp
rm -f /etc/nginx/sites-enabled/laravel
```

Tạo cấu hình Proxy cho Nginx:

<img width="712" height="23" alt="image" src="https://github.com/user-attachments/assets/173dc6d6-d24d-424b-92b9-4a415a2acce5" />

```bash
cat > /etc/nginx/sites-available/proxy.conf << 'EOF'
```

## 1. DEFAULT VHOST (Bắt IP và Domain lạ)

<img width="625" height="205" alt="image" src="https://github.com/user-attachments/assets/beefa092-5e39-41e0-8aef-b4851eaa5d6d" />

```bash
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

## 2. WORDPRESS

<img width="625" height="205" alt="image" src="https://github.com/user-attachments/assets/7636a3f4-19cc-42ec-984d-d08688cd0576" />

```bash
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

<img width="735" height="295" alt="image" src="https://github.com/user-attachments/assets/f73e0fe1-5d31-4506-9eca-833d0dffaffc" />

```bash
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

## 3. LARAVEL

<img width="735" height="206" alt="image" src="https://github.com/user-attachments/assets/def8323a-399a-4515-a1b0-f8562b5d3b69" />

```bash
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
<img width="729" height="302" alt="image" src="https://github.com/user-attachments/assets/8a761cee-4468-4d0e-b0ed-841deb75c3e1" />

```bash
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
```
