aaPanel:
aaPanel là một Bảng điều khiển quản trị máy chủ (Web Hosting Control Panel) miễn phí dành cho hệ điều hành Linux.
3 ưu điểm cốt lõi của aaPanel:

    Triển khai "1 chạm": Cài đặt toàn bộ bộ khung máy chủ LNMP/LAMP (Nginx, Apache, MySQL, PHP) cực nhanh chỉ với một nút bấm.

    Quản lý đa nền tảng: Cho phép chạy song song nhiều website, nhiều phiên bản PHP, dễ dàng thiết lập môi trường cho cả WordPress và Laravel trên cùng một VPS.

    Trực quan & Tối ưu: Tích hợp sẵn Quản lý tệp tin (File Manager), App Store phong phú, biểu đồ theo dõi CPU/RAM theo thời gian thực và đặc biệt là tốn rất ít tài nguyên phần cứng so với cPanel hay DirectAdmin.

1. WP-Optimize (Caching cấp độ Ứng dụng - Application-Level)

    Cơ chế hoạt động: Hoạt động dựa trên PHP. Sử dụng Output Buffering để biên dịch trang web thành các tệp HTML tĩnh và lưu trữ trên ổ cứng.

    Luồng xử lý: Thông qua tập lệnh chuyển hướng (Rewrite Rules), Web Server sẽ trả trực tiếp tệp HTML tĩnh cho người dùng, bỏ qua tiến trình xử lý của PHP-FPM.

    Điều kiện triển khai: Tương thích với mọi nền tảng Web Server tiêu chuẩn (Apache, Nginx, hoặc mô hình Proxy kết hợp). Nguyên nhân là do tiến trình caching được xử lý hoàn toàn ở tầng ứng dụng, không phụ thuộc vào hạ tầng máy chủ cấp dưới.

2. LiteSpeed Cache (Caching cấp độ Máy chủ - Server-Level)

    Cơ chế hoạt động: Engine caching được tích hợp trực tiếp vào nhân (kernel) của Web Server. Plugin trên WordPress chỉ đóng vai trò là giao diện API, gửi các chỉ thị điều khiển qua HTTP Headers để máy chủ tự động lưu hoặc xóa cache.

    Luồng xử lý: Web Server tự kiểm tra và trả dữ liệu trong bộ nhớ đệm trước khi yêu cầu chạm đến tầng ứng dụng, triệt tiêu hoàn toàn thời gian khởi chạy môi trường PHP.

    Điều kiện triển khai: Hoạt động độc quyền trên môi trường OpenLiteSpeed hoặc LiteSpeed Enterprise. Không hỗ trợ và mất hoàn toàn tính năng Page Cache nếu triển khai trên Nginx hoặc Apache do thiếu module tương thích (mod_litespeed).

    

Reset ssh-key:

<img width="1016" height="113" alt="image" src="https://github.com/user-attachments/assets/ee7a7511-ae30-4495-aa61-eab7bacde9f1" />

Update lại driver:

<img width="606" height="119" alt="image" src="https://github.com/user-attachments/assets/918db752-6bb3-4252-a72d-1da4a3247fb6" />

```bash
apt update && apt upgrade -y
```

Cài đặt aaPanel:

<img width="1046" height="248" alt="image" src="https://github.com/user-attachments/assets/bcd206d0-b34b-4391-bc22-ab1be735a565" />

```bash
URL=https://www.aapanel.com/script/install_7.0_en.sh && \
if [ -f /usr/bin/curl ];then curl -ksSO "$URL";else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi; \
bash install_7.0_en.sh aapanel
```

Giao diện sau khi cài đặt xong:

<img width="676" height="179" alt="image" src="https://github.com/user-attachments/assets/599a8390-1d76-4005-88a3-f41dfec72fbb" />

Giao diện aaPanel:

<img width="1843" height="1054" alt="image" src="https://github.com/user-attachments/assets/df82056d-23ce-40bb-a99a-b5890dadccec" />

Tiến hành mở port (Nếu không truy cập được):

<img width="412" height="88" alt="image" src="https://github.com/user-attachments/assets/3cbc1566-22cd-400e-85c5-0b0d063b529a" />

Upload file:

<img width="1843" height="1054" alt="image" src="https://github.com/user-attachments/assets/4d4cd862-f098-4676-9748-c1eed729a32b" />

Sau khi upload thành công:

<img width="1843" height="1054" alt="image" src="https://github.com/user-attachments/assets/5a443b4f-4114-4a71-b38f-8da3514d6302" />

Giải nén:

<img width="759" height="604" alt="image" src="https://github.com/user-attachments/assets/d4f2cd10-f176-49a8-93d9-4501fb97d40b" />


Để liên kết 2 domain:
Trong aaPanel -> chọn Website -> cài đặt package theo yêu cầu:

- Nginx:

<img width="838" height="483" alt="image" src="https://github.com/user-attachments/assets/33b45502-5798-41ab-8146-1330956dd3c9" />

link domains:

<img width="825" height="619" alt="image" src="https://github.com/user-attachments/assets/fdcf8f2d-75b2-48ea-8978-a765ff04ee25" />

