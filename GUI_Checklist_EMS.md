# GUI Checklist — EMS (Event Management System)

> **Sản phẩm nhóm — Task 1A**
> Checklist dùng chung cho tất cả thành viên, phủ 4 Interface Aspect (IA-01 → IA-04).
> Dựa trên: 10 Usability Heuristics (Nielsen), 6 Design Principles (Norman), 8 Golden Rules (Shneiderman).

---

## Quy ước ký hiệu nguyên tắc tham chiếu

| Viết tắt | Nguyên tắc |
|---|---|
| **Nielsen #1** | Visibility of System Status |
| **Nielsen #2** | Match Between System and the Real World |
| **Nielsen #3** | User Control and Freedom |
| **Nielsen #4** | Consistency and Standards |
| **Nielsen #5** | Error Prevention |
| **Nielsen #6** | Recognition Rather Than Recall |
| **Nielsen #7** | Flexibility and Efficiency of Use |
| **Nielsen #8** | Aesthetic and Minimalist Design |
| **Nielsen #9** | Help Users Recognize, Diagnose, and Recover from Errors |
| **Nielsen #10** | Help and Documentation |
| **Norman #1** | Visibility (Affordance) |
| **Norman #2** | Feedback |
| **Norman #3** | Constraints |
| **Norman #4** | Mapping |
| **Norman #5** | Consistency |
| **Norman #6** | Affordance |
| **Shneiderman #1** | Strive for Consistency |
| **Shneiderman #2** | Seek Universal Usability |
| **Shneiderman #3** | Offer Informative Feedback |
| **Shneiderman #4** | Design Dialogs to Yield Closure |
| **Shneiderman #5** | Prevent Errors |
| **Shneiderman #6** | Permit Easy Reversal of Actions |
| **Shneiderman #7** | Keep Users in Control |
| **Shneiderman #8** | Reduce Short-Term Memory Load |

---

## Bảng Checklist GUI (48 tiêu chí)

