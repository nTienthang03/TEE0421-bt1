## 🌍 G. Triển khai ứng dụng đến End-user (Cloudflare Tunnel)

### 📌 1. Mục tiêu

Triển khai ứng dụng từ môi trường local lên Internet để người dùng có thể truy cập thông qua domain mà không cần mở port trực tiếp.

---

### ☁️ 2. Tạo Cloudflare Tunnel

1. Đăng nhập Cloudflare: https://dash.cloudflare.com
2. Truy cập **Zero Trust Dashboard**
3. Vào: **Networks → Tunnels**
4. Chọn **Add a Tunnel**
5. Đặt tên: `myapp`
6. Chọn loại triển khai: **Docker**
<img width="1502" height="720" alt="image" src="https://github.com/user-attachments/assets/43468b62-59c0-4287-8e29-7008e4cb2516" />

👉 Cloudflare cung cấp lệnh:

```bash
docker run cloudflare/cloudflared:latest tunnel --no-autoupdate run --token <TOKEN>
```

---

### 🔄 3. Cấu hình trong docker-compose

Thêm service `cloudflared` vào file `docker-compose.yml`:

```yaml
cloudflared:
  image: cloudflare/cloudflared:latest
  command: tunnel --no-autoupdate run --token <TOKEN>
  restart: always
  depends_on:
    - nginx
```

---

### 🚀 4. Khởi chạy hệ thống

```bash
cd ~/myapp
docker compose down
docker compose up -d
```

👉 Tất cả service sẽ được khởi chạy:

* nginx
* myapi
* nodered
* cloudflared

---
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/aa383117-0f9b-43f0-a87c-1061b0dcce14" />


### 🌐 5. Cấu hình Public Hostname

Trong Cloudflare Tunnel:

Thêm route:

| Field     | Giá trị         |
| --------- | --------------- |
| Subdomain | app             |
| Domain    | nthangi.id.vn   |
| Service   | http://nginx:80 |
<img width="1502" height="720" alt="image" src="https://github.com/user-attachments/assets/889eab05-6a6c-4e30-97ee-0cda48c5ddf8" />


👉 Ý nghĩa:

* Người dùng truy cập domain
* Cloudflare chuyển request qua tunnel
* Tunnel chuyển tới Nginx
* Nginx proxy tới backend

---

### 🔗 6. Kiểm tra truy cập

Sau khi cấu hình thành công:

* 🌐 Web: https://app.nthangi.id.vn
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/807b269d-9ec3-49d3-a1eb-78ef08c55e3b" />

* 🔗 API: https://app.nthangi.id.vn/api/funny
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8ef52730-b208-40b1-93a2-5d7fbd813d3c" />


👉 Kết quả:

* Trang web hiển thị giao diện
* API trả dữ liệu chính xác

---

### 📁 7. Cấu trúc thư mục

```bash
myapp/
├── docker-compose.yml
├── nginx/
│   └── nginx.conf
├── myweb/
│   └── index.html
├── myapi/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── nodered/
    └── settings.js
```

---

### 🎯 Kết quả đạt được

* ✅ Ứng dụng chạy bằng Docker Compose
* ✅ Reverse proxy bằng Nginx
* ✅ Backend hoạt động (Flask + Node-RED)
* ✅ Public ra Internet bằng Cloudflare Tunnel
* ✅ Truy cập bằng domain thật
