---
id: "speckit.arctic.status"
name: "Arctic Status Report"
description: "Báo cáo tiến độ dự án bằng tiếng Việt, tổng hợp từ spec artifacts"
---

# /speckit.arctic.status

## Mô tả

Đọc toàn bộ spec artifacts hiện có trong project và tạo một **báo cáo tiến độ bằng tiếng Việt**. Lệnh này hữu ích để nhanh chóng nắm bắt trạng thái hiện tại của dự án mà không cần đọc từng file riêng lẻ.

## Đầu vào

Tìm và đọc các file sau (nếu tồn tại):

- `.specify/spec.md` — Tài liệu yêu cầu
- `.specify/plan.md` — Kế hoạch kỹ thuật
- `.specify/tasks.md` — Danh sách nhiệm vụ
- `.specify/constitution.md` — Nguyên tắc dự án
- Bất kỳ file nào trong `.specify/` có suffix `.md`

## Workflow

1. Quét thư mục `.specify/` để tìm tất cả artifacts
2. Đọc nội dung từng file tìm được
3. Từ `tasks.md`, đếm số task đã hoàn thành (✅/[x]) vs chưa hoàn thành (⬜/[ ])
4. Xác định phase hiện tại của dự án (constitution → specify → plan → tasks → implement)
5. Tổng hợp và tạo báo cáo theo format bên dưới

## Output Format

In ra console (không tạo file) một báo cáo theo format:

```
## 📊 Báo Cáo Tiến Độ — <Tên Dự Án>
Ngày báo cáo: <ngày hôm nay>

### 🗺️ Phase Hiện Tại
<Tên phase hiện tại và mô tả ngắn>

### 📋 Tóm Tắt Artifacts
| Artifact | Trạng Thái | Mô Tả Ngắn |
|----------|-----------|------------|
| Constitution | ✅ Có / ❌ Chưa có | <tóm tắt 1 dòng nếu có> |
| Spec | ✅ Có / ❌ Chưa có | <tóm tắt 1 dòng nếu có> |
| Plan | ✅ Có / ❌ Chưa có | <tóm tắt 1 dòng nếu có> |
| Tasks | ✅ Có / ❌ Chưa có | <X/Y tasks hoàn thành> |

### ✅ Tiến Độ Task
Hoàn thành: <X>/<Y> task (<Z>%)
[████████░░] <Z>%

Tasks đã xong:
- <danh sách task hoàn thành>

Tasks còn lại:
- <danh sách task chưa làm>

### 🎯 Bước Tiếp Theo Đề Xuất
<Hướng dẫn cụ thể bước tiếp theo cần làm>
```

## Tiêu chí hoàn thành (Exit Criteria)

- Báo cáo đã được in ra với đầy đủ thông tin
- Không tạo hoặc sửa bất kỳ file nào (read-only)
- Số liệu task phải chính xác dựa trên nội dung file

## Lưu ý

- Đây là lệnh **read-only** — chỉ đọc, không ghi
- Ngôn ngữ báo cáo: **tiếng Việt**
- Nếu `.specify/` chưa tồn tại, thông báo và hướng dẫn chạy `/speckit.constitution` để bắt đầu
