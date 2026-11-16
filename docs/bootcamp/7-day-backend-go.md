# Week 01 — Backend Engineering + Go (Pareto 20/80)

Status: ACTIVE PLAN / NOT_STARTED. Duration: 7 study days; baseline 8 hours/day (56 hours), adjustable after diagnostic. Day numbers are relative to actual start, not calendar deadlines. This is a foundation for reading and independently reconstructing small pieces of the LoRa backend, not a promise of mastery or production readiness.

## Objective and method

By the end, identify entry point, startup vs request/message runtime, package/layer, function contract, inputs/outputs/errors, caller/callee, data source and consumer, variable type/scope/lifetime/ownership, dependencies, side effects, and why each validation or operation occurs in that order. Trace the Join Hello handler from input to storage and a separate HTTP liveness flow. Be able to implement, test and explain small real functions independently.

Pareto selects high-leverage concepts, not a measured claim of 80% code coverage. Default D1–D6 per day: 1.5h selected theory, 2h trace/read, 3h independent practice, 1h test/debug, 0.5h assessment (8h). D7: 1h review, 2h practice, 1h test/debug, 2.5h trace, 1.5h final assessment (8h). If time is shorter, reduce scope, not verification. No full course/video/certificate completion required. Use selected lessons only. Do not force progression when prerequisites fail.

## Source baseline and study instructions

