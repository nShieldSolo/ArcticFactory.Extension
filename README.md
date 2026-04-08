# ArcticFactory.Extension

Một [spec-kit](https://github.com/github/spec-kit) extension cung cấp các lệnh hỗ trợ workflow cho dự án Arctic Factory, với báo cáo bằng **tiếng Việt**.

## 🧩 Lệnh Có Sẵn

| Lệnh | Mô tả |
|------|--------|
| `/speckit.arctic.status` | Báo cáo tiến độ dự án bằng tiếng Việt |
| `/speckit.arctic.health` | Kiểm tra sức khỏe toàn diện project |
| `/speckit.arctic.drift` | Phát hiện sai lệch giữa code và spec |

## ⚡ Cài đặt

### Cách 1: Dùng Specify CLI

```bash
specify extend nShieldSolo/ArcticFactory.Extension
```

### Cách 2: Thêm vào `.specify/extensions.yml`

```yaml
extensions:
  - source: "nShieldSolo/ArcticFactory.Extension"
    version: "0.1.0"
```

## 📖 Mô Tả Từng Lệnh

### `/speckit.arctic.status`

Đọc tất cả spec artifacts trong `.specify/` và tạo báo cáo tiến độ bằng tiếng Việt. Cho biết phase hiện tại, số task hoàn thành, và bước tiếp theo.

```
/speckit.arctic.status
```

### `/speckit.arctic.health`

Kiểm tra toàn diện project và chấm điểm sức khỏe (0-100):
- Kiểm tra cấu trúc artifacts
- Kiểm tra tính đầy đủ từng file
- Kiểm tra tính nhất quán giữa các artifacts

```
/speckit.arctic.health
```

### `/speckit.arctic.drift`

Phân tích sai lệch giữa code đã implement và spec hiện tại. Phát hiện:
- Yêu cầu chưa được implement
- Code được viết ngoài spec
- Logic có thể sai

```
/speckit.arctic.drift
```

## 📋 Yêu Cầu

- [spec-kit](https://github.com/github/spec-kit) >= 0.1.0

## 📁 Cấu Trúc Project

```
ArcticFactory.Extension/
├── extension.yml           # Extension manifest
├── commands/
│   ├── status.md           # Lệnh báo cáo tiến độ
│   ├── health.md           # Lệnh kiểm tra sức khỏe
│   └── drift.md            # Lệnh phát hiện drift
├── README.md
├── CHANGELOG.md
└── LICENSE
```

## 📄 License

[MIT](LICENSE)