<img width="825" height="619" alt="image" src="https://github.com/user-attachments/assets/9ede34d0-05cb-423f-a48f-693bb2571e9f" />

- sau khi xong:
<img width="1611" height="276" alt="image" src="https://github.com/user-attachments/assets/5fb9dd7b-4653-4abf-b61b-810fdc3cf9a0" />

- Cài đặt package cho database:

<img width="1818" height="917" alt="image" src="https://github.com/user-attachments/assets/0040384d-d08e-4174-b049-4dd085804119" />

- Tạo databases:

<img width="1818" height="917" alt="image" src="https://github.com/user-attachments/assets/7bf18e76-2e45-4fc7-85cc-918f4fd51ec3" />

upload database:
- wordpress:

<img width="901" height="345" alt="image" src="https://github.com/user-attachments/assets/5a99ab00-dffd-4f36-aeb1-7dcce73d7286" />

- lavarel:

<img width="901" height="345" alt="image" src="https://github.com/user-attachments/assets/4be301ac-2612-4565-8c0e-99c2c1f0812b" />

- bật auto backup database:

<img width="357" height="68" alt="image" src="https://github.com/user-attachments/assets/87bbc86d-8b29-4b69-93cc-64afb2c21aa0" />

- chỉnh sửa file `wp-config.php` và file `.env` theo database vừa tạo:

<img width="759" height="604" alt="image" src="https://github.com/user-attachments/assets/a267977a-f563-48d5-bbc9-3defc5412bd7" />

<img width="310" height="117" alt="image" src="https://github.com/user-attachments/assets/1263647c-32a5-4861-9702-e88ca60f2d71" />

- clean cache của lavarel:

<img width="908" height="95" alt="image" src="https://github.com/user-attachments/assets/44c0649b-de02-4b05-b010-3a028e9d3ddd" />
```bash
/www/server/php/82/bin/php artisan config:clear
/www/server/php/82/bin/php artisan cache:clear
```

- Chỉnh sửa đường dẫn file để trỏ đến Lavarel:

<img width="871" height="736" alt="image" src="https://github.com/user-attachments/assets/8ba201b6-a7cb-4d4c-a23f-c6324dd0a723" />

- permission wordpress:

<img width="864" height="113" alt="image" src="https://github.com/user-attachments/assets/819cfe7e-25b8-4bbb-9808-b9d042499165" />

```bash
chown -R www:www /www/wwwroot/wp.dangkhoi.vietnix.tech

find /www/wwwroot/wp.dangkhoi.vietnix.tech -type d -exec chmod 755 {} \;
find /www/wwwroot/wp.dangkhoi.vietnix.tech -type f -exec chmod 644 {} \;
```


- Laravel:

<img width="1854" height="1005" alt="image" src="https://github.com/user-attachments/assets/1ead0ec4-65f7-4d9a-add1-35010b7d245e" />

<img width="738" height="221" alt="image" src="https://github.com/user-attachments/assets/05c3867d-ba0d-46dc-ad59-e07f60df3e26" />



Truy cập website Vietnix.vn:

<img width="1832" height="876" alt="image" src="https://github.com/user-attachments/assets/879fa97f-f396-4672-90b6-4cacc5e66898" />


Tải toàn bộ file:
- File sau khi tải:

<img width="694" height="223" alt="image" src="https://github.com/user-attachments/assets/7e4363a6-ed1e-4466-a851-188524b6cc8f" />

- Truy cập WP-Admin:

<img width="1852" height="1051" alt="image" src="https://github.com/user-attachments/assets/3a00d4eb-6840-4a77-9da5-9d635269a279" />

- Giao diện plugins:

<img width="1852" height="1051" alt="image" src="https://github.com/user-attachments/assets/b538dd5d-19fc-473b-977a-7106f63ea722" />

- Giao diện sau khi cài đặt xong:
- 
<img width="1456" height="782" alt="image" src="https://github.com/user-attachments/assets/5bd256b6-5015-4688-9c56-d0ac9582a7f9" />

  MyThemeShop:
  
<img width="1854" height="1045" alt="image" src="https://github.com/user-attachments/assets/c0bbe989-aa18-4a28-b4a0-41f2dfd519f8" />

  Elementor:
  
<img width="1676" height="927" alt="image" src="https://github.com/user-attachments/assets/c842264b-c36a-42b4-9144-c558bcaf684f" />

  Divi:

<img width="1448" height="645" alt="image" src="https://github.com/user-attachments/assets/ff043e44-16f2-4625-a5e4-64ff42e83417" />

- Giao diện wordpress sử dụng Divi Themes:

<img width="1845" height="1007" alt="image" src="https://github.com/user-attachments/assets/9f988d0f-5dc3-412b-bf06-df6703e21c85" />

<img width="707" height="183" alt="image" src="https://github.com/user-attachments/assets/6aab0d3d-3177-4c5d-8550-a9f0ffe572b7" />

- Bật cache bằng công cụ WP-Optimize:

<img width="1672" height="766" alt="image" src="https://github.com/user-attachments/assets/d7d65458-e161-4628-8ff8-2305184881ec" />
