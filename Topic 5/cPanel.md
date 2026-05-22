Giao diện cPanel sau khi vừa đăng nhập:

<img width="1127" height="921" alt="image" src="https://github.com/user-attachments/assets/e14c9648-adce-497a-a8fa-33830439414a" />

# Upload source code và database:

# File Managers:
- Giao diện:

<img width="1122" height="921" alt="image" src="https://github.com/user-attachments/assets/0cecd45b-2ba2-4633-9fff-b92a931925c7" />

- Giao diện upload:

<img width="1122" height="589" alt="image" src="https://github.com/user-attachments/assets/3338e088-05dc-4b01-ba2f-718ae8aa1630" />

- Sau khi upload:

<img width="793" height="65" alt="image" src="https://github.com/user-attachments/assets/ceb861d0-3277-4123-b978-f927fae09679" />

- Giải nén file lavarel:

<img width="1509" height="115" alt="image" src="https://github.com/user-attachments/assets/21d43dd3-c74e-4ccf-a6ad-16c15c0935be" />

- Giải nén xong:

<img width="691" height="442" alt="image" src="https://github.com/user-attachments/assets/f6f392eb-74d2-4170-a97b-eae8b0f27e1c" />

- Tạo thư mục source_code_lavarel để lưu trữ và chuyển tất cả file đã giải nén vào thư mục /public_html/source_code_lavarel

<img width="263" height="323" alt="image" src="https://github.com/user-attachments/assets/ca26a34f-62ca-4dee-8874-a5b15f6d8f95" />

- upload và giải nén tương tự với wordpress

<img width="690" height="448" alt="image" src="https://github.com/user-attachments/assets/549a0430-a29d-4070-8205-93d87a5a3091" />
<img width="805" height="772" alt="image" src="https://github.com/user-attachments/assets/c23e239b-ae85-4bc4-bf38-3ac894ea6a3c" />

# Database:
- Giao diện database:
<img width="1122" height="445" alt="image" src="https://github.com/user-attachments/assets/5db436c5-7d7a-4f65-8765-424f2057124f" />

# bước 1:
<img width="926" height="484" alt="image" src="https://github.com/user-attachments/assets/4ce1d35b-d869-44b3-a2e9-22485f41702c" />

# bước 2:
<img width="1111" height="608" alt="image" src="https://github.com/user-attachments/assets/f5f969d7-427d-46e2-9945-554cef98341d" />

# bước 3:
<img width="1118" height="842" alt="image" src="https://github.com/user-attachments/assets/846b322a-c817-4115-8b2a-aaad12023fb8" />

# bước 4:
## wordpress
<img width="1107" height="437" alt="image" src="https://github.com/user-attachments/assets/f9ba2645-6af6-4e72-9b7d-9d00099d63b2" />

Sau khi tạo database, truy cập vào phpMyAdmin -> Chọn database mới tạo -> Tab Import -> Chọn file .sql.

<img width="1119" height="893" alt="image" src="https://github.com/user-attachments/assets/ecc1b052-0207-42fe-896b-b977512c27ff" />

- kết quả sau khi import:

<img width="1507" height="885" alt="image" src="https://github.com/user-attachments/assets/232e57d2-a464-46a7-a64d-281b55d94c59" />

- chỉnh sửa thông tin database:

<img width="297" height="137" alt="image" src="https://github.com/user-attachments/assets/92cdcaaf-54d2-4180-8c14-bcc1341f5988" />

## Lavarel
- Tạo Lavarel database:

<img width="430" height="162" alt="image" src="https://github.com/user-attachments/assets/50291134-5b9a-4d2d-a3e9-ac60beee2f20" />
<img width="865" height="132" alt="image" src="https://github.com/user-attachments/assets/358c8f5a-a5f0-427f-8d9d-349c764b33a0" />

- Import file .sql của Lavarel:
<img width="1125" height="884" alt="image" src="https://github.com/user-attachments/assets/d2008aef-bbdb-4aae-b394-4e5da502af18" />


# Domains:
- Giao diện:

<img width="1127" height="921" alt="image" src="https://github.com/user-attachments/assets/68cf86c9-7056-480f-b46f-4bb67adbd716" />

- Thêm domains mới
<img width="1132" height="923" alt="image" src="https://github.com/user-attachments/assets/f9d9c7bd-1af8-4bc3-a8e2-b9bfd9c99744" />

- Thêm domains muốn tạo:

<img width="886" height="891" alt="image" src="https://github.com/user-attachments/assets/5e9fab6f-aca5-46f0-af6d-7a7af4de7d14" />

- Upload thành công

<img width="511" height="90" alt="image" src="https://github.com/user-attachments/assets/79bb1c9c-be73-4a27-b128-a30fb8cd5915" />

<img width="1375" height="243" alt="image" src="https://github.com/user-attachments/assets/fc740e49-1129-4d24-8b0e-4a2cb8d57d50" />


# SSL:
- dùng lệnh ```bash cat``` để lấy nội dung
```bash
sudo cat /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/cert.pem
sudo cat /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/privkey.pem
sudo cat /etc/letsencrypt/live/laravel.dangkhoi.vietnix.tech/chain.pem
```
- truy cập SSL:
<img width="1257" height="826" alt="image" src="https://github.com/user-attachments/assets/6dd0e8a9-37e7-46a9-98a4-b5e33d1d9f08" />

## Wordpress:
tạo SSL từ các key trên:

<img width="1257" height="826" alt="image" src="https://github.com/user-attachments/assets/2c747697-5bc1-4af4-baa1-8f09d01ca418" />

<img width="1257" height="269" alt="image" src="https://github.com/user-attachments/assets/ccd99736-84c6-45f7-a40c-d1b5c699a13a" />


## lavarel

<img width="1257" height="434" alt="image" src="https://github.com/user-attachments/assets/171c01e0-2da2-4502-8b86-e69fdf383d47" />

- Quay về trang chủ kiểm tra:

<img width="283" height="243" alt="image" src="https://github.com/user-attachments/assets/19b6acf5-71d6-45db-9d47-5f6b73270919" />


# Trỏ IP về domain
- về cPanel và lưu thông tin:

<img width="295" height="629" alt="image" src="https://github.com/user-attachments/assets/a4af9e9e-8843-4d92-aabf-159755ee2067" />

- trên Ubuntu local truy cập vào file hosts

<img width="519" height="25" alt="image" src="https://github.com/user-attachments/assets/f3df6a18-cfea-496c-82e4-81f22a248f77" />

```bash
sudo nano /etc/hosts
```

- thêm vào file:

<img width="545" height="254" alt="image" src="https://github.com/user-attachments/assets/82e1e13c-ce6a-48f8-8c0d-0a81d937a0b7" />