| ID | Aspect (IA) | Tên tiêu chí | Mô tả chi tiết cách test | Nguyên tắc tham chiếu |
|---|---|---|---|---|
| **GUI-01** | IA-01 | Bố cục tổng thể (Layout) nhất quán giữa các trang | Mở ≥ 3 trang admin (Dashboard, Events, Users, Support Requests). Kiểm tra sidebar, header, vùng nội dung chính có giữ nguyên vị trí, kích thước và tỷ lệ trên mọi trang. Sidebar không bị dịch chuyển, header không thay đổi chiều cao. | Nielsen #4, Shneiderman #1, Norman #5 |
| **GUI-02** | IA-01 | Typography nhất quán (font-family, font-size, line-height) | So sánh tiêu đề trang (h1/h2), nội dung bảng, label của form, placeholder trên ≥ 3 trang. Dùng DevTools kiểm tra font-family, font-size và line-height có thống nhất không. Không có trang nào dùng font khác hoặc cỡ chữ bất thường so với phần còn lại. | Nielsen #4, Shneiderman #1 |
| **GUI-03** | IA-01 | Bảng màu (Color palette) nhất quán và có đủ tương phản | Kiểm tra màu nền, màu chữ, màu nút primary/secondary, màu link trên toàn bộ ứng dụng. Dùng công cụ kiểm tra tương phản (WCAG contrast checker) để đảm bảo tỷ lệ tương phản chữ/nền ≥ 4.5:1 cho text thường và ≥ 3:1 cho text lớn. Các nút cùng loại phải cùng màu trên mọi trang. | Nielsen #4, Shneiderman #2, Norman #1 |
| **GUI-04** | IA-01 | Canh lề (Alignment) và khoảng cách (Spacing) đồng nhất | Kiểm tra khoảng cách giữa các phần tử (padding, margin) trên form, bảng, card KPI. Các phần tử cùng nhóm phải có spacing bằng nhau. Nội dung phải canh lề trái/phải nhất quán (không có phần tử bị lệch so với grid chung). | Nielsen #8, Shneiderman #1 |
| **GUI-05** | IA-01 | Responsive design — hiển thị trên các kích thước màn hình | Thu nhỏ cửa sổ trình duyệt xuống 1024px, 768px, 375px. Kiểm tra: sidebar có collapse/ẩn không, bảng dữ liệu có cuộn ngang hay bị tràn không, các nút có bị chồng lấn không, text có bị cắt không, form có hiển thị đầy đủ không. | Shneiderman #2, Norman #1 |
| **GUI-06** | IA-01 | Trạng thái Empty state hiển thị thông báo rõ ràng | Lọc bảng Events hoặc Users để kết quả trả về 0 dòng (VD: tìm kiếm chuỗi không tồn tại). Kiểm tra có hiển thị thông báo "Không có dữ liệu" / "No results found" kèm icon minh họa không, hay bảng chỉ trống không có giải thích. | Nielsen #1, Norman #2, Shneiderman #3 |
| **GUI-07** | IA-01 | Trạng thái Loading hiển thị rõ ràng | Quan sát khi trang đang tải dữ liệu (F5 refresh, chuyển trang, lọc bảng): có hiện spinner, skeleton loading, hoặc progress bar không? Hay trang chỉ trống rỗng rồi nội dung xuất hiện đột ngột (gây layout shift). | Nielsen #1, Norman #2, Shneiderman #3 |
| **GUI-08** | IA-01 | Hỗ trợ đa ngôn ngữ (i18n EN/VI) chuyển đổi chính xác | Nhấn nút chuyển ngôn ngữ (EN ↔ VI) trên header. Kiểm tra: tất cả label, placeholder, tiêu đề trang, thông báo lỗi, tooltip, nội dung menu sidebar có được dịch đầy đủ không? Có chuỗi nào bị hardcode tiếng Anh khi chuyển sang tiếng Việt (hoặc ngược lại) không? | Shneiderman #2, Nielsen #4 |
| **GUI-09** | IA-01 | Icon có ý nghĩa rõ ràng và nhất quán | Kiểm tra các icon trên sidebar (Users, Events, Support, Settings…), icon action trên bảng (Edit, Delete, View, Block…), icon trên header (notification, language, back). Mỗi icon phải có tooltip hoặc label đi kèm. Cùng một hành động phải dùng cùng icon trên toàn ứng dụng. | Nielsen #6, Norman #6, Shneiderman #8 |
| **GUI-10** | IA-01 | Hình ảnh (thumbnail, avatar, banner) hiển thị đúng tỷ lệ | Kiểm tra ảnh thumbnail sự kiện (4:3), banner (24:9), avatar user. Ảnh không bị méo (stretch/squash), không bị crop sai, có fallback/placeholder khi ảnh không tải được. | Nielsen #8, Norman #1 |
| **GUI-11** | IA-01 | Nút bấm (Button) có trạng thái rõ ràng: default, hover, active, disabled | Rê chuột qua các nút (Add Event, Save, Delete, Export…). Kiểm tra: nút có đổi màu/hiệu ứng khi hover không? Nút disabled (VD: Submit khi form chưa điền) có hiển thị xám và không bấm được không? Nút đang xử lý (loading) có hiện spinner và chặn double-click không? | Nielsen #1, Norman #2, Shneiderman #3 |
| **GUI-12** | IA-01 | Accessibility — Điều hướng bằng bàn phím (Keyboard navigation) | Dùng phím Tab để di chuyển qua các phần tử tương tác (input, button, link, dropdown). Kiểm tra: focus ring có hiển thị rõ không? Thứ tự Tab có logic không (trái→phải, trên→dưới)? Có thể nhấn Enter/Space để kích hoạt nút/link? Dropdown có thể dùng Arrow keys không? | Shneiderman #2, Nielsen #7 |
| **GUI-13** | IA-01 | Accessibility — Thuộc tính ARIA và cấu trúc heading | Dùng DevTools hoặc screen reader (NVDA/VoiceOver) kiểm tra: các phần tử tương tác có aria-label hoặc aria-labelledby không? Heading có đúng thứ bậc (h1 → h2 → h3, không nhảy cấp)? Bảng có `<th>` và scope rõ ràng? Modal/dialog có role="dialog" và aria-modal="true"? | Shneiderman #2, Nielsen #4 |

