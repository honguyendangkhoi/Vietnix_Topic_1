# Setting VPS
- BƯỚC 1: 
ssh vào VPS:
<img width="726" height="324" alt="image" src="https://github.com/user-attachments/assets/99973e83-4d2a-4fc0-803e-356e4257bd9c" />

- Bước 2: 
Cập nhật các gói package cần thiết:
<img width="726" height="246" alt="image" src="https://github.com/user-attachments/assets/dd4ab619-9d9a-46d4-aa57-8da77dc30045" />
``` bash
apt update -y
```

<img width="726" height="192" alt="image" src="https://github.com/user-attachments/assets/37ab6e8f-7df9-4d54-ada4-b5984fa61c08" />
```bash
apt install nginx -y
```

khởi chạy package nginx:
<img width="726" height="100" alt="image" src="https://github.com/user-attachments/assets/ce4e0d80-7789-4e9b-a99a-719c5dc7aa7b" />
```bash
systemctl enable nginx -y
systemctl start nginx```
