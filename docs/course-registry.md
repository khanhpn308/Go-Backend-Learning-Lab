# Course Registry — Backend Engineering + Go

Updated: 2026-11-17. IDs C01–C14 preserve the original 24-week roadmap; C15–C16 are supplemental selections for Week 01. Course IDs are stable local IDs; module numbers and English titles follow Coursera. Module IDs are scoped by Course ID (C05 M01 is different from C06 M01).

## Consolidated Materials repository

- [Backend Engineering Materials](https://github.com/khanhpn308/Getting_Started_with_Go) — repository cấu trúc chung; tên repository trên GitHub vẫn là Getting_Started_with_Go cho đến khi owner hoàn tất Settings rename.
- [courses_manifest.json](https://github.com/khanhpn308/Getting_Started_with_Go/blob/main/courses_manifest.json) — danh mục C01–C16, `AVAILABLE` chỉ với C05; khóa khác là `PLANNED` và `directory=null`.
- [C05 course directory](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go) · [C05 manifest](https://github.com/khanhpn308/Getting_Started_with_Go/blob/main/courses/C05_Getting_Started_with_Go/course_manifest.json). C05 internal module and lesson IDs remain unchanged.
- `TODO_Cxx_COURSE_PATH` denotes a future directory **in this shared Materials repo**, not a separate repository; do not invent URL for planned courses.

## Source status and lookup

- AVAILABLE: repository and index inspected; use its actual file paths and lesson IDs.
- PENDING_USER_MATERIAL: no compiled course directory / module paths verified yet in shared Materials repo. Placeholder remains plain text. Use Coursera plus official references until material is added.
- DEFERRED: no Week 01 study requirement; module mapping can be verified when its phase is planned.
- These are material availability states, not course completion states. All learning/assessment states remain unassessed until evidence exists.
- Coursera public syllabus links below are course-level links; the Mxx and exact module title identify the module even if login or URL routes change. No private course content or enrollment/access is claimed.
- When user adds a course directory to Materials, verify README, manifest, module order and actual paths; replace only the corresponding placeholder. Preserve original Coursera module numbers; do not invent lesson IDs. Prefer compiled Vietnamese material for selected lessons; check against official references and current contracts.
- Do not copy Coursera transcripts/graded answers into this public Lab. Store only own notes and source pointers. C05 manifest currently marks lessons NEEDS_HUMAN_REVIEW; availability is not endorsement.

## Course index

| ID | Course / provider | User-compiled source | Week 01 usage |
|---|---|---|---|
| C01 | [Introduction to Back-End Development](https://www.coursera.org/learn/introduction-to-back-end-development) — Meta | `TODO_C01_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D1, D5 |
| C02 | [The Bits and Bytes of Computer Networking](https://www.coursera.org/learn/computer-networking) — Google | `TODO_C02_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D1–D2 |
| C03 | [Introduction to Software Engineering](https://www.coursera.org/learn/introduction-to-software-engineering) — IBM | `TODO_C03_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D1, D3, D6–D7 |
| C04 | [APIs](https://www.coursera.org/learn/apis) — Meta | `TODO_C04_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D4–D5; concepts only, Go replaces Django |
| C05 | [Getting Started with Go](https://www.coursera.org/learn/golang-getting-started) — University of California, Irvine | [Materials C05](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go) · [Manifest](https://github.com/khanhpn308/Getting_Started_with_Go/blob/main/courses/C05_Getting_Started_with_Go/course_manifest.json) (AVAILABLE) | W01 D1–D7 |
| C06 | [Functions, Methods, and Interfaces in Go](https://www.coursera.org/learn/golang-functions-methods) — University of California, Irvine | `TODO_C06_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D1–D7 |
| C07 | [Concurrency in Go](https://www.coursera.org/learn/golang-concurrency) — University of California, Irvine | `TODO_C07_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D1/D7 selected; deeper concurrency later |
| C08 | [Database Design and Basic SQL in PostgreSQL](https://www.coursera.org/learn/database-design-postgresql) — University of Michigan | `TODO_C08_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D6 |
| C09 | [Intermediate PostgreSQL](https://www.coursera.org/learn/intermediate-postgresql) — University of Michigan | `TODO_C09_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D6 transaction introduction |
| C10 | [Application Security for Developers and DevOps Professionals](https://www.coursera.org/learn/application-security-for-developers-devops) — IBM | `TODO_C10_COURSE_PATH` (PENDING_USER_MATERIAL) | W01 D2, D4, D7 selected |
| C11 | [Introduction to Containers w/ Docker, Kubernetes & OpenShift](https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift) — IBM | `TODO_C11_COURSE_PATH` (PENDING_USER_MATERIAL) | After W01; optional if environment requires it |
| C12 | [Introduction to Git and GitHub](https://www.coursera.org/learn/introduction-git-github) — Google | `TODO_C12_COURSE_PATH` (PENDING_USER_MATERIAL) | After W01 deeper; Git basics as tool only |
| C13 | [Continuous Integration and Continuous Delivery (CI/CD)](https://www.coursera.org/learn/continuous-integration-and-continuous-delivery-ci-cd) — IBM | `TODO_C13_COURSE_PATH` (PENDING_USER_MATERIAL) | After W01 |
| C14 | [Introduction to Cloud Computing](https://www.coursera.org/learn/introduction-to-cloud) — IBM | `TODO_C14_COURSE_PATH` (PENDING_USER_MATERIAL) | After W01; optional |
| C15 | [Node-RED: IoT projects with ESP32, MQTT and Docker](https://www.coursera.org/learn/packt-node-red-iot-projects-with-esp32-mqtt-and-docker) — Packt | `TODO_C15_COURSE_PATH` (PENDING_USER_MATERIAL) | Supplement W01 D2, D7; MQTT theory only, no Node-RED/firmware |
| C16 | [Unit Testing & Test-Driven Development](https://www.coursera.org/learn/unit-testing-test-driven-development) — Coursera supplementary course | `TODO_C16_COURSE_PATH` (PENDING_USER_MATERIAL) | Supplement W01 D1–D7; concepts applied using Go testing |

## Module catalog

### C01 — Introduction to Back-End Development

Coursera: https://www.coursera.org/learn/introduction-to-back-end-development

Material directory: `TODO_C01_COURSE_PATH`

- M01 — Get started with web development · material: `TODO_C01_M01_PATH`

### C02 — The Bits and Bytes of Computer Networking

Coursera: https://www.coursera.org/learn/computer-networking

Material directory: `TODO_C02_COURSE_PATH`

- M01 — Introduction to Networking · material: `TODO_C02_M01_PATH`
- M02 — The Network Layer · material: `TODO_C02_M02_PATH`
- M03 — The Transport and Application Layers · material: `TODO_C02_M03_PATH`
- M04 — Networking Services · material: `TODO_C02_M04_PATH`

### C03 — Introduction to Software Engineering

Coursera: https://www.coursera.org/learn/introduction-to-software-engineering

Material directory: `TODO_C03_COURSE_PATH`

- M01 — The Software Development Lifecycle · material: `TODO_C03_M01_PATH`
- M02 — Introduction to Software Development · material: `TODO_C03_M02_PATH`
- M04 — Software Architecture, Design, and Patterns · material: `TODO_C03_M04_PATH`

### C04 — APIs

Coursera: https://www.coursera.org/learn/apis

Material directory: `TODO_C04_COURSE_PATH`

- M01 — REST APIs · material: `TODO_C04_M01_PATH`
- M02 — Django REST framework · material: `TODO_C04_M02_PATH`

### C05 — Getting Started with Go

Coursera: https://www.coursera.org/learn/golang-getting-started

Material directory: https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go

Manifest: https://github.com/khanhpn308/Getting_Started_with_Go/blob/main/courses/C05_Getting_Started_with_Go/course_manifest.json

- M01 — Getting Started with Go Programming · [Vietnamese module](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go/Module_01_Getting_Started_with_Go_Programming)
- M02 — Basic Data Types · [Vietnamese module](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go/Module_02_Basic_Data_Types)
- M03 — Composite Data Types · [Vietnamese module](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go/Module_03_Composite_Data_Types)
- M04 — Protocols and Formats · [Vietnamese module](https://github.com/khanhpn308/Getting_Started_with_Go/tree/main/courses/C05_Getting_Started_with_Go/Module_04_Protocols_and_Formats)

### C06 — Functions, Methods, and Interfaces in Go

Coursera: https://www.coursera.org/learn/golang-functions-methods

Material directory: `TODO_C06_COURSE_PATH`

- M01 — Functions and Organization · material: `TODO_C06_M01_PATH`
- M02 — Function Types · material: `TODO_C06_M02_PATH`
- M03 — Object Orientation in Go · material: `TODO_C06_M03_PATH`
- M04 — Interfaces for Abstraction · material: `TODO_C06_M04_PATH`

### C07 — Concurrency in Go

Coursera: https://www.coursera.org/learn/golang-concurrency

Material directory: `TODO_C07_COURSE_PATH`

- M01 — Why Use Concurrency? · material: `TODO_C07_M01_PATH`
- M02 — Concurrency Basics · material: `TODO_C07_M02_PATH`
- M03 — Threads in Go · material: `TODO_C07_M03_PATH`
- M04 — Synchronized Communication · material: `TODO_C07_M04_PATH`

### C08 — Database Design and Basic SQL in PostgreSQL

Coursera: https://www.coursera.org/learn/database-design-postgresql

Material directory: `TODO_C08_COURSE_PATH`

- M01 — Introduction to SQL · material: `TODO_C08_M01_PATH`
- M02 — Single Table SQL · material: `TODO_C08_M02_PATH`
- M03 — One-To-Many Data Models · material: `TODO_C08_M03_PATH`

### C09 — Intermediate PostgreSQL

Coursera: https://www.coursera.org/learn/intermediate-postgresql

Material directory: `TODO_C09_COURSE_PATH`

- M01 — SQL Techniques · material: `TODO_C09_M01_PATH`

### C10 — Application Security for Developers and DevOps Professionals

Coursera: https://www.coursera.org/learn/application-security-for-developers-devops

Material directory: `TODO_C10_COURSE_PATH`

- M01 — Introduction to Security for Application Development · material: `TODO_C10_M01_PATH`
- M02 — Security Testing and Mitigation Strategies · material: `TODO_C10_M02_PATH`

### C11 — Introduction to Containers w/ Docker, Kubernetes & OpenShift

Coursera: https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift

Material directory: `TODO_C11_COURSE_PATH`

- M01 — Containers and Containerization · material: `TODO_C11_M01_PATH`

### C12 — Introduction to Git and GitHub

Coursera: https://www.coursera.org/learn/introduction-git-github

Material directory: `TODO_C12_COURSE_PATH`

DEFERRED — verify exact module titles and paths before activating; no Week 01 assignment.

### C13 — Continuous Integration and Continuous Delivery (CI/CD)

Coursera: https://www.coursera.org/learn/continuous-integration-and-continuous-delivery-ci-cd

Material directory: `TODO_C13_COURSE_PATH`

DEFERRED — verify exact module titles and paths before activating; no Week 01 assignment.

### C14 — Introduction to Cloud Computing

Coursera: https://www.coursera.org/learn/introduction-to-cloud

Material directory: `TODO_C14_COURSE_PATH`

DEFERRED — verify exact module titles and paths before activating; no Week 01 assignment.

### C15 — Node-RED: IoT projects with ESP32, MQTT and Docker

Coursera: https://www.coursera.org/learn/packt-node-red-iot-projects-with-esp32-mqtt-and-docker

Material directory: `TODO_C15_COURSE_PATH`

- M04 — MQTT Basics · material: `TODO_C15_M04_PATH`

### C16 — Unit Testing & Test-Driven Development

Coursera: https://www.coursera.org/learn/unit-testing-test-driven-development

Material directory: `TODO_C16_COURSE_PATH`

- M01 — Unit Testing Essentials · material: `TODO_C16_M01_PATH`

## Verified technical references (supplements, not Coursera modules)

| Topic | Official reference / existing project source |
|---|---|
| Go modules, language, functions | [Tutorials](https://go.dev/doc/tutorial/) · [Go spec](https://go.dev/ref/spec) · [A Tour of Go](https://go.dev/tour/) |
| Go errors, tests | [Errors](https://pkg.go.dev/errors) · [Go 1.13 errors](https://go.dev/blog/go1.13-errors) · [Add a test](https://go.dev/doc/tutorial/add-a-test) · [testing](https://pkg.go.dev/testing) |
| Go data and JSON | [encoding/json](https://pkg.go.dev/encoding/json) · [encoding/json/v2](https://pkg.go.dev/encoding/json/v2) · [encoding/hex](https://pkg.go.dev/encoding/hex) · [regexp](https://pkg.go.dev/regexp) |
| HTTP | [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview) · [HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages) · [net/http](https://pkg.go.dev/net/http) · [httptest](https://pkg.go.dev/net/http/httptest) |
| MQTT | [OASIS MQTT 5.0](https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html) · [HiveMQ MQTT Essentials](https://www.hivemq.com/mqtt/) · [Mosquitto docs](https://mosquitto.org/documentation/) |
| SQL/storage | [PostgreSQL tutorial](https://www.postgresql.org/docs/current/tutorial.html) · [Transactions](https://www.postgresql.org/docs/current/tutorial-transactions.html) · [Go database access](https://go.dev/doc/tutorial/database-access) · [database/sql](https://pkg.go.dev/database/sql) · [context](https://pkg.go.dev/context) |
| Security | [OWASP API Security](https://owasp.org/API-Security/) · [Go security](https://go.dev/security/) |
| Linux/Git | [Ubuntu command line](https://ubuntu.com/tutorials/command-line-for-beginners) · [Git book](https://git-scm.com/book/en/v2) |
| LoRa architecture / contracts | [System overview](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/docs/architecture/system-overview.md) · [Interfaces](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/docs/architecture/interfaces.md) · [MQTT topics](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/topics.md) · [Join Hello schema](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/mqtt/schemas/join-hello.schema.json) · [OpenAPI](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/contracts/api/openapi.yaml) |
| LoRa code/tests | [Backend at W01 baseline](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/tree/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go) · [go.mod](https://github.com/khanhpn308/LoRa-P2P-Hybrid-TDMA-MVP/blob/aec70071774e0eb2607eaea8d297d11782ad9c05/backend-go/go.mod) |

The LoRa documentation includes draft/provisional contracts and NOT_VERIFIED integration gates. A link does not imply production approval, current runtime functionality, or successful testing. Exact Go toolchain/API availability must be verified locally before execution.
