<img width="726" height="115" alt="image" src="https://github.com/user-attachments/assets/e6bd06e7-3ec6-412c-88a8-154e2a598458" /># Setting VPS
## BƯỚC 1: 
ssh vào VPS:
<img width="726" height="324" alt="image" src="https://github.com/user-attachments/assets/99973e83-4d2a-4fc0-803e-356e4257bd9c" />

## Bước 2: 
- Cập nhật các gói package cần thiết:
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

- khởi chạy các packages:
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
## Bước 3:
### Bật Remote MySQL và cấu hình user ROOT:

- Đổi IP lắng nghe của MySQL thành 0.0.0.0 và khởi động lại:
<img width="730" height="65" alt="image" src="https://github.com/user-attachments/assets/d0bcab32-e228-4e13-b62b-e209fdfa234e" />

- Tạo USER:
<img width="730" height="23" alt="image" src="https://github.com/user-attachments/assets/00e38a2e-701e-4009-92d8-9784fc3cce85" />


## Bước 5:
### Cài đặt phpMyAdmin truy cập qua IP:
- Tải và thiết lập thư mục phpMyAdmin:
<img width="730" height="131" alt="image" src="https://github.com/user-attachments/assets/2d800569-e860-4218-8198-3b724598cf5d" />

## Bước 6:
- Truy cập vào website sử dụng IP VPS:
<img width="460" height="488" alt="image" src="https://github.com/user-attachments/assets/517d9706-cffe-46b1-b425-9e3286ee682c" />

- Giao diện sau khi đăng nhập thành công:
<img width="1266" height="888" alt="image" src="https://github.com/user-attachments/assets/fb76e47c-3525-465a-b74c-7af991c0ee2b" />

## Bước 7:
### Tạo tài khoản FTP
