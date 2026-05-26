# Cyber Panel
- cập nhật lại VPS sau khi đã reset

<img width="580" height="164" alt="image" src="https://github.com/user-attachments/assets/2e2921a7-716d-44aa-9b17-616233424a3e" />

```bash
apt update && apt upgrade -y
apt install -y curl wget unzip git ufw
```

- Cài đặt Cyber Panel:

<img width="733" height="47" alt="image" src="https://github.com/user-attachments/assets/23220d67-e4ca-495c-b770-cbb845e017e0" />

```bash
sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)
```

<img width="453" height="163" alt="image" src="https://github.com/user-attachments/assets/87623f26-2161-493b-8eca-040956a24268" />
<img width="1032" height="943" alt="image" src="https://github.com/user-attachments/assets/9dad3f96-5783-4e58-9d44-76a5e9e210eb" />

```bash
Install CyberPanel? -> 1
Install CyberPanel with OpenLiteSpeed -> 1
Full service -> Y
Remote MySQL -> N
Password -> default (1234567) * sẽ đổi lại sau
Memcached -> Y
Redis -> Y
WatchDog -> no
``

- reset lại vps sau khi cài đặt xong:

<img width="1032" height="943" alt="image" src="https://github.com/user-attachments/assets/1e619c74-2a55-486c-96df-771ec9b1ea02" />

