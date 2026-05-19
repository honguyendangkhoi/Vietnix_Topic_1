# PING
<img width="696" height="173" alt="image" src="https://github.com/user-attachments/assets/a5693056-4ef1-4f84-bb33-b273713bf5cc" />

- Giải thích:
ping: sử dụng giao thức ICMP để gửi gói tin, chủ yếu để kiểm tra độ trễ và khả năng kết nối mạng cơ bản nhanh chóng
-trong đó:
ttl: là số bước nhảy (hop) qua các router
time: là thời gian trễ (latency) từ lúc máy tính gửi gói tin đến lúc gói tin được phản hồi về

# Hping3
<img width="734" height="171" alt="image" src="https://github.com/user-attachments/assets/322ef77d-af23-4529-9731-3afacaa3af63" />

- Giải thích:
hping3: là một công cụ phân tích và lắp ráp gói tin mạng TCP/IP thông qua command line

hping3 được gửi theo cú pháp:
hping 3 + loại gói tin + target + port + cách gửi
ví dụ:
hping 3 -1 google.com -p 80 -c 3
trong đó:
-1: là loại gói tin được gửi, ở đây là ICMP 
-target: là ip hoặc domain, ở đây là google.com
-p: là port, ở đây là 80
-c: là cách gửi, ở đây là gửi 3 gói tin

# CAT
<img width="676" height="119" alt="image" src="https://github.com/user-attachments/assets/3254291f-b512-4270-9541-032a02789a0f" />
xem nội dung 1 file

<img width="731" height="67" alt="image" src="https://github.com/user-attachments/assets/1566459a-60a7-4aaf-bd95-8c9f2621206f" />
xem dòng thứ '<n>' trong file

<img width="731" height="155" alt="image" src="https://github.com/user-attachments/assets/2356f8d1-f22d-41bd-87e0-33c9113fc546" />
ghi nhiều dòng vào 1 file sử bằng EOF

# ECHO
<img width="728" height="169" alt="image" src="https://github.com/user-attachments/assets/41a643c2-69a3-4184-9922-3886d1f52283" />
chèn thêm 1 dòng vào cuối file

<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/48b0ce6f-41cc-44aa-90be-99ecfc48ee28" />
overwrite nội dung

# HEAD
<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/2e895f02-fd7c-451d-8e4b-2cd2b792822b" />
in ra 3 dòng đầu của file

# TAIL
<img width="728" height="83" alt="image" src="https://github.com/user-attachments/assets/18fdf963-e01e-464c-8734-b2ddae9a2ef7" />
in ra 3 dòng cuối của file

=> Head là lệnh xem đầu file, tail là lệnh xem cuối file

# TAILF
<img width="1039" height="213" alt="image" src="https://github.com/user-attachments/assets/653fb7d0-9e70-4744-abe1-de6779757ccf" />

## SỰ KHÁC NHAU CỦA TAILF VÀ TAIL:
TAILF: theo dõi file liên tục có thêm dòng mới không
TAIL: xem cuối file
