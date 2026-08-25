# BÀI NỘP LAB TRACK 1 - DAY 23: PRODUCT METRICS LAB
## Từ Core Action tới Tracking

* **Họ và tên:** Trần Thị Vân Anh
* **Mã học viên (MSHV):** 2A202601411
* **Dự án thực tế:** P-190 — APA Platform (Nền tảng Tự động hóa Kế toán Công nợ — Đối soát 3 chiều PO - GRN - Bill)
* **Tệp tài liệu Metrics Pack:** [METRICS_PACK.md](./METRICS_PACK.md)
* **Nhật ký tương tác AI:** [ai-support-log.md](./ai-support-log.md)

---

## 📌 Tóm tắt dự án P-190 (APA Platform - AI Accounting Agent)

* **Persona:** Kế toán thanh toán / Kế toán viên công nợ (AP Accountant) tại các doanh nghiệp vừa và nhỏ (SMEs).
* **Core Job:** Giúp kế toán loại bỏ việc kiểm tra thủ công từng dòng giữa Đơn đặt hàng (PO), Phiếu nhập kho (GRN) và Hóa đơn nhà cung cấp (Bill), tự động phát hiện sai lệch giá/số lượng và hạch toán chính xác vào phần mềm kế toán Xero.
* **Core Action:** Phê duyệt kết quả đối soát 3 chiều và đồng bộ hóa đơn sang Xero (`Approve 3-Way Match & Sync Bill`).
* **Cadence:** Weekly / Per Batch (theo chu kỳ nhận lô chứng từ giao hàng và lịch thanh toán công nợ định kỳ của doanh nghiệp).
* **North Star Metric:** Weekly High-Confidence Matched & Synced Bills (Số Hóa đơn Đối soát 3 Chiều Chuẩn xác được Đồng bộ Hàng tuần).

---

## 💡 Điều tôi mang về áp dụng cho dự án thật (Key Takeaways)

1. **Không đo "thao tác OCR" hay "lượt hỏi AI" mà phải đo "chứng từ được hạch toán thành công":**
   * Trong một sản phẩm AI Kế toán như P-190, việc AI trích xuất OCR tốt hay trả lời tóm tắt nhanh chỉ là giá trị trung gian (Intermediate Output). Giá trị kinh doanh thực sự chỉ phát sinh khi kế toán viên **ra quyết định phê duyệt và dữ liệu được đồng bộ hợp lệ vào sổ cái Xero** (`bill_match_approved_and_synced`).

2. **Cadence kế toán xuất phát từ dòng chảy chứng từ thực tế (Nature), không ép theo DAU/D1:**
   * Nghiệp vụ kế toán công nợ vận hành theo dòng chảy giao nhận hàng hóa và chu kỳ thanh toán định kỳ hàng tuần/tháng. Vì vậy, chỉ số Retention và Engagement phải được đo lường theo chu kỳ tuần (`Weekly / Per Batch`) thay vì cố ép user mở app hàng ngày.

3. **Product Loop phải tạo ra Trí tuệ Tích lũy (Compounding Mapping Intelligence):**
   * Một sản phẩm AI Accounting Agent giữ chân được người dùng lâu dài nhờ khả năng tự học: mỗi lần kế toán duyệt một quy tắc ánh xạ (Vendor SKU sang Account Code), hệ thống tự động ghi nhớ để các lần sau đạt tỷ lệ tự động hoàn toàn (Straight-Through Processing) cao hơn, giải phóng tối đa sức lao động.

4. **Tracking Contract kỹ thuật là rào chắn chống rủi ro tài chính:**
   * Trong lĩnh vực kế toán tài chính, việc bắn trùng event hay bắn sớm khi backend chưa xác nhận sẽ dẫn đến sai lệch dữ liệu phân tích nghiêm trọng. Hệ thống tracking bắt buộc phải có tiêu chí nghiệm thu chặt chẽ: chỉ phát event khi nhận mã `HTTP 200/201` từ Xero API và có khóa `idempotency` chống ghi nhận lặp.
