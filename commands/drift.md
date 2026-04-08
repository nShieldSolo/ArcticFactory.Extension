---
id: "speckit.arctic.drift"
name: "Arctic Spec Drift Detector"
description: "Phát hiện sai lệch (drift) giữa code đã implement và spec hiện tại"
---

# /speckit.arctic.drift

## Mô tả

Phân tích sự **sai lệch (drift)** giữa code đã được implement và những gì spec yêu cầu.

Spec drift xảy ra khi:
- Code implement tính năng không có trong spec
- Code bỏ qua yêu cầu trong spec
- Code implement sai logic so với spec mô tả

Kết quả báo cáo bằng **tiếng Việt**.

## Đầu vào

- `.specify/spec.md` — Yêu cầu gốc
- `.specify/plan.md` — Kế hoạch kỹ thuật
- `.specify/tasks.md` — Danh sách task
- Mã nguồn của project (files có extension phổ biến: `.ts`, `.tsx`, `.js`, `.py`, `.cs`, `.go`, v.v.)

## Workflow

### Bước 1: Trích xuất yêu cầu từ spec

Đọc `spec.md` và liệt kê tất cả:
- User stories / scenarios
- Tính năng được đề cập
- Acceptance criteria
- Ràng buộc phi chức năng (performance, security, v.v.)

### Bước 2: Trích xuất những gì đã implement

Scan các file source code trong project:
- Tìm các function, class, API endpoint, component chính
- Liệt kê các tính năng đã được code

### Bước 3: Đối chiếu (Cross-reference)

So sánh hai danh sách:

**Spec có nhưng code chưa có (Missing Implementation):**
- Những yêu cầu trong spec chưa thấy code implement

**Code có nhưng spec không đề cập (Undocumented Implementation):**
- Những thứ được code mà spec không yêu cầu

**Có thể sai logic (Potential Misalignment):**
- Những điểm cần xem xét kỹ hơn vì logic có thể không khớp

### Bước 4: Phân loại mức độ

Mỗi sai lệch được phân loại:
- 🔴 **Cao** — ảnh hưởng trực tiếp đến chức năng chính
- 🟡 **Trung bình** — ảnh hưởng đến trải nghiệm người dùng hoặc hiệu năng
- 🟢 **Thấp** — sai lệch nhỏ, có thể tạm chấp nhận

### Bước 5: Tạo báo cáo

## Output Format

```
## 🔍 Báo Cáo Spec Drift — <Tên Dự Án>
Ngày kiểm tra: <ngày hôm nay>

### 📊 Tổng Quan

| Loại | Số Lượng |
|------|---------|
| Yêu cầu trong spec | X |
| Đã implement | Y |
| Chưa implement | Z |
| Implement ngoài spec | W |
| Điểm mức độ phủ | X% |

---

### 🔴 Chưa Implement (Ưu tiên cao)

Những yêu cầu trong spec CHƯA được implement:

1. **[Tên yêu cầu]**
   - Spec yêu cầu: <mô tả từ spec>
   - Mức độ: 🔴 Cao / 🟡 Trung bình
   - Đề xuất: <lệnh hoặc hành động>

---

### 🟡 Implement Ngoài Spec

Những thứ được code nhưng không có trong spec:

1. **[Tên tính năng/file]**
   - Mô tả: <những gì code đang làm>
   - Rủi ro: <có thể là over-engineering, security risk, v.v.>
   - Đề xuất: Cập nhật spec HOẶC xóa code

---

### ⚠️ Cần Xem Xét Thêm

Những điểm có thể sai logic — cần kiểm tra thủ công:
- <danh sách điểm cần kiểm tra>

---

### ✅ Đã Implement Đúng Spec

- <danh sách yêu cầu đã implement đúng>

---

### 🔧 Hành Động Đề Xuất

**Ngay lập tức:**
1. <task cấp bách>

**Trong sprint này:**
1. <task quan trọng>

**Dài hạn:**
1. <task cải thiện>
```

## Tiêu chí hoàn thành (Exit Criteria)

- Báo cáo drift đã được in đầy đủ
- Tất cả sai lệch được phân loại theo mức độ
- Không sửa file nào (read-only)
- Nếu không có sai lệch, thông báo rõ ràng

## Lưu ý

- Lệnh này **read-only** — không sửa code hoặc spec
- Báo cáo bằng **tiếng Việt**
- Nếu thiếu `spec.md`, yêu cầu chạy `/speckit.specify` trước
- Phân tích dựa trên best-effort — cần xem xét thủ công các điểm phức tạp
