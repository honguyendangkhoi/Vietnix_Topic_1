# Tổng Quan Về Server Control Panel
# 1. Lợi Ích Của Server Control Panel

- **Cài đặt và quản lý phần mềm**
  - Cài nhanh WordPress, Drupal, Joomla...
  - Hỗ trợ triển khai web chỉ bằng vài cú click

- **Quản lý tệp tin (File Manager)**
  - Tạo tài khoản FTP
  - Backup dữ liệu
  - Upload/xóa/nén/đổi tên file
  - Bảo vệ thư mục

- **Quản lý Domain**
  - Thêm/xóa domain
  - Redirect domain
  - Tạo subdomain

- **Quản lý cơ sở dữ liệu**
  - Tích hợp phpMyAdmin
  - Quản lý MySQL/MariaDB

- **Bảo mật**
  - Quản lý SSL/TLS
  - Thiết lập SSH

- **Giám sát hệ thống**
  - Monitor
  - Logs
  - Statistics

---

# 2. DirectAdmin

DirectAdmin (DA) là một trong những control panel lâu đời và phổ biến nhất hiện nay, nổi bật với giao diện đơn giản, dễ sử dụng và khá nhẹ.

## Thông Tin Chung & Yêu Cầu Hệ Thống

- **Nhà phát triển:** JBMC Software
- **Ra mắt:** 01/03/2003

### Hệ điều hành hỗ trợ

- CloudLinux
- CentOS
- Ubuntu
- Debian
- Red Hat
- Fedora Core
- FreeBSD

> Không hỗ trợ Windows.

### Cấu hình tối thiểu

| Thành phần | Yêu cầu |
|---|---|
| CPU | 500 MHz |
| RAM | 1GB (khuyến nghị 2GB) |
| Swap | 2GB |
| HDD | 2GB trống |

---

## Ưu Điểm và Nhược Điểm

### Ưu điểm

- Giao diện trực quan
- Chia 3 cấp quản trị:
  - Administrator
  - Reseller
  - User
- Chuyển đổi giữa các cấp dễ dàng
- Giá rẻ
- Có bản dùng thử
- Hỗ trợ ticket trực tiếp
- Ổn định cao
- Ít tốn tài nguyên
- Hỗ trợ command line

### Nhược điểm

- Plugin mở rộng hạn chế
- Một số tính năng phải trả phí
- Unicode chưa tốt
- Community nhỏ hơn cPanel
- Người mới dễ bị rối

---

## Phân cấp quản trị

### Administrator

- Quản lý toàn hệ thống
- Tạo Admin/Reseller
- Quản trị DNS
- Quản lý IP
- Quản lý Mail Queue
- Theo dõi dịch vụ
- DNS Clustering
- Quản lý License

### Reseller

- Tạo/sửa/xóa User
- Tạo hosting package
- Xem thống kê
- Quản lý giao diện
- Cấp phát IP
- Tạo Name Server riêng

### User

- Quản lý Email
- FTP
- DNS
- Subdomain
- File Manager
- MySQL
- Backup
- SSL
- Cron Job
- PHP Selector

---

## Cấu trúc File hệ thống

| Chức năng | Đường dẫn |
|---|---|
| Core Directory | `/usr/local/directadmin/` |
| Config chính | `/usr/local/directadmin/conf/directadmin.conf` |
| CustomBuild | `/usr/local/directadmin/custombuild/` |
| Config MySQL | `/usr/local/directadmin/conf/my.cnf` |
| Config User | `/usr/local/directadmin/data/users/[USERNAME]` |
| Logs | `/var/log/[service]` |

### API

```bash
https://www.directadmin.com/api.php
```

---

# 3. aaPanel

aaPanel là control panel miễn phí, phiên bản quốc tế hóa của BAOTA Panel.

Nó nổi tiếng vì nhẹ, dễ cài và hợp với VPS yếu. Kiểu “server chạy được là mừng rồi” nhưng surprisingly vẫn khá ổn.

---

## Thông Tin Chung & Yêu Cầu Hệ Thống

### Hỗ trợ

- LEMP
- LAMP

### Chức năng

- Quản lý Web
- Database
- FTP
- File Manager

### Hệ điều hành hỗ trợ

- CentOS
- Debian
- Ubuntu
- Fedora

> Yêu cầu hệ điều hành sạch, chưa cài PHP/Nginx/Apache/MySQL trước đó.

### Cấu hình tối thiểu

| Thành phần | Yêu cầu |
|---|---|
| RAM | 128MB |
| CPU | 1 Core |

### Khuyến nghị

- RAM: 512MB
- aaPanel dùng khoảng 10MB RAM

---

## Ưu Điểm và Nhược Điểm

### Ưu điểm

- Rất nhẹ
- Dễ cài
- Chỉnh config trực tiếp trên GUI
- App Store tích hợp:
  - Redis
  - Memcached
  - Google Drive
