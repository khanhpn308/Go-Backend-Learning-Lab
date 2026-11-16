# Learning Roadmap — Long-term Direction

**Active plan:** [Week 01 — Pareto 20/80](bootcamp/7-day-backend-go.md). [Course Registry](course-registry.md) maps courses/modules and learning materials. Week 01 is first, not a replacement for the long-term learning objectives. The earlier Go-first candidate sequence below is a reference pool, not the active day schedule.

Lộ trình dự kiến, không phải checklist cố định. Bắt đầu bằng diagnostic; chưa có bằng chứng thì không tự gán level. Giáo trình [Getting Started with Go](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main) là nguồn chính; bổ sung các chủ đề còn thiếu trước practice. Đọc source tại commit xác định khi giao bài.

| Giai đoạn | Go / backend | Practice ứng viên từ LoRa |
|---|---|---|
| 1 | Chương trình, biến, kiểu, chuỗi, function, package | BuildJoinHelloTopic (internal/mqtt/topic.go) |
| 2 | Điều kiện, string slicing, errors, testing | ParseJoinHelloTopic (internal/mqtt/topic.go) |
| 3 | Struct, pointer, method, custom type, map | NodeHealth.Validate (internal/domain/health.go) |
| 4 | HTTP, JSON, interface, routing, httptest | HealthHandler (internal/api/health_handler.go) |
| 5 | Generics, JSON boundary, validation, data ownership | DecodeObject (internal/jsonboundary/decoder.go) |
| 6 | SQL, context, repository, transactions | Chọn function storage sau khi đọc source và schema |
| 7 | Concurrency, mutex, time, cancellation, queue | TokenBucketLimiter.Allow (internal/mqtt/rate_limiter.go); presence/realtime sau khi đủ nền |
| 8 | Interface, dependency injection, lifecycle | app.New (internal/app/wiring.go), business handlers |
| 9 | Tổng hợp, security, integration | JoinHelloIngestHandler.Handle (internal/mqtt/handler.go) và flow đã xác minh |

Các ứng viên là định hướng, chưa phải practice đã giao hoặc đã hoàn thành. Không pin commit giả; pin khi tạo bài. Thứ tự có thể thay đổi theo prerequisites, yêu cầu học và source hiện hành.

## Giáo trình nền tảng

- M01: Go overview, tooling, packages, variables và initialization. Objects/concurrency ở mức giới thiệu; đi sâu sau khi có nền.
- M02: pointers, scope, memory/GC, basic types, strings, constants, control flow.
- M03: arrays, slices, hash tables, maps, structs.
- M04: RFC, JSON, file I/O.

Bổ sung function, method, interface, error handling, modules, testing, context, generics và concurrency khi cần. Kiểm tra các API/toolchain hiện hành, không mặc định ví dụ cũ là best practice.

## Mốc năng lực

- Tự dự đoán và giải thích code Go cơ bản.
- Tự viết function thuần và test cases, xử lý lỗi.
- Tự xây dựng handler nhỏ và kiểm chứng HTTP/JSON.
- Hiểu domain, storage, MQTT, authentication, realtime và dependency boundaries qua từng flow.
- Tự trace, debug và thiết kế thay đổi nhỏ có test/review trên branch riêng của LoRa.

Week 01 is agreed as seven study days; hours are a planning assumption. Beyond Week 01, use actual evidence to adjust duration. Đánh giá khả năng vận dụng độc lập thay vì số lượng bài.


## Long-term reference (original 24-week roadmap)

The user-supplied original plan has 8 phases. Retain direction, not a fixed calendar after the new Week 01. Detailed post-Week-01 module scheduling will be designed later, not expanded in this change.

| Phase | Original schedule | Focus | Course IDs |
|---|---|---|---|
| P01 | Week 1 | Backend fundamentals | C01,C02,C03,C04,C11 |
| P02 | Weeks 2–5 | Go core | C05,C06,C07 |
| P03 | Weeks 6–8 | PostgreSQL/storage | C08,C09 |
| P04 | Weeks 9–11 | MQTT/event processing | C15 + OASIS/HiveMQ/Mosquitto |
| P05 | Weeks 12–14 | REST/WebSocket | C04 + Go docs |
| P06 | Weeks 15–17 | Security/testing | C10,C16 |
| P07 | Weeks 18–20 | Docker/Git/CI/CD | C11,C12,C13 |
| P08 | Weeks 21–24 | Deployment/operations | C14 + official docs |

The user supplied a full 24-week outline; this table preserves its phase sequence, not all lesson details. No certification, production release, or integration verification inferred.
