---
taskId: [TASK-ID]
verifiedAt: [YYYY-MM-DD HH:mm JST]
overallMatchScore: [0-100]
designSource: [Canva URL hoặc tên file ảnh Canva]
actualSource: [Tên file ảnh chụp thực tế]
---

# Báo cáo Kiểm thử Giao diện (UI Verification Report) — [TASK-ID]

Báo cáo này liệt kê danh sách các điểm sai lệch giữa thiết kế Canva và UI thực tế chạy ở local.  
Developer sử dụng danh sách này làm đầu vào để sửa lỗi giao diện khớp với thiết kế.

---

## 1. Kết quả Đánh giá Tổng quan

- **Mức độ tương thích (Match Score)**: **[overallMatchScore]%**
- **Tổng số lỗi phát hiện**: **[N]** lỗi lệch giao diện.
  - 🔴 **Nghiêm trọng (High)**: [Count] lỗi (Vỡ layout, thiếu chức năng chính).
  - 🟡 **Trung bình (Medium)**: [Count] lỗi (Lệch màu sắc, sai font chữ chính, spacing lớn).
  - 🟢 **Thấp (Low)**: [Count] lỗi (Lệch spacing nhỏ, hover micro-interactions).

---

## 2. Bảng Danh sách lỗi lệch UI (Visual Diffs Table)

| ID | Component | Loại lỗi | Chi tiết lỗi (Design vs Actual) | Độ nghiêm trọng | Trạng thái | Hướng dẫn sửa đổi (Fix advice) |
|----|-----------|----------|--------------------------------|-----------------|------------|--------------------------------|
| [ID-001] | [Component name] | `color|typography|spacing|missing|layout` | **Design**: [Mô tả trạng thái thiết kế]<br>**Actual**: [Mô tả thực tế bị lệch] | `High|Medium|Low` | `Open|Fixed` | [Hướng dẫn cụ thể cho dev sửa CSS/HTML] |

---

## 3. So sánh Hình ảnh Trực quan (Visual Comparison)

### Màn hình Thiết kế Canva (Design)
![Canva Design](file:///[đường dẫn ảnh design Canva])

### Màn hình Thực tế (Actual UI)
![Actual UI](file:///[đường dẫn ảnh thực tế])

---

## 4. Nhật ký Sửa lỗi (Fix Log)

*Phần này dành cho Developer ghi lại quá trình sửa lỗi.*

| ID lỗi | File sửa đổi | Cách đã xử lý | Người sửa | Ngày sửa | Trạng thái kiểm tra lại |
|--------|--------------|---------------|-----------|----------|-------------------------|
| [ID-001] | | | | | Chưa test lại / Đã đạt |
