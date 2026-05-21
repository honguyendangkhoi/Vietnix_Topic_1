Từ mô hình LEMP tiếp tục xây dựng mô hình reverse proxy:

yêu cầu:
Kết hợp giữa 2 webserver là **_nginx_** và **_apache_**
Tìm hiểu vì sao nginx đứng trước apache
Thao tác xây dựng 2 web với 2 domain trước đó sử dụng vhost:
+ 1 Website chạy wordpress
+ 1 Website chạy laravel
(chạy bằng 2 source code được cấp)
SSL sử dụng cert SSL đã tạo
Bất kỳ domain nào khác khi trỏ về IP VPS hoặc truy cập qua IP phải cần qua 1 default vhost.
Chạy cả 2 website tại cả http và https:
+ https -> https
+ http -> http

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

# Bước 2:
- Tạo Virtual Host trên Apache
```bash
cat > /etc/apache2/sites-available/all-vhosts.conf << 'EOF'
```
## 1. DEFAULT VHOST (IP & phpMyAdmin)
```bash
<VirtualHost *:8080>
    ServerName localhost
    DocumentRoot /var/www/html
</VirtualHost>
```
## 2. WORDPRESS VHOST
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
