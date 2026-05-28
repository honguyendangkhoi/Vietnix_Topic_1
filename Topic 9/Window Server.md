# Windows Server Lab Report

---

## Mục lục

1. Remmina
2. Windows Firewall
3. IIS Web Server
4. SQL Server 2016
5. WordPress
6. SSL

---

## 1. Remmina

### Cài đặt

```
sudo apt-add-repository ppa:remmina-ppa-team/remmina-next
sudo apt update
sudo apt install remmina remmina-plugin-rdp remmina-plugin-secret
```

### Giao diện Remmina

<img width="596" height="440" alt="image" src="https://github.com/user-attachments/assets/22e50ea7-6f63-4b9b-9681-e2e0e71e1af6" />

### Thiết lập kết nối

<img width="621" height="464" alt="image" src="https://github.com/user-attachments/assets/e90605d7-354a-49c0-8905-d3525bca7ce7" />

### Giao diện sau khi kết nối thành công

<img width="1847" height="1031" alt="image" src="https://github.com/user-attachments/assets/899ac198-940f-491c-83f8-91451b658f56" />

---

## 2. Windows Firewall

### Mở Windows Firewall

Nhấn `Windows` → tìm `wf.msc` → `Enter`

<img width="348" height="646" alt="image" src="https://github.com/user-attachments/assets/cf38de45-716f-4b73-8992-ad218497fa3d" />

Giao diện Windows Firewall

<img width="1027" height="774" alt="image" src="https://github.com/user-attachments/assets/b1f3b057-96ea-42ce-9c3d-5eb46c7af9fd" />

---

### 2.1 Allow Port

Chọn `New Rule` bên phải → `Port` → nhập port → `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/53d58a0d-f998-4be9-a13f-b751ba9fe149" />

Chọn `Allow the connection` → `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/c24666c5-4c58-47be-bdce-7ef68135d97f" />

Chọn cả 3: `Domain`, `Private`, `Public` → `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/d400dace-60e1-4de8-91d4-5d98a276c692" />

Đặt tên → `Finish`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/4de80b13-d559-48d2-8a0c-8e3c54d7c7a1" />

Kiểm tra bằng nmap (port 3389 đang được sử dụng bởi RDP nên sẽ hiện service đang chạy):

```
nmap -p 3389 14.225.204.109
```

<img width="692" height="173" alt="image" src="https://github.com/user-attachments/assets/0e17d869-21f2-4016-9290-a7869b3b60b3" />

---

### 2.2 Block Port

Chọn `New Rule` bên phải → `Port` → nhập port → `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/da04e56c-e5d5-4c81-8e4e-2a2f4942d7d7" />

Chọn `Block the connection` → `Next`

<img width="708" height="478" alt="image" src="https://github.com/user-attachments/assets/ab627588-1402-4e1e-869b-e7253dee5903" />

Chọn cả 3: `Domain`, `Private`, `Public` → `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/d400dace-60e1-4de8-91d4-5d98a276c692" />

Đặt tên → `Finish`

<img width="712" height="548" alt="image" src="https://github.com/user-attachments/assets/6f1cdfd1-c67a-4c4a-ba20-271a1b3c0b57" />

Kiểm tra port 8083 đã bị block:

```
nmap -p 8083 14.225.204.109
```

<img width="692" height="162" alt="image" src="https://github.com/user-attachments/assets/adc853c7-cb2d-4d8f-86d8-1da3e1f83e93" />

---

### 2.3 Allow IP

Chọn `New Rule` → `Custom` → `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/da53eafd-bc87-4dfc-b910-d84c0baed01e" />

`All programs` → `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/68f5165b-3e58-4948-ac6e-f7b174f8f79b" />

`Protocol and Ports` → `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/065ad4d1-820e-4f7f-8fca-cc6fb4aa51be" />

Tại bước `Scope`: giữ nguyên phần `Which local IP addresses` và thêm IP vào phần `Which remote IP addresses` → `These IP addresses` → `Add` → nhập IP → `OK` → `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/3a3f67ab-1498-4e43-a43f-f1396fbafafe" />

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/143bc4b9-cf4f-4a67-847e-6c883d505ce7" />

`Allow the connection` → `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/8970b12e-6eb8-4ba3-a554-69bb7148dbf9" />

