# Thông Tin Sinh Viên

- **Họ và tên:** Nguyễn Tiến Thắng  
- **Mã sinh viên:** K225480106058
- **Lớp:**  : K58.KTP
# Đề bài 
Bài tập 01:
https://github.com/duycop/Developing-applications-with-open-source



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
