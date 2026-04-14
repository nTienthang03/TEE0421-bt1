## 🚀 E. Triển khai (Level Test) ứng dụng

### 📌 1. Khởi chạy hệ thống

Di chuyển vào thư mục project:

```bash
cd ~/myapp
```

Chạy toàn bộ hệ thống:

```bash
docker compose up -d
```

👉 Lệnh này sẽ khởi chạy các service:

* 🌐 Nginx (web + reverse proxy)
* 🔴 Node-RED (backend)
* ⚙️ MyAPI (Flask API)

---

### 🔍 2. Kiểm tra trạng thái container

```bash
docker compose ps
```

👉 Kết quả:

* Các container ở trạng thái `Up` hoặc `healthy`
* Không có container bị `Restart` hoặc `Exited`

---

### 🛠 3. Kiểm tra log (nếu cần)

```bash
docker logs myapp-nginx-1
docker logs myapp-myapi-1
docker logs myapp-nodered-1
```

👉 Dùng để debug khi có lỗi xảy ra

---

### 🌐 4. Kiểm tra các service trên localhost

* 🌍 Web: http://localhost
* 🔴 Node-RED: http://localhost:1880
* ⚙️ MyAPI: http://localhost:9630

👉 Các service đều truy cập được bình thường

---

### 🔗 5. Kiểm tra API qua Nginx

```bash
curl localhost/api/funny
```

👉 Kết quả trả về:

* Một câu joke ngẫu nhiên 😆
* Chứng tỏ Nginx đã proxy thành công tới backend

---

### 🌍 6. Kiểm tra truy cập qua IP

Lấy địa chỉ IP của máy Ubuntu:

```bash
ip a
```

Ví dụ:

```
192.168.102.87
```

Truy cập từ trình duyệt:

* 🌐 Web: http://192.168.102.87

  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7dac5dd1-bc6f-4831-9cce-3b484e1ba659" />

 🔴 Node-RED: http://192.168.102.87:1880
 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cf0512ca-c05e-4349-b69b-46073bc277c4" />

 ⚙️ MyAPI: http://192.168.102.87:9630

 <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5368a789-d5fd-4cfa-8c08-a9efe7c2ce50" />

 🔗 API: http://192.168.102.87/api/funny
 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/362d80a3-07a3-46cc-a09b-30bcdc0a2371" />

👉 Tất cả đều truy cập thành công

## 🛠 F. Gỡ lỗi (Debug & Monitoring)

### 📌 1. Kiểm tra nhanh trạng thái container

Sử dụng lệnh:

```bash id="7h3k2q"
docker compose ps
```

👉 Mục đích:

* Xem container nào đang chạy (`Up`)
* Phát hiện container lỗi (`Restarting`, `Exited`)

---

### 📌 2. Xem log để tìm lỗi

Khi container bị lỗi, sử dụng:

```bash id="2k9x1p"
docker logs myapp-nginx-1
docker logs myapp-myapi-1
docker logs myapp-nodered-1
```

👉 Giúp:

* Xác định lỗi cấu hình (nginx.conf)
* Lỗi code (Flask, Node-RED)
* Lỗi port hoặc dependency

---

### 📌 3. Thêm healthcheck cho service

Trong file `docker-compose.yml`:

```yaml id="kq7z2l"
myapi:
  build: ./myapi
  ports:
    - "9630:9630"
  healthcheck:
    test: ["CMD", "curl", "-f", "http://localhost:9630"]
    interval: 10s
    timeout: 5s
    retries: 3
```

👉 Ý nghĩa:

* Docker kiểm tra service có hoạt động không
* Trạng thái sẽ hiển thị:

  * `healthy` ✅
  * `unhealthy` ❌

---

### 📌 4. Giới hạn tài nguyên (RAM)

Trong `docker-compose.yml`:

```yaml id="h0t7bx"
myapi:
  deploy:
    resources:
      limits:
        memory: 512M
```

👉 Mục đích:

* Tránh service chiếm quá nhiều RAM
* Giữ hệ thống ổn định

---

### 📌 5. Theo dõi tài nguyên container

```bash id="u1g8fh"
docker stats
```

👉 Hiển thị:

* RAM usage
* CPU usage
* Network

---

### 📌 6. Các lỗi thường gặp

| Lỗi                    | Nguyên nhân       | Cách xử lý                      |
| ---------------------- | ----------------- | ------------------------------- |
| Restarting             | Sai config nginx  | Kiểm tra nginx.conf             |
| Port already allocated | Trùng port        | Đổi port hoặc stop container cũ |
| 404 API                | Sai proxy_pass    | Thêm `/` cuối URL               |
| Cannot connect         | Service chưa chạy | Kiểm tra docker compose ps      |
