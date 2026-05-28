# Window Server
## Remmina

Cài đặt Remmina

<img width="732" height="223" alt="image" src="https://github.com/user-attachments/assets/b7750211-bc96-497b-8fd5-8afa017b0bf0" />

```
sudo apt-add-repository ppa:remmina-ppa-team/remmina-next
sudo apt update
sudo apt install remmina remmina-plugin-rdp remmina-plugin-secret
```

Giao diện Remmina:

<img width="596" height="440" alt="image" src="https://github.com/user-attachments/assets/22e50ea7-6f63-4b9b-9681-e2e0e71e1af6" />

Thiết lập kết nối:

<img width="621" height="464" alt="image" src="https://github.com/user-attachments/assets/e90605d7-354a-49c0-8905-d3525bca7ce7" />


Giao diện sau khi kết nối

<img width="1847" height="1031" alt="image" src="https://github.com/user-attachments/assets/899ac198-940f-491c-83f8-91451b658f56" />

---

## Port Firewall:

Nhấn `Window` -> tìm `wf.msc` -> `enter`

<img width="348" height="646" alt="image" src="https://github.com/user-attachments/assets/cf38de45-716f-4b73-8992-ad218497fa3d" />

Giao diện

<img width="1027" height="774" alt="image" src="https://github.com/user-attachments/assets/b1f3b057-96ea-42ce-9c3d-5eb46c7af9fd" />

---

### Allow port:

Chọn `New rules` bên phải -> `Port` nhập port bất kỳ -> `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/53d58a0d-f998-4be9-a13f-b751ba9fe149" />

`Allow the connection` -> `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/c24666c5-4c58-47be-bdce-7ef68135d97f" />

Chọn cả 3 `Domain`, `Private`, `Public` -> `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/d400dace-60e1-4de8-91d4-5d98a276c692" />

Đặt tên bất kỳ -> `Finish`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/4de80b13-d559-48d2-8a0c-8e3c54d7c7a1" />

Kiểm tra:

kiểm tra port 3389 vì RDP đang sử dụng port 3389 nên sẽ hiện service chạy

<img width="692" height="173" alt="image" src="https://github.com/user-attachments/assets/0e17d869-21f2-4016-9290-a7869b3b60b3" />

```
nmap -p 3389 14.225.204.109
```

---

### Block port:

Chọn `New rules` bên phải -> `Port` nhập port bất kỳ -> `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/da04e56c-e5d5-4c81-8e4e-2a2f4942d7d7" />

`Block the connection` -> `Next`

<img width="708" height="478" alt="image" src="https://github.com/user-attachments/assets/ab627588-1402-4e1e-869b-e7253dee5903" />

Chọn cả 3 `Domain`, `Private`, `Public` -> `Next`

<img width="705" height="569" alt="image" src="https://github.com/user-attachments/assets/d400dace-60e1-4de8-91d4-5d98a276c692" />

Đặt tên bất kỳ -> `Finish`

<img width="712" height="548" alt="image" src="https://github.com/user-attachments/assets/6f1cdfd1-c67a-4c4a-ba20-271a1b3c0b57" />

kiểm tra port 8083 đã block

<img width="692" height="162" alt="image" src="https://github.com/user-attachments/assets/adc853c7-cb2d-4d8f-86d8-1da3e1f83e93" />

```
nmap -p 8083 14.225.204.109
```

---

## IP

### Allow IP:

Chọn `New rules` bên phải -> `Custom` -> `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/da53eafd-bc87-4dfc-b910-d84c0baed01e" />

`All program` -> `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/68f5165b-3e58-4948-ac6e-f7b174f8f79b" />

`Protocol and Ports` -> `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/065ad4d1-820e-4f7f-8fca-cc6fb4aa51be" />

- `Scope` -> có 2 phần `Which local IP addresses does this rule apply to` và `Which remote IP addresses does this rule apply to`

- Giữ nguyên `Which local IP addresses does this rule apply to` và thêm IP ở phần `Which remote IP addresses does this rule apply to`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/3a3f67ab-1498-4e43-a43f-f1396fbafafe" />

`Add` -> nhập IP muốn thêm -> `Ok` -> `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/143bc4b9-cf4f-4a67-847e-6c883d505ce7" />

`Allow the connections` -> `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/8970b12e-6eb8-4ba3-a554-69bb7148dbf9" />

Chọn cả 3 `Domain`, `Private`, `Public` -> `Next`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/4adfafd6-c17c-419b-aa9a-10596d021dcb" />

Đặt tên bất kỳ -> `Finish`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/a4b3c261-d116-48ce-8493-79b26ff5ed3e" />

---

### Block IP

Tương tự với Allow IP nhưng đến bước `Action` -> Chọn `Block the connections`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/812d5d2a-f4a4-4e2b-9515-d1853c9f42b2" />

Đặt tên bất kỳ -> `Finish`

<img width="698" height="557" alt="image" src="https://github.com/user-attachments/assets/85e9be3b-974f-40cc-bf3f-2d25058d5e84" />

---
## Giới hạn IP/Port

### IP



---

## SQL

Giải nén file ISO

<img width="620" height="301" alt="image" src="https://github.com/user-attachments/assets/01c0816e-8b05-43bf-91bf-6a7ecc39454c" />

Upload file ISO

<img width="724" height="92" alt="image" src="https://github.com/user-attachments/assets/bd8c58d0-139e-45df-882d-181c34ef9464" />
