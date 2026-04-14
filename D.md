## 🧩 D. Bonus - Xây dựng MyAPI (Flask)

### 📌 Mục tiêu

Xây dựng một service API đơn giản sử dụng **Python + Flask**, tích hợp vào hệ thống Docker Compose và được truy cập thông qua Nginx (`/api`).

---

### 📁 Cấu trúc thư mục

```
myapi/
├── app.py
├── requirements.txt
└── Dockerfile
```

---

### 🐍 1. Tạo ứng dụng Flask

File: `myapi/app.py`

```python
from flask import Flask
import random

app = Flask(__name__)

@app.route('/')
def home():
    return "🚀 MyAPI is running"

@app.route('/funny')
def funny():
    jokes = [
        "DevOps không ngủ, chỉ deploy thôi 😆",
        "Code chạy là do may mắn 😅",
        "Fix bug = thêm print() 🐛"
    ]
    return random.choice(jokes)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=9630)
```

---

### 📦 2. Khai báo thư viện

File: `myapi/requirements.txt`

```
flask
```

---

### 🐳 3. Dockerfile

File: `myapi/Dockerfile`

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 9630

CMD ["python", "app.py"]
```

---

### ⚙️ 4. Tích hợp vào docker-compose

Thêm service `myapi` vào `docker-compose.yml`:

```yaml
myapi:
  build: ./myapi
  ports:
    - "9630:9630"
  healthcheck:
    test: ["CMD", "curl", "-f", "http://localhost:9630"]
```

---

### 🌐 5. Cấu hình Nginx

File: `nginx/nginx.conf`

```nginx
location /api/ {
    proxy_pass http://myapi:9630;
}
```

👉 Giúp chuyển hướng request từ `/api` → service MyAPI

---

### 🚀 6. Chạy hệ thống

```bash
docker compose up -d --build
```

---

### 🔍 7. Kiểm thử

#### Truy cập trực tiếp API:

```
http://localhost:9630
http://localhost:9630/funny
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2d72bd79-6709-42e2-a8a9-ca81d0c20345" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d8993747-3da4-4eae-a1c2-69af5617242f" />


#### Truy cập qua Nginx (chuẩn hệ thống):

```
http://localhost/api
http://localhost/api/funny
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3e44432f-15fc-4243-8703-5478e0357e8b" />

* `localhost:9630` → truy cập trực tiếp service
* `localhost/api` → truy cập qua Nginx (production-ready)
