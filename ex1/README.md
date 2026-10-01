# Bài 1: Khởi tạo Droplet trên DigitalOcean

## Mục tiêu
Khởi tạo thành công một Droplet chạy Ubuntu Server trên hạ tầng đám mây DigitalOcean, cấu hình xác thực an toàn bằng cặp khóa SSH (thay cho mật khẩu thô) và kết nối thành công từ máy cá nhân bằng tài khoản `root`.

## Môi trường thực hiện
- Hệ điều hành máy cá nhân: macOS / Windows / Linux
- Hệ điều hành Droplet: Ubuntu 22.04 LTS
- Nhà cung cấp hạ tầng: DigitalOcean

## Các bước thực hiện

### Bước 1: Tạo cặp khóa SSH trên máy cá nhân
Mở Terminal và chạy:

```bash
ssh-keygen -t ed25519 -C "email_cua_ban@example.com"
```

- Nhấn Enter để lưu khóa ở vị trí mặc định `~/.ssh/id_ed25519`.
- Khóa công khai sẽ nằm ở `~/.ssh/id_ed25519.pub`.

Xem nội dung khóa công khai để copy:

```bash
cat ~/.ssh/id_ed25519.pub
```

### Bước 2: Thêm khóa công khai vào DigitalOcean
- Đăng nhập DigitalOcean, vào **Settings > Security > SSH Keys > Add SSH Key**.
- Dán toàn bộ nội dung file `.pub`, đặt tên cho khóa và lưu lại.

### Bước 3: Khởi tạo Droplet
Vào **Create > Droplets** và chọn cấu hình:

| Mục | Lựa chọn |
|-----|----------|
| Image | Ubuntu 22.04 LTS |
| Plan | Basic |
| CPU options | Regular SSD, CPU Shared ($4 hoặc $6/tháng) |
| Datacenter region | Singapore |
| Authentication | SSH Keys (chọn khóa đã thêm ở Bước 2) |

Nhấn **Create Droplet**, chờ khởi tạo xong và ghi lại **địa chỉ IP** của Droplet.

### Bước 4: Kết nối tới Droplet qua SSH
Trên máy cá nhân, chạy (thay `<IP_ADDRESS_DROPLET>` bằng IP thật):

```bash
ssh -i ~/.ssh/id_ed25519 root@<IP_ADDRESS_DROPLET>
```

Lần đầu kết nối sẽ hỏi xác nhận fingerprint, gõ `yes` để tiếp tục.

## Kết quả
Kết nối thành công vào giao diện dòng lệnh của Droplet mà **không cần nhập mật khẩu**. Terminal hiển thị thông tin chào mừng của Ubuntu Server.

![Màn hình quản lý Droplet trên DigitalOcean Console](./droplet-console.png)
![Log kết nối SSH thành công từ Terminal](./ssh-login.png)

## Kết luận
Đã hoàn thành việc tạo Droplet trên DigitalOcean, cấu hình xác thực an toàn bằng SSH key và kết nối thành công từ máy cá nhân bằng tài khoản `root`.
