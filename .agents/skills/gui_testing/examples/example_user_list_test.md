# Ví dụ thực thi — GUI Testing Skill

## Kịch bản: Test màn hình "User List" trên EMS

### Bước 1: Người dùng kích hoạt Skill

```
User: Hãy test màn hình User List tại URL https://prod-dev.ems-fitus.cloud/users
```

### Bước 2: AI trích xuất và phân tích

```
SCREEN_NAME = "User List"
TARGET_URL  = "https://prod-dev.ems-fitus.cloud/users"
Kịch bản: Admin (Sử dụng tài khoản mặc định)
```

### Bước 3: AI thông báo và bắt đầu

```
AI: Bắt đầu kiểm thử màn hình User List. 
Sử dụng tài khoản Admin mặc định: admin@gmail.com
Đang chạy Phase 0 (Khởi tạo & Đăng nhập)...
```

### Bước 4: AI chạy Phase 0 (đăng nhập)

```
browser_subagent: Mở https://prod-dev.ems-fitus.cloud/login → Nhập admin@gmail.com → Admin@123 → Login
Kết quả: Đăng nhập thành công, redirect về Dashboard.
```

### Bước 5: AI chạy Phase 1 (IA-01)

```
browser_subagent: Kiểm tra layout, typography, color, responsive...
Kết quả:
  - FAIL: Sidebar không collapse ở 375px
  - FAIL: Tên user ALL CAPS không nhất quán  
  - PASS: Font nhất quán (Roboto)
  - PASS: Spacing đều đặn
```

### Bước 6: HITL Checkpoint #1

```
AI: ✅ Hoàn thành IA-01. Tìm thấy 2 vấn đề:
    1. Sidebar không collapse trên mobile (Medium)
    2. Tên user ALL CAPS không nhất quán (Medium)
    
    Bạn muốn tiếp tục?
    [Tiếp tục IA-02]  [Xem Bug Report]  [Điều chỉnh]  [Dừng]
```

### Bước 7: Người dùng phản hồi

```
User: "Sidebar không collapse nên là High vì ảnh hưởng toàn bộ mobile. Tiếp tục."
```

### Bước 8: AI cập nhật + tiếp tục Phase 2

```
AI: Đã cập nhật GT-001 lên High. Bắt đầu kiểm tra IA-02 (Form & Validation)...
```

_(Tiếp tục tương tự cho Phase 3, 4, 5)_

---

## Kết quả cuối cùng

Artifact `Bug_Report_UserList.md` được tạo với:
- 8 issues tổng cộng
- Phân bổ: 0 Critical | 2 High | 4 Medium | 2 Low
- Mỗi issue có screenshot chứng minh
- Đã được người dùng xác nhận qua 4 HITL Checkpoint
