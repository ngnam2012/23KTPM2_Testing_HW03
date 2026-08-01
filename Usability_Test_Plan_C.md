# Kế hoạch Kiểm thử Tính tiện dụng (Usability Test Plan)

**Dự án:** Event Management System (EMS)

**Kịch bản:** C - Admin quản lý người dùng

**Mục tiêu kiểm thử:** Đánh giá trải nghiệm của người dùng trong vai trò Admin khi thực hiện các tác vụ tìm kiếm, phân quyền và xuất dữ liệu người dùng.

---

## 1. Kịch bản Tác vụ (Task Scenario)

**Bối cảnh (Context):**
Bạn là một Quản trị viên (Admin) của hệ thống quản lý sự kiện (EMS) tại trường Đại học. Chuẩn bị cho học kỳ mới, ban tổ chức các sự kiện lớn đang có sự thay đổi về mặt nhân sự và bạn được phân công cập nhật lại hệ thống phân quyền.

**Tài khoản**: admin@gmail.com

**Mật khẩu**: Admin@123

**Nhiệm vụ (Task):**
"Sáng nay, Trưởng phòng Công tác Sinh viên gửi cho bạn một yêu cầu cập nhật quyền hạn cho thành viên ban tổ chức.
Bạn cần tìm tài khoản của sinh viên có tên là **'test test'** (hoặc email: *vanminhtop1hcmus@gmail.com*) trong hệ thống. Hãy cấp cho sinh viên này quyền **'Event Manager'** thay vì quyền thành viên bình thường như hiện tại, và đảm bảo trạng thái tài khoản của bạn này đang là **'Active'**.
Sau khi cập nhật xong, sếp cần một danh sách tổng hợp các quản lý sự kiện hiện tại. Hãy lọc và trích xuất danh sách tất cả những người dùng đang có quyền **'Event Manager'** và ở trạng thái **'Active'** ra một file Excel để gửi báo cáo."

---

## 2. Các chỉ số đo lường (Metrics & Observation Checklist)

Trong quá trình người dùng thực hiện, Tester sử dụng bảng sau để ghi chép mà không can thiệp vào tiến trình của họ:

| Tiêu chí                                | Chi tiết đánh giá                                                                                                                                                                                         | Ghi chú của Tester |
| :-------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------- |
| **Mức độ hoàn thành (Task Success)**    | [ ] Hoàn thành dễ dàng (Không cần trợ giúp)<br>[ ] Hoàn thành với khó khăn (Mất nhiều thời gian tự mò)<br>[ ] Hoàn thành có trợ giúp (Tester phải gợi ý)<br>[ ] Thất bại / Bỏ cuộc                        |                    |
| **Thời gian (Time on Task)**            | - Bắt đầu: **_ : _** <br>- Kết thúc: **_ : _** <br>**- Tổng thời gian: \_**\_ phút \_\_** giây**                                                                                                          |                    |
| **Tỷ lệ lỗi (Error Rate)**              | - Số lần click sai nút / nhầm tab: \_**\_<br>- Số lần nhập sai / lọc sai dẫn đến không ra kết quả: \_\_**<br>- Lỗi nghiêm trọng (vd: export sai danh sách do quên filter): \_\_\_\_                       |                    |
| **Độ lúng túng (Hesitation/Confusion)** | - Số lần dừng lại suy nghĩ/khựng lại trên 5 giây: \_**\_<br>- Số câu hỏi/phàn nàn phát ra (vd: "Nút xuất file ở đâu nhỉ?"): \_\_**<br>- Biểu hiện hành vi (nhíu mày, rà chuột liên tục không định hướng): |                    |

---

## 3. Bộ câu hỏi phỏng vấn sau test (Post-Task Questionnaire)

### Phần A: Thang đo SUS (System Usability Scale)

_(Người dùng đánh giá từ 1: Hoàn toàn không đồng ý -> 5: Hoàn toàn đồng ý)_

1. Tôi nghĩ rằng tôi sẽ muốn sử dụng hệ thống này thường xuyên.
2. Tôi thấy hệ thống này phức tạp một cách không cần thiết.
3. Tôi thấy hệ thống này rất dễ sử dụng.
4. Tôi nghĩ tôi sẽ cần sự hỗ trợ của người am hiểu kỹ thuật để có thể sử dụng hệ thống này.
5. Tôi thấy các chức năng trong hệ thống này được tích hợp với nhau rất tốt.
6. Tôi thấy hệ thống này có quá nhiều sự thiếu nhất quán.
7. Tôi có thể hình dung ra việc hầu hết mọi người sẽ học được cách sử dụng hệ thống này rất nhanh.
8. Tôi thấy hệ thống này rất cồng kềnh và rườm rà khi sử dụng.
9. Tôi cảm thấy rất tự tin khi sử dụng hệ thống này.
10. Tôi cần phải học/tìm hiểu rất nhiều điều trước khi có thể bắt tay vào sử dụng hệ thống này.

### Phần B: Câu hỏi mở (Open-ended Questions)

