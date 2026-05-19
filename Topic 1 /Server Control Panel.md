# Chuyên Đề: Server Control Panel
# Chương I: DirectAdmin

DirectAdmin là một bảng điều khiển (Control Panel) web hosting phổ biến nhờ giao diện đơn giản, trực quan và dễ sử dụng.

Phần mềm được thiết kế để hỗ trợ các công việc hàng ngày của webmaster, kể cả những người ít hoặc không có kinh nghiệm.

## 1. Thông Tin Chung & Yêu Cầu Hệ Thống

- **Nhà phát triển:** JBMC Software  
- **Ra mắt:** 01/03/2003
- **Hệ điều hành hỗ trợ:**
  - CloudLinux
  - CentOS
  - Ubuntu
  - Debian
  - Red Hat
  - Fedora Core
  - FreeBSD
- **Không hỗ trợ:** Windows

### Cấu hình tối thiểu

| Thành phần | Yêu cầu |
|---|---|
| CPU | 500 MHz |
| RAM | 1GB (khuyến nghị 2GB) |
| Swap | Tối thiểu 2GB |
| Ổ cứng | 2GB trống sau khi cài Linux |

---

## 2. Ưu Điểm và Nhược Điểm

### Ưu điểm

- Giao diện trực quan, chia 3 cấp:
  - Administrator
  - Reseller
  - User
- Hỗ trợ chuyển đổi nhanh giữa các cấp tài khoản
- Giá rẻ, từ khoảng 2 USD/tháng
- Có bản dùng thử miễn phí
- Hỗ trợ kỹ thuật trực tiếp qua ticket
- Ổn định, có khả năng tự khởi động lại dịch vụ khi lỗi
- Tốc độ xử lý nhanh, ít tốn tài nguyên
- Hỗ trợ cấu hình qua Command Line

### Nhược điểm

- Khả năng mở rộng hạn chế hơn cPanel
- Một số chức năng phải trả phí
- Unicode không tương thích tốt
- Cộng đồng nhỏ hơn nên khó tìm tài liệu nâng cao
- Người mới có thể bị rối vì chia nhiều cấp quản trị

---

## 3. Phân Cấp Tính Năng Quản Trị

### Administrator

- Quản lý Admin và Reseller
- Tạo package hosting
- Quản lý toàn bộ user
- Quản trị DNS
- Quản lý IP
- Quản lý Mail Queue
- Theo dõi hệ thống
- DNS Clustering
- Công cụ chống spam
- Cập nhật license

### Reseller

- Tạo/sửa/xóa User
- Tạo User Package
- Xem thống kê sử dụng
- Gửi tin nhắn hàng loạt
- Quản lý giao diện
- Cấp phát IP
- Theo dõi trạng thái hệ thống
- Tạo Name Server riêng

### User

- Quản trị Email
- FTP
- DNS
- File Manager
- MySQL
- Backup
- Subdomain
- SSL
- Cron Job
- PHP Selector
- Password Protection
- Error Pages

---

# Chương II: aaPanel

aaPanel là một Control Panel miễn phí, phiên bản quốc tế của BAOTA Panel, giúp đơn giản hóa việc cài đặt và quản trị VPS/Server.

## 1. Thông Tin Chung & Yêu Cầu Hệ Thống

- Hỗ trợ triển khai:
  - LEMP
  - LAMP
- Chức năng:
  - Quản lý Web
  - Database
  - FTP
  - File Manager

### Hệ điều hành hỗ trợ

- CentOS
- Debian
- Ubuntu
- Fedora

> Yêu cầu hệ điều hành sạch, chưa cài PHP/Apache/Nginx/MySQL trước đó.

### Cấu hình tối thiểu

| Thành phần | Yêu cầu |
|---|---|
| RAM | 128MB |
| CPU | 1 Core |

### Khuyến nghị

- RAM: 512MB
- aaPanel chỉ dùng khoảng 10MB RAM để vận hành

---

## 2. Ưu Điểm và Nhược Điểm

### Ưu điểm

- Nhẹ, chạy tốt trên VPS yếu
- Dễ cài đặt và sử dụng
- Chỉnh cấu hình PHP/Webserver trực tiếp trên GUI
- App Store cài:
  - Redis
  - Memcached
  - Google Drive
- File Manager thân thiện
- Có Code Editor
- Backup lên:
  - Google Drive
  - FTP
  - Amazon S3