---

| ID | Aspect (IA) | Tên tiêu chí | Mô tả chi tiết cách test | Nguyên tắc tham chiếu |
|---|---|---|---|---|
| **GUI-14** | IA-02 | Label của form field rõ ràng và đặt đúng vị trí | Mở form Add/Edit Event, form đăng ký, form Support Request. Kiểm tra: mỗi input đều có label nhìn thấy được (không chỉ placeholder), label đặt phía trên hoặc bên trái input theo chuẩn. Label phải mô tả chính xác dữ liệu cần nhập. | Nielsen #6, Norman #1, Shneiderman #8 |
| **GUI-15** | IA-02 | Trường bắt buộc được đánh dấu rõ ràng (dấu * hoặc "(Required)") | Kiểm tra tất cả form: trường bắt buộc có ký hiệu * màu đỏ hoặc text "(Required)" bên cạnh label không? Có legend/ghi chú ở đầu form giải thích ý nghĩa dấu * không? | Nielsen #5, Shneiderman #5, Norman #3 |
| **GUI-16** | IA-02 | Validation inline — hiển thị lỗi ngay tại trường lỗi | Bỏ trống trường bắt buộc rồi nhấn Submit (hoặc blur ra khỏi trường). Kiểm tra: thông báo lỗi có hiển thị ngay bên dưới trường lỗi (inline) không? Hay chỉ có alert/toast chung ở trên cùng trang mà không chỉ rõ trường nào lỗi? Viền trường lỗi có đổi sang màu đỏ không? | Nielsen #9, Shneiderman #5, Norman #2 |
| **GUI-17** | IA-02 | Thông báo lỗi mang tính hướng dẫn (constructive error message) | Nhập sai định dạng email, ngày không hợp lệ, mật khẩu quá ngắn. Kiểm tra nội dung thông báo: có giải thích lỗi gì, điều kiện đúng là gì, và gợi ý cách sửa không? VD: "Email phải có dạng example@domain.com" thay vì chỉ "Invalid". | Nielsen #9, Shneiderman #3 |
| **GUI-18** | IA-02 | Validation ngày/giờ — ngày kết thúc phải sau ngày bắt đầu | Trên form Add/Edit Event: nhập End Date trước Start Date, hoặc End Time trước Start Time cùng ngày. Kiểm tra hệ thống có chặn và báo lỗi không? Date picker có tự disable các ngày không hợp lệ không? | Nielsen #5, Shneiderman #5, Norman #3 |
| **GUI-19** | IA-02 | Upload hình ảnh — hiển thị preview, kiểm tra kích thước và định dạng | Trên form Add/Edit Event: thử upload ảnh thumbnail (4:3) và banner (24:9). Kiểm tra: (1) Có preview ảnh sau khi chọn không? (2) Thử upload file không phải ảnh (.pdf, .exe) → có thông báo lỗi định dạng không? (3) Thử upload ảnh quá lớn (>5MB) → có giới hạn và thông báo không? (4) Có nút xóa ảnh đã upload không? | Nielsen #5, Norman #3, Shneiderman #5 |
| **GUI-20** | IA-02 | Rich-Text Editor hoạt động đúng | Trên form Add/Edit Event (phần mô tả): kiểm tra thanh công cụ RTE (bold, italic, underline, list, link, image). Thử format text và kiểm tra kết quả hiển thị trên trang chi tiết sự kiện. Editor không bị tràn container, không có lỗi khi paste nội dung từ Word/web. | Nielsen #4, Shneiderman #1 |
| **GUI-21** | IA-02 | Form giữ lại dữ liệu đã nhập khi validation fail | Điền đầy đủ form Add Event nhưng cố tình sai 1 trường (VD: bỏ trống tiêu đề). Nhấn Submit. Kiểm tra: các trường đã nhập đúng có còn giữ giá trị không? Hay form bị reset trắng và người dùng phải nhập lại toàn bộ? | Shneiderman #6, Nielsen #5 |
| **GUI-22** | IA-02 | Dropdown / Select có thể tìm kiếm khi danh sách dài | Mở dropdown chọn Category, Event Type, hoặc Role trên các form. Nếu danh sách > 10 mục, kiểm tra có ô tìm kiếm (search/filter) bên trong dropdown không? Có hỗ trợ gõ để lọc nhanh không? | Nielsen #7, Shneiderman #7, Norman #6 |
| **GUI-23** | IA-02 | Giới hạn ký tự (character limit) được hiển thị cho các trường có giới hạn | Kiểm tra các trường text như Tên sự kiện, Mô tả ngắn. Nếu có giới hạn ký tự, có hiện bộ đếm "x/200 ký tự" không? Khi nhập vượt giới hạn, có chặn hoặc cảnh báo không? | Nielsen #1, Shneiderman #5, Norman #3 |
| **GUI-24** | IA-02 | Placeholder text không thay thế label và biến mất khi focus | Kiểm tra: placeholder trong input chỉ đóng vai trò gợi ý (VD: "Nhập tên sự kiện…"), không phải label duy nhất. Khi click vào trường, placeholder biến mất → user vẫn biết trường đó yêu cầu gì nhờ label bên trên. | Nielsen #6, Shneiderman #8 |
| **GUI-25** | IA-02 | Tab order trong form đúng logic (trên→dưới, trái→phải) | Dùng phím Tab để di chuyển qua các trường trong form Add/Edit Event. Kiểm tra: thứ tự focus có theo thứ tự visual (từ trên xuống dưới, trái sang phải) không? Có bị nhảy lung tung giữa các nhóm trường không? | Shneiderman #2, Nielsen #7 |
| **GUI-26** | IA-02 | Xác nhận trước khi mất dữ liệu form chưa lưu | Điền một phần form Add Event, sau đó nhấn nút Back hoặc chuyển trang khác (click menu sidebar). Kiểm tra: có dialog xác nhận "Bạn có muốn rời trang? Dữ liệu chưa lưu sẽ mất" không? Hay form bị hủy mà không cảnh báo? | Nielsen #5, Shneiderman #5, Norman #3 |

