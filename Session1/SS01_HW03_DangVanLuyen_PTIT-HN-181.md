### Prompt mới do bạn thiết kế

> Hãy đóng vai trò là một Java Developer thực hiện code review. Phân tích đoạn code dưới đây và kiểm tra các lỗi logic nghiệp vụ, đặc biệt trong trường hợp giá trị `amount` bằng 0 hoặc là số âm. Thuế VAT chỉ được tính cho hóa đơn có giá trị dương. Nếu phát hiện lỗi, hãy giải thích ngắn gọn và sửa lại code Java để chặn các trường hợp đầu vào không hợp lệ.

---

### Đoạn code Java đã được AI sửa đổi

```java
public class TaxCalculator {

    public static double calculateVAT(double amount) {

        if (amount <= 0) {
            throw new IllegalArgumentException(
                "Amount phải lớn hơn 0 để tính VAT"
            );
        }

        return amount * 0.1;
    }
}
```

**Giải thích:**

* Nếu `amount <= 0`, hàm sẽ ném ra `IllegalArgumentException` vì giá trị hóa đơn không hợp lệ.
* Chỉ khi `amount > 0` mới thực hiện tính VAT bằng công thức `amount * 0.1`.
* Điều này giúp tránh lỗi logic nghiệp vụ khi tính thuế cho hóa đơn âm hoặc bằng 0.
