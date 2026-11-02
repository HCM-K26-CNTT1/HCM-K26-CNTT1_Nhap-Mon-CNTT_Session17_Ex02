# BÀI 2: XỬ LÝ SỰ CỐ CACHE VÀ PHIÊN ĐĂNG NHẬP TRONG DOANH NGHIỆP

## Phần 1. Phân tích

**1. Tại sao CSS không cập nhật?**

Nguyên nhân là do Browser Cache đang lưu phiên bản CSS cũ trên máy tính. Khi An nhấn F5, trình duyệt có thể sử dụng lại file CSS đã lưu thay vì tải file mới từ Server. Vì vậy, nút "Thanh toán" vẫn hiển thị màu xanh cũ.

**2. Tại sao phiên đăng nhập bị mất?**

Nguyên nhân là do Cookie đăng nhập chưa có thuộc tính Max-Age hoặc Expires.

- **Session Cookies:** Cookie chỉ tồn tại trong phiên làm việc của trình duyệt. Khi đóng trình duyệt, Cookie thường bị xóa nên An phải đăng nhập lại.
- **Persistent Cookies:** Cookie được lưu trong một khoảng thời gian xác định nhờ thuộc tính Max-Age hoặc Expires. Khi mở trình duyệt lại, Cookie vẫn còn nếu chưa hết hạn.

## Phần 2. Sửa lỗi

**Hành động 1: Cập nhật giao diện ngay lập tức**

An nhấn tổ hợp phím `Ctrl + Shift + R` (Hard Reload) để yêu cầu trình duyệt tải lại tài nguyên từ Server, hạn chế sử dụng CSS cũ trong Cache.

**Hành động 2: Duy trì trạng thái đăng nhập lâu dài**

An cần cấu hình Cookie đăng nhập thành Persistent Cookie bằng cách thêm thuộc tính Max-Age hoặc Expires.

Ví dụ:

```http
Set-Cookie: ptit_session=TOKEN_123; Max-Age=604800; Path=/; HttpOnly; Secure; SameSite=Lax
```

Trong đó:
- `Max-Age=604800`: Cookie tồn tại trong 7 ngày.
- `HttpOnly`: Ngăn JavaScript đọc giá trị Cookie.
- `Secure`: Chỉ gửi Cookie qua HTTPS.
- `SameSite=Lax`: Hạn chế Cookie được gửi trong một số yêu cầu từ website khác.

## Kết luận

Browser Cache lưu tài nguyên như CSS để tăng tốc độ tải trang, còn Cookie lưu thông tin giúp duy trì phiên đăng nhập. An cần dùng Hard Reload để cập nhật giao diện và cấu hình Persistent Cookie để không phải đăng nhập lại sau mỗi lần đóng trình duyệt.