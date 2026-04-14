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
