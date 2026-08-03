---
name: gui_testing
description: >
  Kỹ năng kiểm thử GUI & Usability tự động trên nền tảng Web (EMS).
  Kích hoạt khi người dùng yêu cầu "hãy test màn hình [Tên] tại URL [Link]".
  Sử dụng browser_subagent để tương tác thật với trình duyệt, kiểm tra theo
  4 khía cạnh (Layout, Form Validation, Navigation, Feedback), áp dụng
  Human-in-the-Loop (HITL) sau mỗi section, và xuất báo cáo lỗi dạng artifact.
---

# GUI Testing Skill — Hướng dẫn thực thi cho AI Agent

> **Phiên bản:** 1.0  
> **Tác giả:** AI Engineer / QA Automation  
> **Mục tiêu:** Tự động hóa kiểm thử GUI & Usability cho hệ thống EMS thông qua
> browser_subagent, có cơ chế Human-in-the-Loop (HITL) mạnh mẽ.

---

## 1. Điều kiện kích hoạt (Trigger)

Skill này được kích hoạt khi người dùng gửi yêu cầu khớp với mẫu sau:

- `"hãy test màn hình [Tên màn hình] tại URL [Link]"`
- `"kiểm thử GUI cho [Tên màn hình] tại [URL]"`
- `"test giao diện [Tên màn hình] ở [URL]"`

Khi phát hiện trigger, AI **PHẢI** trích xuất `SCREEN_NAME` và `TARGET_URL`.

**Cấu hình Mặc định (SUT):**
- URL cơ sở: `https://prod-dev.ems-fitus.cloud`

**Xử lý Tài khoản Đăng nhập:**
AI cần phân tích `SCREEN_NAME` hoặc hỏi người dùng xem kịch bản test thuộc nhóm nào (Admin hay User) để lấy tài khoản:

1. **Kịch bản Admin** (Dành cho kịch bản A, C và phần admin của D):
   - Sử dụng tài khoản mặc định (có role ADMIN):
     - `USERNAME`: `admin@gmail.com`
     - `PASSWORD`: `Admin@123`
   - Bỏ qua bước hỏi thông tin đăng nhập từ người dùng.

2. **Kịch bản User** (Dành cho người dùng bình thường):
   - AI **PHẢI** sử dụng `ask_question` (hoặc nhắc người dùng) cung cấp tài khoản test trước khi chuyển sang bước khởi tạo trình duyệt.

---

## 2. Quy trình tổng quát (Workflow Overview)

```
┌─────────────────────────────────────┐
│  PHASE 0: Khởi tạo & Đăng nhập     │
├─────────────────────────────────────┤
│  PHASE 1: IA-01 — UI/Layout        │  ──▶ HITL Checkpoint #1
├─────────────────────────────────────┤
│  PHASE 2: IA-02 — Form/Validation  │  ──▶ HITL Checkpoint #2
├─────────────────────────────────────┤
│  PHASE 3: IA-03 — Navigation       │  ──▶ HITL Checkpoint #3
├─────────────────────────────────────┤
│  PHASE 4: IA-04 — Feedback/Toast   │  ──▶ HITL Checkpoint #4
├─────────────────────────────────────┤
│  PHASE 5: Tổng hợp Bug Report      │
└─────────────────────────────────────┘
```

> [!CAUTION]
> **KHÔNG ĐƯỢC** chạy liên tục từ Phase 1 đến Phase 4 mà không dừng.
> Sau mỗi Phase, AI **BẮT BUỘC** phải dừng lại tại HITL Checkpoint.

---

## 3. PHASE 0 — Khởi tạo & Đăng nhập

### 3.1 Khởi tạo artifact Bug Report

Trước khi bắt đầu test, tạo artifact trống:

- **File:** `Bug_Report_{SCREEN_NAME}.md`
- **Nội dung ban đầu:** Header bảng với các cột: ID, Vị trí, Mô tả, Heuristic vi phạm, Mức nghiêm trọng, Screenshot.

### 3.2 Đăng nhập (nếu cần)