---

| ID | Aspect (IA) | Tên tiêu chí | Mô tả chi tiết cách test | Nguyên tắc tham chiếu |
|---|---|---|---|---|
| **GUI-27** | IA-03 | Menu sidebar hiển thị mục đang active | Nhấn vào từng mục sidebar (Dashboard, Events, Users, Support…). Kiểm tra: mục đang chọn có được highlight (đổi màu nền, chữ đậm, hoặc có indicator bar) không? Khi refresh trang, mục active có đúng không? | Nielsen #1, Norman #4, Shneiderman #1 |
| **GUI-28** | IA-03 | Breadcrumb hiển thị đúng đường dẫn phân cấp | Trên trang chi tiết (VD: Events → Event Detail, Users → User Detail): kiểm tra breadcrumb có hiển thị đúng chuỗi phân cấp (Dashboard > Events > [Tên sự kiện]) không? Mỗi mắt xích có thể nhấn để quay lại cấp trên không? | Nielsen #1, Nielsen #6, Shneiderman #8 |
| **GUI-29** | IA-03 | Nút Back / Return hoạt động đúng và không mất dữ liệu | Từ trang chi tiết sự kiện, nhấn nút Back (nếu có trên UI) hoặc nút Back của trình duyệt. Kiểm tra: có quay về đúng trang danh sách trước đó không? Bộ lọc/tìm kiếm đã áp dụng có còn được giữ không? Hay bị reset về trạng thái mặc định? | Nielsen #3, Shneiderman #6, Norman #4 |
| **GUI-30** | IA-03 | Deep link / URL trực tiếp dẫn đến đúng trang | Copy URL của một trang cụ thể (VD: `/admin/events/123/edit`), mở trình duyệt mới (hoặc tab incognito), paste URL. Kiểm tra: (1) Có redirect về trang login nếu chưa đăng nhập? (2) Sau khi đăng nhập có quay lại đúng trang đó không? (3) URL có phản ánh đúng trạng thái trang (bộ lọc, tab, trang phân trang)? | Nielsen #7, Shneiderman #7 |
| **GUI-31** | IA-03 | Tabs chuyển đổi đúng nội dung và có indicator | Trên trang Support Requests (tab Pending / Resolved) hoặc trang Event Detail (các tab con): nhấn từng tab. Kiểm tra: (1) Tab active có underline/highlight rõ ràng? (2) Nội dung thay đổi đúng? (3) URL có cập nhật để reflect tab đang chọn không? | Nielsen #1, Norman #4, Shneiderman #1 |
| **GUI-32** | IA-03 | Pagination hoạt động đúng và hiển thị thông tin trang | Trên bảng Events hoặc Users có nhiều dòng: kiểm tra phân trang (nếu có). (1) Có hiện thông tin "Showing 1-10 of 50"? (2) Nút Previous/Next hoạt động đúng? (3) Có thể chọn số dòng/trang? (4) Nút Previous bị disable ở trang 1, Next bị disable ở trang cuối? | Nielsen #1, Shneiderman #3, Norman #1 |
| **GUI-33** | IA-03 | Menu sidebar collapse/expand trên màn hình nhỏ | Thu nhỏ trình duyệt hoặc dùng thiết bị mobile. Kiểm tra: sidebar có tự ẩn hoặc chuyển thành hamburger menu không? Khi mở hamburger, sidebar có overlay đúng không? Có nút đóng để thu lại sidebar? | Shneiderman #2, Nielsen #7 |
| **GUI-34** | IA-03 | Link/nút điều hướng dẫn đến đúng đích | Nhấn vào tên sự kiện trong danh sách → phải mở trang chi tiết đúng sự kiện đó. Nhấn vào avatar/tên user → phải mở profile hoặc chi tiết user đó. Kiểm tra không có link bị hỏng (404) hoặc dẫn sai trang. | Nielsen #4, Shneiderman #1 |
| **GUI-35** | IA-03 | Nút quay lại trang người dùng từ admin (và ngược lại) | Trên header admin có icon "Back to User Dashboard" (hoặc tương tự). Nhấn vào kiểm tra có chuyển đúng về trang người dùng công khai không? Ngược lại, từ trang user có nút vào Admin dashboard (nếu role Admin)? | Nielsen #3, Shneiderman #6, Norman #4 |
| **GUI-36** | IA-03 | Scroll-to-top khi chuyển trang hoặc tải nội dung mới | Từ cuối bảng Events (đã scroll xuống), nhấn vào sự kiện chi tiết hoặc chuyển trang phân trang. Kiểm tra: trang mới có tự cuộn lên đầu không? Hay user phải scroll lên thủ công? | Shneiderman #2, Nielsen #7 |

