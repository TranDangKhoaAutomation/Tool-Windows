# ITSO Windows Checker 2.0.0

Công cụ PowerShell hỗ trợ kiểm tra trạng thái kích hoạt, loại giấy phép và phát hiện dấu hiệu can thiệp bản quyền trên Windows.

- **Chủ sở hữu bản quyền**: Trần Đăng Khoa
- **Phiên bản**: 2.0.0
- **Nền tảng**: Windows 10/11
- **Yêu cầu**: quyền Administrator

## Chức năng

### 1. Kiểm tra bản quyền Windows
Quét 8 hạng mục phát hiện dấu vết crack và đánh giá tổng thể:
- **KMS Crack**: Phát hiện máy chủ KMS lậu, service crack, file Hosts bị chặn Microsoft
- **MAS / HWID**: Phát hiện lịch sử chạy script Microsoft Activation Scripts
- **KMS38 Hook**: Phát hiện cấu trúc thời hạn bất thường (2038, ExtendedGrace)
- **Logic Bản Quyền**: Kiểm tra Generic Key, Digital License, OEM, Retail, MAK
- **Thư mục Tool**: Phát hiện thư mục chứa công cụ crack
- **Tác vụ ẩn (Task)**: Phát hiện Scheduled Task của tool lậu
- **Registry**: Phát hiện khóa NoGenTicket và cấu hình KMS trái phép
- **Office / Ohook**: Kiểm tra trạng thái kích hoạt Microsoft Office và phát hiện Ohook

### 2. Khôi phục Key gốc từ BIOS
Đọc OEM Key từ mainboard (nếu có) và kích hoạt Windows bằng key gốc.
- Kiểm tra tương thích BIOS key với phiên bản Windows hiện tại trước khi thay đổi
- Tự động backup license hiện tại

### 3. Gỡ bỏ key và xóa crack
Dọn dẹp toàn bộ dấu vết crack trên hệ thống:
- Xóa key và cấu hình KMS
- Diệt service và scheduled task của tool crack
- Xóa thư mục chứa tool lậu
- Xóa file MAS còn sót trong Temp
- Dọn Registry (NoGenTicket, KMS Policy)
- Xóa Ohook (SppExtComObjHook.dll)
- Khôi phục file Hosts về mặc định
- **Tự động backup** toàn bộ trạng thái trước khi thay đổi
- **Cảnh báo** trước khi xóa MAK hoặc Retail hợp lệ

### 4. Cách thức hoạt động
Giải thích chi tiết về 5 bước kiểm tra của tool.

### 5. Thay đổi phiên bản Windows
Chuyển đổi giữa các phiên bản (Pro, Enterprise, Education) mà không cần cài lại.
- Tự động phục hồi Firewall nếu thao tác thất bại

## Kết quả đánh giá

| Kết luận | Ý nghĩa |
|----------|---------|
| **CRACK** | Phát hiện bằng chứng crack (≥1 critical evidence) |
| **LEGAL** | Bản quyền hợp lệ (Retail/OEM/KMS Doanh nghiệp) |
| **MAK_KEY** | Key doanh nghiệp (MAK) - không phải crack |
| **UNKNOWN** | Không đủ bằng chứng để kết luận |

## Cách chạy

### Chạy trực tiếp bằng PowerShell — không cần tải hoặc clone

Mở **PowerShell với quyền Administrator** rồi chạy một lệnh duy nhất:

```powershell
irm https://raw.githubusercontent.com/TranDangKhoaTechnology/Tool-Windows/main/check.ps1 | iex
```

Lệnh đầy đủ tương đương:

```powershell
Invoke-RestMethod https://raw.githubusercontent.com/TranDangKhoaTechnology/Tool-Windows/main/check.ps1 | Invoke-Expression
```

Nếu đang dùng **PowerShell 7 (`pwsh`)**, có thể chạy từ CMD/Run/Terminal bằng:

```powershell
pwsh -NoProfile -Command "irm https://raw.githubusercontent.com/TranDangKhoaTechnology/Tool-Windows/main/check.ps1 | iex"
```

> **Lưu ý:** Tool yêu cầu quyền Administrator. Cách chạy trực tiếp ở trên lấy phiên bản `check.ps1` mới nhất từ nhánh `main` của repository mỗi lần chạy.

### Chạy sau khi tải repository

Nhấp đúp vào `run_tool-check.bat`, chọn **Yes** khi Windows yêu cầu quyền Administrator.

Hoặc mở PowerShell với quyền Administrator và chạy:

```powershell
powershell.exe -NoLogo -NoProfile -ExecutionPolicy Bypass -File .\check.ps1
```

## Lưu ý an toàn

- Tool chạy 100% bằng lệnh hệ thống Microsoft, không chứa mã độc
- Đọc kỹ thông báo trước khi chọn chức năng thay đổi
- Tự động backup trước mọi thao tác destructive (Hosts, Registry, License)
- Một số thao tác yêu cầu khởi động lại Windows
- Nên tạo điểm khôi phục hệ thống trước khi thay đổi cấu hình

## Cảnh báo pháp lý

Công cụ này chỉ dành cho mục đích kiểm tra bản quyền hợp pháp. 
Không sử dụng để vi phạm bản quyền phần mềm.
Việc sử dụng Windows/Office crack là bất hợp pháp và vi phạm điều khoản sử dụng của Microsoft.

## Khắc phục lỗi

- **Thiếu quyền Admin**: Nhấp chuột phải vào PowerShell, chọn Run as Administrator
- **PowerShell bị chặn**: Mở Properties của file, chọn Unblock
- **Lỗi ExecutionPolicy**: Chạy lệnh `Set-ExecutionPolicy Bypass -Scope Process`

## Bản quyền

Copyright (c) 2026 Trần Đăng Khoa. All rights reserved.

Xem điều khoản đầy đủ trong [LICENSE](LICENSE).
