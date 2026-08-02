# Phân tích GUI & Usability — Màn hình C3: Export Users (Xuất Excel)

> **Kịch bản C — Admin quản lý người dùng**
> Phân tích dựa trên: 10 Heuristics (Nielsen), 6 Principles (Norman), 8 Golden Rules (Shneiderman)
> Đối chiếu với [GUI_Checklist_EMS.md](GUI_Checklist_EMS.md)

---

## 1. Mô tả luồng tính năng (Dựa trên 3 ảnh)

Chức năng Export dữ liệu người dùng ra file Excel hoạt động qua các bước:

1. **Ảnh 1 (Web UI)**: Nút "Export" màu xanh lá (kèm icon tải xuống) nằm ở góc phải phía trên bảng dữ liệu. Bấm vào nút này để khởi chạy tính năng.
2. **Ảnh 2 (Browser Download)**: Trình duyệt hiển thị popup tải file hoàn tất với tên file là `users-export-1785338916926.xlsx`. Không thấy hiển thị thông báo (toast) nào từ giao diện của hệ thống EMS.
3. **Ảnh 3 (Excel File)**: File mở trong phần mềm Excel (ở chế độ Protected View). File có tiêu đề "USER REPORT", thông tin người xuất file. Các cột dữ liệu: _Last Name, First Name, Email, Phone, Card Code, Role, Status, Created At_.

---

## 2. Bảng phát hiện vấn đề (Findings)

| #   | Vị trí                                  | Vấn đề cụ thể                                                                                                                                                                                                                                                                                                                                                                                        | Heuristic / Nguyên tắc bị vi phạm                                                                                              | Mức nghiêm trọng (0–4) | Đề xuất sửa                                                                                                                                                                                           | Checklist ID           |
| --- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| 1   | File tải xuống (Tên file)               | Tên file là `users-export-1785338916926.xlsx`. Hệ thống sử dụng chuỗi Unix timestamp (1785338916926) làm hậu tố. Dãy số này dài, khó đọc đối với con người và không mang lại ý nghĩa về ngày tháng rõ ràng.                                                                                                                                                                                          | **Nielsen #2** (Match Between System & Real World), **Shneiderman #8** (Reduce Short-Term Memory Load)                         | **1**                  | Đổi tên file theo định dạng chuẩn, thân thiện với người dùng (human-readable): `users_export_YYYY-MM-DD.xlsx` (Ví dụ: `users_export_2026-07-29.xlsx`).                                                | GUI-46                 |
| 2   | Màn hình Web (Phản hồi hệ thống)        | Sau khi bấm nút Export, **hoàn toàn không có dấu hiệu Loading nào** trên nút (nút không mờ đi, không có spinner, không đổi chữ thành "Exporting"). Đồng thời cũng **không có Toast Notification** báo thành công. Người dùng chỉ nhận biết qua popup download mặc định của trình duyệt web. Do nút vẫn giữ nguyên trạng thái bấm được, nếu mạng chậm hoặc file lớn, admin dễ tưởng hệ thống đơ và bấm liên tục nhiều lần.                                                                                                                    | **Nielsen #1** (Visibility of System Status), **Norman #2** (Feedback), **Shneiderman #3** (Informative Feedback)              | **2**                  | Ngay khi bấm Export: disable nút, thêm spinner và đổi chữ thành "Exporting...". Khi xử lý xong: hiện Toast thông báo "Export thành công" và phục hồi lại trạng thái nút.                                            | GUI-37, GUI-40, GUI-46 |
| 3   | File Excel (Tiêu đề cột)                | **Không nhất quán thuật ngữ** giữa Web và file Excel. Trên web, mã người dùng gọi là `MEMBER CODE`, nhưng trong file Excel lại là cột `Card Code`.                                                                                                                                                                                                                                                   | **Nielsen #4** (Consistency & Standards), **Norman #4** (Mapping), **Shneiderman #1** (Strive for Consistency)                 | **2**                  | Đổi tiêu đề cột trong file Excel từ `Card Code` thành `Member Code` để đồng bộ 100% với giao diện hiển thị trên web.                                                                                  | GUI-08, GUI-46         |
| 4   | File Excel (Dữ liệu & Đa ngôn ngữ i18n) | **Trộn lẫn ngôn ngữ (EN/VI)** một cách thiếu kiểm soát: Web UI đang dùng tiếng Anh (Status: `Active`), nhưng file export lại xuất data tiếng Việt (`Hoạt động`). Phần thông tin header ghi "Exporter: Admin Tôi là" (trộn EN/VI và ngữ pháp kỳ lạ).                                                                                                                                                  | **Nielsen #4** (Consistency & Standards), **Shneiderman #1** (Consistency)                                                     | **2**                  | Đảm bảo cơ chế i18n áp dụng nhất quán cả trên data export. Nếu user đang dùng UI tiếng Anh, giá trị Status trong Excel phải là `Active`. Dịch thuật / format lại chuỗi "Admin Tôi là" cho đúng logic. | GUI-08                 |
| 5   | Luồng thao tác (Nút Export)             | Nút Export xuất toàn bộ dữ liệu mà **không có Tùy chọn (Options)** hay Confirm. Admin không thể chọn chỉ xuất các user đang hiển thị trên trang hiện tại, hay xuất theo filter/search hiện tại. (Thiếu cột Checkbox như đã phân tích ở C1 làm mất đi khả năng Export Selected).                                                                                                                      | **Nielsen #3** (User Control & Freedom), **Nielsen #7** (Flexibility & Efficiency), **Shneiderman #7** (Keep Users in Control) | **2**                  | Khi bấm Export, nên hiển thị 1 dropdown hoặc modal nhỏ hỏi: "Export All Users" hoặc "Export Filtered/Current Page". Tốt nhất là bổ sung checkbox từng dòng để chọn "Export Selected".                 | GUI-46                 |
| 6   | File Excel (Thiếu thông tin)            | File Excel **thiếu cột `UPDATED`** (ngày cập nhật cuối). Cột này có trên bảng danh sách Web nhưng bị bỏ sót khi xuất file.                                                                                                                                                                                                                                                                           | **Nielsen #4** (Consistency & Standards)                                                                                       | **1**                  | Bổ sung cột `Updated At` vào dữ liệu xuất Excel để đảm bảo tính toàn vẹn thông tin báo cáo cho admin.                                                                                                 | GUI-46                 |
| 7   | Trạng thái mạng (Offline)               | Khi người dùng bị mất mạng (Offline), hệ thống không có bất kỳ thông báo (Toast/Banner) nào để cảnh báo. Mặc dù tính năng Export có thể chạy ngầm ở Client-side không cần mạng, nhưng việc không thông báo trạng thái kết nối có thể khiến người dùng nhầm lẫn, tưởng rằng máy tính vẫn đang online bình thường.                                                                                             | **Nielsen #1** (Visibility of System Status)                                                                                   | **1**                  | Hiển thị một banner nhỏ màu vàng/đỏ ở góc hoặc đầu trang: "You are currently offline" khi trình duyệt mất mạng (lắng nghe sự kiện `window.addEventListener('offline')`).                      | GUI-42                 |