---

| ID | Aspect (IA) | Tên tiêu chí | Mô tả chi tiết cách test | Nguyên tắc tham chiếu |
|---|---|---|---|---|
| **GUI-37** | IA-04 | Toast notification hiển thị sau hành động thành công | Thực hiện hành động: lưu sự kiện, xóa sự kiện, assign role, block user, reset password. Kiểm tra: có toast/snackbar xuất hiện ở góc màn hình thông báo "Thành công" / "Success" không? Toast có tự biến mất sau vài giây không? Có nút đóng (×) không? | Nielsen #1, Norman #2, Shneiderman #3 |
| **GUI-38** | IA-04 | Dialog xác nhận trước hành động hủy hoại (destructive action) | Thực hiện: xóa sự kiện, block user, reset password. Kiểm tra: có dialog xác nhận hiện ra với câu hỏi rõ ràng (VD: "Bạn có chắc muốn xóa sự kiện X?") không? Dialog có 2 nút rõ ràng (Xác nhận / Hủy)? Nút hủy hoại có màu cảnh báo (đỏ)? Có thể đóng dialog bằng ESC hoặc click bên ngoài? | Nielsen #5, Shneiderman #5, Norman #3 |
| **GUI-39** | IA-04 | Màu trạng thái (status color) nhất quán và có ý nghĩa | Kiểm tra badge/chip trạng thái trên bảng Events (Draft, Published, Ended…), Support Requests (Pending, Resolved), Users (Active, Blocked). Màu có tuân theo quy ước: xanh lá = tích cực/active, đỏ = nguy hiểm/blocked, vàng/cam = chờ xử lý, xám = draft/inactive? Cùng trạng thái trên các trang khác nhau có cùng màu? | Nielsen #4, Norman #4, Shneiderman #1 |
| **GUI-40** | IA-04 | Progress bar / indicator cho hành động mất thời gian | Thực hiện hành động tốn thời gian: upload ảnh lớn, export Excel, publish sự kiện. Kiểm tra: có progress bar, spinner, hoặc phần trăm hoàn thành hiển thị không? Nút submit có chuyển sang trạng thái loading (spinner + text "Đang xử lý…") không? | Nielsen #1, Norman #2, Shneiderman #3 |
| **GUI-41** | IA-04 | Badge/counter hiển thị số lượng chưa xử lý | Kiểm tra badge trên sidebar (VD: Support Requests có badge "5" đỏ cho pending). Badge trên icon Notification (số thông báo chưa đọc). Counter có cập nhật realtime khi có item mới hoặc khi xử lý xong? | Nielsen #1, Norman #1, Shneiderman #3 |
| **GUI-42** | IA-04 | Thông báo lỗi hệ thống (server error) hiển thị thân thiện | Ngắt mạng hoặc gọi API lỗi (nếu có thể mô phỏng). Kiểm tra: có thông báo lỗi thân thiện "Đã xảy ra lỗi, vui lòng thử lại" không? Hay hiển thị raw error/stack trace? Có nút "Thử lại" (Retry) không? | Nielsen #9, Shneiderman #3, Norman #2 |
| **GUI-43** | IA-04 | Double-click / Double-submit bị chặn | Nhấn nút Submit/Save liên tục 2-3 lần nhanh. Kiểm tra: hệ thống có chặn gửi trùng không? Nút có bị disable sau lần nhấn đầu tiên cho đến khi xử lý xong? Không tạo ra bản ghi trùng lặp. | Nielsen #5, Shneiderman #5 |
| **GUI-44** | IA-04 | Cập nhật real-time (nếu có) — dữ liệu tự refresh | Trên trang Check-in hoặc Dashboard KPI: mở 2 tab trình duyệt. Ở tab 1 thực hiện check-in, ở tab 2 xem số liệu KPI hoặc log. Kiểm tra: dữ liệu ở tab 2 có tự cập nhật không (real-time qua WebSocket) hay phải refresh thủ công? | Nielsen #1, Norman #2 |
| **GUI-45** | IA-04 | Trạng thái phiên đăng nhập (Session) — timeout và thông báo | Đăng nhập rồi để yên ứng dụng khoảng 30-60 phút (hoặc theo timeout cấu hình). Kiểm tra: khi session hết hạn, có thông báo "Phiên đã hết hạn, vui lòng đăng nhập lại" không? Hay chỉ redirect về login mà không giải thích? Có cơ chế "Remember me" hoặc tự động refresh token? | Nielsen #9, Shneiderman #3 |
| **GUI-46** | IA-04 | Export file (Excel) — phản hồi tải xuống rõ ràng | Nhấn nút Export trên trang Users hoặc Participants. Kiểm tra: (1) Có hiện spinner/loading khi đang tạo file? (2) File có tự download hoặc có notification "File đã sẵn sàng, nhấn để tải"? (3) Tên file có ý nghĩa (VD: users_export_2026-07-28.xlsx)? (4) File mở được và dữ liệu đầy đủ? | Nielsen #1, Shneiderman #3, Norman #2 |
| **GUI-47** | IA-04 | Lightbox / Modal ảnh hoạt động đúng | Trên trang Support Request detail: nhấn vào ảnh đính kèm. Kiểm tra: ảnh mở trong lightbox/modal phóng to? Có nút đóng (×)? Có thể đóng bằng ESC hoặc click nền? Nếu nhiều ảnh, có nút Previous/Next? Ảnh hiển thị đúng tỷ lệ trong lightbox? | Nielsen #3, Norman #6, Shneiderman #6 |
| **GUI-48** | IA-04 | Undo / Hoàn tác hành động vừa thực hiện | Sau khi thực hiện hành động (VD: block user, delete event): kiểm tra có tùy chọn Undo trong toast notification hoặc có nút Unblock/Restore ngay lập tức không? Nếu không có Undo, dialog xác nhận ở bước trước (GUI-38) có đủ rõ ràng để ngăn lỗi không? | Nielsen #3, Shneiderman #6 |

