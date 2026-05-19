# Hướng Dẫn Sử Dụng Chi Tiết Hệ Thống cPanel

---

## I. Giao Diện Tổng Quan Của cPanel

Sau khi đăng nhập, giao diện cPanel được chia thành 4 vùng chính cần nắm rõ:

1. **Search bar:** Thanh tìm kiếm nhanh. Rất hữu ích vì cPanel có nhiều tính năng, chỉ cần gõ từ khóa (ví dụ: "File") để truy cập nhanh.
2. **General Information:** Chứa các thông tin cơ bản của gói Hosting và server cPanel (User, Domain chính, IP Server, Theme).
3. **Statistics:** Bảng thống kê chi tiết các tài nguyên đang sử dụng như RAM, CPU, Processes, Addon Domain, Email Account, Bandwidth.
4. **Features:** Khu vực hiển thị toàn bộ tính năng của cPanel mà Admin cấp quyền cho người dùng sử dụng.

---

## II. Chi Tiết Các Tính Năng Quản Trị (Features)

### 1. Khu Vực Email (Email Section)
Khu vực này chứa các công cụ quản trị hệ thống thư điện tử của tên miền:

* **Email Accounts:** Chức năng chính để tạo mới, xóa, kiểm tra và quản lý dung lượng email, cung cấp thông số cấu hình cho Mail Client.
* **Forwarders:** Dùng để chuyển tiếp (forward) email đến một địa chỉ khác. Ví dụ: gửi vào `test@hosting.com` sẽ tự động chuyển tiếp về `tech@vietnix.vn`.
* **Email Routing:** Cấu hình định tuyến email. *Lưu ý:* Luôn luôn để ở chế độ `Local Mail Exchanger`, đổi sang giá trị khác sẽ không gửi được mail.
* **Autoresponders:** Cấu hình tự động trả lời email khi đi vắng hoặc ngoài giờ làm việc.
* **Default Address (Catch-all Email):** Khi ai đó gửi mail đến một địa chỉ không tồn tại trên hosting (ví dụ gõ sai tên), hệ thống sẽ không báo lỗi "No Such User Here" mà sẽ gom các email đó gửi về địa chỉ Default này.
* **Mailing Lists:** Tạo group email (ví dụ: `tech@vietnix.vn`). Khi có thư gửi vào group, hệ thống sẽ phân phối đồng thời cho tất cả các email thành viên bên trong.
* **Track Delivery:** Theo dõi trạng thái của email gửi ra (Thành công - Success, Tạm hoãn - Deferred, Thất bại - Failures).
* **Global Email Filters & Email Filters:** Tạo bộ lọc email cho toàn bộ tài khoản trên hosting (Global) hoặc cho từng tài khoản cụ thể.
* **Email Deliverability:** Kiểm tra và lấy thông số cấu hình DKIM, SPF, PTR để đảm bảo email không bị vào Spam.
* **Address Importer:** Import hàng loạt email account lên hosting bằng file `.csv` (Cấu trúc: `User, Password, Disk Quota`).
* **Spam Filters:** Cài đặt bộ lọc thư rác (dùng Apache SpamAssassin™) và cấu hình Whitelist/Blacklist. *(Lưu ý: Dịch vụ Email Hosting không sử dụng bộ lọc này).*
* **BoxTrapper:** Yêu cầu người gửi email phải xác minh họ là người thật thông qua thao tác phản hồi lại thư tự động. Quản lý Whitelist/Blacklist người gửi. *(Lưu ý: Không có trên Email Hosting).*
* **Email Disk Usage:** Công cụ xem thống kê dung lượng lưu trữ của từng hòm thư (INBOX, Trash, Sent...).
* **ASSP Antispam:** Hệ thống bảo vệ Email chuyên sâu với các tính năng:
  * *Spam Scoring:* Điều chỉnh mức độ lọc thư rác (từ Lowest đến Highest).
  * *Delaying Filter (Greylisting):* Khi nhận email, hệ thống lưu lại IP/Domain và trả về lỗi 451 để yêu cầu máy chủ gửi thử lại (cơ chế Syn Proxy). Giúp lọc spam tự động. *(Lưu ý: Mặc định tắt trên Mail Hosting, nếu bị lỗi 451 cần vào tắt đi).*
  * *No local addresses filter:* Chỉ nhận email nếu tài khoản người nhận thực sự tồn tại. Khi bật, tính năng Catch-all sẽ bị vô hiệu hóa.
  * *Virus Protection:* Quét và lọc email chứa virus.
  * *Trace Log:* Xem lịch sử hoạt động để khắc phục sự cố.

