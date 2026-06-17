### Nội dung Prompt sau khi tối ưu

> Hãy giải thích ngắn gọn hàm Java dưới đây. Mô tả rõ điều kiện rẽ nhánh `if`, giá trị đầu vào `points`, và kết quả trả về trong từng trường hợp để tôi hiểu được logic nghiệp vụ phân loại hạng thành viên.

---

### Phản hồi nhận được từ AI sau khi chạy prompt

Hàm `checkLevel(int points)` dùng để xác định hạng thành viên dựa trên số điểm tích lũy của khách hàng.

* Nếu `points >= 1000` thì điều kiện `if` đúng và hàm trả về `"VIP"`.
* Nếu `points < 1000` thì điều kiện `if` sai và hàm trả về `"Standard"`.

Ý nghĩa nghiệp vụ:

* Khách hàng có từ 1000 điểm trở lên được xếp hạng **VIP**.
* Khách hàng có dưới 1000 điểm được xếp hạng **Standard**.

Ví dụ:

* `checkLevel(1200)` → `"VIP"`
* `checkLevel(1000)` → `"VIP"`
* `checkLevel(850)` → `"Standard"`
