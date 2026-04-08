---
id: "speckit.arctic.health"
name: "Arctic Project Health Check"
description: "Kiểm tra sức khỏe toàn diện của project: cấu trúc, tính nhất quán của spec, và chất lượng task"
---

# /speckit.arctic.health

## Mô tả

Chạy kiểm tra sức khỏe (health check) toàn diện cho project, bao gồm:
- Kiểm tra cấu trúc thư mục spec
- Kiểm tra tính đầy đủ của từng artifact
- Kiểm tra tính nhất quán giữa các artifact với nhau
- Kiểm tra chất lượng task list

Kết quả được báo cáo bằng **tiếng Việt** với điểm số sức khỏe.

## Đầu vào

- Toàn bộ thư mục `.specify/`
- Cấu trúc project hiện tại

## Workflow

### Bước 1: Kiểm tra cấu trúc (Structure Check)

Xác nhận các file sau có tồn tại:
- [ ] `.specify/constitution.md`
- [ ] `.specify/spec.md`
- [ ] `.specify/plan.md`
- [ ] `.specify/tasks.md`

Tính điểm: mỗi file = 25 điểm, tổng tối đa 100

### Bước 2: Kiểm tra tính đầy đủ (Completeness Check)

Với mỗi artifact tìm được:

**constitution.md** — Kiểm tra có đủ:
- Nguyên tắc về chất lượng code
- Nguyên tắc về testing
- Nguyên tắc về UX/UI (nếu có frontend)
- Quy trình review

**spec.md** — Kiểm tra có đủ:
- Mô tả vấn đề/mục tiêu rõ ràng
- User stories hoặc scenarios
- Acceptance criteria
- Các ràng buộc phi chức năng

**plan.md** — Kiểm tra có đủ:
- Tech stack được chọn
- Kiến trúc hệ thống
- Các quyết định kỹ thuật quan trọng
- Rủi ro và giải pháp

**tasks.md** — Kiểm tra có đủ:
- Tasks có ID hoặc đánh số rõ ràng
- Mỗi task có mô tả đủ để implement
- Tasks được chia nhỏ hợp lý (không quá lớn)
- Thứ tự ưu tiên hoặc dependencies

### Bước 3: Kiểm tra tính nhất quán (Consistency Check)

- So sánh tên/scope trong `spec.md` và `plan.md` — có khớp nhau không?
- Các tasks trong `tasks.md` có cover đủ yêu cầu trong `spec.md` không?
- Plan có phù hợp với nguyên tắc trong `constitution.md` không?

### Bước 4: Tính điểm và tạo báo cáo

Tổng hợp các vấn đề phát hiện và tạo báo cáo.

## Output Format

```
## 🏥 Báo Cáo Sức Khỏe Project — <Tên Dự Án>

### 🎯 Điểm Sức Khỏe Tổng Thể: <X>/100

| Hạng Mục | Điểm | Trạng Thái |
|----------|------|-----------|
| Cấu trúc artifacts | X/25 | 🟢/🟡/🔴 |
| Tính đầy đủ | X/25 | 🟢/🟡/🔴 |
| Tính nhất quán | X/25 | 🟢/🟡/🔴 |
| Chất lượng tasks | X/25 | 🟢/🟡/🔴 |

**Đánh giá:** 🟢 Tốt (≥80) / 🟡 Cần cải thiện (50-79) / 🔴 Nguy hiểm (<50)

---

### ❌ Vấn Đề Phát Hiện

**🔴 Nghiêm trọng:**
- <danh sách vấn đề cần xử lý ngay>

**🟡 Cần cải thiện:**
- <danh sách vấn đề nên xử lý>

**💡 Gợi ý:**
- <danh sách gợi ý để cải thiện>

---

### ✅ Điểm Mạnh

- <những gì đang làm tốt>

---

### 🔧 Hành Động Đề Xuất (theo thứ tự ưu tiên)

1. <hành động cấp thiết nhất>
2. <hành động tiếp theo>
3. <hành động dài hạn>
```

## Tiêu chí hoàn thành (Exit Criteria)

- Báo cáo đã được in đầy đủ
- Tất cả vấn đề được phân loại theo mức độ nghiêm trọng
- Điểm sức khỏe đã được tính
- Không sửa bất kỳ file nào (read-only)

## Lưu ý

- Lệnh này **read-only** — không tạo hoặc sửa file
- Báo cáo bằng **tiếng Việt**
- Thang điểm: 🟢 ≥80, 🟡 50-79, 🔴 <50