---

### 2. Khu Vực Quản Lý Tệp Tin (Files)
* **File Manager:** Công cụ quản lý tệp tin trực tiếp. Hỗ trợ Upload, xóa, sửa file, nén và giải nén. Để hiển thị file ẩn (như `.htaccess`, `.env`), người dùng cần click vào *Settings (Preferences)* và chọn *Show Hidden Files*.
* **Images:** Công cụ chỉnh sửa ảnh cơ bản của cPanel bao gồm Thumbnailer (Tạo ảnh thu nhỏ), Scaler (Thay đổi kích thước) và Converter (Chuyển đổi định dạng tệp, ví dụ `.jpg` sang `.png`).
* **Directory Privacy:** Cài đặt User/Password bảo vệ cho các thư mục cụ thể trên cPanel (Tương tự cơ chế `htpasswd`).
* **Disk Usage:** Thống kê biểu đồ dung lượng ổ đĩa đang sử dụng bởi các thư mục, cơ sở dữ liệu và email.
* **Web Disk:** Quản lý dữ liệu web như một ổ đĩa mạng cục bộ (giống Google Drive, OneDrive), hỗ trợ giao thức truyền tải WebDAV.
* **FTP Accounts:** Tạo tài khoản FTP và phân quyền truy cập cho từng thư mục cụ thể.
* **Backup & Backup Wizard:** Tính năng sao lưu mặc định của cPanel. *(Lưu ý: Không sử dụng).*
* **Git Version Control:** Hỗ trợ làm việc với kho lưu trữ Git (GitHub), tự động Pull code khi có bản cập nhật mới trên Repo.
* **JetBackup 5:** Công cụ khôi phục dữ liệu chuyên dụng, quan tâm 3 lựa chọn chính:
  * *Full Backups:* Khôi phục toàn bộ hosting (bao gồm code, database, SSL...).
  * *Home Directory:* Khôi phục mã nguồn (có thể chọn khôi phục từng file riêng lẻ).
  * *Databases:* Khôi phục lại Database.

---

### 3. Khu Vực Cơ Sở Dữ Liệu (Databases)
* **phpMyAdmin:** Giao diện quản trị Database trực quan (đăng nhập bằng tài khoản MySQL).
* **MySQL Databases:** Thực hiện thủ công các bước: Tạo Database -> Tạo User -> Add User vào Database -> Phân quyền (Grant).
* **MySQL Database Wizard:** Trình hướng dẫn tạo Database theo từng bước (Step-by-step), giúp người mới không bị quên các thao tác gán quyền.
* **Remote MySQL:** Mở khóa và cho phép các địa chỉ IP từ xa kết nối vào MySQL trên hosting.

---

### 4. Khu Vực Tên Miền (Domains)
* **WP Toolkit / WordPress Manager by Softaculous:** Trình quản lý chuyên biệt, hỗ trợ cài đặt WordPress tự động, cài Themes, Plugins và bảo mật.
* **Site Publisher:** Tạo nhanh một website HTML cơ bản bằng các Template có sẵn của cPanel (ví dụ: trang Under Construction).
* **Domains:** Giao diện thêm mới (Addon), xóa tên miền và quản lý thư mục gốc (Document Root).
* **Redirects:** Công cụ cấu hình chuyển hướng tên miền.
* **Zone Editor:** Cấu hình các bản ghi DNS (A, CNAME, MX, TXT...) sau khi tên miền đã trỏ NameServer về Hosting (ví dụ: `ns1.host212.vietnix.vn`).
* **Dynamic DNS:** Xử lý cho các mạng có IP động. cPanel cấp 1 URL, khi IP thay đổi chỉ cần `curl` đến URL này để tự động cập nhật hệ thống.
* **IP Manager:** *(Chỉ có trên Hosting SEO)* Tính năng dùng để thay đổi địa chỉ IP độc lập cho từng tên miền (phục vụ SEO vệ tinh).

---