Sử dụng tài khoản đã xác định ở Bước 1 (Admin mặc định hoặc do User cung cấp).
Truy cập URL đăng nhập mặc định (`https://prod-dev.ems-fitus.cloud/login` hoặc URL tương đương):

```
browser_subagent:
  Task: |
    1. Mở trình duyệt và truy cập {LOGIN_URL}.
    2. Chờ trang tải xong (đợi xuất hiện form đăng nhập).
    3. Điền {USERNAME} vào trường email/username.
    4. Điền {PASSWORD} vào trường password.
    5. Nhấn nút Login/Đăng nhập.
    6. Chờ đến khi trang redirect thành công (URL thay đổi hoặc xuất hiện Dashboard).
    7. Nếu gặp CAPTCHA hoặc OTP: DỪNG LẠI và báo cáo về cho agent chính.
    8. Chụp screenshot trang sau đăng nhập.
    9. BÁO CÁO: Trạng thái đăng nhập (thành công/thất bại), URL hiện tại, có CAPTCHA/OTP không.
  RecordingName: login_flow
```

> [!IMPORTANT]
> Nếu browser_subagent báo gặp CAPTCHA hoặc OTP, AI **PHẢI** dùng `ask_question`
> để yêu cầu người dùng hỗ trợ thủ công:
> ```
> ask_question:
>   question: "Hệ thống yêu cầu CAPTCHA/OTP. Bạn có thể hoàn thành bước xác thực
>              thủ công trên trình duyệt không? Sau khi xong, hãy nhấn 'Đã hoàn thành'."
>   options:
>     - "Đã hoàn thành xác thực"
>     - "Bỏ qua, dùng URL trực tiếp không cần đăng nhập"
>     - "Hủy bỏ test"
> ```

### 3.3 Điều hướng đến màn hình đích

```
browser_subagent:
  Task: |
    1. Từ trang hiện tại, điều hướng đến {TARGET_URL}.
    2. Chờ trang tải hoàn chỉnh.
    3. Chụp screenshot toàn trang (full-page nếu có thể).
    4. BÁO CÁO: URL hiện tại, tiêu đề trang, có tải thành công không.
  RecordingName: navigate_to_screen
```

---

## 4. PHASE 1 — IA-01: UI / Layout / Màu sắc

### 4.1 Lệnh cho browser_subagent

```
browser_subagent:
  Task: |
    Bạn là một QA Tester đang kiểm tra trang "{SCREEN_NAME}" tại {TARGET_URL}.
    Hãy thực hiện kiểm tra UI/Layout theo danh sách dưới đây.
    Với MỖI mục, hãy quan sát kỹ và ghi nhận kết quả (PASS / FAIL + mô tả):

    1. BỐ CỤC TỔNG THỂ (Layout):
       - Header, sidebar, vùng nội dung chính có đúng vị trí không?
       - Có phần tử nào bị chồng lấn (overlap) không?

    2. TYPOGRAPHY:
       - Font chữ có nhất quán (cùng font-family) không?
       - Kích thước chữ tiêu đề vs nội dung có hợp lý không?
       - Có text nào bị cắt (truncated) mà không có tooltip không?

    3. MÀU SẮC & TƯƠNG PHẢN:
       - Các nút cùng loại có cùng màu không?
       - Màu chữ trên nền có đủ tương phản (đọc được rõ) không?
       - Có phần tử nào dùng màu không nhất quán với phần còn lại không?

    4. ALIGNMENT & SPACING:
       - Các phần tử trong form/bảng có canh lề đều không?
       - Khoảng cách (padding/margin) giữa các mục có đồng nhất không?

    5. RESPONSIVE (nếu có thể):
       - Thu nhỏ cửa sổ xuống 768px: có bị vỡ layout không?
       - Thu nhỏ xuống 375px: sidebar có collapse không? Bảng có cuộn ngang không?

    6. EMPTY STATE & LOADING:
       - Trang có hiển thị skeleton/spinner khi đang tải không?
       - Nếu không có dữ liệu, có thông báo "No data" / "Không có dữ liệu" không?

    7. ICON & HÌNH ẢNH:
       - Các icon có sắc nét, kích thước phù hợp (≥24px) không?
       - Có icon nào bị mờ, vỡ, hoặc không hiển thị không?
       - Avatar (nếu có) có hiển thị đúng không?

    Chụp screenshot cho MỖI vấn đề phát hiện được (nếu có).
    BÁO CÁO CHI TIẾT: Liệt kê từng mục với trạng thái PASS/FAIL và ghi chú cụ thể.
  RecordingName: ia01_ui_layout
```

