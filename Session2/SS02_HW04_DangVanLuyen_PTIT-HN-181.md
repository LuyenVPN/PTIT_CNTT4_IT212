## Đáp án: **Phương án B**

### Phân tích lý do lựa chọn

Phương án B thể hiện đúng tinh thần của **liêm chính học thuật** và vai trò **người kiểm duyệt (reviewer)** khi sử dụng AI.

AI là công cụ hỗ trợ, không phải nguồn chân lý tuyệt đối. Người học có trách nhiệm:

1. **Đánh giá tính đúng đắn của kết quả AI tạo ra**

    * Đoạn code dùng `double` có thể chạy đúng với các bộ test đơn giản.
    * Tuy nhiên trong lĩnh vực tài chính, sai số dấu phẩy động là rủi ro kỹ thuật đã được biết đến rộng rãi.

2. **Tra cứu tài liệu chính thức**

    * Tài liệu Java khuyến nghị sử dụng lớp `BigDecimal` cho các phép tính tài chính cần độ chính xác cao.
    * `BigDecimal` tránh được lỗi biểu diễn nhị phân của `double` và `float`.

3. **Cải thiện prompt**

    * Không chấp nhận đầu ra đầu tiên của AI một cách thụ động.
    * Thiết kế prompt mới yêu cầu:

        * Dùng `BigDecimal`.
        * Chỉ rõ `RoundingMode`.
        * Giải thích cơ sở kỹ thuật.

4. **Tự kiểm thử**

    * Viết thêm hàm `main`.
    * Thử các trường hợp:

        * Số tiền rất lớn.
        * Lãi suất rất nhỏ.
        * Thời gian gửi rất dài.
    * Xác minh kết quả thay vì tin tưởng hoàn toàn vào AI.

Đây chính là quy trình làm việc của một lập trình viên chuyên nghiệp:

```text
AI đề xuất
      ↓
Đọc hiểu
      ↓
Kiểm chứng tài liệu
      ↓
Cải tiến giải pháp
      ↓
Kiểm thử độc lập
      ↓
Mới sử dụng kết quả
```

---

## Vì sao phương án A không phù hợp?

### A. Sao chép nguyên văn vì AI nói đúng

Đây là hành vi thiếu trách nhiệm học thuật.

Các vấn đề:

* Tin tưởng AI tuyệt đối mà không kiểm chứng.
* Không đánh giá tính phù hợp của giải pháp.
* Chỉ quan tâm việc "qua test" thay vì chất lượng kỹ thuật.

Ví dụ:

```java
System.out.println(0.1 + 0.2);
```

Kết quả:

```text
0.30000000000000004
```

Nếu tính lãi hàng nghìn hoặc hàng triệu giao dịch:

* Sai số có thể tích lũy.
* Gây chênh lệch tiền thực tế.

Do đó việc "AI bảo đúng" không phải là căn cứ kỹ thuật đủ mạnh để nộp bài.

---

## Vì sao phương án C không phù hợp?

### C. Đổi từ double sang float

Đây là giải pháp sai về bản chất.

`float` còn kém chính xác hơn `double`.

Độ chính xác xấp xỉ:

| Kiểu dữ liệu | Số chữ số chính xác     |
| ------------ | ----------------------- |
| float        | ~7 chữ số               |
| double       | ~15-16 chữ số           |
| BigDecimal   | Theo số chữ số khai báo |

Do đó:

```java
double → float
```

không khắc phục được lỗi làm tròn mà còn làm sai số lớn hơn.

Ngoài ra phương án này còn:

* Không tra cứu tài liệu.
* Không kiểm thử.
* Không đánh giá rủi ro nghiệp vụ.

Đây là ví dụ điển hình của việc sửa đổi theo cảm tính thay vì dựa trên bằng chứng kỹ thuật.

---

## Kết luận

**Chọn B.**

Vì phương án B:

* Nhận diện được hạn chế của đầu ra AI.
* Kiểm chứng bằng tài liệu Java chính thức.
* Áp dụng giải pháp chuẩn ngành (`BigDecimal` + `RoundingMode`).
* Chủ động xây dựng bộ kiểm thử để xác nhận kết quả.

Đây là cách sử dụng AI có trách nhiệm, phù hợp với yêu cầu của liêm chính học thuật và quy trình phát triển phần mềm trong thực tế.
