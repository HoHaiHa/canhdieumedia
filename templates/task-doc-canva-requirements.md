---
sessionId: [TASK-ID-YYYYMMDD-HHMM]
createdAt: [YYYY-MM-DD HH:mm JST]
updatedAt: [YYYY-MM-DD HH:mm JST]
commitSha: [short-sha]
roundCount: 0
lang: vi
---

# [Tên Feature/Màn hình từ Thiết kế Canva]

**Task ID**: [PROJECT-XXX]  
**Ngày tạo**: [YYYY-MM-DD]  
**BA**: [Name]  
**Thiết kế Canva**: [Link Canva Design hoặc Tên File thiết kế]  
**Trạng thái**: Draft / Review / Approved  
**Lane**: tiny | normal | high-risk

---

## 1. Bối cảnh & Vấn đề

[Mô tả bối cảnh nghiệp vụ của màn hình/tính năng này. Tại sao màn hình này tồn tại và giải quyết vấn đề gì?]

## 2. Mục tiêu giao diện

- [Mục tiêu UI/UX 1: ví dụ Tăng tỷ lệ hoàn thành form đăng ký]
- [Mục tiêu UI/UX 2: ví dụ Tối giản hóa các trường nhập liệu]

## 3. Ràng buộc & Quy tắc Thiết kế Canva

| Loại | Quy định thiết kế | Lý do |
|------|-------------------|-------|
| Màu sắc | [Màu thương hiệu chủ đạo, màu phụ] | [Tuân thủ Brand Guidelines] |
| Font chữ | [Font chính và các cỡ chữ quy chuẩn] | [Đảm bảo tính nhất quán visual] |
| Responsive | [Hành vi co giãn trên các kích thước màn hình] | [Đáp ứng Mobile First hoặc Desktop Standard] |

## 4. Bố cục Giao diện (Layout Structure)

[Mô tả cấu trúc phân vùng chính của giao diện phát hiện từ Canva]
- **Vùng Header**: [Chứa logo, menu điều hướng, thông tin profile user...]
- **Vùng Nội dung chính (Main Content)**: [Chứa form, danh sách, biểu đồ...]
- **Vùng Footer**: [Chứa thông tin bản quyền, link chính sách...]

## 5. Chi tiết Component & Trường dữ liệu (Components & Fields Specs)

| Component / Field | Loại element | Yêu cầu nhập liệu / Validation | Trạng thái hiển thị (States) | Logic tương tác / Action |
|-------------------|--------------|--------------------------------|------------------------------|--------------------------|
| [Ví dụ: Input SĐT] | Text Input | Số điện thoại VN hợp lệ (10 số), Bắt buộc | Default: Trống / Error: Viền đỏ khi sai định dạng | Nhập đủ 10 số mới kích hoạt nút 'Gửi OTP' |
| [Ví dụ: Nút Gửi OTP] | Button | N/A | Default: Disabled / Active: Màu xanh thương hiệu | Bấm nút thì call API gửi OTP, bắt đầu đếm ngược 60s |

## 6. Logic Tương tác & Luồng Chuyển trang (Interaction & Navigation Flow)

### Luồng nghiệp vụ chính (Happy Path)
1. User truy cập vào màn hình `/route-url`.
2. Hệ thống hiển thị giao diện mặc định.
3. User tương tác với các component theo thứ tự...
4. Kết quả mong đợi: Chuyển hướng sang màn hình tiếp theo `/success-route`.

### Luồng thay thế & Xử lý ngoại lệ
- **Lỗi kết nối / API Fail**: Hiển thị Toast thông báo lỗi ở góc trên bên phải, giữ nguyên data đã nhập.
- **User click nút Huỷ (Cancel)**: Hiển thị Modal xác nhận huỷ bỏ. Nếu đồng ý → chuyển hướng về `/previous-route`.

## 7. Business Rules

| ID | Rule nghiệp vụ | Ghi chú từ thiết kế |
|----|----------------|---------------------|
| BR-001 | [Mô tả rule nghiệp vụ] | [Ví dụ: Chỉ cho phép gửi OTP tối đa 3 lần/ngày] |

## 8. Acceptance Criteria (Tiêu chí nghiệm thu UI/UX)

- [ ] AC-001: Bố cục, font chữ, màu sắc khớp hoàn toàn với thiết kế Canva.
- [ ] AC-002: Các trạng thái (Hover, Active, Disabled, Loading) của các button hoạt động đúng đặc tả.
- [ ] AC-003: Giao diện hiển thị tốt trên Mobile (responsive không bị tràn viền, font size tự điều chỉnh).

## 9. Câu hỏi mở (Open Questions)

| ID | Câu hỏi cần làm rõ | Người trả lời | Deadline | Status |
|----|-------------------|---------------|----------|--------|
| Q-001 | [Các điểm mâu thuẫn hoặc thiếu thông tin trên thiết kế Canva] | [Khách hàng / Designer] | | Open |

## 10. Harness Delta

- [ ] Không có friction phát hiện trong task này
- [ ] [Mô tả friction nếu có]

## 11. Lịch sử Q&A (Q&A History)

### Round 1 — [YYYY-MM-DD HH:mm JST]
- **Q1**: [Câu hỏi làm rõ thiết kế]  
  - **Answer**: [Câu trả lời từ human/khách hàng]  
  - **Impact**: [Section nào của spec được cập nhật theo câu trả lời này]
