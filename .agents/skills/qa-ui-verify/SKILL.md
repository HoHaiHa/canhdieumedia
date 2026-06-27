---
name: qa-ui-verify
description: >
  Kiểm thử giao diện UI thực tế chạy local so với thiết kế Canva và lập báo cáo lỗi giao diện.
  Trigger khi: user nói "kiểm thử ui", "test ui so với canva", "check giao diện", "ui verify", hoặc gõ /qa-ui-verify.
---

# Skill: /qa-ui-verify
**Role**: QA  
**Mục đích**: So sánh trực quan thiết kế Canva gốc và màn hình UI thực tế chạy ở local để chỉ ra các lỗi lệch giao diện, lưu thành báo cáo phản hồi cho Developer sửa đổi.

---

## Hướng dẫn thực hiện

### Bước 1 — Thu thập đầu vào

Yêu cầu người dùng cung cấp thông tin đầu vào sau:
- Mã định danh Task (`[TASK-ID]`).
- Đường dẫn thiết kế Canva: Mặc định sẽ đọc từ `docs/tasks/[TASK-ID]/canva-design.png` (nếu đã chạy `/ba-canva-spec`). Nếu chưa có, yêu cầu người dùng cung cấp đường dẫn ảnh Canva local.
- Chọn phương án thu thập ảnh chụp màn hình UI thực tế chạy ở local:
  - **Phương án A**: Người dùng tự chạy ứng dụng local, chụp ảnh màn hình giao diện cần test và cung cấp đường dẫn tuyệt đối đến file ảnh đó.
  - **Phương án B (Tự động)**: Tự động chạy ứng dụng local và chụp ảnh màn hình bằng browser. Người dùng cần cung cấp:
    - Route cần test (ví dụ: `http://localhost:3000/login` hoặc `http://localhost:5173/profile`).
    - Lệnh khởi chạy server (ví dụ: `npm run dev` hoặc `yarn dev`).
    - Thư mục chạy lệnh (Cwd - mặc định là folder frontend).

### Bước 2 — Chụp màn hình UI thực tế chạy local (Nếu dùng Phương án B - Tự động)

Nếu dùng Phương án B:
1. Đảm bảo thư mục làm việc frontend chính xác (ví dụ: `c:\work\canhdieumedia\canhdieumedia-frontend`).
2. Khởi chạy ứng dụng local ở background thông qua việc đề xuất chạy command của người dùng. Thiết lập thời gian chờ để dev server sẵn sàng (ví dụ: `WaitMsBeforeAsync: 3000`).
3. Sử dụng **Browser subagent** truy cập vào URL route local cần kiểm tra.
4. Chờ trang load xong, thực hiện chụp ảnh màn hình giao diện thực tế.
5. Lưu ảnh chụp vào thư mục: `docs/tasks/[TASK-ID]/actual-ui.png`.
6. Sử dụng lệnh terminal thích hợp hoặc manager_task tool để tắt dev server vừa bật sau khi chụp xong để tiết kiệm tài nguyên.

*Nếu dùng Phương án A, sao chép file ảnh từ đường dẫn của người dùng vào `docs/tasks/[TASK-ID]/actual-ui.png`.*

### Bước 3 — So sánh trực quan giao diện

Sử dụng **Agent tool** để spawn subagent `ui-comparator` (sử dụng model `sonnet` để xử lý hình ảnh):

```
Agent({
  description: "ui-comparator: so sánh ảnh Canva và UI thực tế",
  prompt: "ẢNH THIẾT KẾ CANVA (DESIGN):\nfile:///c:/work/canhdieumedia/docs/tasks/[TASK-ID]/canva-design.png\n\nẢNH CHỤP MÀN HÌNH UI THỰC TẾ (ACTUAL):\nfile:///c:/work/canhdieumedia/docs/tasks/[TASK-ID]/actual-ui.png\n\nTÀI LIỆU ĐẶC TẢ GIAO DIỆN:\n(Đọc từ file docs/tasks/[TASK-ID]/requirements.md nếu tồn tại)",
  model: "sonnet"
})
```

Nhận kết quả JSON trả về chứa match score và danh sách các điểm sai lệch.

### Bước 4 — Lập báo cáo UI Feedback

Tạo file báo cáo phản hồi lỗi giao diện tại: `docs/tasks/[TASK-ID]/ui-feedback.md`.  
Sử dụng template `templates/ui-feedback.md` và điền đầy đủ các thông tin:
- Tỉ lệ tương thích (Match Score) và tổng hợp số lỗi theo độ nghiêm trọng.
- Bảng danh sách lỗi chi tiết (Visual Diffs Table): ghi rõ ID lỗi, Component bị lệch, loại lệch (font, spacing, màu...), chi tiết Design vs Actual, mức độ nghiêm trọng, và gợi ý cách fix cụ thể cho Developer.
- Đường dẫn ảnh so sánh trực quan.

### Bước 5 — Gate: Review báo cáo visual testing

Trình bày tóm tắt kết quả kiểm thử UI:

```
## Báo cáo kiểm thử giao diện cho [TASK-ID] đã hoàn tất.

- **Match Score**: [Match Score]%
- **Tổng số lỗi lệch**: [Count] lỗi
  - 🔴 Nghiêm trọng (High): [Count]
  - 🟡 Trung bình (Medium): [Count]
  - 🟢 Thấp (Low): [Count]

Báo cáo chi tiết đã được ghi nhận vào `docs/tasks/[TASK-ID]/ui-feedback.md`.

| | Lựa chọn |
|---|---------|
| A | Đồng ý kết quả — Xác nhận hoàn thành |
| B | Cần chạy kiểm thử lại (re-test) |
```

**Chờ người dùng xác nhận.**
Sau khi người dùng xác nhận, kết thúc và nhắc nhở:
- "Lập trình viên khi triển khai sửa lỗi qua `/dev-implement` hoặc sửa lỗi qua `/dev-debug` sẽ tự động quét và sửa các lỗi lệch giao diện này dựa trên file `ui-feedback.md`."

Ghi nhận lịch sử chạy skill vào `docs/tasks/[TASK-ID]/audit.md`.
