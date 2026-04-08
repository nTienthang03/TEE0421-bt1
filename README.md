# TEE0421-bt1
# Thông Tin Sinh Viên

- **Họ và tên:** Nguyễn Tiến Thắng  
- **Mã sinh viên:** K225480106058
- **Lớp:**  : K58.KTP
# A. Đăng ký tên miền cá nhân

## 1. Chọn và đăng ký domain
- Có  sử dụng các nhà cung cấp như **Mắt Bão**,
- Lựa chọn:
  - `*.id.vn`: **miễn phí** cho công dân Việt Nam ≤ 23 tuổi
- Tiến hành đăng ký domain theo thông tin cá nhân : nthangi.id.vn
<img width="1798" height="651" alt="image" src="https://github.com/user-attachments/assets/03d7d490-02a2-4689-90b7-9275f48a5cf5" />

  
## 2. Đăng ký tài khoản Cloudflare
- Truy cập: https://dash.cloudflare.com
- Tạo tài khoản bằng email cá nhân
- Xác nhận email để kích hoạt tài khoản
  <img width="1917" height="418" alt="image" src="https://github.com/user-attachments/assets/58148f9f-d3bd-4f56-8ca4-ec3c733af336" />


## 3. Thêm domain vào Cloudflare
- Sau khi đăng nhập, chọn **Add**

<img width="1502" height="896" alt="image" src="https://github.com/user-attachments/assets/b65fbbc0-0dff-40b1-a3db-6a0ffcf0ef4f" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b8cd5584-2759-4775-9509-39435d5adad4" />

- Nhập tên domain đã đăng ký
- Chọn gói **Free**
- Cloudflare sẽ quét DNS hiện tại

## 4. Lấy Nameserver (NS)
- Sau khi thêm domain, Cloudflare sẽ cung cấp **2 dòng Nameserver**
  - Ví dụ:
  <img width="1502" height="844" alt="image" src="https://github.com/user-attachments/assets/65bc4f67-aa3c-4577-8ad9-66cf77038644" />


## 5. Cấu hình Nameserver tại nhà đăng ký domain
- Đăng nhập vào trang quản lý domain (ví dụ: Mắt Bão)
- Tìm mục **Nameserver**
- Thay thế Nameserver mặc định bằng 2 dòng từ Cloudflare
- <img width="1913" height="888" alt="image" src="https://github.com/user-attachments/assets/2edd4a1e-f36e-42d5-8afd-67d466f5a7f6" />
- Thành công
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ae20d840-8f4b-43ac-a1b2-40134d585a61" />

- Chờ từ vài phút đến vài giờ để DNS cập nhật
## Ghi chú
- Cloudflare giúp:
  - Tăng tốc website (CDN)
  - Bảo mật (chống DDoS)
  - Quản lý DNS dễ dàng

# B. Cài đặt Ubuntu + Docker

## 1. Cài đặt Ubuntu 24.04.4 LTS

### 🔽 Tải Ubuntu

* Truy cập: [https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)
* Tải file: **Ubuntu 24.04.4 LTS (.iso)**
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5a829430-6a19-4729-8981-8a076a8be1a7" />

---

## 2. Tạo máy ảo ( sử dụng VMware)
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/670cdeb0-2a23-4291-bafc-4698ddba0d05" />


## 3. Cài đặt Ubuntu

* Gắn file ISO vào máy ảo
* Start máy ảo
* Chọn: **Install Ubuntu**
* Tạo user (ví dụ: `admin`)
* Đặt password
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/97c3f6bf-a4e7-48fa-81c9-133ee85284e7" />


---

## 4. Cấu hình mạng để SSH

### Trong VirtualBox:

* Vào **Settings → Network**
* Chọn: **Bridged Adapter**
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/191e5722-d5f6-4e7d-a0c1-ad43803c372c" />

---

### Lấy IP Ubuntu:

```bash
ip -4 addr
```

Ví dụ:

```
192.168.100.123
```

---

## 5. SSH từ Windows

Mở CMD và chạy:

```bash
ssh admin@192.168.100.123
```

* Nhập password (không hiển thị)
* Nếu thành công → vào terminal Ubuntu

---

## 6. Các lệnh cơ bản Ubuntu

### Liệt kê file

```bash
ls
```

### Tạo thư mục

```bash
mkdir nameFolder
```

### Chuyển thư mục

```bash
cd path
```

### Copy file

```bash
cp file_nguon file_dich
```

### Phân quyền

```bash
sudo chmod 777 filename
```

### Edit file

```bash
sudo nano tenfile
```

* CTRL + O → lưu
* CTRL + X → thoát

### Xem IP

```bash
ip -4 addr
```

---

## 7. Cài đặt Docker

### Cập nhật hệ thống

```bash
sudo apt update
```

### Cài Docker

```bash
sudo apt install docker.io -y
```

### Kiểm tra version

```bash
docker --version
```

---

## 8. Cài Docker Compose

```bash
sudo apt install docker-compose -y
```

### Kiểm tra:

```bash
docker-compose --version
```

---

## 9. Chạy Docker không cần sudo

```bash
sudo usermod -aG docker $USER
```

👉 Sau đó:

* Logout → Login lại

---

## 10. Lệnh Docker cơ bản

### Test Docker

```bash
docker run hello-world
```

### Xem container

```bash
docker ps
```

### Xem tất cả

```bash
docker ps -a
```

### Xóa container

```bash
docker rm container_id
```

---

## 11. Docker Compose

### Chạy service

```bash
docker-compose up -d
```

### Dừng

```bash
docker-compose down
```

---

## 12. Cấu hình tường lửa

### Cho phép port

```bash
sudo ufw allow 80
sudo ufw allow 1880
sudo ufw allow 9630
```

### Bật firewall

```bash
sudo ufw enable
```

---

## ✅ Kết quả đạt được

* Cài Ubuntu thành công
* SSH từ Windows vào Ubuntu
* Cài Docker & Docker Compose
* Chạy container thành công
* Mở các port cần thiết

---

