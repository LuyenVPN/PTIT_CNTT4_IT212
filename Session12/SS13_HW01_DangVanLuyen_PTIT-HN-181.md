# File 01 - `History_Prompts.txt`

```text
============================================================
PROJECT
Online Bank Account Opening (eKYC)
============================================================

Prompt 01

# Role

Đóng vai một Senior Business Analyst có hơn 10 năm kinh nghiệm trong lĩnh vực FinTech và Ngân hàng số.

Nhiệm vụ của bạn là phân tích yêu cầu nghiệp vụ cho hệ thống mở tài khoản ngân hàng trực tuyến (eKYC).

============================================================

Bối cảnh

Ngân hàng số ABC Bank muốn số hóa hoàn toàn quy trình mở tài khoản.

Khách hàng thực hiện:

- Tải ứng dụng
- Đăng ký thông tin cơ bản
- Chụp ảnh hai mặt CCCD
- Quét khuôn mặt (Liveness Check)
- Hệ thống đối chiếu dữ liệu
- Nếu hợp lệ thì cấp số tài khoản tự động

Mục tiêu:

Zero Manual Operation.

============================================================

Hãy phân tích:

1. Business Objectives

2. Scope

3. Actors

4. Business Flow

5. System Modules

6. External Systems

7. Risks

8. Constraints

Trình bày bằng Markdown.

============================================================

Prompt 02

Dựa trên kết quả ở trên, hãy phân tích Functional Requirements.

Yêu cầu:

- Chia theo module
- Mỗi chức năng có:
    - ID
    - Name
    - Description
    - Priority

============================================================

Prompt 03

Tiếp tục phân tích Non Functional Requirements.

Bao gồm:

- Security
- Performance
- Availability
- Reliability
- Scalability
- Maintainability
- Audit Logging
- Compliance
- Backup
- Disaster Recovery

Trình bày thành bảng.

============================================================

Prompt 04

Tiếp tục phân tích Business Rules.

Ví dụ:

- Điều kiện CCCD hợp lệ
- Điều kiện khuôn mặt hợp lệ
- Điều kiện cấp tài khoản
- Điều kiện từ chối

Nếu còn quy tắc nghiệp vụ khác hãy bổ sung.

============================================================

Prompt 05

Tiếp tục xác định Assumptions của hệ thống.

Bao gồm:

- Giả định về khách hàng
- Giả định về thiết bị
- Giả định về Internet
- Giả định về AI OCR
- Giả định về AI Face Matching
- Giả định về Core Banking

============================================================

Prompt 06

Dựa trên toàn bộ phân tích ở trên.

Sinh User Stories theo chuẩn:

As a ...
I want ...
So that ...

Mỗi User Story gồm:

- ID
- Priority
- Acceptance Criteria

============================================================

Prompt 07

Tiếp tục sinh danh sách Use Case.

Mỗi Use Case gồm:

- Use Case ID
- Name
- Actor
- Preconditions
- Main Flow
- Alternative Flow
- Exception Flow
- Post Conditions

============================================================

Prompt 08

Tổng hợp toàn bộ kết quả thành tài liệu Business Analysis hoàn chỉnh bằng Markdown.

Bao gồm:

- Introduction
- Scope
- Actors
- Business Flow
- Functional Requirements
- Non Functional Requirements
- Business Rules
- Assumptions
- User Stories
- Use Cases

Định dạng đẹp và chuyên nghiệp.
```

---

# File 02 - `Business_Analysis.md`