---

## Tổng hợp phân bổ theo Aspect

| Aspect | Số tiêu chí | Phạm vi ID |
|---|---|---|
| **IA-01**: Chuẩn UI chung | 13 | GUI-01 → GUI-13 |
| **IA-02**: Forms | 13 | GUI-14 → GUI-26 |
| **IA-03**: Navigation | 10 | GUI-27 → GUI-36 |
| **IA-04**: Feedback / State | 12 | GUI-37 → GUI-48 |
| **Tổng cộng** | **48** | |

---

## Tổng hợp phân bổ theo Nguyên tắc

| Nguyên tắc | Số lần tham chiếu |
|---|---|
| **Nielsen #1** — Visibility of System Status | 13 |
| **Nielsen #2** — Match Between System and the Real World | 1 |
| **Nielsen #3** — User Control and Freedom | 5 |
| **Nielsen #4** — Consistency and Standards | 8 |
| **Nielsen #5** — Error Prevention | 8 |
| **Nielsen #6** — Recognition Rather Than Recall | 4 |
| **Nielsen #7** — Flexibility and Efficiency of Use | 6 |
| **Nielsen #8** — Aesthetic and Minimalist Design | 4 |
| **Nielsen #9** — Help Users Recognize, Diagnose, and Recover from Errors | 4 |
| **Nielsen #10** — Help and Documentation | 0 (*xem ghi chú bên dưới) |
| **Norman #1** — Visibility | 5 |
| **Norman #2** — Feedback | 7 |
| **Norman #3** — Constraints | 6 |
| **Norman #4** — Mapping | 4 |
| **Norman #5** — Consistency | 2 |
| **Norman #6** — Affordance | 3 |
| **Shneiderman #1** — Strive for Consistency | 7 |
| **Shneiderman #2** — Seek Universal Usability | 6 |
| **Shneiderman #3** — Offer Informative Feedback | 9 |
| **Shneiderman #4** — Design Dialogs to Yield Closure | 0 (*xem ghi chú bên dưới) |
| **Shneiderman #5** — Prevent Errors | 7 |
| **Shneiderman #6** — Permit Easy Reversal of Actions | 4 |
| **Shneiderman #7** — Keep Users in Control | 3 |
| **Shneiderman #8** — Reduce Short-Term Memory Load | 4 |

