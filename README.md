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
  

## 6. Kiểm tra và hoàn tất
- Chờ từ vài phút đến vài giờ để DNS cập nhật
- Quay lại Cloudflare → nếu trạng thái là **Active** là thành công

---

## Ghi chú
- Cloudflare giúp:
  - Tăng tốc website (CDN)
  - Bảo mật (chống DDoS)
  - Quản lý DNS dễ dàng