Chọn cả 3: `Domain`, `Private`, `Public` → `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/4adfafd6-c17c-419b-aa9a-10596d021dcb" />

Đặt tên → `Finish`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/a4b3c261-d116-48ce-8493-79b26ff5ed3e" />

---

### 2.4 Block IP

Thực hiện tương tự Allow IP, nhưng tại bước `Action` chọn `Block the connection`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/812d5d2a-f4a4-4e2b-9515-d1853c9f42b2" />

Đặt tên → `Finish`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/85e9be3b-974f-40cc-bf3f-2d25058d5e84" />

---

### 2.5 Giới hạn IP - Chỉ cho phép IP chỉ định truy cập

Phương pháp: Block toàn bộ trước, sau đó Allow riêng IP được chỉ định.

#### Bước 1: Tạo rule Block all cho port 80

`wf.msc` → `Inbound Rules` → `New Rule`

<img width="704" height="561" alt="image" src="https://github.com/user-attachments/assets/1e42ec80-198e-4846-8b27-209af31aec24" />

Chọn `Port` → `TCP` → nhập `80` → `Next`

<img width="704" height="561" alt="image" src="https://github.com/user-attachments/assets/855b241c-937c-4daa-bd4e-48ba3e00441a" />

Chọn `Block the connection` → `Next` → `Next` → `Finish`

<img width="704" height="561" alt="image" src="https://github.com/user-attachments/assets/8720f436-f24a-4144-933d-fa4664a8a4fc" />

<img width="504" height="88" alt="image" src="https://github.com/user-attachments/assets/4f2a8830-f800-4c7d-a29d-bf75f4825075" />

#### Bước 2: Tạo rule Allow riêng IP chỉ định vào port 80

`New Rule` → `Custom` → `Next` → `Next`

<img width="715" height="566" alt="image" src="https://github.com/user-attachments/assets/8e2d3cc0-8e58-4faa-8f8b-37f00f987933" />

Protocol: `TCP` → Local port: `Specific` → nhập `80` → `Next`

<img width="715" height="566" alt="image" src="https://github.com/user-attachments/assets/e49b674a-cfb1-4402-a4c8-140270bd9beb" />

`Scope` → Remote IP → `These IP addresses` → `Add IP` → `Next`

<img width="715" height="566" alt="image" src="https://github.com/user-attachments/assets/eba1eab4-80ec-4795-a6e0-3c0222ab451b" />

`Allow the connection` → `Next` → `Next` → `Finish`

<img width="715" height="566" alt="image" src="https://github.com/user-attachments/assets/f59c9067-63a6-4e10-ac8b-6958c91593aa" />

> Lưu ý: Rule Allow luôn thắng rule Block cùng cấp trong Windows Firewall.

---

## 3. IIS Web Server

Mở `Server Manager` → `Add roles and features`

<img width="788" height="552" alt="image" src="https://github.com/user-attachments/assets/75bd2bee-f7aa-428e-99bb-f016a18311c5" />

Nhấn `Next` liên tục đến bước `Server Roles`

<img width="1153" height="869" alt="image" src="https://github.com/user-attachments/assets/0395c8d2-ac07-4de3-b0f6-6ee121c5ca35" />

Chọn `Web Server (IIS)` → `Add Features`

<img width="788" height="552" alt="image" src="https://github.com/user-attachments/assets/d5664306-4f26-46ee-8013-2968f1919146" />

`Next` → `Next` → `Install` → chờ cài xong

<img width="1791" height="938" alt="image" src="https://github.com/user-attachments/assets/f7802488-4ddc-4397-ac0d-c5f3219ceded" />

Kiểm tra bằng cách truy cập `http://localhost` trên trình duyệt

<img width="1791" height="938" alt="image" src="https://github.com/user-attachments/assets/67e338e7-6323-4602-b159-40b34cfa1397" />

---

## 4. SQL Server 2016

### Tải xuống

Truy cập `https://software.vietnix.tech/datastore/sources/SQL_Server/sql2016/` → Download

<img width="1791" height="938" alt="image" src="https://github.com/user-attachments/assets/897e5381-b716-4c6c-a6ea-f0e849108f89" />

<img width="971" height="84" alt="image" src="https://github.com/user-attachments/assets/5fdcdf0c-da31-4852-9b45-ae388883f756" />

<img width="1131" height="242" alt="image" src="https://github.com/user-attachments/assets/f8b2aa08-0576-459d-a501-abc442127bae" />

### Cài đặt

Chuột phải vào file ISO → `Mount`

<img width="1131" height="398" alt="image" src="https://github.com/user-attachments/assets/e6754cfa-69b6-4b91-a1c6-39de7610c3b8" />

Vào ổ đĩa vừa mount → chọn `setup.exe`

<img width="1131" height="398" alt="image" src="https://github.com/user-attachments/assets/01fb5f16-7376-4369-ae77-a3e293db5c0d" />

Chọn `Installation` → `New SQL Server stand-alone installation or add features to an existing installation`

Nhập key → `Next`

<img width="783" height="594" alt="image" src="https://github.com/user-attachments/assets/856031cc-3123-431d-9d1b-51f07eb0f538" />

Chọn `I accept the license terms` → `Next`

<img width="783" height="594" alt="image" src="https://github.com/user-attachments/assets/eb0cc146-c3a7-4bed-8e2e-82e54856f4a5" />