```markdown
# Business Analysis Document
## Online Bank Account Opening System (eKYC)

---

# 1. Introduction

ABC Bank xây dựng hệ thống mở tài khoản trực tuyến nhằm số hóa toàn bộ quy trình eKYC, cho phép khách hàng mở tài khoản mà không cần đến quầy giao dịch.

Mục tiêu:

- Zero Manual Operation
- Giảm thời gian mở tài khoản
- Tăng trải nghiệm khách hàng
- Đảm bảo an toàn và tuân thủ pháp luật

---

# 2. Scope

## In Scope

- Đăng ký tài khoản
- OCR CCCD
- Face Matching
- Liveness Detection
- Sinh số tài khoản
- Thông báo kết quả

## Out of Scope

- Mở thẻ tín dụng
- Đăng ký khoản vay
- Internet Banking nâng cao

---

# 3. Actors

| Actor | Vai trò |
|--------|----------|
| Customer | Mở tài khoản |
| OCR Service | Đọc thông tin CCCD |
| Face Recognition AI | So khớp khuôn mặt |
| Liveness AI | Kiểm tra người thật |
| Core Banking | Sinh tài khoản |
| Notification Service | Gửi SMS/Email |

---

# 4. Business Flow

1. Khách hàng tải App.
2. Đăng ký thông tin.
3. Nhập số điện thoại.
4. Xác thực OTP.
5. Chụp CCCD mặt trước.
6. Chụp CCCD mặt sau.
7. OCR đọc dữ liệu.
8. Kiểm tra tính hợp lệ.
9. Chụp khuôn mặt.
10. Thực hiện Liveness.
11. Face Matching.
12. Đối chiếu dữ liệu.
13. Kiểm tra trùng khách hàng.
14. Sinh CIF.
15. Sinh số tài khoản.
16. Thông báo thành công.

---

# 5. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR01 | Đăng ký tài khoản |
| FR02 | Xác thực OTP |
| FR03 | Upload CCCD |
| FR04 | OCR CCCD |
| FR05 | Face Matching |
| FR06 | Liveness Detection |
| FR07 | Kiểm tra dữ liệu |
| FR08 | Sinh CIF |
| FR09 | Sinh số tài khoản |
| FR10 | Gửi Email |
| FR11 | Gửi SMS |
| FR12 | Audit Log |

---

# 6. Non Functional Requirements

| Category | Requirement |
|-----------|-------------|
| Security | AES-256 Encryption |
| Authentication | OTP |
| Authorization | JWT |
| Performance | <3 giây OCR |
| Availability | 99.9% |
| Scalability | 10.000 request/phút |
| Logging | Audit toàn bộ giao dịch |
| Backup | Daily Backup |
| Compliance | KYC & AML |

---

# 7. Business Rules

BR01. CCCD phải còn hiệu lực.

BR02. Khách hàng từ 18 tuổi trở lên.

BR03. Face Matching ≥ 95%.

BR04. Liveness phải PASS.

BR05. Không được mở tài khoản nếu CCCD tồn tại.

BR06. OTP chỉ có hiệu lực trong 5 phút.

BR07. Sai OTP quá 5 lần sẽ khóa phiên.

BR08. Tự động cấp số tài khoản nếu hợp lệ.

---

# 8. Assumptions

- Khách hàng có CCCD gắn chip.
- Có kết nối Internet.
- Camera hoạt động bình thường.
- OCR chính xác trên 98%.
- AI Face Matching hoạt động ổn định.
- Core Banking luôn sẵn sàng.

---

# 9. User Stories

US01

As a customer

I want to register online

So that I don't need to visit the bank.

---

US02

As a customer

I want to upload my ID card

So that the system can verify my identity.

---

US03

As a customer

I want to verify my face

So that the bank knows I am the real owner.

---

US04

As a customer

I want to receive OTP

So that my phone number is verified.

---

US05

As a customer

I want the account number generated automatically

So that I can use banking services immediately.

---

# 10. Use Cases

## UC01 Register

Actor:
Customer

Main Flow:

- Open App
- Register
- Verify OTP

---

## UC02 Upload ID

Actor:
Customer

Main Flow:

- Capture front image
- Capture back image
- OCR

---

## UC03 Face Verification

Actor:
Customer

Main Flow:

- Capture face
- Liveness
- Face Matching

---

## UC04 Open Account

Actor:
Core Banking

Main Flow:

- Validate information
- Create CIF
- Generate Account Number

---

## UC05 Notification

Actor:
Notification Service

Main Flow:

- Send SMS
- Send Email
```