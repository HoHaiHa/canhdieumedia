---
name: ba-canva-spec
description: >
  Đọc thiết kế giao diện từ Canva và yêu cầu thô để soạn đặc tả nghiệp vụ giao diện chi tiết.
  Trigger khi: user nói "đọc canva", "viết spec từ canva", "canva spec", "thiết kế canva", hoặc gõ /ba-canva-spec.
---

# Skill: /ba-canva-spec
**Role**: Business Analyst  
**Mục đích**: Phân tích ảnh thiết kế Canva và yêu cầu thô để soạn tài liệu đặc tả giao diện & nghiệp vụ chi tiết cho lập trình viên.

---

## Hướng dẫn thực hiện

### Bước 1 — Thu thập đầu vào

Yêu cầu người dùng cung cấp thông tin đầu vào sau:
- Mã định danh Task (`[TASK-ID]`).
- Yêu cầu nghiệp vụ thô (mô tả tính năng, mong muốn).
- Một trong hai phương thức sau để đọc thiết kế Canva:
  - **Phương án A**: Đường dẫn tuyệt đối đến file ảnh chụp màn hình thiết kế Canva đã lưu local.
  - **Phương án B**: Link Canva Design công khai (URL public).

### Bước 2 — Chụp màn hình thiết kế Canva (Nếu dùng Phương án B - Link Canva)

Nếu người dùng cung cấp link Canva public:
1. Sử dụng **Browser subagent** truy cập link Canva đó.
2. Chờ trang load xong, thực hiện chụp ảnh màn hình Canva.
3. Lưu ảnh chụp màn hình thiết kế vào thư mục nhiệm vụ: `docs/tasks/[TASK-ID]/canva-design.png` (hoặc tạo thư mục `docs/tasks/[TASK-ID]` nếu chưa có).
4. Sử dụng đường dẫn ảnh này cho bước tiếp theo.

*Nếu dùng Phương án A, sao chép file ảnh từ đường dẫn của người dùng vào `docs/tasks/[TASK-ID]/canva-design.png`.*

### Bước 3 — Phân tích thiết kế Canva

Sử dụng **Agent tool** để spawn subagent `canva-reader` (sử dụng model `sonnet` để xử lý hình ảnh):

```
Agent({
  description: "canva-reader: đọc ảnh thiết kế và yêu cầu thô",
  prompt: "YÊU CẦU NGHIỆP VỤ THÔ:\n[Mô tả yêu cầu thô từ Bước 1]\n\nẢNH THIẾT KẾ CANVA:\nfile:///c:/work/canhdieumedia/docs/tasks/[TASK-ID]/canva-design.png",
  model: "sonnet"
})
```

Nhận kết quả JSON trả về từ subagent.

### Bước 4 — Gate: Trình bày hiểu biết ban đầu + Hỏi làm rõ

Dựa trên JSON từ subagent, hiển thị tóm tắt hiểu biết của bạn về giao diện và liệt kê các câu hỏi nghiệp vụ/UI chưa rõ.  
**Không tự ý giả định** các logic tương tác phức tạp hoặc nguồn dữ liệu.

Trình bày theo định dạng:

```
## Tôi hiểu thiết kế màn hình này như sau:

- **Tên màn hình**: [Tên màn hình]
- **Bố cục chính (Layout)**: [Mô tả layout]
- **Các thành phần giao diện chính**:
  1. [Component 1] — [Logic cơ bản]
  2. [Component 2] — [Logic cơ bản]

## Trước khi tôi soạn spec chi tiết, hãy làm rõ các câu hỏi sau từ thiết kế:

| # | Câu hỏi từ thiết kế Canva | Lựa chọn gợi ý |
|---|---------------------------|----------------|
| 1 | [Câu hỏi về logic của component X] | _(điền vào)_ |
| 2 | [Câu hỏi về responsive hoặc edge cases giao diện] | _(điền vào)_ |
| 3 | [Câu hỏi về luồng chuyển trang khi click nút Y] | A: Chuyển về màn hình ___ / B: Mở Modal / C: Khác: ___ |
```

**Chờ người dùng trả lời (human confirm) trước khi tiếp tục.**

### Bước 5 — Soạn Đặc tả Giao diện & Nghiệp vụ (Canva Spec Document)

Sau khi nhận được câu trả lời từ người dùng, tạo file đặc tả nhiệm vụ tại: `docs/tasks/[TASK-ID]/requirements.md`.  
Sử dụng template `templates/task-doc-canva-requirements.md` làm khung sườn và điền đầy đủ các phần:
- Bối cảnh & Mục tiêu giao diện.
- Ràng buộc & Quy tắc Thiết kế Canva (ghi nhận Brand color, Font family từ thiết kế).
- Bố cục Giao diện (Layout Structure).
- Chi tiết Component & Trường dữ liệu (phân tích chi tiết từng trường nhập liệu, trạng thái component, logic hover/active/disabled).
- Logic Tương tác & Luồng Chuyển trang (Happy path + Exception flows).
- Các Business Rules suy ra từ thiết kế hoặc đã làm rõ.
- Danh sách Acceptance Criteria (AC).
- Lịch sử Q&A (ghi nhận các câu hỏi và câu trả lời ở Bước 4 làm căn cứ).

Đồng thời, tạo/cập nhật tài liệu baseline màn hình tương ứng tại `docs/screens/[feature]/screen.md` sử dụng template `templates/baseline-screen.md`.

### Bước 6 — Gate cuối: Review và xác nhận đặc tả

Trình bày tài liệu đặc tả đã viết dưới dạng tóm tắt các điểm quan trọng và hỏi:

```
## Đặc tả giao diện dựa trên Canva đã soạn xong tại `docs/tasks/[TASK-ID]/requirements.md`.

Hãy xác nhận các thông tin cuối:
- Các quy định CSS (màu, font) đã khớp thiết kế?
- Có hành vi tương tác nào chưa được đặc tả?
- Đã đủ thông tin để Developer triển khai chưa?

Nếu đã sẵn sàng, hãy xác nhận để lưu spec. Bạn có thể tiếp tục với /ba-user-story hoặc đưa vào /dev-analyze để lên phương án code.
```

**Chờ human xác nhận.**
Ghi nhận lịch sử chạy skill vào `docs/tasks/[TASK-ID]/audit.md`.

---

## Lưu ý quan trọng
- Báo cáo rõ ràng mọi điểm khác nhau giữa mô tả nghiệp vụ thô và giao diện Canva được thiết kế. Giao diện thực tế được coi là ground truth cho phần Layout & Visual.
- Luôn giữ tính nhất quán của Brand guidelines (color palette, typography) trích xuất được từ Canva.