- [Course registry](../course-registry.md): maps Course/Module IDs to the [shared Materials catalog](https://github.com/khanhpn308/Getting_Started_with_Go/blob/main/courses_manifest.json), the existing C05 course directory and TODO placeholders for future compiled course folders.
- [Go manifest](https://github.com/khanhpn308/Getting_Started_with_Go/blob/main/courses/C05_Getting_Started_with_Go/course_manifest.json): C05 lesson IDs are actual repository IDs; they differ from lecture labels. Read selected files before teaching.
- LoRa repo: https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP, pinned commit [aec70071774e0eb2607eaea8d297d11782ad9c05](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/commit/aec70071774e0eb2607eaea8d297d11782ad9c05). The links below are static source/test references; no tests executed. Recheck at practice assignment and use this pin unless a deliberate rebaseline is recorded.
- [Architecture](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/docs/architecture/system-overview.md), [interfaces](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/docs/architecture/interfaces.md), [MQTT topics](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/topics.md), [Join Hello draft schema](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/schemas/join-hello.schema.json), [OpenAPI draft](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/api/openapi.yaml). The design direction is not evidence of implementation or integration. Backend README still says scaffold; code contains handlers, storage and wiring. Distinguish target, source and verified runtime.
- [go.mod](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/go.mod) declares Go 1.27.3 at this baseline. Verify `go version` and Lab module locally; do not automatically change production Go/dependencies or download toolchains. C05 older examples are conceptual references, not necessarily current API best practice.
- Before each practice: read protocol and testing standards; source/tests/contracts and callers; provide signature/contract and tests without full implementation. Source links are tutor/reviewer references; learner opens implementation only after independent attempt unless explicitly requesting it. Never use real credentials, keys or production database/broker.

## Day 1 — W01-D01: Process, startup, package, variables and functions

Question: Backend starts from where? Why separate configuration, app construction and execution?

| Learning topic | Course → module (selected lessons) | Supplement / project |
|---|---|---|
| Client/server, backend, web server, ports at overview | [C01 M01 — Get started with web development](https://www.coursera.org/learn/introduction-to-back-end-development) — developer roles, Internet, web server, APIs | [C02 M03 — The Transport and Application Layers](https://www.coursera.org/learn/computer-networking) — transport layer, ports |
| Process, memory vs program, environment variables | [C07 M02 — Concurrency Basics](https://www.coursera.org/learn/golang-concurrency) — M2.1.1 Processes; [C05 M01 — Getting Started with Go Programming](https://www.coursera.org/learn/golang-getting-started) — Go tool and variables | [os.Getenv](https://pkg.go.dev/os#Getenv), [main](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/cmd/server/main.go), [config](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/config/config.go); Linux ps/ss optional |
| Go toolchain, module/package/import, entry point, variables and initialization | [C05 M01 — Getting Started with Go Programming](https://www.coursera.org/learn/golang-getting-started) — M01-L07–L11 | [Go tutorial](https://go.dev/doc/tutorial/create-module) |
| Constants, strings, function parameter and result, pure function | [C05 M02 — Basic Data Types](https://www.coursera.org/learn/golang-getting-started) — M02-L08, L10; [C06 M01 — Functions and Organization](https://www.coursera.org/learn/golang-functions-methods) — M1.1.1, M1.1.2 | [topic source](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/topic.go) |
| Test basics, expected vs actual | [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — test structure, naming; [C03 M01 — The Software Development Lifecycle](https://www.coursera.org/learn/introduction-to-software-engineering) — Software Testing | [Add a test](https://go.dev/doc/tutorial/add-a-test) |

Trace: [main.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/cmd/server/main.go) → config.Load → [app.New](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/app/wiring.go) → [App.Run](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/app/lifecycle.go). Identify startup-time cfg/application/err/ctx; not all lines must be understood now. MQTT topic is an address-like string, not an identity credential.

**W01-P01 — BuildJoinHelloTopic**
- Source: [topic.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/topic.go); tests: [topic_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/topic_test.go) / TestBuildJoinHelloTopic.
- Signature: `func BuildJoinHelloTopic(gatewayID string) string`.
- Contract: input gw-alpha → iot/v1/gw/gw-alpha/uplink/join-hello; gw01 → iot/v1/gw/gw01/uplink/join-hello. Builds string only; no ID validation, no network side effects. Empty input can produce malformed topic; distinguish builder contract from parser contract.
- Independent task: design algorithm, implement in isolated Lab package; tests for two valid IDs and characterize empty ID. Explain parameter vs global, const vs var, return value.
- Completion: runnable small program, actual test evidence, explain startup vs helper and data origin. Do not assert a production caller for builder without inspecting call sites.

## Day 2 — W01-D02: Networking, MQTT, string parsing and errors

Question: Why reject malformed network data before using a Gateway ID?

| Learning topic | Course → module | Supplement / project |
|---|---|---|
| TCP/IP layers, IP, route, TCP/UDP, ports/socket, DNS | [C02 M01 — Introduction to Networking](https://www.coursera.org/learn/computer-networking); [C02 M02 — The Network Layer](https://www.coursera.org/learn/computer-networking); [C02 M03 — The Transport and Application Layers](https://www.coursera.org/learn/computer-networking); [C02 M04 — Networking Services](https://www.coursera.org/learn/computer-networking) — five-layer model, IP, TCP handshake, socket states, name resolution | `ss -tuln`, `ip addr`, DNS observation if Linux available |
| MQTT publisher/subscriber/broker/topic, QoS, retained messages | [C15 M04 — MQTT Basics](https://www.coursera.org/learn/packt-node-red-iot-projects-with-esp32-mqtt-and-docker) — terminology, topics, QoS, retained | [MQTT 5.0](https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html), [topic contract](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/topics.md) |
| String bytes, slicing, length, bool, condition/loop, scope | [C05 M02 — Basic Data Types](https://www.coursera.org/learn/golang-getting-started) — M02-L04, L08–L11 | [strings](https://pkg.go.dev/strings), [regexp](https://pkg.go.dev/regexp) |
| Multiple returns, error and early return, wrapping | [C06 M01 — Functions and Organization](https://www.coursera.org/learn/golang-functions-methods) — M1.1.2; [C06 M04 — Interfaces for Abstraction](https://www.coursera.org/learn/golang-functions-methods) — M4.2.3 Error Handling | [Go errors](https://go.dev/blog/go1.13-errors) |
| Trust boundary, TLS vs application validation, invalid inputs | [C10 M01 — Introduction to Security for Application Development](https://www.coursera.org/learn/application-security-for-developers-devops) — TLS/SSL, security terminology | [OWASP API security](https://owasp.org/API-Security/); LoRa identity binding contract |
| Edge cases, parameterized tests | [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — Parameterized and Edge-Case Testing | [testing](https://pkg.go.dev/testing) |

**W01-P02 — ParseJoinHelloTopic**
- Source/tests: [topic.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/topic.go), [topic_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/topic_test.go); TestParseJoinHelloTopic_Success and TestParseJoinHelloTopic_Malformed. ID regex defined in [envelope.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/envelope.go).
- Signature: `func ParseJoinHelloTopic(topic string) (string, error)`.
- Contract: canonical iot/v1/gw/{gateway_id}/uplink/join-hello; ID ASCII A–Z/a–z/0–9/_/- (1–32 chars). Return extracted ID + nil on success, empty ID + error matching ErrMalformedTopic on failure; invalid regex path also matches ErrInvalidGatewayID in source.
- Tests: valid ID, empty input, short topic, empty ID, wrong prefix/suffix, embedded slash, punctuation, length 1/32/33, errors.Is; no panic on short input.
- Trace: [JoinHelloIngestHandler.Handle](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/handler.go) receives req.Topic → topicGWID, err → early return or identity checks. Topic validity alone is not authentication.
- Completion: independently write parser, table-driven tests, explain why length check precedes slicing, local scope and why caller must stop on error.

## Day 3 — W01-D03: Domain model, struct, pointer, method

Question: Why group device state and enforce domain invariants before storage?

| Learning topic | Course → module | Supplement / project |
|---|---|---|
| Architecture, layers, modular monolith, separation of concerns | [C03 M04 — Software Architecture, Design, and Patterns](https://www.coursera.org/learn/introduction-to-software-engineering) — approaches, architecture patterns, design/modeling | [System overview](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/docs/architecture/system-overview.md); project-specific layering is an application, not a course guarantee |
| Integer width, uint8/uint32, custom type, zero value, scope | [C05 M02 — Basic Data Types](https://www.coursera.org/learn/golang-getting-started) — M02-L03–L04, L07–L08 | [Go spec](https://go.dev/ref/spec) |
| Struct, map at overview, pointer/value semantics | [C05 M03 — Composite Data Types](https://www.coursera.org/learn/golang-getting-started) — M03-L06–L07; [C06 M01 — Functions and Organization](https://www.coursera.org/learn/golang-functions-methods) — M1.1.3 | [NodeHealth](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/domain/health.go) |
| Method, receiver, encapsulation, nil pointer | [C06 M03 — Object Orientation in Go](https://www.coursera.org/learn/golang-functions-methods) — M3.2.1–M3.2.3 | [Go methods](https://go.dev/tour/methods/1) |
| Invariants, validation and failure tests | [C04 M02 — Django REST framework](https://www.coursera.org/learn/apis) — Deserialization and validation (concept only); [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — edge cases | [health tests](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/domain/health_test.go) |

**W01-P03 — NodeHealth.Validate**
- Source: [health.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/domain/health.go); tests: [health_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/domain/health_test.go) / TestNodeHealth_Validation_Success, InvalidNodeID, InvalidStatus.
- Signature: `func (h *NodeHealth) Validate() error`.
- Contract: reject nil receiver, empty GatewayID, NodeID outside 1–254, HealthStatus outside ONLINE/OFFLINE/UNKNOWN. No mutation. Do not silently add required timestamp/counter checks not in source contract.
- Tests: nil, empty ID, 0/1/254/255, each allowed status and invalid status, no mutation. Use error identity where source defines sentinel.
- Trace: [status_consumer.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/status_consumer.go) validates a health record; inspect actual caller and subsequent persistence when assigned. This is a separate flow from Join Hello. Project logical Node identity is (gateway_id, node_id), not globally unique node_id. Beacon alone does not establish Node health.
- Completion: write method independently, explain each field/receiver, how validation protects state and why pointer receiver permits nil-check without implying mutation.

## Day 4 — W01-D04: JSON, DTO, byte slices and data ownership

Question: Why is successfully decoded JSON not necessarily valid business data?

| Learning topic | Course → module | Supplement / project |
|---|---|---|
| JSON serialization/deserialization, struct tags, DTO | [C05 M04 — Protocols and Formats](https://www.coursera.org/learn/golang-getting-started) — M04-L03 JSON; [C04 M02 — Django REST framework](https://www.coursera.org/learn/apis) — Serializers and Deserialization and validation (concept only) | [encoding/json](https://pkg.go.dev/encoding/json), [Join Hello draft schema](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/schemas/join-hello.schema.json) |
| Array, slice, []byte, pointer destination, zero values | [C05 M03 — Composite Data Types](https://www.coursera.org/learn/golang-getting-started) — M03-L02–L04; [C05 M02 — Basic Data Types](https://www.coursera.org/learn/golang-getting-started) — M02-L03; [C06 M01 — Functions and Organization](https://www.coursera.org/learn/golang-functions-methods) — M1.1.3–M1.1.4 | [Go spec](https://go.dev/ref/spec) |
| Size limits, untrusted input, strict decode vs semantic validation | [C10 M01 — Introduction to Security for Application Development](https://www.coursera.org/learn/application-security-for-developers-devops) — Security by Design; [C04 M02 — Django REST framework](https://www.coursera.org/learn/apis) — validation | [json/v2](https://pkg.go.dev/encoding/json/v2); project decoder/tests |
| Error wrapping, destination unchanged on failure, generic type parameter recognition | [C06 M04 — Interfaces for Abstraction](https://www.coursera.org/learn/golang-functions-methods) — M4.2.3; [C06 M01 — Functions and Organization](https://www.coursera.org/learn/golang-functions-methods) — function parameters (foundation only, not a generics module) | [Go generics tutorial](https://go.dev/doc/tutorial/generics), [errors](https://pkg.go.dev/errors); generic version optional |
| Malformed and boundary tests | [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — edge-case testing | [decoder tests](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/jsonboundary/decoder_test.go) |

**W01-P04 — DecodeObject**
- Source: [decoder.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/jsonboundary/decoder.go); tests: [decoder_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/jsonboundary/decoder_test.go) / TestDecodeObjectAcceptsTypedEnvelope, RejectsUntrustedInput, RejectsInvalidLimit, CommitsOnlySuccessfulDecode, RejectsNilDestination, AcceptsExactByteLimit, DoesNotClaimSchemaValidation.
- Original signature: `func DecodeObject[T any](payload []byte, maxBytes int, dst *T) error`.
- Required beginner variant: typed DTO-specific decoder, e.g. `func DecodeEnvelope(payload []byte, maxBytes int, dst *Envelope) error` (learning signature). Positive byte limit, reject oversized, empty/non-object/malformed/trailing data, nil destination; reject unknown fields; update destination only after success and reset stale fields. Test exact limit and unchanged destination after failure. No DB writes or MQTT ACK.
- Full equivalence optional only after toolchain verification: original uses json/v2 strict rules (duplicate keys, invalid UTF-8, unknown members, other malformed encodings). A v1 solution is a limited variant, not claimed equivalent; record unverified differences, do not change production toolchain.
- Trace: [Handle](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/handler.go) decodes req.Payload into envelope, checks identity and envelope.Validate afterwards. Explain temporary decoded variable, lifetime, pointer output and semantic validation as distinct responsibility.
- Completion: implement and test beginner variant independently, state exact differences from source; explain why decode failure must not partially modify trusted destination.

## Day 5 — W01-D05: HTTP, REST, router, handler, interface

Question: What happens between curl sending GET /healthz and the HTTP response?

| Learning topic | Course → module | Supplement / project |
|---|---|---|
| HTTP client/server, request/response, header/body, method/status, REST resource | [C01 M01 — Get started with web development](https://www.coursera.org/learn/introduction-to-back-end-development) — Introduction to HTTP, APIs and services; [C04 M01 — REST APIs](https://www.coursera.org/learn/apis) — What you know about HTTP, RESTfulness, REST best practices | [MDN HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview) |
| Routing, handler, JSON response, status/header ordering | [C04 M01 — REST APIs](https://www.coursera.org/learn/apis) — Organizing an API project, debugging; [C05 M04 — Protocols and Formats](https://www.coursera.org/learn/golang-getting-started) — M04-L03 | [net/http](https://pkg.go.dev/net/http), [OpenAPI](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/api/openapi.yaml) |
| Interfaces, methods, constructor, request pointer, callback registration | [C06 M04 — Interfaces for Abstraction](https://www.coursera.org/learn/golang-functions-methods) — M4.1.2, M4.1.3, M4.2.1; [C06 M03 — Object Orientation in Go](https://www.coursera.org/learn/golang-functions-methods) — receiver | [net/http](https://pkg.go.dev/net/http); Go-specific details supplemental |
| HTTP test, test doubles, observable response | [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — test doubles/isolation; [C04 M01 — REST APIs](https://www.coursera.org/learn/apis) — debugging APIs | [httptest](https://pkg.go.dev/net/http/httptest) |

**W01-P05 — HealthHandler.handleHealthz**
- Source: [health_handler.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/api/health_handler.go); test: [health_handler_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/api/health_handler_test.go) / TestHealthHandler_Healthz.
- Signature: `func (h *HealthHandler) handleHealthz(w http.ResponseWriter, r *http.Request)`.
- Contract: GET /healthz → HTTP 200, Content-Type application/json; charset=utf-8, JSON object {"status":"ok"}. It is liveness only, not DB/broker/Node/RF readiness. Recreate minimal constructor and RegisterRoutes in Lab; use modern method-specific routing only if supported by Lab Go.
- Tests: status, content type, parsed body, unsupported method (POST) through router; distinguish handler vs routing behavior. Run loopback server with curl (no public exposure), then httptest.
- Trace startup [main](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/cmd/server/main.go) → [app.New](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/app/wiring.go) → [BuildServeMux](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/api/router.go) → RegisterRoutes; [App.Run](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/app/lifecycle.go) starts HTTP server. Runtime: request → ServeMux → handler → ResponseWriter.
- Completion: explain why registration is not execution, why w interface/r pointer, and demonstrate real curl output and test results.

## Day 6 — W01-D06: SQL, repository, context and persistence

Question: Why separate business orchestration from database queries and transactions?

| Learning topic | Course → module | Supplement / project |
|---|---|---|
| Relational database, tables/rows, SQL CRUD, WHERE, types, keys | [C08 M01 — Introduction to SQL](https://www.coursera.org/learn/database-design-postgresql); [C08 M02 — Single Table SQL](https://www.coursera.org/learn/database-design-postgresql) — Introduction to SQL, Single Table SQL | [PostgreSQL tutorial](https://www.postgresql.org/docs/current/tutorial.html) |
| Primary/foreign key, relational design, JOIN | [C08 M03 — One-To-Many Data Models](https://www.coursera.org/learn/database-design-postgresql) — Relational Database Design, Keys, normalization | [join_storage.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/storage/join_storage.go); educational schema only |
| Repository interface, dependency injection, layer boundary | [C03 M04 — Software Architecture, Design, and Patterns](https://www.coursera.org/learn/introduction-to-software-engineering) — architecture patterns; [C06 M04 — Interfaces for Abstraction](https://www.coursera.org/learn/golang-functions-methods) — Interfaces, Using Interfaces; [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — Dependency Injection for Testing | [JoinRepository](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/storage/join_storage.go) |
| Parameterized query, Scan, SQL error, ctx cancellation | [C08 M02 — Single Table SQL](https://www.coursera.org/learn/database-design-postgresql) — query foundation; [C06 M04 — Interfaces for Abstraction](https://www.coursera.org/learn/golang-functions-methods) — error handling | [Go database access](https://go.dev/doc/tutorial/database-access), [context](https://pkg.go.dev/context), [database/sql](https://pkg.go.dev/database/sql) (Go-specific API supplemental) |
| Transaction, rollback, row locking, replay/idempotency overview | [C09 M01 — SQL Techniques](https://www.coursera.org/learn/intermediate-postgresql) — Concurrency and Transactions; [C15 M04 — MQTT Basics](https://www.coursera.org/learn/packt-node-red-iot-projects-with-esp32-mqtt-and-docker) — QoS as transport foundation | [PostgreSQL transactions](https://www.postgresql.org/docs/current/tutorial-transactions.html), LoRa RecordJoinHello, MQTT contract; no full transaction reimplementation |
| Dependency failure, fake DB, integration vs unit | [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — test doubles/isolation; [C03 M01 — The Software Development Lifecycle](https://www.coursera.org/learn/introduction-to-software-engineering) — Software Testing | [Testing standards](../testing-standards.md) |

**W01-P06 — GetActiveDevice**
- Source: [join_storage.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/storage/join_storage.go); tests: [join_storage_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/storage/join_storage_test.go) / TestGetActiveDevice_Success, NotFound, NotActive. Existing tests use mock DB; do not call them PostgreSQL integration evidence.
- Signature: `func (s *PostgresJoinStorage) GetActiveDevice(ctx context.Context, networkID uint32, mac [6]byte) (*DeviceRecord, error)`.
- Contract: find registered device with matching network/MAC and active generation; active device returns record; no matching joined row → ErrDeviceNotFound; non-ACTIVE device → ErrDeviceNotActive; other query failures propagated/wrapped. Use fake credentials and test data, no real K_JOIN.
- Beginner scope: write SQL SELECT/JOIN with fake rows/local isolated DB, then independent typed lookup function using a fake dependency; distinguish fake from actual adapter. If ready, implement actual parameterized database/sql adapter with context and scan, without copying source; no real DB requirement if blocked.
- Test success, not found, inactive, query error, context cancellation where supported. Verify SQL separately if only fake used. Read `RecordJoinHello` for transaction and locks, not rewrite security/persistence-critical flow.
- Trace: [Handle](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/handler.go) → JoinRepository.GetActiveDevice → PostgresJoinStorage → DB; explain status/gen/local err, db field, context and return pointer; review why actual source checks device status and active generation.
- Completion: explain query and interface, write and test scoped lookup, record fake/integration scope honestly.

## Day 7 — W01-D07: Independent transfer and Join Hello reverse engineering

Question: How do data, dependencies, and validation travel through a larger handler, and why in this order?

| Learning topic | Course → module | Supplement / project |
|---|---|---|
| Strings, bytes, arrays/slices, error handling, method transfer | [C05 M02 — Basic Data Types](https://www.coursera.org/learn/golang-getting-started) — M02-L08–L11; [C05 M03 — Composite Data Types](https://www.coursera.org/learn/golang-getting-started) — M03-L02–L03; [C06 M03 — Object Orientation in Go](https://www.coursera.org/learn/golang-functions-methods); [C06 M04 — Interfaces for Abstraction](https://www.coursera.org/learn/golang-functions-methods) | [encoding/hex](https://pkg.go.dev/encoding/hex), envelope source |
| Architecture, call graph, data flow, side effects | [C03 M04 — Software Architecture, Design, and Patterns](https://www.coursera.org/learn/introduction-to-software-engineering) — Software Design and Modeling, Architectural Patterns | [Architecture](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/docs/architecture/system-overview.md), handler/source/tests |
| Authentication vs authorization, trust boundary, replay/identity | [C10 M01 — Introduction to Security for Application Development](https://www.coursera.org/learn/application-security-for-developers-devops) — TLS/SSL and security concepts; [C04 M01 — REST APIs](https://www.coursera.org/learn/apis) — authentication/access control; [C15 M04 — MQTT Basics](https://www.coursera.org/learn/packt-node-red-iot-projects-with-esp32-mqtt-and-docker) — QoS | [MQTT topic contract](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/topics.md), [Join Hello schema](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/schemas/join-hello.schema.json) |
| Startup and cancellation/concurrency recognition | [C07 M02 — Concurrency Basics](https://www.coursera.org/learn/golang-concurrency); [C07 M03 — Threads in Go](https://www.coursera.org/learn/golang-concurrency); [C07 M04 — Synchronized Communication](https://www.coursera.org/learn/golang-concurrency) — processes, goroutines, channels, select (selected reading only) | [App.Run](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/app/lifecycle.go), [context](https://pkg.go.dev/context); no full concurrent implementation |
| Test/debug, failure path, independent explanation | [C16 M01 — Unit Testing Essentials](https://www.coursera.org/learn/unit-testing-test-driven-development) — tests and edge cases; [C03 M01 — The Software Development Lifecycle](https://www.coursera.org/learn/introduction-to-software-engineering) — Software Testing | [Testing standards](../testing-standards.md), handler tests |

**W01-P07 — JoinHelloEnvelope.DecodeRawFrameHex**
- Source: [envelope.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/envelope.go); test: [envelope_test.go](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/envelope_test.go) / TestJoinHelloEnvelope_DecodeRawFrameHex.
- Signature: `func (e *JoinHelloEnvelope) DecodeRawFrameHex() ([]byte, error)`.
- Contract: 136 valid hexadecimal chars → 68 bytes; wrong length → ErrInvalidRawFrameHex; invalid hex → error (source wraps decode error). No authentication or persistence. Non-nil receiver precondition; do not claim nil handling absent in source.
- Tests: valid lower/uppercase hex, exact length, empty/short/long, invalid hex. Learner writes algorithm and tests before seeing original. No crypto implementation.
- Completion: independent implementation, actual tests, explain receiver/return bytes/length rules and why parsing is not frame authentication.

**Final trace (static implementation, not runtime certification)**

Read [JoinHelloIngestHandler.Handle](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/handler.go) and [handler tests](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/internal/mqtt/handler_test.go). Trace:
1. IngestRequest topic/payload/broker identity → payload size check, ParseJoinHelloTopic.
2. Compare authenticated broker identity if present; rate limit Gateway. Contract requires identity binding; source conditional check is not proof the runtime always supplies verified identity.
3. DecodeObject → payload gateway ID matches topic → envelope.Validate.
4. Gateway registry lookup/authorization; raw-frame decode/parse; per-device rate limit.
5. JoinRepository.GetActiveDevice → unwrap key and verify frame (understand responsibility only; no crypto rewrite).
6. SHA-256 identity comparison, RecordJoinHello storage transaction/anti-replay; verify result status HELLO_AUTHENTICATED_PENDING_GRANT.
7. IngestResponse (transaction ID/status/replay flag/counter). Authentication pending grant is not permission to transmit data.

Draw separate HTTP liveness flow and NodeHealth validation flow; do not merge unrelated call chains. Identify actual caller/wiring of Join Hello if present; if unverified, stop at Handle input and record gap. Gateway owns RF TDMA execution; backend plans/versions, Gateway ACK and MQTT PUBACK do not prove PostgreSQL commit. Never infer online Node from Gateway Beacon. Existing implementation/tests do not prove RF/HIL, security or runtime integration gates.

## Completion gate and evidence

- Mandatory target: independently reconstruct P01/P02/P03/P05/P07 with tests, P04 typed variant, P06 scoped lookup/SQL exercise. Full generic decoder and real PostgreSQL adapter are optional stretch, not implied by beginner variants.
- Explain at least two different flows: startup + HTTP request, and Join Hello ingestion through storage; identify NodeHealth separately.
- Complete [Function Analysis Sheet](../function-analysis-template.md) for each practice (short version for P01); explain at least req, topicGWID, err, envelope, gwInfo, deviceRecord, txInput, txResult, h.joinRepo, ctx in final handler.
- Score conceptual 20, function/variable/contract reading 25, trace/dependency 25, independent implementation 20, test/debug 10; target >=80/100 plus real test evidence, no critical security/data integrity misunderstanding. Score is not Skill Map level; two independent evidences still required for level increase.
- Diagnose with one question at a time; assess with new variant, code reasoning and failure scenario. Record incomplete items honestly; repeat as needed. Update current-session, skill-map, progress, misconceptions, review-queue when user authorizes persistence. Do not mark progress from this plan.

## Scope after Week 01

Defer full concurrency, WebSocket implementation, real MQTT integration and reliability, production auth, advanced PostgreSQL, Docker/Compose, CI/CD, deployment/monitoring. They remain in [long-term roadmap](../roadmap.md). Week 01 is the foundation, not a staging release or certification.