### 4.2 Xử lý kết quả & Ghi nhận lỗi

Sau khi browser_subagent trả kết quả:
- Phân tích từng mục FAIL.
- Với mỗi lỗi, xác định Heuristic vi phạm (dựa trên bảng tham chiếu ở `references/heuristic_mapping.md`).
- Gán mức nghiêm trọng: 1 (Low), 2 (Medium), 3 (High), 4 (Critical).
- Ghi vào artifact `Bug_Report_{SCREEN_NAME}.md`.

### 4.3 ★ HITL Checkpoint #1

**BẮT BUỘC DỪNG TẠI ĐÂY.** Sử dụng `ask_question` để báo cáo cho người dùng:

```
ask_question:
  question: |
    ✅ **Hoàn thành kiểm tra IA-01 (UI/Layout/Màu sắc) cho "{SCREEN_NAME}".**

    **Tóm tắt:** Tìm thấy {N} vấn đề:
    - [Liệt kê ngắn gọn top 3 vấn đề nghiêm trọng nhất]

    Bạn muốn tôi làm gì tiếp?
  options:
    - "Tiếp tục sang IA-02 (Form & Validation)"
    - "Xem chi tiết Bug Report trước khi tiếp tục"
    - "Kiểm tra lại Responsive kỹ hơn ở nhiều breakpoint"
    - "Điều chỉnh mức nghiêm trọng của một số lỗi"
    - "Dừng test tại đây, xuất báo cáo hiện tại"
```

---

## 5. PHASE 2 — IA-02: Form & Validation

### 5.1 Lệnh cho browser_subagent

```
browser_subagent:
  Task: |
    Bạn là một QA Tester kiểm tra Form & Validation trên trang "{SCREEN_NAME}".
    Tìm TẤT CẢ các form trên trang và với MỖI form, thực hiện:

    1. SUBMIT FORM TRỐNG:
       - Xóa sạch tất cả các trường, nhấn nút Submit/Save.
       - Có thông báo lỗi (validation error) không?
       - Thông báo lỗi có rõ ràng, chỉ ra đúng trường lỗi không?
       - Thông báo lỗi hiển thị ở đâu (inline dưới field hay popup)?

    2. NHẬP SAI ĐỊNH DẠNG:
       - Email: nhập "abc", "abc@", "@gmail.com" → có validate không?
       - Số điện thoại: nhập "abcdef", "12345" (quá ngắn) → có validate không?
       - Trường số: nhập chữ cái → có validate không?

    3. BOUNDARY VALUE:
       - Nhập chuỗi rất dài (>255 ký tự) vào mỗi trường text → xem có bị tràn không?
       - Nhập ký tự đặc biệt (<script>alert(1)</script>) → xem có bị XSS không?
       - Nhập khoảng trắng đầu/cuối → hệ thống có trim không?

    4. DẤU HIỆU TRƯỜNG BẮT BUỘC:
       - Các trường required có đánh dấu (*) đỏ không?
       - Có phân biệt được đâu là trường bắt buộc, đâu là tùy chọn không?

    5. REAL-TIME VALIDATION:
       - Khi rời trường (on blur), có validate ngay không hay phải đợi submit?
       - Khi sửa lại đúng, thông báo lỗi có tự mất không?

    6. TRẠNG THÁI NÚT SUBMIT:
       - Nút Submit có bị disable khi chưa điền gì không?
       - Nút Submit có disable khi đang xử lý (tránh double-click) không?

    Chụp screenshot cho MỖI trường hợp thử nghiệm.
    BÁO CÁO CHI TIẾT kết quả từng mục.
  RecordingName: ia02_form_validation
```

### 5.2 ★ HITL Checkpoint #2

**BẮT BUỘC DỪNG TẠI ĐÂY.**

