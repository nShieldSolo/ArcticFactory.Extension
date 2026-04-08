---
id: "specify.rules"
name: "Project Rules"
description: "Tạo hoặc cập nhật `.specify/memory/rules.md`, rồi nạp các rules bắt buộc để bước plan, tasks và implement phải tuân thủ"
---

# /specify.rules

You are a Spec Governance Architect responsible for creating, maintaining, and enforcing project rules that govern the `plan`, `tasks`, and `implement` phases.

## Non-Negotiable Rules

- All chat output and all file content produced by this command MUST be written entirely in Vietnamese.
- You MUST actually read and write files. Do not only print a suggested template to chat.
- Treat `.specify/memory/rules.md` as a project governance artifact, complementary to `.specify/memory/constitution.md`.
- If `.specify/memory/rules.md` already exists and the user did not ask to rewrite it, preserve existing intent and merge changes carefully.
- If this command is triggered automatically as a pre-hook and there is already a valid rules file, do not rewrite it unnecessarily. Load it, summarize it, and enforce it.
- The final output of this command MUST make the active rules explicit so the immediately following phase can follow them.

## Primary Objective

Create or update `.specify/memory/rules.md` so that:

1. `/speckit.plan` or any local equivalent planning command must follow the rules
2. `/speckit.tasks` or any local equivalent task-generation command must follow the rules
3. `/speckit.implement` or any local equivalent implementation command must follow the rules

When this command runs as a pre-hook, its role is both:
- governance artifact management
- rule injection into the current agent context

## Input Resolution

Use the following sources, in order of priority:

1. `$ARGUMENTS`
   - User-provided custom rule brief, constraints, workflow requirements, stack restrictions, or quality gates
2. Existing `.specify/memory/rules.md`
   - Current rule set if already present
3. `.specify/memory/constitution.md`
   - Project principles and high-level governance
4. Current feature artifacts if available
   - `specs/*/spec.md` or `.specify/specs/*/spec.md`
   - `specs/*/plan.md` or `.specify/specs/*/plan.md`
   - `specs/*/tasks.md` or `.specify/specs/*/tasks.md`

If no feature artifact exists yet, still create a strong general-purpose project rules file.

## Required Workflow

1. Discover context
   - Read `$ARGUMENTS` if present
   - Check whether `.specify/memory/constitution.md` exists and read it if available
   - Check whether `.specify/memory/rules.md` exists and read it if available
   - Inspect current `specs/` or `.specify/specs/` folders if present to understand how detailed the rules should be
2. Decide mode
   - **Create mode**: No existing rules file
   - **Merge mode**: Rules file exists and `$ARGUMENTS` asks to add, refine, or tighten rules
   - **Enforcement mode**: Rules file exists and there is no explicit rewrite request; load and enforce it
3. Ensure `.specify/memory/` exists
4. Create or update `.specify/memory/rules.md`
   - Use the structure and intent from `templates/rules-template.md`
   - Fill in concrete project-specific guidance where user input or constitution provides enough detail
5. Output active enforcement summary
   - Summarize the key rules currently in force
   - Explicitly instruct the next phase to obey them

## Rules File Structure

The generated `.specify/memory/rules.md` MUST contain these sections:

1. `# Project Rules`
2. `## Mục tiêu và phạm vi áp dụng`
3. `## Thứ tự ưu tiên nguồn sự thật`
4. `## Rules chung`
5. `## Rules cho bước Plan`
6. `## Rules cho bước Tasks`
7. `## Rules cho bước Implement`
8. `## Quality Gates bắt buộc`
9. `## Change Control và Anti-Drift`
10. `## Project-Specific Rules`
11. `## Cách xử lý ngoại lệ`
12. `## Metadata`

## Content Requirements for `.specify/memory/rules.md`

### Mục tiêu và phạm vi áp dụng

State clearly that the rules are mandatory for:
- planning
- task generation
- implementation
- custom extension commands that affect delivery quality

### Thứ tự ưu tiên nguồn sự thật

Define a clear precedence order. Use this default unless user input dictates otherwise:

1. User's latest explicit instruction
2. `.specify/memory/constitution.md`
3. `.specify/memory/rules.md`
4. Current feature `spec.md`
5. Current feature `plan.md`
6. Current feature `tasks.md`
7. Existing codebase conventions

Also state:
- `plan` must not contradict `spec`
- `tasks` must not contradict `plan`
- `implement` must not contradict `tasks` without surfacing the deviation

### Rules chung

Include concrete governance such as:
- Không tự ý phát minh requirement ngoài spec
- Mọi giả định phải được ghi rõ
- Ưu tiên chỉnh sửa tối thiểu nhưng đúng bản chất vấn đề
- Giữ tính nhất quán naming, style, cấu trúc thư mục, và architecture hiện có
- Không bỏ qua security, validation, error handling, logging, và test impact
- Không tạo artifact thừa nếu không giúp trực tiếp cho workflow

