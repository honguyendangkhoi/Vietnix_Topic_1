# Tổng Quan Về Hệ Thống Phân Giải Tên Miền (DNS)

> [!NOTE]
> **Khái niệm:** DNS (Domain Name System - Hệ thống phân giải tên miền) là một hệ thống sắp xếp danh mục có thứ bậc dành cho các máy tính, dịch vụ hoặc bất kỳ tài nguyên nào kết nối với mạng Internet. Nhiệm vụ cốt lõi của DNS là dịch chuyển tên miền (Domain Name) dạng ký tự dễ nhớ sang địa chỉ IP (Internet Protocol) dạng số mà máy tính có thể hiểu được, đóng vai trò như một "danh bạ điện thoại" của toàn bộ mạng Internet.

---

## 1. Nguyên Lý Và Cách Thức Hoạt Động Của Hệ Thống DNS

Khi người dùng nhập một tên miền (Ví dụ: `vietnix.vn`) vào trình duyệt, hệ thống DNS sẽ bắt đầu quy trình truy vấn qua 4 máy chủ phân giải theo thứ tự để tìm ra địa chỉ IP chính xác:

1. **DNS Recursor (Trình đệ quy DNS):** Là máy chủ đầu tiên tiếp nhận yêu cầu từ trình duyệt của người dùng. Nó đóng vai trò là một người giao dịch, chịu trách nhiệm đi hỏi các máy chủ DNS khác để lấy về địa chỉ IP chuẩn xác nhất.
2. **Root Nameserver (Máy chủ tên miền gốc):** Là bước đầu tiên trong quá trình tìm kiếm. Máy chủ gốc không lưu trữ địa chỉ IP của từng web cụ thể, mà nó điều hướng DNS Recursor đến máy chủ quản lý phần mở rộng (TLD) tương ứng (như `.vn` hoặc `.com`).
3. **TLD Nameserver (Máy chủ tên miền cấp cao nhất):** Máy chủ này quản lý toàn bộ thông tin của một phần mở rộng tên miền cụ thể. Tại đây, nó sẽ trỏ DNS Recursor đến máy chủ có quyền quản lý trực tiếp tên miền của bạn (Authoritative Nameserver).
4. **Authoritative Nameserver (Máy chủ tên miền có thẩm quyền):** Đây là điểm dừng cuối cùng trong chuỗi truy vấn. Máy chủ này chứa bản ghi cấu hình chính thức của tên miền. Nó sẽ trả về địa chỉ IP đích (Ví dụ: `123.45.67.89`) cho DNS Recursor để gửi về trình duyệt.

---

## 2. Các Loại Bản Ghi DNS Cơ Bản Và Phổ Biến Nhất

Để cấu hình hoạt động cho tên miền, người quản trị mạng cần sử dụng các loại bản ghi (DNS Records) khác nhau trong vùng cấu hình (Zone file):

* **Bản ghi A (Address Record):** Bản ghi cơ bản nhất, dùng để ánh xạ (trỏ) trực tiếp một tên miền về một địa chỉ IPv4 vật lý của máy chủ.
* **Bản ghi AAAA:** Tương tự như bản ghi A, nhưng được sử dụng để ánh xạ tên miền về một địa chỉ IPv6.
* **Bản ghi CNAME (Canonical Name Record):** Cho phép một tên miền đóng vai trò là bí danh (alias) của một tên miền gốc khác, giúp nhiều sub-domain chạy chung một cấu hình mà không cần tạo nhiều bản ghi A riêng lẻ.
* **Bản ghi MX (Mail Exchange Record):** Bản ghi chuyên dụng dùng để xác định máy chủ nào sẽ chịu trách nhiệm tiếp nhận và xử lý luồng thư điện tử (Email) gửi đến của tên miền đó.
* **Bản ghi TXT (Text Record):** Dùng để lưu trữ các chuỗi văn bản thuần túy dạng text. Thường được sử dụng để xác thực quyền sở hữu tên miền với bên thứ ba (như Google, Facebook) hoặc cấu hình các cơ chế bảo mật email như SPF, DKIM.

---

## 3. Khái Niệm DNS Caching (Bộ Nhớ Đệm DNS)

* **Bản chất:** Quá trình truy vấn DNS qua cả 4 máy chủ mất một khoảng thời gian nhất định (độ trễ). Để tối ưu hóa, công nghệ **DNS Caching** ra đời nhằm lưu trữ tạm thời kết quả địa chỉ IP đã phân giải vào bộ nhớ đệm.
* **Các cấp độ lưu trữ Cache:** Dữ liệu DNS có thể được lưu trữ tạm thời ngay trên Trình duyệt web, hệ điều hành máy tính cá nhân (OS Cache) hoặc tại máy chủ của nhà cung cấp dịch vụ Internet (ISP).
* **Giá trị TTL (Time To Live):** Quyết định thời gian (tính bằng giây) mà một bản ghi DNS được phép lưu lại trong bộ nhớ đệm trước khi hết hạn và bắt buộc hệ thống phải thực hiện một chu kỳ truy vấn mới từ đầu để cập nhật thông tin.

---

## 4. Tầm Quan Trọng Của DNS Trong An Ninh Mạng

Hạ tầng DNS là mục tiêu hàng đầu của các cuộc tấn công mạng, đòi hỏi các biện pháp bảo mật chuyên sâu:
* **DNS Spoofing / Cache Poisoning (Giả mạo DNS):** Kẻ tấn công ghi dữ liệu IP giả vào bộ nhớ đệm DNS, khiến người dùng bị điều hướng đến các website lừa đảo dù họ gõ đúng tên miền hợp pháp.
* **Giải pháp bảo mật - DNSSEC (Domain Name System Security Extensions):** Bộ tiêu chuẩn mở rộng giúp bổ sung chữ ký số mật mã vào các bản ghi DNS. Hệ thống này giúp xác thực nguồn dữ liệu trả về là hoàn toàn chính xác, nguyên vẹn và chưa bị chỉnh sửa trên đường truyền mạng.

---

## 5. Câu Hỏi Thường Gặp (FAQs)

### Tại sao sau khi đổi bản ghi DNS, website vẫn chưa hoạt động ngay?
Hiện tượng này gọi là **Thời gian cập nhật DNS (DNS Propagation)**. Khi bạn thay đổi hoặc thêm mới bản ghi, các máy chủ DNS trên toàn thế giới cần thời gian để xóa bỏ bộ nhớ đệm cũ (dựa trên thời gian TTL cũ) và đồng bộ hóa dữ liệu mới. Quá trình này có thể diễn ra từ vài phút cho đến 24 hoặc 48 giờ tùy thuộc vào nhà mạng ISP.

### Thay đổi DNS trên máy tính cá nhân (như đổi sang 8.8.8.8) để làm gì?
Mặc định máy tính sẽ dùng DNS của nhà mạng ISP cung cấp đường truyền. Việc chủ động đổi cấu hình sang các hệ thống DNS công cộng lớn (như Google `8.8.8.8` / `8.8.4.4` hoặc Cloudflare `1.1.1.1`) giúp tăng tốc độ phân giải tên miền nhanh hơn, tăng tính bảo mật, tránh tình trạng nghẽn mạch DNS của nhà mạng và hỗ trợ truy cập vào các trang web bị chặn do lỗi phân giải cấu hình nội địa.
