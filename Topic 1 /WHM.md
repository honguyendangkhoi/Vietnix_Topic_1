# Hướng Dẫn Quản Trị Hệ Thống Qua WHM (WebHost Manager)

**Khái niệm:** WHM (WebHost Manager) là giao diện quản trị cấp cao dành cho người quản trị máy chủ (Server Administrator) hoặc đại lý (Reseller). Nếu cPanel dùng để quản trị một website đơn lẻ, thì WHM cho phép bạn quản lý cấu hình toàn bộ máy chủ, tạo/xóa các tài khoản cPanel con, gán gói cước và theo dõi trạng thái hệ thống máy chủ.

---

## 1. Đổi Tên Miền Chính (Primary Domain) Của Một Tài Khoản cPanel

Khi người dùng cần đổi tên miền chính của một gói Hosting hiện có, bạn thực hiện qua các bước sau trên WHM:

1. Tìm kiếm và chọn tính năng **Modify an Account** ở thanh tìm kiếm (Search Bar) bên trái.
2. Tìm kiếm User hoặc Domain cần thay đổi trong danh sách (Có thể search theo Domains, IP Address, Owner...).
3. Nhấp vào nút **Modify** tương ứng với tài khoản đó.
4. Tại giao diện *Editing User*, nhập tên miền mới vào ô **Primary Domain**.
5. Nhấn **Save** để lưu lại.

**Các trường hợp có thể xảy ra khi Save:**
* *Thành công:* Tên miền được đổi bình thường.
* *Lỗi "Domain đã tồn tại":* WHM báo lỗi nếu tên miền này đã được add vào hệ thống trước đó. Bạn cần kiểm tra xem người dùng có đang gắn tên miền này dưới dạng *Addon Domain* hoặc *Parked Domain* trong cPanel hay không. Nếu có, yêu cầu họ phải gỡ ra trước thì mới có thể đổi thành Primary Domain được.

---

## 2. Migrate và Transfer (Chuyển Dữ Liệu Hosting)

Tính năng **Transfer Tool** giúp bạn di chuyển (migrate) tài khoản cPanel từ một máy chủ (Server cũ) sang máy chủ hiện tại (Server mới) một cách nhanh chóng.

### Các bước thực hiện:
1. Tại WHM của Server mới, tìm và truy cập công cụ **Transfer Tool**.
2. **Cấu hình Remote Server Information:**
   * *Remote Server Address:* Nhập địa chỉ IP của máy chủ cũ (nơi chứa data cần chuyển).
   * *Remote SSH Port:* Mặc định là `22` (hoặc port SSH custom của server cũ).
3. **Cấu hình Authentication (Xác thực):**
   * *Login:* Chọn **Root**.
   * *Authentication Method:* Chọn **SSH Public Key**.
   * *SSH Key:* Chọn key có tên là `transfer`.
4. Bấm chọn **Scan Remote Server**. Hệ thống sẽ quét toàn bộ danh sách user trên server cũ.
5. Tick chọn (☑) vào các Domain/User cần chuyển, sau đó bấm nút **Copy** để bắt đầu tiến trình Migrate.

*(Lưu ý: Thông thường sau khi quá trình transfer hoàn tất, tài khoản trên server cũ sẽ tự động bị Suspend (khóa) để tránh xung đột, nhưng kỹ thuật viên nên vào kiểm tra lại thủ công để đảm bảo an toàn).*

---

## 3. Các Lệnh Terminal Cơ Bản Dành Cho Kỹ Thuật (Tech)

Từ giao diện Terminal của máy chủ, Tech có thể thực hiện nhanh các thao tác kiểm tra lỗi (troubleshooting):

* **Reload Hosting / Cập nhật CageFS cho một User:**
    ```bash
    cagefsctl -m <tên-user>
    ```
* **Kiểm tra nhật ký truy cập (Domlogs):** Nơi chứa file log của các request truy cập vào domain.
    * *Với Domain không có SSL (HTTP):* `cat /var/log/apache2/domlogs/<domain>`
    * *Với Domain có SSL (HTTPS):* `cat /var/log/apache2/domlogs/<domain>-ssl_log`
* **Kiểm tra các tiến trình (Process) đang chạy của một User:**
    ```bash
    ps aux | grep <tên-user>
    ```
* **Tìm xem một Addon Domain đang thuộc sở hữu của User nào:**
    ```bash
    cat /etc/userdatadomains | grep "ten-domain-can-tim.com"
    ```
    *(Mẹo: Bạn cũng có thể tra cứu thông tin này bằng giao diện WHM thông qua tính năng **List Subdomains**).*

---

## 4. Quản Trị Hệ Thống Mail (Exim Configuration Manager)

WHM sử dụng Exim làm máy chủ gửi/nhận mail chính. Để kiểm tra cấu hình SMTP Relay (port gửi mail):

1. Truy cập **Exim Configuration Manager** > Chọn tab **Advanced Editor**.
2. Nhấn `Ctrl + F` và tìm từ khóa `POSTMAILCOUNT`.
3. Tìm đến cấu hình router (ví dụ: `route_list = "10.23.158.1:587"`). Cấu hình này cho biết hosting đang kết nối tới Mail Relay Server thông qua Port 587.

---

## 5. Phân Tích Lỗi Chậm Website Bằng PHP X-Ray (CloudLinux)

**PHP X-Ray** là một công cụ mạnh mẽ thuộc hệ sinh thái CloudLinux, dùng để trace (truy vết) chi tiết thời gian thực thi của từng function PHP. Nó giúp Tech phát hiện chính xác hàm (function) hay plugin nào đang gây chậm website của khách.

### Các bước thực hiện Tracing:
1. Truy cập **CloudLinux Manager** trên WHM.
2. Mở tab **X-Ray** và nhấn nút **Start Tracing**.
3. Cấu hình thông số:
   * *URL:* Điền chính xác đường dẫn đang bị chậm (URL khách báo lỗi).
   * *Client's IP:* Điền địa chỉ IP của máy bạn (Tech) để trace riêng bạn, hoặc để dấu `*` để trace mọi IP truy cập vào URL đó.
   * *Record for:* Chọn **Time period** (Trace theo thời gian) hoặc **Request** (Trace theo số lượng request chỉ định, ví dụ 20 request).
4. Nhấn **Run** để bắt đầu.
5. Tech cần mở trình duyệt và F5 tải lại đường link URL trên vài lần để công cụ lấy mẫu dữ liệu.
6. Quay lại bảng kết quả X-Ray, click vào biểu tượng con mắt (**View**) tại mục Actions để xem thống kê.

Hệ thống sẽ hiển thị **Top issues** liệt kê các PHP Function (như `preg_replace_callback`, `curl_exec`...) và **Top software modules/plugins** tiêu tốn nhiều thời gian xử lý (Duration %) nhất. Nếu thấy file hoặc hàm nào quá chậm, Tech sẽ dựa vào đó để tư vấn hoặc hỗ trợ khách hàng tối ưu lại mã nguồn.