1. **Sự rõ ràng (Clarity):** Bạn cảm thấy giao diện danh sách người dùng và các bộ lọc (filter) có dễ hiểu và dễ tìm kiếm đúng mục tiêu không? Có thông tin hay nút bấm nào làm bạn bị rối mắt không?
2. **Khả năng phục hồi lỗi (Error recovery):** Trong quá trình chỉnh sửa phân quyền cho người dùng, nếu bạn lỡ thao tác sai, bạn thấy việc nhận ra lỗi và hoàn tác (hoặc sửa lại) có dễ dàng không? Hệ thống có thông báo hay phản hồi (feedback) gì giúp bạn không?
3. **Tốc độ & Hiệu quả (Speed):** Bạn đánh giá thế nào về tốc độ và sự liền mạch của quá trình: từ lúc tìm kiếm, chỉnh sửa đến lúc xuất file Excel? Có bước nào bạn thấy rườm rà và muốn rút ngắn lại không?
4. **Độ tin cậy (Trust):** Khi tải xuống file Excel, bạn có cảm thấy tự tin rằng file xuất ra đã chính xác chứa đúng những dữ liệu bạn đã lọc không? Chi tiết nào trên giao diện khiến bạn có (hoặc không có) cảm giác đó?

---

## 4. Template Báo cáo Kiểm thử Tính tiện dụng (Usability Report)

_(Sử dụng Dàn ý dưới đây để điền kết quả vào báo cáo cuối cùng sau khi đã kiểm thử xong 5 người)_

# Báo Cáo Kiểm Thử Tính Tiện Dụng (Usability Testing Report)

**Dự án:** Event Management System (EMS)
**Module:** User Management (Kịch bản C)
**Ngày thực hiện:** DD/MM/YYYY
**Người thực hiện (Tester):** [Tên của bạn]

## 1. Mục tiêu kiểm thử (Test Objectives)

- Đánh giá khả năng hoàn thành luồng công việc của Admin: Tìm kiếm -> Phân quyền -> Xuất dữ liệu.
- Xác định các điểm nút thắt (bottlenecks) gây lúng túng cho người dùng.
- Đo lường mức độ hài lòng tổng thể thông qua thang đo SUS.

## 2. Thông tin người tham gia (Participants Profile)

_(Ghi chú: Ẩn thông tin định danh cá nhân của người tham gia)_

| Participant ID | Độ tuổi | Chuyên môn / Ngành học | Kinh nghiệm dùng phần mềm quản lý |
| :------------- | :------ | :--------------------- | :-------------------------------- |
| P1             | 20      | CNTT                   | Thường xuyên                      |
| P2             | 21      | Kinh tế                | Thỉnh thoảng                      |
| P3             | ...     | ...                    | ...                               |
| P4             | ...     | ...                    | ...                               |
| P5             | ...     | ...                    | ...                               |

## 3. Tổng hợp Chỉ số (Metrics & Results)

### 3.1. Task Performance (Hiệu suất tác vụ)

| Participant    | Task Success           | Time on Task | Số lỗi (Errors) | Số lần do dự (Hesitations) |
| :------------- | :--------------------- | :----------- | :-------------- | :------------------------- |
| P1             | Hoàn thành dễ dàng     | 1m 20s       | 0               | 0                          |
| P2             | Hoàn thành có trợ giúp | 3m 45s       | 2               | 3                          |
| P3             | ...                    | ...          | ...             | ...                        |
| P4             | ...                    | ...          | ...             | ...                        |
| P5             | ...                    | ...          | ...             | ...                        |
| **Trung bình** | **-**                  | **Xm Ys**    | **Z lỗi**       | **W lần**                  |

### 3.2. Kết quả thang đo SUS (SUS Score)

- Điểm SUS của P1: ...
- Điểm SUS của P2: ...
- Điểm SUS của P3: ...
- Điểm SUS của P4: ...
- Điểm SUS của P5: ...
- **Điểm SUS Trung bình:** .../100
- **Đánh giá chung:** (Ví dụ: Chấp nhận được / Tốt / Cần cải thiện nhiều)

## 4. Phân tích Phát hiện & Trải nghiệm (Findings & Observations)

### 4.1. Những điểm tốt (Positives)

- (Ví dụ: Người dùng P1 và P3 đều thấy form Edit User rất trực quan và dễ thao tác...)
- ...

### 4.2. Những vấn đề về Usability (Usability Issues)

_(Sắp xếp theo mức độ nghiêm trọng: High - Medium - Low)_

- **Issue 1: [Tên lỗi] (High Severity)**
  - _Mô tả:_ (Ví dụ: 3/5 người dùng không nhận ra nút Export vì nó nằm lẫn với thanh phân trang ở góc dưới).
  - _Hậu quả:_ (Ví dụ: Mất trung bình 40 giây chỉ để tìm nút xuất file).
- **Issue 2: [Tên lỗi] (Medium Severity)**
  - _Mô tả:_ ...
- **Issue 3: [Tên lỗi] (Low Severity)**
  - _Mô tả:_ ...

## 5. Phân tích Câu hỏi mở (Qualitative Feedback)

- **Clarity:** (Đa số cho rằng... nhưng vẫn có ý kiến về việc...)
- **Error Recovery:** (Hệ thống chưa làm tốt ở điểm...)
- **Speed:** (Người dùng đánh giá...)
- **Trust:** (Người dùng hoàn toàn tin tưởng / hoặc cảm thấy mơ hồ vì không có toast thông báo...)

## 6. Đề xuất Cải thiện (Recommendations)

_(Dựa trên các vấn đề Issues ở mục 4, đề xuất phương án UI/UX giải quyết)_

1. **[Gắn với Issue 1]:** Dời vị trí nút Export lên góc trên bên phải, cạnh thanh Search và đổi sang màu nổi bật để dễ chú ý hơn.
2. **[Gắn với Issue 2]:** ...
3. **[Gắn với Issue 3]:** Cần thêm Toast Message "Cập nhật quyền thành công" hiển thị góc phải màn hình trong 3s sau khi lưu ở trang Edit User để người dùng yên tâm.
