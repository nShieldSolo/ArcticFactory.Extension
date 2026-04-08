<div align="center">
  <h1>ArcticFactory Extension</h1>
  <p><em>Spec-Kit extensions for professional QA and project configuration</em></p>
</div>

A [spec-kit](https://github.com/github/spec-kit) extension providing advanced workflow utilities for Arctic Factory projects. It includes automated skill configuration and a powerful, senior-level QA test case generator tailored for enterprise standards.

> [!NOTE]
> All reports and generated structures from this extension are fully localized in **Vietnamese**.

## 🧩 Available Commands

| Command | Description |
|---------|-------------|
| `/specify.tester` | Phân tích spec và tự động tạo/cập nhật test plan theo chuẩn OneShop (`.specify/test-plan.md`), với tư duy QA senior. |
| `/specify.skills-check` | Tự động đọc cấu hình động (`skills.json`) để kiểm tra và cài đặt các Skills cần thiết cho dự án. |

## ⚡ Installation

### Option 1: Using Specify CLI

```bash
specify extend nShieldSolo/ArcticFactory.Extension
```

### Option 2: Add to `.specify/extensions.yml`

Add the following to your project's `.specify/extensions.yml`:

```yaml
extensions:
  - source: "nShieldSolo/ArcticFactory.Extension"
    version: "0.1.0"
```

## 📖 Command Details

### `/specify.tester`

Acts as a Senior QA Strategist. This command reads a feature specification and automates the creation of comprehensive test cases directly into a Markdown file mimicking the structure of `OneShop_WEB.xlsx`.

**Core Capabilities:**
- Coverage spans happy paths, negative paths, boundary values, state transitions, role permissions, and integration scenarios.
- Automatically initializes and manages a global `.specify/test-plan.md` file shared across all project features.
- Dynamically recalculates metrics (Critical, Major, Minor counts) and manages feature-specific "sheets" (Markdown tables).
- Follows the AAA (Arrange, Act, Assert) model.

**Usage:**
```text
/specify.tester [Tùy chọn: Tên Feature hoặc Đường dẫn tới file Spec]
```

### `/specify.skills-check`

Automates environment setup by checking and downloading necessary Spec-Kit external skills. 

**Core Capabilities:**
- Looks for `skills.json` at the project's root directory (or `.specify/`) to fetch dynamic configurations.
- Generates a default `skills.json` structure if one does not exist.
- Executes `npx skills add` to setup environment dependencies accurately.

**Usage:**
```text
/specify.skills-check
```

## 📋 Requirements

- [spec-kit](https://github.com/github/spec-kit) `>= 0.1.0`
