# Go-Backend-Learning-Lab

Learning Lab cá nhân học Backend Engineering + Go từ vấn đề hệ thống, thông qua đọc hiểu, reverse engineering, tự triển khai và kiểm thử function nhỏ của dự án LoRa-P2P-Hybrid-TDMA-MVP.

**Kế hoạch hiện hành:** [Week 01 — Pareto 20/80 (7 ngày)](docs/bootcamp/7-day-backend-go.md). Mục tiêu: đọc hiểu function, biến, dependencies, startup/request flow và Join Hello; tự viết lại và test các function liên quan.

## Nguồn học tập

| Repository | Vai trò |
|---|---|
| [Getting Started with Go](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main) | Giáo trình lý thuyết, bài học và mental models |
| [LoRa Backend](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/tree/main/backend-go) | Mã nguồn tham chiếu, tests, business rules và kiến trúc |
| Repository này | Code tự viết, tests, review và trạng thái học |

Không sao chép toàn bộ codebase LoRa. Không sửa main của dự án gốc trong quá trình học.

## Tài liệu điều phối

- [Project Instructions](docs/project-instructions.md): bản ngắn để dán vào Project Settings của ChatGPT.
- [Learning Protocol](docs/learning-protocol.md): Socratic Tutor, quy trình practice, source traceability và đánh giá.
- [Testing Standards](docs/testing-standards.md): kiểm chứng hành vi, review, integration và failure modes.
- [Week 01 — 7-day Backend + Go](docs/bootcamp/7-day-backend-go.md): kế hoạch ưu tiên hiện hành, Course → Module → Topic → Practice.
- [Course Registry](docs/course-registry.md): nguồn đã có, placeholder tài liệu biên soạn và Coursera module chính xác.
- [Function Analysis Sheet](docs/function-analysis-template.md): mẫu phân tích function/variable/flow.
- [Learning Roadmap](docs/roadmap.md): định hướng dài hạn, sau Week 01.
- [Learning State](learning-state/README.md): cách lưu và tiếp tục phiên học.

## Cấu trúc

```text
docs/                 # Quy tắc học tập và roadmap
learning-state/       # Skill Map, tiến độ và review queue
fundamentals/         # Bài tập Go nền tảng (tạo khi cần)
practices/            # Function tái triển khai (tạo khi cần)
architecture/         # Call graph và business flows (tạo khi cần)
notes/                # Mental models và ghi chú (tạo khi cần)
go.mod                # Khởi tạo khi bắt đầu bài tập Go đầu tiên
```

## Cách học

1. Mở Project Golang, dán nội dung docs/project-instructions.md vào Instructions.
2. Gửi `continue learning` để đọc trạng thái và tiếp tục. Đọc Week 01, Course Registry và trạng thái; nếu chưa đánh giá, bắt đầu diagnostic Backend + Go.
3. Học lý thuyết, dự đoán hành vi, tự thiết kế và viết code, chạy test, review và trace luồng.
4. Commit phần code do mình thực hiện. Dùng `save state` để chuẩn bị bản ghi tiến độ; yêu cầu ghi GitHub khi muốn lưu.

Repository công khai: chỉ lưu thông tin kỹ thuật cần thiết; không ghi credentials, secrets, payload thật nhạy cảm, dữ liệu cá nhân hoặc chi tiết riêng tư của người học. Có thể chuyển Lab sang private nếu cần lưu ghi chú riêng tư.

Trạng thái khởi tạo: chưa đánh giá năng lực, chưa có practice hoàn thành, chưa chạy tests.
