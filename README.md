# MTProxy - Trình Cài Đặt Tự Động

Script cài đặt và quản lý MTProto Proxy với giao diện tiếng Việt, hỗ trợ Ubuntu/Debian và CentOS. Được phát triển để đơn giản hóa việc triển khai MTProxy server.

## Tính Năng

- ✅ **Cài đặt tự động**: Một lệnh duy nhất để cài đặt hoàn chỉnh
- ✅ **Menu tương tác**: Giao diện tiếng Việt dễ sử dụng
- ✅ **Hỗ trợ đa hệ điều hành**: Ubuntu, Debian, CentOS
- ✅ **Port ngẫu nhiên**: Tự động chọn port không bị xung đột
- ✅ **Fake-TLS**: Ngụy trang traffic như HTTPS
- ✅ **Hỗ trợ NAT**: Tương thích với AWS và các cloud provider
- ✅ **BBR**: Tối ưu hóa tốc độ kết nối
- ✅ **Quản lý secret**: Thêm/xóa secret dễ dàng
- ✅ **Tường lửa tự động**: Cấu hình firewall tự động
- ✅ **Systemd service**: Chạy nền và tự khởi động
- ✅ **Cập nhật tự động**: Cập nhật cấu hình hàng ngày

## Yêu Cầu Hệ Thống

- **Hệ điều hành**: Ubuntu 18.04+, Debian 10+, CentOS 7+
- **Quyền**: Root hoặc sudo
- **RAM**: Tối thiểu 512MB
- **CPU**: 1 core (khuyến nghị 2+ cores)
- **Băng thông**: Không giới hạn

## Cài Đặt Nhanh

### Cài đặt tương tác (Khuyến nghị)

```bash
curl -o install_mtproxy.sh -L https://raw.githubusercontent.com/n4t1412dev/MTProxy-GetPageSpeed/refs/heads/master/install_mtproxy.sh
sudo bash install_mtproxy.sh
```

### Chọn ngôn ngữ

Script hỗ trợ cả tiếng Việt và tiếng Anh:

```bash
# Tiếng Việt (mặc định)
sudo bash install_mtproxy.sh --lang=vi

# Tiếng Anh
sudo bash install_mtproxy.sh --lang=en
```

### Cài đặt tự động (Keyless)

```bash
sudo bash install_mtproxy.sh -s <secret> -p <port> -t <tag>
```

**Ví dụ:**

```bash
sudo bash install_mtproxy.sh -s 00000000000000000000000000000000 -p 443 -t dcbe8f1493fa4cd9ab300891c0b5b326
```

## Tham Số Dòng Lệnh

| Tham số             | Mô tả                             | Ví dụ                                 |
| ------------------- | --------------------------------- | ------------------------------------- |
| `-s, --secret`      | Secret 32 ký tự hex               | `-s 00000000000000000000000000000000` |
| `-p, --port`        | Port proxy (mặc định: ngẫu nhiên) | `-p 443`                              |
| `-t, --tag`         | TAG quảng cáo từ @MTProxybot      | `-t dcbe8f1493fa4cd9ab300891c0b5b326` |
| `--workers`         | Số worker (mặc định: số CPU)      | `--workers 4`                         |
| `--disable-updater` | Tắt cập nhật tự động              | `--disable-updater`                   |
| `--tls`             | Domain fake-TLS                   | `--tls www.google.com`                |
| `--custom-args`     | Tham số tùy chỉnh                 | `--custom-args "-v"`                  |
| `--no-nat`          | Tắt kiểm tra NAT                  | `--no-nat`                            |
| `--no-bbr`          | Tắt BBR                           | `--no-bbr`                            |
| `--lang=vi`         | Ngôn ngữ tiếng Việt               | `--lang=vi`                           |
| `--lang=en`         | Ngôn ngữ tiếng Anh                | `--lang=en`                           |

## Quản Lý Proxy

Sau khi cài đặt, chạy lại script để quản lý:

```bash
sudo bash install_mtproxy.sh
```

### Menu quản lý:

1. **Hiển thị liên kết kết nối** - Xem link proxy
2. **Thay đổi TAG** - Cập nhật TAG quảng cáo
3. **Thêm secret** - Thêm secret mới (tối đa 16)
4. **Xóa secret** - Xóa secret không cần thiết
5. **Thay đổi số lượng Worker** - Tối ưu hiệu suất
6. **Thay đổi cài đặt NAT** - Cấu hình cho cloud
7. **Thay đổi tham số tùy chỉnh** - Tùy chỉnh nâng cao
8. **Tạo quy tắc tường lửa** - Cấu hình firewall
9. **Gỡ cài đặt Proxy** - Xóa hoàn toàn
10. **Thông tin** - Hiển thị thông tin script

## Quản Lý Service

```bash
# Khởi động proxy
sudo systemctl start MTProxy

# Dừng proxy
sudo systemctl stop MTProxy

# Khởi động lại proxy
sudo systemctl restart MTProxy

# Xem trạng thái
sudo systemctl status MTProxy

# Xem log
sudo journalctl -u MTProxy -f

# Bật tự khởi động
sudo systemctl enable MTProxy
```