---

## 3. Đối chiếu Checklist — Kết quả chạy trên màn hình C3

| Checklist ID | Tên tiêu chí                                      | Kết quả       | Ghi chú                                                                                                                        |
| ------------ | ------------------------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| GUI-03       | Bảng màu nhất quán                                | **Passed** | Nút Export màu xanh lá — khác biệt với màu đỏ (destructive), hợp lý cho chức năng "Tạo file".                                  |
| GUI-08       | Hỗ trợ đa ngôn ngữ (i18n)                         | **Failed** | Trộn lẫn EN/VI trong file xuất ("Active" thành "Hoạt động", "Exporter: Admin Tôi là"). Xem Finding #4.                         |
| GUI-37       | Toast notification                                | **Failed** | Không có thông báo "Export thành công" từ hệ thống. Xem Finding #2.                                                            |
| GUI-40       | Progress bar / Indicator                          | **Failed** | Không hề có trạng thái loading/exporting trên nút khi đang xử lý (dù test với mạng chậm). Nút vẫn bấm được liên tục. Xem Finding #2. |
| GUI-42       | Thông báo lỗi server                              | **Failed** | Không có thông báo hay cảnh báo mất mạng khi trình duyệt chuyển sang Offline. Xem Finding #7.                                                  |
| GUI-46       | Export file (Excel) — Phản hồi và chất lượng file | **Failed** | (1) Không loading/toast; (2) Tên file timestamp; (3) File mở được nhưng thiếu cột Updated; (4) Khác biệt tên cột Card Code.    |

---

## 4. Tổng hợp theo mức nghiêm trọng

| Mức                   | Mô tả                   | Số vấn đề | Finding #                                                                                 |
| --------------------- | ----------------------- | --------- | ----------------------------------------------------------------------------------------- |
| **4 — Catastrophe**   | Usability catastrophe   | **0**     | —                                                                                         |
| **3 — Major**         | Major usability problem | **0**     | —                                                                                         |
| **2 — Minor**         | Minor usability problem | **4**     | #2 (Thiếu Toast UI), #3 (Sai tên cột Card Code), #4 (Lỗi i18n), #5 (Thiếu Options Export) |
| **1 — Cosmetic**      | Cosmetic problem only   | **3**     | #1 (Tên file Timestamp), #6 (Thiếu cột Updated), #7 (Thiếu cảnh báo Offline)    |
| **0 — Not a problem** | Nhận xét chung          | **1**     |                                                                                         |

---

## 5. Đánh giá chung về chức năng Export Users

Tính năng Export hoạt động cơ bản tốt (xuất được file, mở file không bị lỗi file corrupt). Tuy nhiên, **tính đánh bóng (polish)** và **trải nghiệm người dùng (UX)** đang ở mức chưa hoàn thiện.

**3 điểm cần cải thiện ngay:**

1. **UX Phản hồi hệ thống**: Cần bổ sung Loading spinner trên nút Export và Toast message khi file được xử lý xong. Điều này rất quan trọng khi lượng user tăng lên (VD: xuất 10,000 users mất 5-10 giây) để tránh admin bấm liên tục nhiều lần.
2. **Chuẩn hóa dữ liệu xuất**: Tên file phải dùng chuẩn YYYY-MM-DD. Header cột phải khớp 100% với Web UI (Member Code). Đặc biệt không được tự ý dịch Status sang tiếng Việt khi giao diện Web đang là tiếng Anh.
3. **Cơ chế Control**: Phải cho phép admin xuất theo danh sách đang filter. Bấm Export nên hỏi "Export toàn bộ hay Export kết quả tìm kiếm", tránh phải xuất một file khổng lồ rồi tự dùng Excel lọc tay.