Đến phần `Feature Selection` → chọn các Feature cần thiết → `Next`

<img width="625" height="497" alt="image" src="https://github.com/user-attachments/assets/65ab7106-f919-4877-9e58-65549242c5ad" />

Đến phần `Database Engine Configuration` → chọn `Mixed Mode` → `Add Current User` → `Next`

<img width="1605" height="778" alt="image" src="https://github.com/user-attachments/assets/af6dc845-7ca7-49f9-9902-4ecdc0a26c66" />

`Install`

<img width="1777" height="802" alt="image" src="https://github.com/user-attachments/assets/da1725dd-2cda-436e-bf8a-a6896503a0a7" />

`Complete`

<img width="1777" height="802" alt="image" src="https://github.com/user-attachments/assets/7736cee8-7719-4348-a1c6-990699440678" />

### Cài đặt SSMS và .NET Framework 4.7.2

Truy cập Internet Explorer → tải tại `https://aka.ms/ssmsfullsetup` và `https://go.microsoft.com/fwlink/?LinkId=863262`

<img width="595" height="51" alt="image" src="https://github.com/user-attachments/assets/3b9e8ae4-375d-4c06-a967-990d680c8537" />

Cài đặt .NET Framework 4.7.2 trước

<img width="499" height="461" alt="image" src="https://github.com/user-attachments/assets/1f043ede-5c29-4a67-a9a7-09db361f0780" />

`Finish`

<img width="499" height="461" alt="image" src="https://github.com/user-attachments/assets/4465f6d4-6e76-4661-9562-2ae81ac24b64" />

Restart và cài đặt SSMS

<img width="680" height="583" alt="image" src="https://github.com/user-attachments/assets/01317b9a-0db5-48b2-91e1-0d3f828afb34" />

Hoàn tất cài đặt

<img width="680" height="583" alt="image" src="https://github.com/user-attachments/assets/b9039822-7330-4fd1-b09f-5625c63ef826" />

### Kết nối SSMS

Mở SSMS

<img width="826" height="434" alt="image" src="https://github.com/user-attachments/assets/a5d623c9-a5b1-4d85-9cb7-fde7a1ae6478" />

Thiết lập thông tin kết nối → `Connect`

<img width="1790" height="851" alt="image" src="https://github.com/user-attachments/assets/f6c53cb4-68b4-449f-ad45-7e8ce87043e2" />

Kết nối thành công

<img width="1790" height="851" alt="image" src="https://github.com/user-attachments/assets/d8f08e2c-7d32-4636-a949-9d321f3689c4" />

---

## 5. WordPress

### 5.1 Cài đặt PHP

Truy cập `https://windows.php.net/download/` → chọn bản PHP phù hợp → Download

<img width="1790" height="851" alt="image" src="https://github.com/user-attachments/assets/9848c362-8b5f-4669-94fb-993ac1eef2a2" />

<img width="1790" height="851" alt="image" src="https://github.com/user-attachments/assets/c1120b9e-b26d-46f1-b7d0-dcf411c6ec05" />

Giải nén file vừa tải

<img width="1790" height="851" alt="image" src="https://github.com/user-attachments/assets/caf290d9-39a3-470b-b335-471474e29a50" />

Tìm file `php.ini-production` → đổi tên thành `php.ini`

<img width="600" height="23" alt="image" src="https://github.com/user-attachments/assets/9bb4f07e-d86e-4073-b75f-cc04be84a827" />

Mở `php.ini` bằng Notepad → bỏ dấu `;` ở các dòng sau:

```
extension=mysqli
extension=openssl
extension=mbstring
extension=gd
```

<img width="547" height="454" alt="image" src="https://github.com/user-attachments/assets/1cebd04d-54a5-4a16-a8f2-2e60001bb696" />

Mở IIS Manager → `Handler Mappings` → `Add Module Mapping` → nhập thông tin → `Yes`

```
Request path: *.php
Module: FastCgiModule
Executable: C:\PHP\php-cgi.exe
Name: PHP_via_FastCGI
```

<img width="1373" height="687" alt="image" src="https://github.com/user-attachments/assets/5b267e70-87ba-4876-977b-30f08e92c02a" />

---

### 5.2 Cài đặt MySQL

Truy cập `https://dev.mysql.com/downloads/installer/` → Download bản MySQL 8.0

<img width="785" height="595" alt="image" src="https://github.com/user-attachments/assets/146ec993-2fc9-4812-b56e-38f6850c7148" />

<img width="593" height="23" alt="image" src="https://github.com/user-attachments/assets/03cb7191-a614-4e3c-ba97-10b9e727c177" />

Cài đặt → `Server only` → `Next` → `Execute` → `Next` → tại bước `Authentication Method` chọn `Use Legacy Authentication Method`

<img width="787" height="587" alt="image" src="https://github.com/user-attachments/assets/5d53c669-d502-4b93-8bf0-41c8ab3277d8" />

