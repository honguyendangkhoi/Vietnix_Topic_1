# BƯỚC 1: Setting VPS
<img width="726" height="115" alt="image" src="https://github.com/user-attachments/assets/e6bd06e7-3ec6-412c-88a8-154e2a598458" />

# BƯỚC 2: 
## ssh vào VPS:
<img width="726" height="324" alt="image" src="https://github.com/user-attachments/assets/99973e83-4d2a-4fc0-803e-356e4257bd9c" />

# Bước 3: 
## Cập nhật các gói package cần thiết:
<img width="726" height="246" alt="image" src="https://github.com/user-attachments/assets/dd4ab619-9d9a-46d4-aa57-8da77dc30045" />

``` bash
apt update -y
```

- Cài đặt nginx:
<img width="726" height="192" alt="image" src="https://github.com/user-attachments/assets/37ab6e8f-7df9-4d54-ada4-b5984fa61c08" />

```bash
apt install nginx -y
```

- Cài đặt MySQL Server:
<img width="726" height="78" alt="image" src="https://github.com/user-attachments/assets/ff4fee9c-ca43-4e5f-bab3-a5c5da6cb57a" />
```bash
apt install mysql-server -y
```

- Cài đặt PHP 8.1 và các thư viện cần thiết:
<img width="726" height="115" alt="image" src="https://github.com/user-attachments/assets/4182993b-3d06-4d73-bf72-7aa7e944320c" />
```bash
apt install php8.1-fpm php8.1-mysql php8.1-curl php8.1-gd php8.1-mbstring php8.1-xml php8.1-xmlrpc php8.1-soap php8.1-intl php8.1-zip php8.1-bcmath unzip -y
```

## khởi chạy các packages:
<img width="726" height="100" alt="image" src="https://github.com/user-attachments/assets/ce4e0d80-7789-4e9b-a99a-719c5dc7aa7b" />

```bash
systemctl enable nginx -y
systemctl start nginx
```

<img width="726" height="101" alt="image" src="https://github.com/user-attachments/assets/7b1fe42f-847e-483c-a2da-8cbc3871f828" />
``` bash
systemctl enable mysql -y
systemctl start mysql
```
# Bước 4:
## Bật Remote MySQL và cấu hình user ROOT:

- Đổi IP lắng nghe của MySQL thành 0.0.0.0 và khởi động lại:
<img width="730" height="65" alt="image" src="https://github.com/user-attachments/assets/d0bcab32-e228-4e13-b62b-e209fdfa234e" />

- Tạo USER:
<img width="730" height="23" alt="image" src="https://github.com/user-attachments/assets/00e38a2e-701e-4009-92d8-9784fc3cce85" />

# Bước 5:
## Cài đặt phpMyAdmin truy cập qua IP:
- Tải và thiết lập thư mục phpMyAdmin:
<img width="730" height="131" alt="image" src="https://github.com/user-attachments/assets/2d800569-e860-4218-8198-3b724598cf5d" />

# Bước 6:
- Truy cập vào website sử dụng IP VPS:
<img width="460" height="488" alt="image" src="https://github.com/user-attachments/assets/517d9706-cffe-46b1-b425-9e3286ee682c" />

- Giao diện sau khi đăng nhập thành công:
<img width="1266" height="888" alt="image" src="https://github.com/user-attachments/assets/fb76e47c-3525-465a-b74c-7af991c0ee2b" />

# Bước 7:

## Tạo tài khoản FTP:
- Cài đặt package:
<img width="525" height="79" alt="image" src="https://github.com/user-attachments/assets/6433b37f-15a3-4293-8c62-ec0e81556087" />

- cấu hình FTP:
<img width="727" height="133" alt="image" src="https://github.com/user-attachments/assets/a3a7c8d9-ac6e-4c8f-888c-daa9116575bc" />

- Tạo mật khẩu cho user FTP:
<img width="727" height="319" alt="image" src="https://github.com/user-attachments/assets/18b62718-0c11-419e-bb42-d93912f60dd6" />

- Phân quyền quản lý thư mục code cho tài khoản vừa tạo:
<img width="727" height="42" alt="image" src="https://github.com/user-attachments/assets/c73805c5-8f16-4198-b1ac-a05e892c4d39" />

# Bước 8:
## WordPress:
- Tải và thiết lập thư mục WordPress:
<img width="586" height="151" alt="image" src="https://github.com/user-attachments/assets/c4eeeba4-efbc-4e46-a200-344e780f4552" />

## Laravel:
- Cài Composer và tạo project Laravel mặc định:
<img width="730" height="161" alt="image" src="https://github.com/user-attachments/assets/ad95836f-c9ec-47eb-b067-bcb97c3917bc" />

# Bước 9: 
## Cấu hình Nginx và Cài SSL bằng Certbot:
### Nginx:

- Tạo file cấu hình Nginx cho WordPress:
<img width="730" height="314" alt="image" src="https://github.com/user-attachments/assets/857cb20f-dc20-411e-8e0c-fc3e7c4c9d70" />

- Tạo file cấu hình Nginx cho Laravel:
<img width="734" height="328" alt="image" src="https://github.com/user-attachments/assets/493d4e7a-c1a5-444e-994b-dc911f049776" />

- Kích hoạt 2 website và khởi động lại Nginx:
<img width="734" height="133" alt="image" src="https://github.com/user-attachments/assets/7ca1efeb-c9d3-4ba4-a64e-10b731b6c312" />

### Certbot:
- Cài đặt công cụ Certbot:
<img width="708" height="76" alt="image" src="https://github.com/user-attachments/assets/2e6a0463-b1fc-4237-8c54-a896601af73f" />

- Cài đặt SSL cho WordPress:
<img width="708" height="44" alt="image" src="https://github.com/user-attachments/assets/858932b4-6424-4ba4-8a50-cb3603afa287" />
- Kết quả:
<img width="1262" height="886" alt="image" src="https://github.com/user-attachments/assets/b1cf569b-dbd7-4975-964c-82b0f07932d7" />

- Cài đặt SSL cho Lavarel:
<img width="728" height="57" alt="image" src="https://github.com/user-attachments/assets/ff5a5e07-d59f-45d8-9c52-3b50c1eac8a9" />
- Kết quả:
<img width="1262" height="886" alt="image" src="https://github.com/user-attachments/assets/c0feb6c9-ead0-4d77-ad3b-034b15ad80f8" />


