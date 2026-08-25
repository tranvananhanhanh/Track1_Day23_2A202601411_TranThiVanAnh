# AI Support Log

**Học viên:** Trần Thị Vân Anh  
**MSHV:** 2A202601411  
**Dự án thực tế:** P-190 — APA Platform (AI Accounting Agent / Accounts Payable Automation)  

---

### AI đã giúp tôi ở đâu?

* Brainstorm danh sách các ứng viên Core Action tiềm năng cho nghiệp vụ kế toán công nợ (AP) và đưa ra các câu hỏi phản biện để tôi tự tranh luận, phân biệt rõ giữa thao tác kỹ thuật trung gian (như upload file, xem kết quả OCR) với hành động tạo ra giá trị hạch toán thực tế.
* Đóng vai "Kế toán trưởng khó tính" để thử thách lại Core Job và kiểm tra tính thực tế của quy trình đối soát 3 chiều (PO - GRN - Bill) theo chu kỳ nhận hóa đơn.
* Gợi ý cấu trúc đặt tên sự kiện tracking chuẩn định dạng `object_action` (như `documents_extracted`, `three_way_match_evaluated`, `bill_match_approved_and_synced`) và khung tiêu chí nghiệm thu (Acceptance Criteria) kỹ thuật gắn liền với kết nối Xero API.

---

### AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?

* Ban đầu AI đề xuất Core Action khá hời hợt và mang tính thao tác kỹ thuật: *"Tải file lên hệ thống (Upload file)"* hoặc *"Xem kết quả OCR"*, vốn chỉ là bước xử lý trung gian, chưa đảm bảo dữ liệu được đối soát đúng và hạch toán vào sổ cái.
* AI đề xuất bộ chỉ số sai lệch Nature của nghiệp vụ kế toán doanh nghiệp khi gợi ý đo lường `DAU`, `D1 Retention` và `D7 Retention` theo thói quen dashboard thông thường, trong khi kế toán công nợ xử lý chứng từ theo lô (Batch) và theo chu kỳ thanh toán hàng tuần.
* AI có xu hướng gợi ý track các thao tác click chuột ở giao diện (Client UI) mà không gắn với mã phản hồi thành công từ backend và Xero API.

---

### Tôi đã tự sửa hoặc quyết định lại điều gì?

* **Tự quyết định Core Action:** Bác bỏ gợi ý "xem OCR/upload" của AI, tự chọn **"Phê duyệt kết quả đối soát 3 chiều và đồng bộ hóa đơn sang Xero (Approve 3-Way Match & Sync)"** (`bill_match_approved_and_synced`) để gắn liền với giá trị hoàn tất hạch toán kế toán thực tế.
* **Tự chốt Cadence và Retention:** Sửa nhịp độ sang **Weekly / Per Batch** (ở cấp Kế toán viên và Doanh nghiệp), xây dựng bảng Retention 6 thành phần theo các mốc tuần (`W1, W2, W4, W8`) khớp đúng bản chất chu kỳ xử lý hóa đơn và thanh toán công nợ.
* **Tự xây dựng Metric Hypothesis:** Trực tiếp viết giả thuyết liên kết giữa cơ chế tự học quy tắc ánh xạ (Compounding Mapping Intelligence) của Product Loop với mức tăng trưởng 35% của North Star Metric trong 6 tuần.
* **Tự siết chặt Tracking Contract:** Tự tay viết 2 tiêu chí nghiệm thu (Acceptance Criteria) bắt buộc Xero API phản hồi `HTTP 200/201 Created` mới phát event và áp dụng khoá idempotency `(session_id, bill_id)` để triệt tiêu hoàn toàn lỗi đếm trùng do reload/retry.
