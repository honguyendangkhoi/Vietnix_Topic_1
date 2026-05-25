aaPanel

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


Truy cập website Vietnix.vn:

<img width="1832" height="876" alt="image" src="https://github.com/user-attachments/assets/879fa97f-f396-4672-90b6-4cacc5e66898" />


Tải toàn bộ file:
- File sau khi tải:

<img width="694" height="223" alt="image" src="https://github.com/user-attachments/assets/7e4363a6-ed1e-4466-a851-188524b6cc8f" />

