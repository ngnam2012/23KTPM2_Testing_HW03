# Bảng tham chiếu Heuristic — Dùng cho GUI Testing Skill

## Nielsen's 10 Usability Heuristics

| ID         | Tên                                                      | Mô tả ngắn                                                                     |
| ---------- | --------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Nielsen #1 | Visibility of System Status                               | Hệ thống phải luôn cho người dùng biết đang xảy ra gì (loading, success, error) |
| Nielsen #2 | Match Between System and the Real World                   | Ngôn ngữ, khái niệm phải phù hợp với thế giới thực của người dùng               |
| Nielsen #3 | User Control and Freedom                                  | Hỗ trợ Undo, Redo, Exit — cho phép thoát khỏi trạng thái không mong muốn        |
| Nielsen #4 | Consistency and Standards                                 | Giao diện nhất quán, tuân theo convention của nền tảng                            |
| Nielsen #5 | Error Prevention                                          | Thiết kế ngăn ngừa lỗi trước khi xảy ra (confirm dialog, validation)            |
| Nielsen #6 | Recognition Rather Than Recall                            | Giảm tải bộ nhớ — dùng label, breadcrumb, menu visible                          |
| Nielsen #7 | Flexibility and Efficiency of Use                         | Hỗ trợ shortcut, bulk action cho người dùng thành thạo                           |
| Nielsen #8 | Aesthetic and Minimalist Design                           | Không hiển thị thông tin không cần thiết, giữ UI gọn gàng                        |
| Nielsen #9 | Help Users Recognize, Diagnose, and Recover from Errors   | Thông báo lỗi rõ ràng, chỉ dẫn cách sửa                                        |
| Nielsen #10| Help and Documentation                                    | Cung cấp tài liệu hướng dẫn dễ tìm, dễ hiểu                                    |

## Norman's 6 Design Principles

| ID       | Tên           | Mô tả ngắn                                                        |
| -------- | ------------- | ------------------------------------------------------------------ |
| Norman #1| Visibility    | Phần tử quan trọng phải dễ nhìn thấy (affordance)                  |
| Norman #2| Feedback      | Hệ thống phải phản hồi hành động của người dùng                    |
| Norman #3| Constraints   | Giới hạn hành động sai (disable nút, giới hạn input)               |
| Norman #4| Mapping       | Mối liên hệ giữa controls và hiệu ứng phải tự nhiên               |
| Norman #5| Consistency   | Thiết kế nhất quán xuyên suốt hệ thống                             |
| Norman #6| Affordance    | Giao diện phải gợi ý cách sử dụng (nút trông như nút, link có gạch chân) |

## Shneiderman's 8 Golden Rules

| ID             | Tên                                  | Mô tả ngắn                                                           |
| -------------- | ------------------------------------- | --------------------------------------------------------------------- |
| Shneiderman #1 | Strive for Consistency                | Nhất quán về hành động, thuật ngữ, layout, màu sắc                    |
| Shneiderman #2 | Seek Universal Usability              | Hỗ trợ đa nền tảng, responsive, accessibility                        |
| Shneiderman #3 | Offer Informative Feedback            | Phản hồi cho mọi hành động (toast, progress, inline message)          |
| Shneiderman #4 | Design Dialogs to Yield Closure       | Các workflow có đầu-cuối rõ ràng (wizard step, confirmation)          |
| Shneiderman #5 | Prevent Errors                        | Validate input, confirm dialog, disable nút khi chưa sẵn sàng        |
| Shneiderman #6 | Permit Easy Reversal of Actions       | Cho phép Undo, Cancel, hoàn tác hành động                            |
| Shneiderman #7 | Keep Users in Control                 | Người dùng là chủ thể, hệ thống phản hồi theo lệnh                  |
| Shneiderman #8 | Reduce Short-Term Memory Load         | Không bắt người dùng nhớ thông tin qua nhiều bước                    |

---

## Ma trận ánh xạ nhanh: Loại lỗi → Heuristic

Bảng dưới đây giúp AI nhanh chóng xác định heuristic vi phạm dựa trên loại lỗi:

| Loại lỗi GUI/UX                            | Heuristic khuyến nghị (chọn 1-3)         |
| ------------------------------------------- | ----------------------------------------- |
| Không có loading spinner / skeleton         | Nielsen #1, Norman #2, Shneiderman #3    |
| Không có toast sau hành động CRUD           | Nielsen #1, Norman #2, Shneiderman #3    |
| Font/Màu/Spacing không nhất quán            | Nielsen #4, Shneiderman #1, Norman #5    |
| Thiếu dấu (*) trường bắt buộc              | Nielsen #5, Shneiderman #5, Norman #3    |
| Form submit không validate                  | Nielsen #5, Nielsen #9, Shneiderman #5   |
| Error message mơ hồ / sai trường           | Nielsen #9, Shneiderman #3, Norman #2    |
| Thiếu breadcrumb                            | Nielsen #6, Shneiderman #8               |
| Thiếu confirm dialog (delete, undo)         | Nielsen #3, Nielsen #5, Shneiderman #6   |
| Responsive vỡ layout                        | Shneiderman #2, Norman #1                |
| Icon quá nhỏ / khó nhấn                     | Nielsen #5, Shneiderman #5, Norman #3    |
| Thiếu tooltip                               | Nielsen #6, Norman #1                    |
| Focus trap không hoạt động trên modal       | Shneiderman #2, Nielsen #7, WCAG 2.1    |
| Nút luôn enable dù chưa sẵn sàng           | Nielsen #5, Nielsen #1, Shneiderman #5   |
| Tên cột / label trộn ngôn ngữ (EN/VI)       | Nielsen #4, Shneiderman #1               |
| Thiếu empty state message                   | Nielsen #1, Norman #2, Shneiderman #3    |
| Thiếu bulk action / shortcut                 | Nielsen #7, Shneiderman #7               |
