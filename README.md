# Windows License Checker

Công cụ PowerShell hỗ trợ kiểm tra trạng thái kích hoạt, loại giấy phép và các dấu hiệu can thiệp bản quyền trên Windows.

- Chủ sở hữu bản quyền: **Trần Đăng Khoa**
- Phiên bản: **1.2.1**
- Nền tảng: Windows 10/11
- Yêu cầu: quyền Administrator

## Chức năng

1. Kiểm tra trạng thái bản quyền Windows trên máy đang sử dụng.
2. Kiểm tra và khôi phục khóa OEM được lưu trong BIOS, nếu có.
3. Gỡ khóa và dấu vết của các phương thức kích hoạt không hợp lệ.
4. Hiển thị cách chương trình thực hiện kiểm tra.
5. Chuyển edition Windows mà không cài đặt lại.
6. Thoát chương trình.

Chương trình không còn chức năng mua key hoặc mở trang bán key.

## Cách chạy

Giữ hai tệp sau trong cùng một thư mục:

- `check.ps1`
- `run_tool-check.bat`

Nhấp đúp vào `run_tool-check.bat`, sau đó chọn **Yes** khi Windows yêu cầu quyền Administrator.

Bạn cũng có thể mở PowerShell bằng quyền Administrator và chạy trực tiếp:

```powershell
powershell.exe -NoLogo -NoProfile -ExecutionPolicy Bypass -File .\check.ps1
```

## Lưu ý an toàn

- Đọc kỹ thông báo trước khi chọn chức năng thay đổi edition, gỡ key hoặc khôi phục key OEM.
- Một số thao tác thay đổi dịch vụ, firewall, khóa sản phẩm hoặc yêu cầu khởi động lại Windows.
- Chỉ sử dụng khóa Windows hợp lệ và phù hợp với edition được cài đặt.
- Nên tạo điểm khôi phục hệ thống và sao lưu dữ liệu quan trọng trước khi thay đổi cấu hình.

## Khắc phục lỗi

Nếu PowerShell báo thiếu quyền, hãy nhấp chuột phải vào `run_tool-check.bat` và chọn **Run as administrator**.

Nếu Windows chặn tập lệnh được tải từ Internet, mở Properties của các tệp, chọn **Unblock** nếu tùy chọn này xuất hiện, rồi chạy lại.

## Bản quyền

Copyright (c) 2026 Trần Đăng Khoa. All rights reserved.

Xem điều khoản đầy đủ trong [LICENSE](LICENSE).
