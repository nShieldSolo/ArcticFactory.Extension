# Project Rules

## Mục tiêu và phạm vi áp dụng

- Tài liệu này định nghĩa các rules bắt buộc cho toàn bộ workflow `plan`, `tasks`, và `implement`.
- Các rules này phải được đọc cùng với `.specify/memory/constitution.md`.
- Khi có xung đột, thứ tự ưu tiên nguồn sự thật phải được áp dụng như mô tả bên dưới.

## Thứ tự ưu tiên nguồn sự thật

1. Chỉ thị rõ ràng mới nhất từ người dùng
2. `.specify/memory/constitution.md`
3. `.specify/memory/rules.md`
4. `spec.md` của feature hiện tại
5. `plan.md` của feature hiện tại
6. `tasks.md` của feature hiện tại
7. Codebase conventions hiện có

## Rules chung

- Không tự ý phát minh requirement ngoài spec.
- Mọi giả định ảnh hưởng đến solution phải được ghi rõ.
- Ưu tiên thay đổi tối thiểu nhưng giải quyết đúng root cause.
- Tôn trọng conventions hiện có về naming, architecture, và tổ chức thư mục.
- Không bỏ qua validation, error handling, security, logging, và test impact ở các luồng quan trọng.
- Không tạo thêm artifacts nếu chúng không phục vụ trực tiếp cho workflow hoặc traceability.

## Rules cho bước Plan

- Plan phải truy vết được về spec và constitution.
- Plan phải nêu rõ kiến trúc, major decisions, rủi ro, dependencies, và assumptions.
- Không thêm tech stack hoặc dependency mới nếu không có lý do rõ ràng.
- Phải nêu rõ các điểm cần test, security review, performance consideration, và migration impact nếu có.

## Rules cho bước Tasks

- Tasks phải bám plan, không tự mở scope.
- Tasks phải rõ ràng, có action cụ thể, tránh mơ hồ.
- Tasks nên nêu file path, module, hoặc vùng ảnh hưởng khi có thể.
- Tasks phải phản ánh dependency order và khả năng chạy song song nếu phù hợp.
- Nếu feature cần test, task list phải có test tasks tương ứng.

## Rules cho bước Implement

- Luôn đọc `plan.md` và `tasks.md` trước khi sửa code.
- Thực hiện theo phase và dependency đã được xác định.
- Không âm thầm đổi thiết kế mà không phản ánh lại vào artifacts liên quan.
- Cập nhật trạng thái task khi hoàn thành.
- Chạy validation phù hợp với stack nếu có thể.
- Ưu tiên fix root cause, không vá tạm nếu có thể tránh.

## Quality Gates bắt buộc

- Thay đổi phải khớp với spec và plan hiện hành.
- Luồng chính phải có validation và error handling phù hợp.
- Regression impact phải được cân nhắc.
- Test/lint/build hoặc kiểm tra tương ứng phải được chạy khi hợp lý.
- Không phá conventions hiện có mà không nêu lý do.

## Change Control và Anti-Drift

- Nếu implement lệch khỏi plan, phải nêu rõ lệch ở đâu và vì sao.
- Nếu plan phát hiện spec thiếu, phải ghi assumption hoặc yêu cầu clarification.
- Không sửa artifacts theo cách làm mất traceability.

## Project-Specific Rules

- [Điền rules riêng của project hoặc từ user input tại đây]

## Cách xử lý ngoại lệ

- Chỉ được phá vỡ rule khi người dùng override rõ ràng.
- Mọi override phải được nêu rõ trong phản hồi.

## Metadata

- Ngày cập nhật: [YYYY-MM-DD]
- Nguồn đầu vào chính: [User input / constitution / existing rules / feature artifacts]
- Phạm vi hiệu lực: [Toàn project hoặc feature cụ thể]