> **Ghi chú:** Nielsen #10 (Help and Documentation) và Shneiderman #4 (Design Dialogs to Yield Closure) không được tham chiếu trực tiếp trong bảng chính nhưng được cover gián tiếp qua các tiêu chí: GUI-10 (Help/Documentation có thể kiểm tra qua mục User Guide trên sidebar), GUI-38 và GUI-26 (dialog xác nhận tạo closure cho hành động).

---

## Phụ lục: Prompt AI sử dụng để sinh Checklist

### Prompt 1: Sinh bộ checklist ban đầu

- **Mục tiêu**: Tạo ra khung checklist cơ bản phủ 4 khía cạnh giao diện (IA).
- **Nội dung câu lệnh**:

  ```text
  Đóng vai là một chuyên gia kiểm thử phần mềm (QA/QC Engineer) chuyên về GUI và Usability. Tôi đang cần tạo một Checklist GUI cho một hệ thống quản lý sự kiện (EMS) trên nền tảng Web.
  Link: https://prod-dev.ems-fitus.cloud

  Tài khoản Admin (cho kịch bản A và C, và phần admin của D): admin@gmail.com / Admin@123 - tài khoản phải có role ADMIN trên EMS.

  Hãy tạo cho tôi một bảng Checklist gồm ít nhất 40 tiêu chí, dựa trên các nguyên tắc chuẩn: 10 Usability Heuristics của Jakob Nielsen, 6 nguyên tắc thiết kế của Don Norman và 8 quy tắc vàng của Ben Shneiderman.

  Vui lòng phân loại các tiêu chí này thành 4 nhóm chính sau:

  IA-01: Chuẩn UI chung (layout, typography, màu sắc, tính nhất quán, trạng thái empty/loading).
  IA-02: Forms (label, validation, vị trí báo lỗi, trường bắt buộc).
  IA-03: Navigation (menu, breadcrumb, tab, nút back, deep link).
  IA-04: Feedback / state (toast, dialog xác nhận, progress bar, màu trạng thái).
  Trình bày dưới dạng bảng gồm các cột: [ID], [Aspect (IA)], [Tên tiêu chí], [Mô tả chi tiết cách test], [Nguyên tắc tham chiếu].
  ```

