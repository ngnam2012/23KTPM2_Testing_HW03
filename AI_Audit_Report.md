# AI Audit Report

**Khai báo:** I use AI tools for the following tasks.

## 1. Nhật ký sử dụng AI

| Công cụ AI     | Ngày giờ         | Prompt của sinh viên                                                                                                     | Output của AI                                                                                                |
| -------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| Gemini 3.1 Pro | 28/07/2026 21:14 | Đóng vai là một chuyên gia kiểm thử... Hãy tạo cho tôi một bảng Checklist gồm ít nhất 40 tiêu chí...                     | Tạo file `GUI_Checklist_EMS.md` gồm 48 tiêu chí dựa trên Nielsen, Norman, Shneiderman, phân thành 4 nhóm.    |
| Gemini 3.1 Pro | 29/07/2026 21:36 | Bối cảnh: Tôi đang làm bài kiểm thử GUI... Đây là ảnh chụp màn hình trang "Danh sách Users"... Hãy phân tích ảnh này...  | Tạo file `C1_UserList_Analysis.md` phát hiện 23 vấn đề GUI/Usability trên màn hình User List.                |
| Gemini 3.1 Pro | 29/07/2026 21:51 | Bối cảnh: Tiếp tục bài kiểm thử GUI... Đây là ảnh chụp màn hình chức năng "Assign Role"... Hãy phân tích ảnh này...      | Tạo file `C2_EditUser_Analysis.md` phát hiện 20 vấn đề, trong đó có 3 lỗi Major liên quan form validation.   |
| Gemini 3.1 Pro | 29/07/2026 22:33 | Bối cảnh: Tiếp tục bài kiểm thử GUI... Đây là ảnh chụp màn hình chức năng "Export Users"... Hãy phân tích ảnh này...     | Tạo file `C3_ExportUsers_Analysis.md` phát hiện 8 vấn đề về UX, i18n, feedback khi xuất file.                |
| Gemini 3.1 Pro | 31/07/2026 20:55 | Bạn là chuyên gia UX Researcher... giúp tôi thiết kế Kế hoạch User Testing (cho 5 người dùng thật)...                    | Tạo file `Usability_Test_Plan_C.md` bao gồm task scenario, metrics, SUS questionnaire, và report template.   |
| Gemini 3.1 Pro | 01/08/2026 20:52 | Đóng vai một chuyên gia kiểm thử... thiết kế ma trận kiểm thử tương thích (Cross-Browser / Cross-Platform)... rút gọn... | Tạo file `CrossBrowser_Test_Matrix_C.md` với bộ 6 ca kiểm thử tối ưu theo kỹ thuật Pair-wise/Orthogonal.     |
| Gemini 3.1 Pro | 02/08/2026 22:31 | Đóng vai là một QA/QC Engineer... giúp tôi thực hiện 2 việc tổng hợp: tạo Bug Findings Log và README.md...               | Cập nhật file `Bug_And_Usability_Findings.md` (tổng hợp 51 issue) và `README.md` (tổng hợp số liệu báo cáo). |
| Gemini 3.1 Pro | 03/08/2026 21:10 | Từ những dữ kiện này hãy làm AI Audit Report và thiết kế lên một AI Skills (có HITL)...                                  | Tạo `AI_Audit_Report.md` và thiết kế Agent Skill tự động kiểm thử GUI cho EMS.                               |

## 2. AI Critique (Phản biện AI)

Quá trình sử dụng AI (Gemini) cho bài tập kiểm thử GUI & Usability trên EMS mang lại tốc độ và sự toàn diện khi thiết kế checklist, nhưng cũng bộc lộ một số giới hạn rõ rệt:

1. **Thiếu hụt ngữ cảnh động (Dynamic Context):** Khi phân tích ảnh chụp màn hình tĩnh (như trang Users List hay Form Assign Role), AI chỉ nhìn thấy bề nổi. Nó có thể chỉ ra lỗi thiếu dấu sao đỏ ở trường bắt buộc, nhưng không thể biết chắc chắn rằng khi bấm "Save" mà không nhập dữ liệu thì hệ thống có báo lỗi (validation) hay không. Nó đưa ra giả định thay vì khẳng định xác đáng.
2. **Hiện tượng "ảo giác" (Hallucination) và bịa lỗi:** AI có thể "nhìn nhầm" các chi tiết UI do hạn chế về nhận diện hình ảnh, dẫn đến việc bịa ra những lỗi hoàn toàn không có thật (ví dụ: báo cáo sai màu sắc nút bấm, sai font chữ, hoặc tưởng tượng ra một thành phần UI bị lệch dù thực tế nó hiển thị chuẩn). Ngoài ra, ở tác vụ logic như thiết kế ma trận Cross-browser, AI có lúc đề xuất thiếu thực tế (ví dụ gợi ý test Safari trên Windows 11). Điều này đòi hỏi con người phải luôn kiểm chứng lại (verify) bằng mắt thật trên hệ thống thực.
3. **Sự máy móc trong đánh giá Heuristic:** AI đôi khi gán ép một lỗi nhỏ (như màu nút Export đỏ) vào quá nhiều nguyên tắc của Nielsen, Norman và Shneiderman cùng lúc để cố làm "dày" báo cáo, dẫn đến rườm rà và làm loãng mức độ nghiêm trọng thực sự của lỗi.

**Nguyên tắc cộng tác rút ra:** AI là một trợ lý Exploratory Testing tuyệt vời để tạo framework (checklist, test plan) và "quét" bề mặt UI nhanh chóng. Tuy nhiên, nó không thể thay thế thao tác tương tác thật. Người kiểm thử phải đóng vai trò "Human-in-the-Loop" (HITL): dùng AI chỉ ra _nơi có thể có lỗi_, sau đó tự mình kiểm chứng các hành vi ẩn (state loading, error toast, keyboard navigation) trước khi đưa ra kết luận cuối cùng.