- Cộng đồng khá lớn

### Nhược điểm

- MySQL/MariaDB mặc định cấu hình hơi nặng
- VPS yếu dễ bị crash MySQL
- Không hỗ trợ phân quyền nhiều user
- Chỉ phù hợp:
  - VPS cá nhân
  - Server nhỏ

---

# Chương III: CyberPanel

CyberPanel là Control Panel miễn phí sử dụng OpenLiteSpeed làm webserver và có hỗ trợ tiếng Việt.

## 1. Phân Loại Phiên Bản

### CyberPanel

- Miễn phí
- Dùng OpenLiteSpeed
- Không giới hạn domain

### CyberPanel Ent

- Dùng LiteSpeed Enterprise
- Chỉ miễn phí cho 1 domain

---

## 2. Tính Năng Nổi Bật

- Giao diện hiện đại
- Hỗ trợ:
  - LSCache
  - Multi PHP
  - Redis
  - Memcached
- Hỗ trợ MariaDB nhiều phiên bản
- Tự động gia hạn SSL Let's Encrypt
- Tích hợp:
  - Lightweight DNS
  - Rainloop Webmail
  - FirewallD
  - SpamAssassin
  - ModSecurity
- One-click install:
  - WordPress
  - Drupal
  - Magento
- Hỗ trợ Git:
  - GitHub
  - GitLab

---

# Chương IV: VestaCP

VestaCP là mã nguồn mở miễn phí, sử dụng mô hình Nginx + Apache:

- Nginx xử lý static
- Apache xử lý dynamic

Giúp phục vụ nhiều request với mức tiêu thụ tài nguyên thấp.

## 1. Hệ Điều Hành Hỗ Trợ

- RHEL 5/6/7
- CentOS 5/6/7
- Debian 7
- Ubuntu 12.04 → 16.04

---

## 2. Tính Năng & Ứng Dụng

### Tính năng

- Miễn phí hoàn toàn
- Giao diện đơn giản
- Tự động cập nhật
- Hỗ trợ:
  - SSL/SNI
  - Wildcard SSL
  - DKIM
  - Backup
  - Antivirus
  - AntiSpam
  - Monitoring
  - WHMCS

### Phù hợp cho

- Web PHP/MySQL
- Mail Server
- Webmail
- DNS Server
- Backup
- Firewall
- FTP
- Phân quyền user

---

# Chương V: Bảng So Sánh Các Control Panel

| Tiêu Chí | DirectAdmin | aaPanel | CyberPanel | VestaCP |
|---|---|---|---|---|
| Miễn phí | Không | Freemium | Freemium | Có |
| Giới hạn user/domain | Theo gói | 1 user | Nhiều | Nhiều |
| Webserver mặc định | Apache | Apache/Nginx | OpenLiteSpeed | Apache/Nginx |
| SSL | Có | Có | Có | Có nhưng chưa ổn định |
| File Manager | Có | Có | Có | Phải bật thủ công |
| FTP / PHPMyAdmin | Có | Có | Có | Có |
| DNS Server | Có | Có | Có | Có |
| Email Server | Có | Không | Có | Có |
| Backup/Restore | Thủ công | Thủ công | Thủ công | Có sẵn |
| Docker | Không | Có | Có | Không |
| Multi PHP | Có | Có | Có mặc định | Có nhưng thủ công |
| Reseller | Có | Không | Có | Không |
| NodeJS/Python | Chỉ PRO | Có | Không | Không |
| Dễ cài đặt | Dễ | Dễ | Khó | Khó |
| Firewall | CSF/LFD GUI | Cơ bản | Có | Có |
| Terminal GUI | Không | Có | Không | Không |
| Hosting Packages | Có | Không | Có | Có |
| Hỗ trợ LiteSpeed | Có | Trả phí | Chỉ OpenLiteSpeed | Có |
| Tính năng trả phí | Có | Plugin | Plugin | Plugin |
| API | Có | Có | Có | Không |

---

# Tổng Kết

| Nhu cầu | Panel phù hợp |
|---|---|
| Hosting chuyên nghiệp | DirectAdmin |
| VPS cá nhân nhỏ nhẹ | aaPanel |
| WordPress tốc độ cao | CyberPanel |
| Mã nguồn mở nhẹ | VestaCP |
