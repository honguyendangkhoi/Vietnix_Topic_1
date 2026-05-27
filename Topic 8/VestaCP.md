# VestaCP

## Giới Thiệu

VestaCP (Vesta Control Panel) là một control panel mã nguồn mở dành cho Linux server, cho phép quản lý web hosting thông qua giao diện web trực quan. VestaCP hỗ trợ quản lý tên miền, database, email, DNS, SSL certificate và nhiều tính năng khác.

---

Tải VestaCP:

<img width="725" height="218" alt="image" src="https://github.com/user-attachments/assets/9bf970a9-ec02-4890-a93f-9e7fd948268d" />

- Cài đặt VestaCP:

<img width="727" height="340" alt="image" src="https://github.com/user-attachments/assets/2a99b456-4af5-44b1-a8a4-4639c8760564" />

- Thiết lập:

<img width="650" height="113" alt="image" src="https://github.com/user-attachments/assets/a93c1117-5e29-4b78-9e6b-87e110e3501b" />

```
Would you like to continue [y/n]: y

Please enter admin email address: dngkhoyy@gmail.com

Please enter Vesta port number (press enter for 8083):

Please enter FQDN hostname [training-dangkhoi.vietnix.vn]:

Installation backup directory: /root/vst_install_backups/1779860859
```

- Kết quả sau khi tải xong:

<img width="674" height="629" alt="image" src="https://github.com/user-attachments/assets/34023176-d548-41f5-a08b-d7798649f460" />

- Mở port:

<img width="957" height="290" alt="image" src="https://github.com/user-attachments/assets/a8e86756-e1e7-4249-bf4a-a00ae26872b5" />

- Giao diện truy cập web:

<img width="1831" height="1009" alt="image" src="https://github.com/user-attachments/assets/ec0f328c-7ea4-49b5-b048-28b782f3496b" />

<img width="1831" height="1009" alt="image" src="https://github.com/user-attachments/assets/57392a08-0dfe-4ee7-b827-35050cffd61f" />

- Add 2 domains:
username `admin`

<img width="813" height="73" alt="image" src="https://github.com/user-attachments/assets/bb957c7b-24fa-4a73-97bc-198201393688" />

```
v-add-domain admin laravel.dangkhoi.vietnix.tech
v-add-domain admin wp.dangkhoi.vietnix.tech
```

- kiểm tra:

<img width="811" height="109" alt="image" src="https://github.com/user-attachments/assets/aa7f6372-ef83-4a72-aeec-7ae06f366ba9" />

```
v-list-web-domains admin
```

- Gắn gói PHP 8.1

<img width="983" height="46" alt="image" src="https://github.com/user-attachments/assets/93389d06-e0fe-42f7-8beb-d60a6d3824a7" />

```
v-change-web-domain-tpl admin laravel.dangkhoi.vietnix.tech PHP-8_1
v-change-web-domain-tpl admin wp.dangkhoi.vietnix.tech PHP-8_1
```

- Kiểm tra:

<img width="988" height="118" alt="image" src="https://github.com/user-attachments/assets/9fb98089-d0ce-4e6d-8565-2ff5414b2bdc" />

```
v-list-web-domains admin
```

- Tạo database:

<img width="1167" height="41" alt="image" src="https://github.com/user-attachments/assets/79e7e259-899b-4620-b564-b45139e9e1f9" />

```
v-add-database admin laraveldb lrvluser "BXu36OcU4OhpPh3qgvJK"
v-add-database admin wpdb wpuser "BXu36OcU4OhpPh3qgvJK"
```

- Kiểm tra:

<img width="1167" height="109" alt="image" src="https://github.com/user-attachments/assets/5695828e-7c03-4592-81ca-2d4593dffb8d" />

```
v-list-databases admin
```

- Kiểm tra database đã vào chưa:

### Laravel:

<img width="1345" height="669" alt="image" src="https://github.com/user-attachments/assets/113eb1f2-1d08-4e40-9c5d-ab590aac9df7" />

### Wordpress:

<img width="1345" height="812" alt="image" src="https://github.com/user-attachments/assets/941897ee-72b8-489a-be4d-96393067c6b9" />

- sửa thông tin database:

### Wordpress:

<img width="1618" height="427" alt="image" src="https://github.com/user-attachments/assets/3d781db2-52b5-4d99-9322-92f22d3ba1d2" />

```
cat /home/admin/web/wp.dangkhoi.vietnix.tech/public_html/wp-config.php | grep "DB_"

sed -i "s/define( 'DB_NAME', 'linhlt_wp_lodoz' );/define( 'DB_NAME', 'admin_wpdb' );/" \
  /home/admin/web/wp.dangkhoi.vietnix.tech/public_html/wp-config.php

sed -i "s/define( 'DB_USER', 'root' );/define( 'DB_USER', 'admin_wpuser' );/" \
  /home/admin/web/wp.dangkhoi.vietnix.tech/public_html/wp-config.php

sed -i "s/define( 'DB_PASSWORD', '@FLs%K@LUaC^6F(.Wp)tRB' );/define( 'DB_PASSWORD', 'BXu36OcU4OhpPh3qgvJK' );/" \
  /home/admin/web/wp.dangkhoi.vietnix.tech/public_html/wp-config.php

cat /home/admin/web/wp.dangkhoi.vietnix.tech/public_html/wp-config.php | grep "DB_"
```

