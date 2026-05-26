# Cyber Panel
- cập nhật lại VPS sau khi đã reset

<img width="580" height="164" alt="image" src="https://github.com/user-attachments/assets/2e2921a7-716d-44aa-9b17-616233424a3e" />

```bash
apt update && apt upgrade -y
apt install -y curl wget unzip git ufw
```

- Cài đặt Cyber Panel:

<img width="733" height="47" alt="image" src="https://github.com/user-attachments/assets/23220d67-e4ca-495c-b770-cbb845e017e0" />

```bash
sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)
```

<img width="453" height="163" alt="image" src="https://github.com/user-attachments/assets/87623f26-2161-493b-8eca-040956a24268" />
<img width="1032" height="943" alt="image" src="https://github.com/user-attachments/assets/9dad3f96-5783-4e58-9d44-76a5e9e210eb" />

```bash
Install CyberPanel? -> 1
Install CyberPanel with OpenLiteSpeed -> 1
Full service -> Y
Remote MySQL -> N
Password -> default (1234567) * sẽ đổi lại sau
Memcached -> Y
Redis -> Y
WatchDog -> no
```

- reset lại vps sau khi cài đặt xong:

<img width="1032" height="943" alt="image" src="https://github.com/user-attachments/assets/1e619c74-2a55-486c-96df-771ec9b1ea02" />

-ssh lại vào VPS sau khi reboot:

<img width="661" height="440" alt="image" src="https://github.com/user-attachments/assets/7e010a4d-7d3b-44f8-9e6c-3f94c4ebcb1f" />

<img width="661" height="440" alt="image" src="https://github.com/user-attachments/assets/48a62e9c-03fb-4ee2-bf1b-bc6daf5649c8" />

- Vào đường link `https://14.225.204.109:8090` -> Browser sẽ báo ```Your connection is not private``` -> Chọn ```Advanced``` ```Proceed anyway```

<img width="1366" height="885" alt="image" src="https://github.com/user-attachments/assets/b708e0eb-5454-494a-828b-56d6645a48bc" />

- Giao diện truy cập của Cyber Panel:

<img width="1835" height="1045" alt="image" src="https://github.com/user-attachments/assets/93d79156-adf1-402f-be85-50d5ee559565" />

- Sau khi truy cập thành công:

<img width="1835" height="1045" alt="image" src="https://github.com/user-attachments/assets/f40dd063-c8fc-48b2-9728-3c8b4cb5f0b6" />

- Thao tác trên Cyber Panel:

## Lavarel:

`websites` -> `create website` -> `chọn các thông tin của trang web`

<img width="1824" height="956" alt="image" src="https://github.com/user-attachments/assets/69c07b48-b533-4e64-9fec-b1421793bcbc" />

- Tạo thành công:

<img width="1414" height="707" alt="image" src="https://github.com/user-attachments/assets/2594cee4-0c32-4e1c-9d98-c6b31e8e6903" />

## Wordpress:

<img width="1434" height="779" alt="image" src="https://github.com/user-attachments/assets/365a5ef3-9fb8-4c67-915c-768c5aab5369" />

- Tạo thành công:

<img width="1434" height="779" alt="image" src="https://github.com/user-attachments/assets/5048ea83-734f-49ab-9f64-ab69616b1b77" />

- Kiểm tra danh sách đã tạo:

<img width="1516" height="552" alt="image" src="https://github.com/user-attachments/assets/74aa741d-51ae-4e80-bdd2-60aa5820e4d2" />

- Kiểm tra domain đã trỏ về VPS chưa:

<img width="572" height="409" alt="image" src="https://github.com/user-attachments/assets/b4581ffb-e8bd-4f9c-9a44-76f3145ad9c7" />

- Gán SSL:

## Lavarel:

- config SSL cho riêng virtual host của Lavarel trong OpenLiteSpeed

<img width="725" height="252" alt="image" src="https://github.com/user-attachments/assets/2d4b9577-90f3-4a1c-a819-c6923471a877" />

```bash
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

- Kiểm tra SSL:

<img width="492" height="395" alt="image" src="https://github.com/user-attachments/assets/3becae3f-7464-4a99-806a-7eed8fc092a6" />


- Upload source code Lavarel:

<img width="1172" height="897" alt="image" src="https://github.com/user-attachments/assets/a9eab30e-8cc3-4507-80e4-27c0021169f5" />

- Kết quả sau khi upload và giải nén:

<img width="1172" height="897" alt="image" src="https://github.com/user-attachments/assets/a3fb63c2-5933-40a3-ad06-25b1973d2a61" />

- Xóa file `index.html`

<img width="1172" height="897" alt="image" src="https://github.com/user-attachments/assets/cc34f1d1-296d-43b8-a36b-0f11fdadeaf8" />

- Sửa đường dẫn `docRoot` để trỏ đến đúng thư mục `/public`

<img width="720" height="481" alt="image" src="https://github.com/user-attachments/assets/5df26cd4-9184-4613-bea2-790b1151a678" />

# Tạo database:
## Laravel:

`Database` -> `Create Database` -> `Chọn website` -> `Nhập thông tin`

<img width="884" height="883" alt="image" src="https://github.com/user-attachments/assets/a1b5687f-6ef0-47b0-96c2-71dc03d4f6d9" />

- Kiểm tra danh sách:

<img width="1504" height="867" alt="image" src="https://github.com/user-attachments/assets/926163bd-4094-4a63-a1c7-9ed4503bfea7" />

- upload file .sql lên phpMyAdmin

<img width="1492" height="949" alt="image" src="https://github.com/user-attachments/assets/94914b08-1a52-4610-83d1-6b71b43385a8" />

- chỉnh sửa file .env

<img width="673" height="949" alt="image" src="https://github.com/user-attachments/assets/dbfda1f6-347e-4380-a2d0-bbc5a13758ed" />

- Kết nối web thành công:

<img width="1855" height="949" alt="image" src="https://github.com/user-attachments/assets/f9442a67-7637-4fe6-a061-c26ec4d4a197" />

<img width="723" height="189" alt="image" src="https://github.com/user-attachments/assets/39f1d974-2137-4eef-bf8f-0161af9a2064" />


## Wordpress:

<img width="1185" height="927" alt="image" src="https://github.com/user-attachments/assets/85b81a66-4076-48ad-b7ac-643554186739" />

- Kiểm tra danh sách:

<img width="1504" height="867" alt="image" src="https://github.com/user-attachments/assets/2b32dcb3-23ea-4cc5-9ea3-a26e579b9515" />

