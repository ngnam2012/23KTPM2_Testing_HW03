# Báo cáo Tổng kết - Kịch bản Quản lý Người dùng (EMS)

## Thông tin Dự án

- **Kịch bản đã chọn:** Kịch bản C (Admin quản lý người dùng / Users Management).
- **Các màn hình đã kiểm tra:**
  - Màn hình C1: Danh sách Users
  - Màn hình C2: Edit User / Assign Role (Popup/Modal)
  - Màn hình C3: Export Users (File Excel sinh ra)

## Tóm tắt Số liệu Kiểm thử (Test Summary)

### Task 1: Kiểm thử Heuristic (GUI & Usability)

- **Số mục checklist thiết kế:** ~47 mục (ước lượng các ID từ GUI-01 đến GUI-47).
- **Số mục đã chạy đánh giá:** 45 mục (được áp dụng vào màn C1, C2, C3).
- **Số mục Pass:** 14 mục.
- **Số mục Fail / Partial:** 30 mục (25 Fail, 5 Partial).
- **Tổng số lỗi (Bug/Usability) tìm thấy:** 45 vấn đề

### Task 2: Usability Testing

- **Số người tham gia user-testing:** 5 người (P1 - P5).
- **Số vấn đề usability phát hiện:**
  - 1 vấn đề Nghiêm trọng cao (High) - Liên quan lỗi xuất Excel hỏng.
  - 1 vấn đề Trung bình (Medium) - Vị trí Admin Dashboard khó tìm.
  - 1 vấn đề Thấp (Low) - Quy trình phần quyền còn rườm rà.

### Task 3: Cross-browser & Platform Compatibility

- **Số ô tương thích đã phủ:** 18 ca kiểm thử (3 màn hình × 6 tổ hợp thiết bị/trình duyệt).
- **Kết quả chung:** Website hoạt động ổn định trên các nền tảng WebKit/Blink Desktop (Edge, Chrome, Safari macOS, Firefox), nhưng gặp lỗi nghiêm trọng trên các thiết bị Mobile (Chrome Android) và trình duyệt cũ (IE 11).

## Video Demo

[https://youtu.be/AR2RLUP8oq8]

## Bảng tự đánh giá (Self-Assessment)

| **STT** | **Tiêu chí**                                                                                    | **Điểm** | **Tự đánh giá** |
| ------- | ----------------------------------------------------------------------------------------------- | -------- | --------------- |
| **1a**  | Task 1A — Checklist dùng chung (> 40 mục, IA-01…IA-04) + nguồn tham khảo + prompt AI _(nhóm)_   | 15       | 15              |
| **1b**  | Task 1B — Chạy checklist trên ≥ 3 màn hình + bug report _(cá nhân)_                             | 15       | 15              |
| **2**   | Task 2 — User testing với 5 người dùng thật (kịch bản + 5 phiên + phân tích → Usability Report) | 25       | 25              |
| **3**   | Task 3 — Ma trận Cross-Browser / Cross-Platform (3 OS × 5 browser × 3 loại thiết bị)            | 25       | 25              |
| **4**   | Nộp Bug & Usability Findings (Google Form) + log tổng hợp                                       | 10       | 10              |
| **5**   | Agent Skills                                                                                    | 10       | 10              |
|         | **Tổng**                                                                                        | **100**  | **100**         |