### Laravel:

<img width="1317" height="427" alt="image" src="https://github.com/user-attachments/assets/dcc1becc-ced8-4aea-9927-910530c6c06b" />

```
cat /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/.env | grep "DB_"

sed -i "s/DB_DATABASE=linhlt_db/DB_DATABASE=admin_laraveldb/" \
  /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/.env

sed -i "s/DB_USERNAME=root/DB_USERNAME=admin_lrvluser/" \
  /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/.env

sed -i "s/DB_PASSWORD=@FLs%K@LUaC^6F(.Wp)tRB/DB_PASSWORD=BXu36OcU4OhpPh3qgvJK/" \
  /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/.env

cat /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/.env | grep "DB_"
```

## SSL:

<img width="948" height="471" alt="image" src="https://github.com/user-attachments/assets/71a82070-cf9c-4ace-97b0-8f6ba2c328a3" />

copy file cert theo đúng format `domain.crt`, `domain.key`, `domain.ca` trong cùng 1 thư mục

```
cp /home/admin/conf/web/ssl.laravel.dangkhoi.vietnix.tech.crt \
   /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.crt

cp /home/admin/conf/web/ssl.laravel.dangkhoi.vietnix.tech.key \
   /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.key

cp /home/admin/conf/web/ssl.laravel.dangkhoi.vietnix.tech.ca \
   /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.ca

cp /home/admin/conf/web/ssl.wp.dangkhoi.vietnix.tech.crt \
   /home/admin/conf/web/wp.dangkhoi.vietnix.tech.crt

cp /home/admin/conf/web/ssl.wp.dangkhoi.vietnix.tech.key \
   /home/admin/conf/web/wp.dangkhoi.vietnix.tech.key

cp /home/admin/conf/web/ssl.wp.dangkhoi.vietnix.tech.ca \
   /home/admin/conf/web/wp.dangkhoi.vietnix.tech.ca
```

Lệnh VestaCP để enable SSL cho domain, truyền vào tên user, domain, và đường dẫn thư mục chứa cert

```bash
v-add-web-domain-ssl admin laravel.dangkhoi.vietnix.tech /home/admin/conf/web
v-add-web-domain-ssl admin wp.dangkhoi.vietnix.tech /home/admin/conf/web
```

kiểm tra

```bash
v-list-web-domains admin
```

- Đổi đường dẫn `DocumentRoot` sang `Public`:

<img width="1706" height="100" alt="image" src="https://github.com/user-attachments/assets/bb610227-2be9-42a0-8902-3621a8de3e59" />

```
sed -i 's|DocumentRoot /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html|DocumentRoot /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/public|' \
  /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.apache2.conf

sed -i 's|<Directory /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html>|<Directory /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/public>|' \
  /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.apache2.conf
```

- Tương tự với file SSL

<img width="1706" height="100" alt="image" src="https://github.com/user-attachments/assets/4ccf0681-2611-45a3-96ab-876183426a80" />

```
sed -i 's|DocumentRoot /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html|DocumentRoot /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/public|' \
  /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.apache2.ssl.conf

sed -i 's|<Directory /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html>|<Directory /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/public>|' \
  /home/admin/conf/web/laravel.dangkhoi.vietnix.tech.apache2.ssl.conf
```

- Cấp quyền đọc/ghi/thực thi cho thư mục storage/ và bootstrap/cache/ để Laravel có thể ghi file vào đó:

<img width="1163" height="106" alt="image" src="https://github.com/user-attachments/assets/cf966f58-c594-4360-ac84-b4525707d379" />

```
chmod -R 775 /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/storage/
chmod -R 775 /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/bootstrap/cache/
chown -R www-data:www-data /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/storage/
chown -R www-data:www-data /home/admin/web/laravel.dangkhoi.vietnix.tech/public_html/bootstrap/cache/
```

- Kết quả:

Laravel:

<img width="1839" height="1008" alt="image" src="https://github.com/user-attachments/assets/2efa5852-5a52-4769-9b28-624a014b9877" />

Wordpress:

<img width="1839" height="1008" alt="image" src="https://github.com/user-attachments/assets/095b518e-25e4-47e9-bf05-4049053ba540" />

## Update Cert SSL — Các File Cần Thay Đổi

Khi cert SSL được renew bằng certbot, cần copy cert mới vào đúng các file mà Nginx và Apache đang sử dụng.

### Cert mới từ Let's Encrypt nằm tại:

```
/etc/letsencrypt/live/DOMAIN/cert.pem      ← certificate
/etc/letsencrypt/live/DOMAIN/privkey.pem   ← private key
/etc/letsencrypt/live/DOMAIN/chain.pem     ← chain (CA)
```

### Các file trong VestaCP cần được cập nhật (7 file mỗi domain):