- File Manager đẹp
- Có code editor
- Backup lên cloud
- Community khá đông

### Nhược điểm

- MySQL mặc định hơi nặng
- VPS yếu dễ crash database
- Chỉ có 1 user admin
- Không hợp môi trường hosting chuyên nghiệp

---

## Cấu trúc File hệ thống

| Chức năng | Đường dẫn |
|---|---|
| Thư mục chính | `/www` |
| Web Root | `/www/wwwroot` |
| Logs | `/www/wwwlogs` |
| Service Config | `/www/server` |
| Backup | `/www/backup` |

### CLI

```bash
bt
```

---

# 4. CyberPanel

CyberPanel là control panel sử dụng OpenLiteSpeed, hỗ trợ tiếng Việt và rất nổi trong cộng đồng WordPress tối ưu tốc độ.

---

## Phân Loại Phiên Bản

### CyberPanel

- Miễn phí
- OpenLiteSpeed
- Unlimited domains

### CyberPanel Ent

- LiteSpeed Enterprise
- Free cho 1 domain

---

## Tính Năng Nổi Bật

- Giao diện hiện đại
- Hỗ trợ:
  - LSCache
  - Redis
  - Memcached
  - Multi PHP
- Hỗ trợ MariaDB
- Auto renew SSL
- Tích hợp:
  - DNS Server
  - Rainloop
  - FirewallD
  - SpamAssassin
  - ModSecurity
- One-click install:
  - WordPress
  - Drupal
  - Magento
- Hỗ trợ GitHub/GitLab

---

## Cấu trúc File hệ thống

| Chức năng | Đường dẫn |
|---|---|
| Config chính | `/usr/local/CyberCP/CyberCP/settings.py` |
| Data Directory | `/usr/local/CyberCP/` |
| User Config | `/home/cyberpanel` |
| Password Info | `/etc/cyberpanel` |

### CLI

```bash
cyberpanel
```

---

# 5. VestaCP

VestaCP là mã nguồn mở miễn phí sử dụng mô hình:

- Nginx xử lý static
- Apache xử lý dynamic

Khá nhẹ và tiết kiệm tài nguyên.

---

## Hệ điều hành hỗ trợ

- RHEL 5/6/7
- CentOS 5/6/7
- Debian 7
- Ubuntu 12.04 → 16.04

---

## Tính Năng & Ứng Dụng

### Ưu điểm

- Miễn phí
- Giao diện đơn giản
- Backup nhanh
- Hỗ trợ DKIM
- Hỗ trợ WHMCS
- Auto update
- Antivirus/Antispam
- SSL/SNI/Wildcard

### Phù hợp cho

- PHP/MySQL
- Mail Server
- DNS
- FTP
- Firewall
- Backup
- Phân quyền user

---

## Cấu trúc File hệ thống

| Chức năng | Đường dẫn |
|---|---|
| Config User/Domain | `/home/[user]/conf` |
| Config chính | `/usr/local/vesta/conf/vesta.conf` |
| Data Directory | `/usr/local/vesta/data/` |
| Web Root | `/home/[user]/web` |

### CLI

```bash
v-add-domain
v-add-user
v-list-web-domains
```

---

# 6. Bảng So Sánh Các Control Panel

| Tiêu Chí | DirectAdmin | aaPanel | CyberPanel | VestaCP |
|---|---|---|---|---|
| Miễn phí | Không | Freemium | Freemium | Có |
| User/Domain | Theo gói | 1 user | Unlimited | Unlimited |
| Webserver | Apache | Apache/Nginx | OpenLiteSpeed | Apache/Nginx |
| SSL | Có | Có | Có | Có nhưng chưa ổn định |
| File Manager | Có | Có | Có | Phải bật thủ công |
| FTP/PHPMyAdmin | Có | Có | Có | Có |
| DNS | Có | Có | Có | Có |
| Email Server | Có | Không | Có | Có |
| Backup | Thủ công | Thủ công | Thủ công | Có sẵn |
| Docker | Không | Có | Có | Không |
| Multi PHP | Có | Có | Có mặc định | Có thủ công |
| Reseller | Có | Không | Có | Không |
| NodeJS/Python | PRO only | Có | Không | Không |
| Dễ sử dụng | Dễ | Dễ | Trung bình | Khó |
| Firewall | CSF/LFD | Basic FW | Có | Có |
| Terminal GUI | Không | Có | Không | Không |
| Hosting Packages | Có | Không | Có | Có |
| LiteSpeed | Có | Trả phí | Có sẵn OLS | Không |
| API | Có | Có | Có | Không |

---

# Tổng Kết

| Nhu cầu | Panel phù hợp |
|---|---|
| Hosting chuyên nghiệp | DirectAdmin |
| VPS cá nhân nhẹ | aaPanel |
| WordPress tốc độ cao | CyberPanel |
| Mã nguồn mở miễn phí | VestaCP |