```
ask_question:
  question: |
    ✅ **Hoàn thành kiểm tra IA-02 (Form & Validation) cho "{SCREEN_NAME}".**

    **Tóm tắt:** Tìm thấy {N} vấn đề validation:
    - [Liệt kê top 3 vấn đề]

    ⚠️ Một số phát hiện cần xác nhận từ bạn:
    - "[Mô tả phát hiện]" — Lỗi này có tính là vi phạm Heuristic #5 (Error Prevention) không?
    - "[Mô tả phát hiện]" — Mức nghiêm trọng nên là Medium hay High?

    Bạn muốn tiếp tục thế nào?
  options:
    - "Xác nhận kết quả, tiếp tục sang IA-03 (Navigation)"
    - "Xem chi tiết Bug Report"
    - "Kiểm tra thêm các trường hợp edge-case khác"
    - "Điều chỉnh heuristic mapping cho lỗi vừa tìm"
    - "Dừng test, xuất báo cáo hiện tại"
```

---

## 6. PHASE 3 — IA-03: Navigation

### 6.1 Lệnh cho browser_subagent

```
browser_subagent:
  Task: |
    Bạn là một QA Tester kiểm tra Navigation trên trang "{SCREEN_NAME}".
    Hãy thực hiện các bài test sau:

    1. NÚT BACK (TRÌNH DUYỆT):
       - Từ trang hiện tại, nhấn nút Back trên trình duyệt.
       - Trang có quay lại đúng trang trước không?
       - Có bị mất dữ liệu đã nhập (nếu đang ở form) không?

    2. BREADCRUMB:
       - Có breadcrumb không? Nếu có, nó có chính xác vị trí hiện tại không?
       - Nhấn vào từng mục breadcrumb: có điều hướng đúng không?

    3. SIDEBAR / MENU:
       - Mục menu hiện tại có được highlight (active state) không?
       - Nhấn vào các mục menu khác: có điều hướng đúng không?
       - Quay lại trang gốc: menu có highlight lại đúng không?

    4. TAB NAVIGATION (Bàn phím):
       - Nhấn Tab liên tục: thứ tự focus có logic (trái→phải, trên→dưới) không?
       - Có focus indicator (viền xanh/outline) rõ ràng trên mỗi phần tử không?
       - Nếu trang có modal/popup: focus có bị "trap" trong modal không (focus trap)?
       - Nhấn Escape: modal có đóng không?

    5. PHÍM TẮT & ACCESSIBILITY:
       - Nhấn Enter khi focus trên nút: có hoạt động như click không?
       - Các link có phân biệt rõ với text thường (gạch chân, màu khác) không?

    6. PAGINATION (nếu có):
       - Nhấn Next/Previous page: dữ liệu có thay đổi đúng không?
       - Nhấn trang cuối rồi Next: có bị lỗi không?
       - URL có thay đổi khi chuyển trang (query param) không?

    Chụp screenshot mỗi khi phát hiện vấn đề.
    BÁO CÁO CHI TIẾT từng bài test.
  RecordingName: ia03_navigation
```

### 6.2 ★ HITL Checkpoint #3

**BẮT BUỘC DỪNG TẠI ĐÂY.**

```
ask_question:
  question: |
    ✅ **Hoàn thành kiểm tra IA-03 (Navigation) cho "{SCREEN_NAME}".**

    **Tóm tắt:** Tìm thấy {N} vấn đề navigation:
    - [Liệt kê top 3 vấn đề]

    ❓ Câu hỏi cần xác nhận:
    - Breadcrumb không tồn tại trên trang này — đây có tính là lỗi (vi phạm
      Nielsen #6: Recognition > Recall) hay là thiết kế có chủ đích?
    - Focus trap trên modal không hoạt động — mức nghiêm trọng nên đánh giá
      là Medium (ảnh hưởng UX) hay High (vi phạm WCAG Accessibility)?

    Bạn muốn tiếp tục thế nào?
  options:
    - "Xác nhận, tiếp tục sang IA-04 (Feedback)"
    - "Xem chi tiết Bug Report"
    - "Test thêm keyboard navigation trên form"
    - "Điều chỉnh kết quả phần Navigation"
    - "Dừng test, xuất báo cáo hiện tại"
```