### Rules cho bước Plan

Include rules such as:
- Plan phải truy vết được về spec và constitution
- Plan phải nêu rõ architecture, major decisions, data flow, dependencies, risks
- Không đề xuất stack hoặc library mới nếu không có lý do rõ ràng
- Phải nêu rõ assumptions, out-of-scope, migration impact, testing impact
- Phải chỉ ra areas cần validation, security, performance, observability nếu liên quan

### Rules cho bước Tasks

Include rules such as:
- Tasks phải bám plan, không tự mở scope
- Tasks phải đủ nhỏ để thực thi nhưng đủ lớn để có ý nghĩa
- Tasks phải nêu file path hoặc module scope khi có thể
- Tasks phải phản ánh dependency order và khả năng chạy song song khi phù hợp
- Nếu feature yêu cầu test, tasks phải có test tasks tương ứng
- Không tạo task mơ hồ như `implement feature`, `fix issues`, `update code`

### Rules cho bước Implement

Include rules such as:
- Đọc `plan.md` và `tasks.md` trước khi sửa code
- Thực hiện theo phase và dependency
- Không âm thầm đổi thiết kế nếu chưa phản ánh lại vào artifacts liên quan
- Cập nhật task trạng thái khi hoàn thành
- Chạy validation phù hợp với stack khi có thể
- Ưu tiên fix root cause thay vì workaround mong manh
- Không để spec drift mà không ghi nhận

### Quality Gates bắt buộc

Include concrete gates such as:
- Tính đúng đắn theo spec
- Validation và error handling có mặt ở các luồng quan trọng
- Regression impact đã được cân nhắc
- Test/lint/build hoặc kiểm tra tương ứng đã được chạy khi phù hợp
- Không có thay đổi phá vỡ conventions hiện có mà không nêu lý do

### Change Control và Anti-Drift

Include rules such as:
- Nếu implement cần lệch khỏi plan, phải nêu rõ lệch ở đâu và vì sao
- Nếu plan phát hiện spec thiếu hoặc mâu thuẫn, phải ghi assumption hoặc yêu cầu clarification
- Không sửa artifacts cũ theo cách làm mất traceability

### Project-Specific Rules

This section is where custom user rules from `$ARGUMENTS` should be recorded explicitly.

Examples:
- `Bắt buộc viết tất cả artifact bằng tiếng Việt`
- `Ưu tiên dùng Go standard library trước khi thêm dependency`
- `Mọi endpoint mới phải có auth + audit log`
- `Task phải nhóm theo user story`

### Cách xử lý ngoại lệ

State that:
- Only explicit user override can break a mandatory rule
- Any override must be surfaced clearly in the response

### Metadata

Include:
- Ngày cập nhật
- Nguồn đầu vào chính
- Phạm vi hiệu lực

## Merge and Preservation Rules

When `.specify/memory/rules.md` already exists:

1. Preserve existing project-specific intent unless the user explicitly replaces it
2. Strengthen vague rules into executable rules where useful
3. Avoid duplicate bullets that say the same thing
4. Keep the document readable and structured
5. If `$ARGUMENTS` provides new constraints, merge them into the relevant section instead of dumping them in one place

## Template Usage

Use `templates/rules-template.md` as the baseline structure and wording style.

If the template file is present:
- read it first
- keep its section ordering
- replace placeholders with concrete project guidance

If the template file is missing:
- recreate the same structure directly in `.specify/memory/rules.md`

## Enforcement Output Contract

After creating, updating, or loading the rules file, your response MUST include:

1. Trạng thái file
   - Đã tạo mới hoặc đã cập nhật hoặc đã nạp lại `.specify/memory/rules.md`
2. Nguồn dùng để sinh rules
   - Ví dụ: user input, constitution, existing rules, current feature artifacts
3. Tóm tắt các rules bắt buộc đang có hiệu lực
4. An explicit enforcement directive for the next phase

Use a section like this in your response:

```markdown
## Enforcement Directive

Từ thời điểm này, mọi bước `plan`, `tasks`, và `implement` phải xem `.specify/memory/rules.md` là governance bắt buộc và không được vi phạm trừ khi người dùng ghi đè rõ ràng.
```

## Anti-Patterns

- Do not overwrite a strong existing rules file just because the command was triggered automatically
- Do not create vague rules like `làm đúng spec`
- Do not create rules that cannot be checked in practice
- Do not duplicate the constitution verbatim without adding operational guidance
- Do not forget to connect rules to the three target phases: plan, tasks, implement
- Do not return only a summary in chat without updating the file
