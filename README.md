# ArcticFactory Extension

Spec-Kit extension cho workflow Arctic Factory, tập trung vào:

- artifact và báo cáo bằng tiếng Việt
- QA planning chi tiết
- project rules governance cho `plan`, `tasks`, `implement`
- helper commands cho setup workflow

> [!NOTE]
> Extension này dùng namespace command `speckit.arc.*` để khớp với schema command name hiện tại của upstream `spec-kit`.

## Available Commands

| Command | Description |
|---------|-------------|
| `/speckit.arc.skills-check` | Đọc `skills.json`, cài các skills cần thiết, và báo cáo kết quả bằng tiếng Việt. |
| `/speckit.arc.rules` | Tạo hoặc cập nhật `.specify/memory/rules.md`. Nếu file này đã tồn tại thì hook sẽ nạp và enforce rules cho `plan`, `tasks`, và `implement`; nếu chưa có thì workflow vẫn tiếp tục bình thường. |
| `/speckit.arc.tester` | Phân tích spec và tạo/cập nhật `.specify/test-plan.md` với coverage theo tư duy QA senior. |

## Rules Governance

Command `/speckit.arc.rules` dùng template nội bộ tại:

```text
templates/rules-template.md
```

để tạo artifact đích trong project:

```text
.specify/memory/rules.md
```

Manifest cũng khai báo các pre-hook:

- `before_plan`
- `before_tasks`
- `before_implement`

Mục tiêu là nạp rules trước khi sang phase tiếp theo nếu project đã có `.specify/memory/rules.md`. Nếu chưa có file này, workflow vẫn tiếp tục bình thường và không bị ép tạo rules.

## Installation

### Cài từ release ZIP

```bash
specify extension add arc --from https://github.com/nShieldSolo/ArcticFactory.Extension/releases/download/v0.0.1/arctic-factory-extension-v0.0.1.zip
```

### Cài local extension vào project hiện tại

```bash
specify extension add arc --dev .
```

### Cài local extension từ thư mục khác

```bash
specify extension add arc --dev /path/to/ArcticFactory.Extension
```

## Command Details

### `/speckit.arc.skills-check`

Đọc `skills.json` trong root project hoặc `.specify/`, sau đó chạy lệnh cài skills cần thiết.

Ví dụ:

```text
/speckit.arc.skills-check
```

### `/speckit.arc.rules`

Tạo hoặc cập nhật `.specify/memory/rules.md` để xác định các nguyên tắc bắt buộc cho:

- bước plan
- bước tasks
- bước implement

Command này có 4 mode thực tế:

- `create mode`: chưa có rules file và người dùng chủ động yêu cầu tạo rules
- `merge mode`: có rules file và người dùng muốn bổ sung/chỉnh rules
- `enforcement mode`: chạy như pre-hook, nạp rules hiện có và ép phase kế tiếp tuân thủ
- `no-op mode`: hook chạy nhưng project chưa có `.specify/memory/rules.md`, nên không enforce gì thêm

Ví dụ:

```text
/speckit.arc.rules Tất cả tasks phải nhóm theo user story, mọi endpoint mới phải có validation, auth và audit log, implement không được thêm dependency mới nếu chưa có lý do rõ ràng.
```

### `/speckit.arc.tester`

Phân tích spec và tạo/cập nhật `.specify/test-plan.md` theo format bảng OneShop. Prompt này đã được tối ưu để AI nghĩ như tester senior:

- happy path, alternate path, negative path
- boundary, empty/null, permission, state transition
- integration, regression, security-minded coverage
- recompute summary từ nội dung thực tế trong file

Ví dụ:

```text
/speckit.arc.tester specs/001-example/spec.md
```

## Project Structure

```text
ArcticFactory.Extension/
├── extension.yml
├── commands/
│   ├── skills-check.md
│   ├── rules.md
│   └── tester.md
├── templates/
│   └── rules-template.md
├── README.md
├── CHANGELOG.md
└── LICENSE
```

## Upstream Notes

Từ tài liệu upstream `spec-kit`, extension system hiện hỗ trợ:

- `extension.yml`
- command markdown files
- optional config templates
- lifecycle hooks như `before_plan`, `before_tasks`, `before_implement`

Nguồn tham khảo:

- Spec Kit repository: https://github.com/github/spec-kit
- Extension API reference: https://raw.githubusercontent.com/github/spec-kit/main/extensions/EXTENSION-API-REFERENCE.md

Tài liệu API này mô tả manifest schema, command file format, hook events, và catalog/install flow. Repo này hiện dùng pattern `speckit.{extension-id}.{command}` với `extension.id = arc`.

## Requirements

- [spec-kit](https://github.com/github/spec-kit) `>= 0.1.0`