---

## 7. PHASE 4 — IA-04: Feedback (Toast, Alert, Progress)

### 7.1 Lệnh cho browser_subagent

```
browser_subagent:
  Task: |
    Bạn là một QA Tester kiểm tra Feedback Mechanisms trên trang "{SCREEN_NAME}".
    Hãy thực hiện các thao tác kích hoạt feedback và quan sát:

    1. TOAST / NOTIFICATION:
       - Thực hiện hành động thành công (VD: Save, Update): có hiện toast "Thành công" không?
       - Toast có tự biến mất sau vài giây không? Có nút đóng (X) không?
       - Màu sắc toast có phù hợp (xanh = thành công, đỏ = lỗi) không?

    2. ERROR MESSAGE:
       - Tạo lỗi có chủ đích (submit form trống, nhập sai): thông báo lỗi có hiện không?
       - Thông báo có chỉ rõ trường nào bị lỗi và cách sửa không?
       - Sau khi sửa lỗi, thông báo có tự cập nhật/biến mất không?

    3. CONFIRMATION DIALOG:
       - Thực hiện hành động nguy hiểm (VD: Delete user): có hiện dialog xác nhận không?
       - Dialog có nội dung rõ ràng ("Bạn có chắc muốn xóa user X?") không?
       - Nhấn Cancel trên dialog: có quay lại trạng thái trước không?

    4. LOADING INDICATOR:
       - Khi thực hiện hành động (save, load data): có spinner/progress bar không?
       - Nút submit có disable khi đang loading không?

    5. UNSAVED CHANGES WARNING:
       - Chỉnh sửa form rồi nhấn Cancel/Back mà chưa Save: có cảnh báo không?
       - Nhấn nút đóng (X) popup khi đang edit: có cảnh báo mất dữ liệu không?

    6. INLINE FEEDBACK:
       - Hover vào nút/icon: có tooltip giải thích không?
       - Hover vào hàng bảng: có highlight row không?
       - Click vào phần tử disabled: có thông báo tại sao bị disable không?

    Chụp screenshot cho MỖI loại feedback tìm thấy (hoặc thiếu).
    BÁO CÁO CHI TIẾT kết quả.
  RecordingName: ia04_feedback
```

### 7.2 ★ HITL Checkpoint #4

**BẮT BUỘC DỪNG TẠI ĐÂY.**

```
ask_question:
  question: |
    ✅ **Hoàn thành kiểm tra IA-04 (Feedback) cho "{SCREEN_NAME}".**

    **Tóm tắt:** Tìm thấy {N} vấn đề feedback:
    - [Liệt kê top 3 vấn đề]

    ❓ Cần xác nhận:
    - Hệ thống không hiển thị toast sau khi Save — bạn có muốn tôi đánh giá
      đây là BUG (vi phạm Nielsen #1) hay chỉ là Usability Improvement?
    - Dialog xác nhận khi Delete không chỉ rõ tên user cụ thể — mức nghiêm trọng?

    Bạn muốn làm gì tiếp?
  options:
    - "Xác nhận tất cả, xuất báo cáo tổng hợp cuối cùng"
    - "Xem chi tiết Bug Report"
    - "Kiểm tra thêm các edge-case feedback"
    - "Điều chỉnh mức nghiêm trọng một số lỗi"
    - "Quay lại kiểm tra bổ sung Phase trước"
```

---

## 8. PHASE 5 — Tổng hợp Bug Report

### 8.1 Cấu trúc artifact đầu ra

Tạo/cập nhật artifact `Bug_Report_{SCREEN_NAME}.md` với cấu trúc:

```markdown
# Bug Report — {SCREEN_NAME}

> **Ngày test:** {DATE}
> **URL:** {TARGET_URL}
> **Tester:** AI Agent + Human Review
> **Tổng số issue:** {TOTAL}
> **Phân bổ:** Critical: {n} | High: {n} | Medium: {n} | Low: {n}

## Danh sách lỗi

| ID       | Vị trí (Aspect)     | Mô tả                          | Heuristic vi phạm                | Mức nghiêm trọng | Screenshot          |
| -------- | -------------------- | ------------------------------- | -------------------------------- | ----------------- | ------------------- |
| GT-001   | IA-01: Layout        | [Mô tả cụ thể]                 | Nielsen #4, Shneiderman #1      | 2 (Medium)        | gt_001_layout.png   |
| GT-002   | IA-02: Validation    | [Mô tả cụ thể]                 | Nielsen #5, Nielsen #9           | 3 (High)          | gt_002_form.png     |
| ...      | ...                  | ...                             | ...                              | ...               | ...                 |

## Tóm tắt theo Aspect

### IA-01: UI/Layout
- Tổng: {n} issues | Highlight: [tóm tắt]

### IA-02: Form & Validation
- Tổng: {n} issues | Highlight: [tóm tắt]

### IA-03: Navigation
- Tổng: {n} issues | Highlight: [tóm tắt]

### IA-04: Feedback
- Tổng: {n} issues | Highlight: [tóm tắt]

## Khuyến nghị ưu tiên sửa chữa
1. [Lỗi nghiêm trọng nhất + lý do cần sửa trước]
2. [Lỗi tiếp theo]
3. ...
```

### 8.2 Quy tắc đặt ID lỗi

- Format: `GT-{số thứ tự 3 chữ số}` (ví dụ: GT-001, GT-002, ...).
- Số thứ tự tăng dần liên tục xuyên suốt tất cả các Phase.

### 8.3 Bảng phân loại mức nghiêm trọng

| Mức | Tên      | Tiêu chí                                                              |
| --- | -------- | ---------------------------------------------------------------------- |
| 1   | Low      | Vấn đề thẩm mỹ nhỏ, không ảnh hưởng chức năng. Cải thiện nếu có thời gian. |
| 2   | Medium   | Ảnh hưởng trải nghiệm người dùng nhưng có workaround. Nên sửa.         |
| 3   | High     | Lỗi gây nhầm lẫn hoặc mất dữ liệu tiềm tàng. Cần sửa sớm.           |
| 4   | Critical | Hệ thống không hoạt động, trắng màn hình, mất chức năng chính.        |

---

## 9. Bảng tham chiếu Heuristic nhanh

Khi gán heuristic vi phạm cho lỗi, sử dụng bảng dưới đây:

| Loại vấn đề                     | Heuristic thường áp dụng              |
| -------------------------------- | -------------------------------------- |
| Thiếu feedback (toast, loading)  | Nielsen #1, Norman #2, Shneiderman #3 |
| Không nhất quán (font, màu, ...) | Nielsen #4, Shneiderman #1, Norman #5 |
| Thiếu xác nhận hành động nguy hiểm | Nielsen #5, Shneiderman #5, Norman #3 |
| Không có breadcrumb/vị trí       | Nielsen #6, Shneiderman #8            |
| Thiếu shortcut, bulk action      | Nielsen #7, Shneiderman #7            |
| UI rối, thông tin dư thừa        | Nielsen #8, Shneiderman #8            |
| Error message mơ hồ              | Nielsen #9, Shneiderman #3, Norman #2 |
| Thiếu help/documentation         | Nielsen #10                           |
| Responsive vỡ layout             | Shneiderman #2, Norman #1             |
| Không undo/cancel được            | Nielsen #3, Shneiderman #6            |

> [!WARNING]
> **Tránh gán ép quá nhiều heuristic** cho một lỗi nhỏ. Mỗi lỗi thường vi phạm
> 1-3 heuristic chính. Chỉ liệt kê những heuristic **thực sự liên quan trực tiếp**.

---

## 10. Nguyên tắc HITL (Human-in-the-Loop) bắt buộc

### 10.1 Khi nào phải dừng

AI **PHẢI** dừng và hỏi người dùng trong các tình huống sau:

