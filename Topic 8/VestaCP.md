# VestaCP
tải VestaCP:

<img width="725" height="218" alt="image" src="https://github.com/user-attachments/assets/9bf970a9-ec02-4890-a93f-9e7fd948268d" />

- Cài đặt VestaCP:

<img width="727" height="340" alt="image" src="https://github.com/user-attachments/assets/2a99b456-4af5-44b1-a8a4-4639c8760564" />

- Thiết lập:

<img width="650" height="113" alt="image" src="https://github.com/user-attachments/assets/a93c1117-5e29-4b78-9e6b-87e110e3501b" />

```
Would you like to continue [y/n]: y

Please enter admin email address: dngkhoyy@gmail.com

Please enter Vesta port number (press enter for 8083):

Please enter FQDN hostname [training-dangkhoi.vietnix.vn]:

Installation backup directory: /root/vst_install_backups/1779860859
```

- Kết quả sau khi tải xong:

<img width="674" height="629" alt="image" src="https://github.com/user-attachments/assets/34023176-d548-41f5-a08b-d7798649f460" />

- Mở port:

<img width="957" height="290" alt="image" src="https://github.com/user-attachments/assets/a8e86756-e1e7-4249-bf4a-a00ae26872b5" />

- Giao diện truy cập web:

<img width="1831" height="1009" alt="image" src="https://github.com/user-attachments/assets/ec0f328c-7ea4-49b5-b048-28b782f3496b" />

<img width="1831" height="1009" alt="image" src="https://github.com/user-attachments/assets/57392a08-0dfe-4ee7-b827-35050cffd61f" />

- Add 2 domains:
username `admin`

<img width="813" height="73" alt="image" src="https://github.com/user-attachments/assets/bb957c7b-24fa-4a73-97bc-198201393688" />

```
v-add-domain admin laravel.dangkhoi.vietnix.tech
v-add-domain admin wp.dangkhoi.vietnix.tech
```

- kiểm tra:

<img width="811" height="109" alt="image" src="https://github.com/user-attachments/assets/aa7f6372-ef83-4a72-aeec-7ae06f366ba9" />

```
v-list-web-domains admin
```

- Gắn gói PHP 8.1

<img width="983" height="46" alt="image" src="https://github.com/user-attachments/assets/93389d06-e0fe-42f7-8beb-d60a6d3824a7" />

```
v-change-web-domain-tpl admin laravel.dangkhoi.vietnix.tech PHP-8_1
v-change-web-domain-tpl admin wp.dangkhoi.vietnix.tech PHP-8_1
```

- Kiểm tra:

<img width="988" height="118" alt="image" src="https://github.com/user-attachments/assets/9fb98089-d0ce-4e6d-8565-2ff5414b2bdc" />

```
v-list-web-domains admin
```

- Tạo database:

<img width="1167" height="41" alt="image" src="https://github.com/user-attachments/assets/79e7e259-899b-4620-b564-b45139e9e1f9" />

```
v-add-database admin laraveldb lrvluser "BXu36OcU4OhpPh3qgvJK"
v-add-database admin wpdb wpuser "BXu36OcU4OhpPh3qgvJK"
```

- Kiểm tra:

<img width="1167" height="109" alt="image" src="https://github.com/user-attachments/assets/5695828e-7c03-4592-81ca-2d4593dffb8d" />

```
v-list-databases admin
```