### Prompt 2: Tinh chỉnh cho ứng dụng EMS (Event Management System)

- **Mục tiêu**: Bổ sung các tiêu chí đặc thù của giao diện web EMS.
- **Nội dung câu lệnh**:

  ```text
  Dựa trên checklist chung vừa sinh, hãy phân tích các điểm thiếu sót khi áp dụng thực tế lên một hệ thống quản lý sự kiện như EMS.

  Biết rằng hệ thống EMS có các tính năng đặc thù như:
  - kéo thả sắp xếp danh mục (reorder)
  - upload banner tỉ lệ lớn (24:9)
  - đa ngôn ngữ Anh - Việt ở Header
  - phân quyền xem nội bộ (Internal Note) cho Admin

  Hãy gợi ý cho tôi các tiêu chí cụ thể cần bổ sung thủ công để bao phủ các tính năng này.
  ```

---

## Nguồn tham khảo

1. Nielsen, J. (1994). *10 Usability Heuristics for User Interface Design.* Nielsen Norman Group. https://www.nngroup.com/articles/ten-usability-heuristics/
2. Norman, D. (2013). *The Design of Everyday Things* (Revised Edition). Basic Books.
3. Shneiderman, B., Plaisant, C., Cohen, M., Jacobs, S., Elmqvist, N., & Diakopoulos, N. (2016). *Designing the User Interface: Strategies for Effective Human-Computer Interaction* (6th Edition). Pearson.
4. WCAG 2.1 — Web Content Accessibility Guidelines. https://www.w3.org/TR/WCAG21/
5. Slide môn học: *GUI + Usability + Compatibility Testing (AI-First, Combined).*
6. ISTQB Foundation Level Syllabus (bản mới nhất).