1. **Sau mỗi Phase (IA-01 → IA-04):** Báo cáo kết quả, xin xác nhận trước khi qua Phase tiếp.
2. **Khi gặp CAPTCHA/OTP:** Không thể tự giải, cần người dùng thao tác thủ công.
3. **Khi không chắc chắn phân loại:** Không rõ lỗi thuộc Bug hay Usability → hỏi.
4. **Khi mức nghiêm trọng gây tranh cãi:** Medium hay High? → hỏi.
5. **Khi hệ thống có hành vi bất thường:** Trang trắng, redirect lạ, lỗi 500 → dừng và báo.

### 10.2 Format báo cáo HITL

Mỗi HITL Checkpoint phải bao gồm:

- **Tóm tắt số liệu:** Số lỗi tìm thấy, phân bổ theo mức nghiêm trọng.
- **Top 3 vấn đề:** Mô tả ngắn gọn 3 vấn đề nghiêm trọng nhất.
- **Câu hỏi cần xác nhận:** Những điểm AI không tự quyết được.
- **Lựa chọn hành động tiếp theo:** Dưới dạng `ask_question` options.

### 10.3 Xử lý phản hồi người dùng

- Nếu người dùng chọn **"Tiếp tục"** → chuyển Phase tiếp theo.
- Nếu người dùng chọn **"Xem chi tiết"** → hiển thị artifact Bug Report hiện tại.
- Nếu người dùng chọn **"Điều chỉnh"** → cập nhật Bug Report theo chỉ dẫn.
- Nếu người dùng chọn **"Dừng test"** → chuyển thẳng sang Phase 5, xuất báo cáo.
- Nếu người dùng **viết tự do** → phân tích yêu cầu và thực hiện tương ứng.

---

## 11. Lưu ý quan trọng cho AI Agent

> [!CAUTION]
> ### Những điều KHÔNG ĐƯỢC làm
> 1. **KHÔNG** bịa lỗi. Chỉ báo cáo những gì **thực sự quan sát được** qua browser.
> 2. **KHÔNG** chạy liên tục hết Phase 1→4 mà không dừng HITL.
> 3. **KHÔNG** gán quá 3 heuristic cho một lỗi nhỏ (severity 1).
> 4. **KHÔNG** đoán mò hành vi ẩn (API response, database state) mà không test thực tế.
> 5. **KHÔNG** bỏ qua screenshot — mỗi lỗi **PHẢI** có ảnh chứng minh.

> [!TIP]
> ### Những điều NÊN làm
> 1. **NÊN** mô tả lỗi cụ thể: "Nút Save màu xám trên nền trắng, tương phản <3:1"
>    thay vì "Nút Save khó nhìn".
> 2. **NÊN** so sánh với best practice: "Thiếu toast notification sau khi save,
>    vi phạm guideline Material Design".
> 3. **NÊN** đề xuất fix ngắn gọn trong mô tả lỗi.
> 4. **NÊN** ghi nhận cả những mục PASS (hoạt động tốt) trong báo cáo HITL.
> 5. **NÊN** nhóm các lỗi liên quan khi báo cáo để người dùng dễ theo dõi.

---

## 12. Ví dụ thực thi mẫu

Khi người dùng nói: **"Hãy test màn hình User List tại URL https://prod-dev.ems-fitus.cloud/users"**

AI thực hiện:

1. Trích xuất: `SCREEN_NAME = "User List"`, `TARGET_URL = "https://prod-dev.ems-fitus.cloud/users"`.
2. Phân tích: Kịch bản liên quan đến "User List" thuộc nhóm quản trị (Admin). AI sẽ sử dụng tài khoản Admin mặc định (`admin@gmail.com`).
3. Tạo artifact `Bug_Report_UserList.md` (trống).
4. Chạy Phase 0 (đăng nhập bằng Admin mặc định tại `https://prod-dev.ems-fitus.cloud/login` + điều hướng đến trang đích).
5. Chạy Phase 1 (IA-01) → ghi nhận lỗi → **DỪNG, HITL Checkpoint #1**.
6. Chờ phản hồi → tiếp Phase 2 (IA-02) → **DỪNG, HITL Checkpoint #2**.
7. Tiếp tục tương tự Phase 3, Phase 4.
8. Cuối cùng, xuất `Bug_Report_UserList.md` hoàn chỉnh.
