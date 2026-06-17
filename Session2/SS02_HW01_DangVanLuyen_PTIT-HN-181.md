BÀI 1: Phân tích & Lựa chọn (Lựa chọn công cụ tối ưu & Hạn chế chuyển đổi ngữ cảnh) (100 điểm)
Bối cảnh: Bạn đang tham gia phát triển dự án hệ thống quản lý thư viện trường học và cần thực hiện 3 đầu việc sau trong khoảng thời gian rất ngắn:
Viết tài liệu hướng dẫn sử dụng API (API Guide): Một tài liệu bằng văn bản Markdown mô tả nghiệp vụ và cấu trúc gọi API cho các lập trình viên khác trong nhóm.
Tái cấu trúc (Refactor) lớp dữ liệu Book: Bạn cần cập nhật định nghĩa và logic của đối tượng Book trên nhiều tệp tin liên quan đang phụ thuộc lẫn nhau bao gồm: Book.java, BookService.java, BookController.java, và BookRepository.java.
Sửa lỗi cú pháp nhỏ (Quick Fix): Khắc phục lỗi thiếu dấu chấm phẩy ; hoặc khai báo sai kiểu dữ liệu tại một dòng cụ thể ở tệp mã nguồn đang mở.
Đề bài: Dựa trên kiến thức về phạm vi hiểu ngữ cảnh (Context Window) và tác hại của việc chuyển đổi ngữ cảnh (Context Switching) đã học ở Lesson 2 & 3, hãy chọn phương án phân bổ công cụ tối ưu nhất dưới đây và giải thích ngắn gọn lý do tại sao các phương án khác chưa tốt:
Phương án A: Sử dụng Web Chat (như ChatGPT/Claude trên trình duyệt web) cho cả 3 tác vụ. Lập trình viên liên tục sao chép nội dung các file từ IDE dán vào Web Chat rồi sao chép ngược lại.
Phương án B: Sử dụng Trợ lý lập trình tiêu chuẩn (Inline Code Assistant như GitHub Copilot inline suggestions) ngay tại chỗ trong IDE để tự động hoàn thành và xử lý cả 3 tác vụ.
Phương án C: Sử dụng Web Chat để phác thảo tài liệu API (tận dụng khả năng lập luận ngôn ngữ tốt); sử dụng Trợ lý lập trình cấp cao (Agentic/Repository-wide Assistant) để phân tích toàn bộ dự án và tự động cập nhật đồng bộ cấu trúc Book trên 4 tệp tin; sử dụng Trợ lý lập trình tiêu chuẩn (Inline completion) để sửa nhanh lỗi cú pháp tại chỗ.
Yêu cầu đầu ra:
Đáp án lựa chọn (A, B hoặc C).
Phân tích chi tiết tại sao phương án đã chọn là tối ưu nhất dựa trên khía cạnh quản lý ngữ cảnh dự án và năng suất lập trình.
Chỉ rõ nhược điểm hoặc giới hạn của 2 phương án còn lại.

## Đáp án: **Phương án C**

### Vì sao phương án C là tối ưu nhất?

Phương án C tận dụng đúng thế mạnh của từng loại công cụ và giảm thiểu tối đa vấn đề **Context Switching (chuyển đổi ngữ cảnh)** cũng như giới hạn **Context Window (phạm vi hiểu ngữ cảnh)**.

#### 1. Viết tài liệu API Guide → Web Chat

Tài liệu API là nội dung thiên về mô tả nghiệp vụ, giải thích luồng xử lý, cấu trúc request/response và hướng dẫn sử dụng.

Web Chat như ChatGPT hoặc Claude có khả năng xử lý ngôn ngữ tự nhiên rất tốt, giúp:

* Tạo tài liệu Markdown nhanh.
* Trình bày rõ ràng, dễ đọc.
* Hỗ trợ diễn giải nghiệp vụ và ví dụ API.

Ở tác vụ này không cần hiểu toàn bộ mã nguồn dự án nên Web Chat là lựa chọn phù hợp.

---

#### 2. Refactor lớp Book → Agentic/Repository-wide Assistant

Đây là tác vụ phức tạp nhất vì liên quan đến nhiều file:

* Book.java
* BookService.java
* BookController.java
* BookRepository.java

Các file có quan hệ phụ thuộc lẫn nhau.

Một Agentic Assistant có thể:

* Quét toàn bộ repository.
* Hiểu dependency giữa các lớp.
* Theo dõi thay đổi xuyên nhiều file.
* Cập nhật đồng bộ tất cả vị trí bị ảnh hưởng.

Điều này tận dụng phạm vi ngữ cảnh lớn của công cụ cấp repository, giúp tránh:

* Bỏ sót file.
* Sai lệch logic giữa các lớp.
* Phải copy/paste hàng loạt mã nguồn.

Năng suất cao hơn rất nhiều so với xử lý thủ công.

---

#### 3. Quick Fix lỗi cú pháp → Inline Assistant

Lỗi như:

```java
int age = "20";
```

hoặc:

```java
System.out.println("Hello")
```

chỉ cần sửa tại một dòng cụ thể.

Inline Assistant trong IDE:

* Hiểu ngữ cảnh cục bộ của file đang mở.
* Đề xuất sửa lỗi tức thì.
* Không cần gửi dữ liệu ra ngoài.
* Không làm gián đoạn luồng làm việc.

Đây là tình huống lý tưởng cho công cụ gợi ý mã trực tiếp.

---

## Tại sao phương án A chưa tốt?

### A. Dùng Web Chat cho cả 3 tác vụ

Nhược điểm:

#### 1. Context Window bị giới hạn

Khi refactor Book trên nhiều file, lập trình viên phải:

* Mở từng file.
* Copy mã nguồn.
* Dán vào Web Chat.

Nếu dự án lớn:

* Dễ vượt giới hạn ngữ cảnh.
* AI không nhìn thấy toàn bộ repository.
* Có thể bỏ sót dependency.

#### 2. Context Switching rất nhiều

Quy trình:

```text
IDE
 ↓
Copy code
 ↓
Web Chat
 ↓
Nhận kết quả
 ↓
Copy lại
 ↓
IDE
```

Lặp đi lặp lại liên tục.

Điều này:

* Mất thời gian.
* Giảm tập trung.
* Tăng nguy cơ lỗi sao chép.

#### 3. Không phù hợp cho Quick Fix

Một lỗi thiếu dấu `;` chỉ mất vài giây trong IDE nhưng lại phải chuyển sang Web Chat là không hiệu quả.

---

## Tại sao phương án B chưa tốt?

### B. Dùng Inline Code Assistant cho cả 3 tác vụ

Nhược điểm:

#### 1. Không mạnh về tài liệu dài

Inline Assistant chủ yếu hoạt động trên:

* Dòng mã.
* Hàm.
* File hiện tại.

Viết một API Guide hoàn chỉnh bằng Markdown sẽ khó khăn hơn nhiều so với Web Chat.

#### 2. Hạn chế về ngữ cảnh toàn dự án

Inline Assistant thường tập trung vào:

* File đang mở.
* Một phạm vi mã tương đối nhỏ.

Khi refactor Book xuyên:

* Controller
* Service
* Repository
* Model

nó có thể không hiểu đầy đủ toàn bộ dependency như Agentic Assistant.

#### 3. Không tận dụng đúng thế mạnh công cụ

Inline Assistant rất mạnh cho:

* Auto-complete.
* Sinh đoạn code ngắn.
* Sửa lỗi cú pháp.

Nhưng không phải lựa chọn tối ưu cho:

* Tài liệu nghiệp vụ dài.
* Phân tích và thay đổi đồng bộ toàn repository.

---

## Kết luận

**Phương án C là lựa chọn tối ưu nhất** vì:

* **Web Chat** → tốt nhất cho tài liệu API và diễn giải nghiệp vụ.
* **Agentic/Repository-wide Assistant** → tốt nhất cho refactor nhiều file phụ thuộc lẫn nhau.
* **Inline Assistant** → tốt nhất cho sửa lỗi cú pháp nhanh tại chỗ.

Cách phân bổ này vừa khai thác đúng năng lực của từng công cụ, vừa giảm tối đa **Context Switching**, đồng thời sử dụng hiệu quả **Context Window** ở từng cấp độ ngữ cảnh của dự án.
