# Testing & Engineering Standards

## Contract trước implementation

Xác định input, output, error contract, business rules, invariants, ownership và side effects. Phân biệt observable behavior với cách triển khai. Code gốc và tests gốc có thể sai hoặc thiếu; kiểm tra với tài liệu nghiệp vụ và callers. Behavioral equivalence không đồng nghĩa correctness.

## Các mức kiểm chứng

| Mức | Mục tiêu |
|---|---|
| Unit | Function/package cô lập, input và kết quả xác định |
| Integration | Phối hợp giữa các thành phần thật hoặc dependency thích hợp, ví dụ PostgreSQL/MQTT |
| System | Luồng hoàn chỉnh và business outcome của hệ thống |

Unit test không chứng minh integration hoặc system đúng. httptest có thể kiểm tra handler/router mà không cần mở socket thật; phân loại theo phạm vi và dependency.

## Workflow

- Đọc go.mod, phiên bản Go và dependency tại source commit, cũng như toolchain Lab. Không tự thay đổi phiên bản.
- Bắt đầu happy path; bổ sung empty/nil, giá trị biên, malformed input, lỗi dependency và invariant phù hợp. Với string parser, cân nhắc input ngắn và ký tự ngoài whitelist. Với error wrapping, kiểm tra errors.Is nếu contract yêu cầu.
- Ưu tiên standard library testing, table-driven tests khi hữu ích, t.Run cho test cases và httptest cho HTTP. Fake/stub/mock khi giúp cô lập dependency; integration test cho behavior phụ thuộc hệ thống thật.
- Test expectation dựa trên contract, không sửa expected output chỉ để implementation pass. Nếu test sai, giải thích và review riêng.
- Chạy gofmt, go test ./... và go vet ./... từ module phù hợp; có thể chạy go test ./practices/<slug> -v cho bài cụ thể. Go test -race ./... cho concurrency khi nền tảng/toolchain hỗ trợ.
- Lưu command, môi trường/Go version, commit hoặc working tree, thời điểm, kết quả pass/fail/blocked/not run, lỗi và phạm vi. Phân biệt kết quả người học báo với kết quả AI trực tiếp quan sát.
- Không nói đã pass nếu chỉ static review, test chưa chạy hoặc không có bằng chứng. Không khẳng định coverage/correctness toàn bộ dựa trên vài test.

## Review kỹ thuật

Ưu tiên đơn giản, rõ ràng, idiomatic Go. Xem error handling, validation, type safety, data ownership, mutability, dependency boundaries, readability, maintainability và side effects. Giải thích vì sao, không chỉ đề xuất sửa syntax.

Security: làm rõ trust boundary, identity, input validation và không lộ secret. Không tự viết thuật toán mật mã production; dùng thư viện phù hợp. Concurrency: xác định shared state, synchronization, ownership, cancellation, race/deadlock/leak. Persistence: transaction, constraint, idempotency, consistency và failure handling. Không thử nghiệm với database/broker production.

## Review evidence

Ghi trong review.md: contract được kiểm tra, tests đã chạy/chưa chạy, kết quả, trường hợp còn thiếu, khác biệt với code gốc, hạn chế, mức hỗ trợ AI và đề xuất. Kết quả test và level Skill Map là hai đánh giá khác nhau.