Tại bước `Accounts and Roles` nhập password → `Next` → `Execute` → `Finish`

<img width="787" height="587" alt="image" src="https://github.com/user-attachments/assets/99c6d56a-33f2-40f6-bad6-30de4628f9a5" />

<img width="787" height="587" alt="image" src="https://github.com/user-attachments/assets/7718e86e-281d-471d-a4e6-9faa6a8225bd" />

---

### 5.3 Cài đặt WordPress

Truy cập `https://wordpress.org/latest.zip` → Download

<img width="706" height="172" alt="image" src="https://github.com/user-attachments/assets/e8be8ef5-383f-4e66-a800-bf266d96f974" />

Giải nén → copy toàn bộ nội dung bên trong thư mục `wordpress` → paste vào `C:\inetpub\wwwroot\`

> Lý do: `C:\inetpub\wwwroot\` là thư mục gốc mặc định của IIS. Khi người dùng truy cập địa chỉ IP hoặc domain, IIS sẽ đọc file từ thư mục này để hiển thị website.

<img width="706" height="172" alt="image" src="https://github.com/user-attachments/assets/c50c33f0-06ef-4424-a4db-6255bf0e116a" />

<img width="663" height="512" alt="image" src="https://github.com/user-attachments/assets/0c75f443-6c45-4add-bf15-f3047b4920ee" />

<img width="663" height="512" alt="image" src="https://github.com/user-attachments/assets/893b1a58-db10-4d20-a56c-dc6ad96d1993" />

### Tạo database cho WordPress

```sql
CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
```

<img width="625" height="400" alt="image" src="https://github.com/user-attachments/assets/a4bf0911-a18c-4289-ba22-5dd1d2cf685f" />

### Cài đặt WordPress qua trình duyệt

Truy cập `http://localhost/wp-admin/setup-config.php`

<img width="937" height="644" alt="image" src="https://github.com/user-attachments/assets/9abbc1c0-5ac4-4e47-861b-3d73e2ff583b" />

Nhập thông tin database và site

<img width="946" height="760" alt="image" src="https://github.com/user-attachments/assets/f0fbe412-1d7f-4ed9-be06-ce93612b2d02" />

<img width="916" height="885" alt="image" src="https://github.com/user-attachments/assets/6aea4b0c-fca5-478e-a212-309cd05949a5" />

Kết quả cài đặt thành công

<img width="916" height="885" alt="image" src="https://github.com/user-attachments/assets/24ac86e5-af8f-4d89-b05f-2892a1e3d624" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/47f00808-19f7-481c-adea-055c5ce51c1d" />

---

## 6. SSL

### Tải và cài đặt Win-ACME

Mở PowerShell với quyền Administrator → chạy các lệnh sau:

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri "https://github.com/win-acme/win-acme/releases/download/v2.2.9.1701/win-acme.v2.2.9.1701.x64.pluggable.zip" -OutFile "C:\win-acme.zip"
Expand-Archive -Path "C:\win-acme.zip" -DestinationPath "C:\win-acme"
cd C:\win-acme
.\wacs.exe
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d7afe8b6-b6b2-433f-a64d-034e430dce57" />

### Thiết lập chứng chỉ SSL

Trước khi chạy wacs.exe, cần thêm binding domain trong IIS Manager: `Sites` → `Default Web Site` → `Bindings` → `Add` → nhập domain.

Sau đó trong wizard Win-ACME, lần lượt chọn:

```
Please choose from the menu: N
Site identifier(s) or <Enter> to choose all: <Enter>
Binding identifiers(s) or menu option: A
Continue with this selection? (y*/n): Y
Open in default application? (y/n*): N
Do you agree with the terms? (y*/n): Y
Enter email(s) for notifications: <Enter>
```

### Kết quả

Chứng chỉ SSL được cài đặt thành công

<img width="573" height="290" alt="image" src="https://github.com/user-attachments/assets/511a8f4f-fb51-4f3c-83ce-a2bdca657eb7" />

Kiểm tra kết quả tại `https://wp.dangkhoi.vietnix.tech`

<img width="280" height="246" alt="image" src="https://github.com/user-attachments/assets/546c5b78-91c0-464c-89cf-a63e3fc929d2" />

---

## Tổng kết

| Hạng mục | Trạng thái |
|---|---|
| Allow port, Allow IP trên Windows Firewall | Hoàn thành |
| Block port, Block IP trên Windows Firewall | Hoàn thành |
| Giới hạn IP chỉ định truy cập | Hoàn thành |
| Cài đặt IIS Web Server | Hoàn thành |
| Cài đặt WordPress trên IIS | Hoàn thành |
| Cài đặt SSL cho WordPress | Hoàn thành |
| Cài đặt SQL Server 2016 | Hoàn thành |