### 5. Khu Vực Thống Kê & Tài Nguyên (Metrics)
* **Visitors (Access Logs):** Hiển thị lịch sử truy cập (IP, Thời gian, URL). Rất hữu ích để kiểm tra dấu hiệu khi hosting bị tấn công (DDoS).
* **Errors:** Hiển thị Apache Error Logs (ví dụ: `[ERROR] Invalid rewrite base`). Dùng để debug lỗi mã nguồn.
* **Bandwidth:** Thống kê lưu lượng truyền tải (traffic) từng ngày theo từng domain.
* **Raw Access:** Tải xuống file nhật ký truy cập thô (Raw Logs) cho khách hàng tự phân tích.
* **Resource Usage:** Bảng theo dõi tài nguyên của máy chủ (dành cho hệ thống chạy CloudLinux). Các thông số bắt buộc nắm rõ:
  * *SPEED:* CPU của gói Hosting.
  * *PMEM:* Dung lượng RAM.
  * *IO:* Tốc độ đọc/ghi dữ liệu.
  * *EP:* Số lượng kết nối đồng thời tối đa.
  * *NPROC:* Số lượng tiến trình tối đa.
  * *IOPS:* Số phép đọc ghi mỗi giây.
  * **Ký hiệu cần nhớ:** `A` (Trung bình hiện tại), `L` (Giới hạn của gói), `F` (Số lần chạm ngưỡng giới hạn).

---

### 6. Khu Vực Bảo Mật (Security)
* **SSH Access:** Bật truy cập dòng lệnh từ xa và quản lý thêm SSH Keys (Public/Private Keys).
* **IP Blocker:** Chặn truy cập từ một IP hoặc một dải mạng (Range IP/CIDR).
* **SSL/TLS:** Quản lý chứng chỉ bảo mật thủ công (Tạo Private Keys, CSR, thêm file CRT).
* **Manage API Tokens:** Tạo các mã API để các phần mềm bên ngoài giao tiếp với cPanel.
* **Hotlink Protection:** Chặn các website khác lấy link trực tiếp hình ảnh/file tĩnh để gắn lên web của họ (chống ăn cắp băng thông).
* **Leech Protection:** Hoạt động cùng *Directory Privacy*. Nếu phát hiện một user lộ pass và chia sẻ cho nhiều người đăng nhập vào thư mục bảo mật, hệ thống sẽ chặn và điều hướng đi chỗ khác.
* **SSL/TLS Status:** Trình quản lý AutoSSL (chứng chỉ bảo mật miễn phí tự động).
* **Two-Factor Authentication:** Cài đặt bảo mật 2 lớp cho tài khoản cPanel.
* **Imunify360:** Hệ thống tự động quét, phát hiện và cách ly mã độc (Malware Scanner).

---

### 7. Phần Mềm & Nền Tảng (Software)
* **PHP PEAR Packages & Perl Modules:** Cài đặt các gói tài nguyên bổ trợ để chạy script PHP/PERL.
* **Site Software:** Cài đặt các ứng dụng thương mại hoặc bảng tin cơ bản.
* **Optimize Website:** Cấu hình bật nén dữ liệu trên Web Server Apache để tối ưu tốc độ load.
* **Application Manager:** Đăng ký và triển khai các ứng dụng tùy chỉnh thông qua Phusion Passenger.
* **MultiPHP Manager:** *(Hỗ trợ bởi cPanel)* Tùy chọn thay đổi các phiên bản PHP khác nhau cho từng website.
* **MultiPHP INI Editor:** Bật/tắt và điều chỉnh các biến môi trường của PHP (như memory_limit, upload_max_filesize).
* **Softaculous Apps Installer:** Kho ứng dụng cho phép cài nhanh WordPress, Laravel, Moodle, NextCloud... chỉ với 1 click.
* **Setup Node.js App:** Trình cài đặt và chạy các ứng dụng viết bằng Node.js.
* **Select PHP Version:** *(Hỗ trợ bởi CloudLinux)* Giao diện chọn phiên bản và bật/tắt các Extensions cho PHP.

---

### 8. Các Chức Năng Nâng Cao (Advanced)
* **LiteSpeed Web Cache Manager:** Cho phép người dùng trực tiếp xóa cache (Flush LSCache) từ trong cPanel nếu đang dùng plugin Litespeed Cache.
* **Terminal:** Cửa sổ dòng lệnh Terminal trực tiếp trên trình duyệt web.
* **Cron Jobs:** Lên lịch chạy các tác vụ lặp đi lặp lại tự động (Ví dụ: Chạy file backup vào 12h đêm mỗi ngày).
* **Track DNS:** Công cụ theo dõi đường đi của mạng (Trace Route) từ PC đến Server để kiểm tra lỗi phân giải tên miền.
* **Indexes:** Tùy chỉnh cách Apache hiển thị cây thư mục (bật/tắt chế độ xem dạng danh sách file).
* **Error Pages:** Tùy biến giao diện của các trang lỗi (như lỗi 404, 403, 500) để hiển thị cho khách hàng.
* **Apache Handlers & MIME Types:** Cấu hình cách máy chủ Apache xử lý các định dạng phần mở rộng tệp tin đặc thù (như .html, .htm).