## Cấu Hình Tường Lửa

### Ubuntu (UFW)

```bash
sudo ufw allow <port>/tcp
```

### CentOS (Firewalld)

```bash
sudo firewall-cmd --zone=public --add-port=<port>/tcp --permanent
sudo firewall-cmd --reload
```

### Debian (iptables)

```bash
sudo iptables -A INPUT -p tcp --dport <port> -j ACCEPT
sudo iptables-save > /etc/iptables/rules.v4
```

## Lấy TAG Quảng Cáo

1. Mở Telegram và tìm [@MTProxybot](https://t.me/MTProxybot)
2. Gửi `/newproxy`
3. Nhập IP server và port
4. Nhập một trong các secret của bạn
5. Bot sẽ trả về TAG để sử dụng

## Fake-TLS

Để sử dụng Fake-TLS (ngụy trang traffic):

1. Cài đặt với domain TLS: `--tls www.cloudflare.com`
2. Link sẽ bắt đầu bằng `ee` thay vì `dd`
3. Traffic sẽ trông giống HTTPS thông thường

## Random Padding

Để tránh phát hiện bởi DPI:

1. Thêm prefix `dd` vào secret: `ddcafe...babe`
2. Hoặc sử dụng Fake-TLS với prefix `ee`

## Cấu Hình NAT (AWS/Cloud)

Nếu server nằm sau NAT:

1. Script sẽ tự động phát hiện IP private
2. Nhập IP public khi được hỏi
3. Hoặc sử dụng `--no-nat` để tắt

## Tối Ưu Hiệu Suất

### BBR (Khuyến nghị)

```bash
# Kiểm tra BBR
sysctl net.ipv4.tcp_congestion_control

# Kích hoạt BBR (script tự động làm)
echo 'net.core.default_qdisc=fq' >> /etc/sysctl.conf
echo 'net.ipv4.tcp_congestion_control=bbr' >> /etc/sysctl.conf
sysctl -p

# Nếu bạn dùng Ubuntu/KVM (không container) 20.4
sudo apt update
sudo apt install --install-recommends linux-generic-hwe-20.04
# Sau đó
sudo reboot

# Rồi kiểm tra lại bằng
uname -r
sysctl net.ipv4.tcp_available_congestion_control
lsmod | grep bbr

```

### Workers

- 1 worker cho mỗi CPU core
- Tối đa 16 workers
- Mỗi worker xử lý ~10,000-16,000 kết nối

## Thống Kê

Xem thống kê proxy:

```bash
curl http://localhost:8888/stats
```

## Cập Nhật

Script tự động cập nhật cấu hình hàng ngày lúc 00:00. Để cập nhật thủ công:

```bash
cd /opt/MTProxy
sudo bash updater.sh
```

## Gỡ Lỗi

### Kiểm tra service

```bash
sudo systemctl status MTProxy -l
sudo journalctl -u MTProxy --no-pager
```

### Kiểm tra port

```bash
sudo netstat -tlnp | grep <port>
sudo ss -tlnp | grep <port>
```

### Kiểm tra firewall

```bash
# Ubuntu
sudo ufw status

# CentOS
sudo firewall-cmd --list-all

# Debian
sudo iptables -L
```

## Khắc Phục Sự Cố

### Lỗi biên dịch

```bash
# Cài đặt dependencies
sudo apt update && sudo apt install build-essential libssl-dev zlib1g-dev
# Hoặc CentOS
sudo yum groupinstall "Development Tools" && sudo yum install openssl-devel zlib-devel
```

### Service không khởi động

```bash
# Kiểm tra cấu hình
sudo systemctl status MTProxy -l
# Kiểm tra port conflict
sudo lsof -i :<port>
```

### Không kết nối được

1. Kiểm tra firewall
2. Kiểm tra port forwarding (nếu có NAT)
3. Kiểm tra secret và link
4. Thử port khác

## Bảo Mật

- Chỉ mở port cần thiết
- Sử dụng secret mạnh (32 ký tự hex)
- Cập nhật hệ điều hành thường xuyên
- Theo dõi log thường xuyên
- Sử dụng Fake-TLS để tránh phát hiện

## Nguồn Gốc

- **MTProxy**: [GetPageSpeed/MTProxy](https://github.com/GetPageSpeed/MTProxy)
- **Telegram Official**: [TelegramMessenger/MTProxy](https://github.com/TelegramMessenger/MTProxy)

## Giấy Phép

MIT License - Xem file [LICENSE](LICENSE) để biết thêm chi tiết.

## Đóng Góp

Mọi đóng góp đều được chào đón! Vui lòng tạo issue hoặc pull request.

## Hỗ Trợ

Nếu gặp vấn đề, vui lòng:

1. Kiểm tra phần [Khắc Phục Sự Cố](#khắc-phục-sự-cố)
2. Tạo issue với thông tin chi tiết
3. Cung cấp log từ `journalctl -u MTProxy`
