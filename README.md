<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3983bab7-acce-4bda-9752-69591bbd189b" /># TEE0421-bt1
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
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2e9e0e79-6815-42b4-82af-c2eb03629a49" />

Ví dụ:

```
192.168.102.87
```

---

## 5. SSH từ Windows

Mở CMD và chạy:

```bash
ssh nguyentienthang@192.168.102.87
```

* Nhập password (không hiển thị)
* Nếu thành công → vào terminal Ubuntu
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/85c14ee4-9d00-4205-b96f-79ea73937b7a" />

---

## 6. Các lệnh cơ bản Ubuntu

### Liệt kê file

```bash
ls
```
<img width="1055" height="209" alt="image" src="https://github.com/user-attachments/assets/54e38f55-255b-4f42-9f2f-ffedf29cba68" />


### Tạo thư mục

```bash
mkdir ThangFolder
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1dad2a55-f109-41df-869e-8ac6dc36b30c" />

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
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f89b3af1-32c7-4478-8e5b-b07bc09ab89d" />

## 8. Cài Docker Compose

```bash
sudo apt install docker-compose -y
```

### Kiểm tra:

```bash
docker-compose --version
```

---
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ff6b9039-e86a-425d-8f90-1ac79a3d1865" />

## 9. Chạy Docker không cần sudo

```bash
sudo usermod -aG docker $USER
```

👉 Sau đó:

* Logout → Login lại

---

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fbb6b1d6-a35d-418f-9074-2d5e128ecc14" />

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
sudo ufw enable
```

### Bật firewall

```bash
sudo ufw enable
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/66fbcf23-abb5-4720-991a-7629a9b2e5b1" />

# C  Docker Compose Project - MyApp

## 📌 Giới thiệu

Dự án này sử dụng **Docker Compose** để triển khai 2 dịch vụ chính:

* 🌐 **Nginx**: Web server (port 80)
* 🔴 **Node-RED**: Xử lý backend (port 1880)

---

## 📁 Cấu trúc thư mục

```
myapp/
│── docker-compose.yml
│
├── myweb/
│   └── index.html
│
├── nginx/
│   └── nginx.conf
│
└── nodered/
    └── settings.js
```

---

## ⚙️ Bước 1: Tạo thư mục

```bash
mkdir -p ~/myapp
cd ~/myapp
mkdir myweb nginx nodered
```

---

## 🌐 Bước 2: Tạo web tĩnh

Tạo file `myweb/index.html`

```
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <title>My DevOps App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            text-align: center;
            color: white;
            margin-top: 100px;
        }
        .card {
            background: rgba(0,0,0,0.5);
            padding: 30px;
            border-radius: 15px;
            display: inline-block;
        }
        h1 {
            margin-bottom: 20px;
        }
        a {
            display: inline-block;
            margin-top: 15px;
            padding: 10px 20px;
            background: #ff9800;
            color: white;
            text-decoration: none;
            border-radius: 8px;
        }
        a:hover {
            background: #e68900;
        }
    </style>
</head>
<body>

    <div class="card">
        <h1>🚀 My DevOps Project</h1>
        <p><b>Họ tên:</b> Nguyễn Tiến Thắng</p>
        <p><b>Ngày sinh:</b> 09/02/2003</p>
        <p><b>Ngành:</b> DevOps</p>

        <a href="http://localhost:1880">🔴 Mở Node-RED</a>
    </div>

</body>
</html>
```

---

## 🐳 Bước 3: docker-compose.yml

```yaml
version: '3.8'

services:
  nodered:
    image: nodered/node-red
    ports:
      - "1880:1880"
    volumes:
      - ./nodered:/data

  nginx:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./myweb:/myweb
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - nodered
```

---
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a7ad05ef-d6bb-4329-b896-93c29f836761" />

## ⚡ Bước 4: Cấu hình Nginx

Tạo file `nginx/nginx.conf`

```nginx
events {}

http {
    server {
        listen 80;
        server_name myapp.local;

        location / {
            root /myweb;
            index index.html;
        }

        location /api/ {
            proxy_pass http://nodered:1880/;
        }
    }
}
```

---

## 🔐 Bước 5: Bật đăng nhập Node-RED

Chạy lần đầu để tạo file cấu hình:

```bash
docker-compose up -d
```

Sau đó sửa file `nodered/settings.js`

Tìm phần `adminAuth` và sửa:

```js
adminAuth: {
    type: "credentials",
    users: [{
        username: "admin",
        password: "$2b$08$xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        permissions: "*"
    }]
},
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/253955f9-561a-4562-a4a0-99ae7239c41a" />


## ▶️ Bước 6: Chạy hệ thống

```bash
docker-compose up -d
```

---

## 🌍 Truy cập

* Web: [http://localhost](http://localhost)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a8509e06-140d-4f82-a9e5-dbc767c56ed3" />

* Node-RED: [http://localhost:1880](http://localhost:1880)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f68e3bac-57df-4e6f-bf2a-632cf209d5f8" />