| File nguồn (Let's Encrypt) | File đích (`/home/admin/conf/web/`) | Sử dụng bởi |
|---|---|---|
| `cert.pem` | `ssl.DOMAIN.crt` | Apache — `SSLCertificateFile` |
| `cert.pem` | `DOMAIN.crt` | VestaCP internal |
| `privkey.pem` | `ssl.DOMAIN.key` | Apache — `SSLCertificateKeyFile` |
| `privkey.pem` | `DOMAIN.key` | VestaCP internal |
| `chain.pem` | `ssl.DOMAIN.ca` | Apache — `SSLCertificateChainFile` |
| `chain.pem` | `DOMAIN.ca` | VestaCP internal |
| `ssl.DOMAIN.crt` + `ssl.DOMAIN.key` | `ssl.DOMAIN.pem` | Nginx — `ssl_certificate` |

### Các file config đang trỏ vào cert:

**Nginx** (`ssl_certificate` và `ssl_certificate_key`):
```
/home/admin/conf/web/laravel.dangkhoi.vietnix.tech.nginx.ssl.conf
/home/admin/conf/web/wp.dangkhoi.vietnix.tech.nginx.ssl.conf
```

**Apache** (`SSLCertificateFile`, `SSLCertificateKeyFile`, `SSLCertificateChainFile`):
```
/home/admin/conf/web/laravel.dangkhoi.vietnix.tech.apache2.ssl.conf
/home/admin/conf/web/wp.dangkhoi.vietnix.tech.apache2.ssl.conf
```

### Script tự động hóa toàn bộ quá trình:

`/usr/local/bin/renew-ssl.sh` — chạy tự động vào ngày 1 và 15 hàng tháng lúc 3:00 AM:

```bash
#!/bin/bash
certbot renew --quiet
for domain in laravel.dangkhoi.vietnix.tech wp.dangkhoi.vietnix.tech; do
  cp /etc/letsencrypt/live/$domain/cert.pem    /home/admin/conf/web/ssl.$domain.crt
  cp /etc/letsencrypt/live/$domain/cert.pem    /home/admin/conf/web/$domain.crt
  cp /etc/letsencrypt/live/$domain/privkey.pem /home/admin/conf/web/ssl.$domain.key
  cp /etc/letsencrypt/live/$domain/privkey.pem /home/admin/conf/web/$domain.key
  cp /etc/letsencrypt/live/$domain/chain.pem   /home/admin/conf/web/ssl.$domain.ca
  cp /etc/letsencrypt/live/$domain/chain.pem   /home/admin/conf/web/$domain.ca
  cat /home/admin/conf/web/ssl.$domain.crt \
      /home/admin/conf/web/ssl.$domain.key \
      > /home/admin/conf/web/ssl.$domain.pem
done
service nginx restart
service apache2 restart
```

---

- Kiểm tra lại toàn bộ:

Nginx:

<img width="1078" height="372" alt="image" src="https://github.com/user-attachments/assets/5a654f9d-01d4-4726-b66c-65a82c784b78" />

Apache:

<img width="1078" height="372" alt="image" src="https://github.com/user-attachments/assets/789536ba-183a-4bdc-979a-b8130b01a116" />

PHP 8.1:

<img width="1078" height="225" alt="image" src="https://github.com/user-attachments/assets/ce71da4b-d71f-43da-ba5b-1c9be2b89aee" />

Vesta:

<img width="1078" height="225" alt="image" src="https://github.com/user-attachments/assets/07273158-18bf-496c-bc49-2992d2a3fd9a" />

MySQL:

<img width="1078" height="183" alt="image" src="https://github.com/user-attachments/assets/9e433612-99c0-46fd-b229-b479a6003e38" />

```
systemctl status nginx --no-pager
systemctl status apache2 --no-pager
systemctl status php8.1-fpm --no-pager
systemctl status vesta --no-pager
systemctl status mysql --no-pager
```

kiểm tra phiên bản php:

<img width="1078" height="78" alt="image" src="https://github.com/user-attachments/assets/bbf6ac45-31b1-499f-9f79-4a7f24eb9256" />

```
/usr/local/php81/bin/php -v
```

Kiểm tra domain và databse:

<img width="821" height="244" alt="image" src="https://github.com/user-attachments/assets/bbb32024-ef0d-4645-8ece-3a534939b6b9" />

```
v-list-web-domains admin

v-list-databases admin
```

Kiểm tra SSL:

<img width="1711" height="589" alt="image" src="https://github.com/user-attachments/assets/60694c37-5400-4bd9-8405-1784862cf966" />

```
# Kiểm tra cert còn hạn bao lâu
certbot certificates

# Kiểm tra cert chi tiết từng domain
openssl x509 -in /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/cert.pem -noout -dates
openssl x509 -in /etc/letsencrypt/live/wp.dangkhoi.vietnix.tech/cert.pem -noout -dates

# Kiểm tra cert trong VestaCP đã được sync chưa
openssl x509 -in /home/admin/conf/web/ssl.laravel.dangkhoi.vietnix.tech.crt -noout -dates
openssl x509 -in /home/admin/conf/web/ssl.wp.dangkhoi.vietnix.tech.crt -noout -dates
```
