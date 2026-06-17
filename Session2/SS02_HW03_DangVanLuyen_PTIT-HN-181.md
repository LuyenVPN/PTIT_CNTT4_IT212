## 1. Giải thích nguyên lý sinh lỗi ảo giác (Hallucination)

Hiện tượng **hallucination** xảy ra khi AI tạo ra thông tin nghe có vẻ hợp lý nhưng thực tế không đúng.

Trong ví dụ này, prompt yêu cầu:

> "Hãy sử dụng StringUtils.hasSpecialCharacters()"

Vấn đề là phương thức `hasSpecialCharacters()` **không tồn tại** trong lớp `StringUtils` của thư viện Apache Commons Lang.

AI dễ sinh lỗi vì:

1. **AI dự đoán xác suất từ tiếp theo**, không phải trình biên dịch Java.

    * AI nhận thấy:

        * Có lớp `StringUtils`.
        * Có yêu cầu kiểm tra ký tự đặc biệt.
    * AI suy luận rằng một phương thức tên `hasSpecialCharacters()` "có vẻ hợp lý" nên sinh ra mã nguồn sử dụng nó.

2. **Prompt mang tính dẫn dắt sai (leading prompt)**.

    * Khi người dùng khẳng định hoặc ngầm giả định một API tồn tại, AI thường ưu tiên làm theo yêu cầu thay vì kiểm chứng.

3. **AI không tự động xác minh thư viện thực tế**.

    * Nếu không được yêu cầu kiểm tra tài liệu chính thức, AI có thể tạo ra:

        * Class không tồn tại.
        * Method không tồn tại.
        * Tham số sai.
        * API đã bị deprecated.

4. **Tên phương thức nghe rất hợp lý**.

    * `hasSpecialCharacters()`
    * `isNumericOnly()`
    * `isEmailValid()`

   Đây đều là những tên mà lập trình viên có thể tự nghĩ ra, nên AI dễ "bịa" nếu không kiểm chứng.

Kết quả là mã nguồn sinh ra có thể:

```java
StringUtils.hasSpecialCharacters(text);
```

và gây lỗi biên dịch:

```text
Cannot resolve method 'hasSpecialCharacters'
```

---

## 2. Prompt tối ưu mới

Hãy viết một hàm Java kiểm tra xem một chuỗi có chứa ký tự đặc biệt hay không.

Yêu cầu:

* Chỉ sử dụng các API chính thức của Java Standard Library hoặc thư viện phổ biến có tài liệu chính thức.
* Không được tự tạo hoặc giả định sự tồn tại của bất kỳ phương thức nào.
* Trước khi viết code, hãy nêu rõ lớp và phương thức sẽ sử dụng.
* Giải thích ngắn gọn tại sao phương thức đó phù hợp.
* Trích dẫn hoặc dẫn nguồn tài liệu chính thức (Oracle Java Documentation hoặc tài liệu chính thức của thư viện được sử dụng) để chứng minh API đó tồn tại.
* Nếu không tìm thấy API phù hợp thì hãy sử dụng biểu thức chính quy (Regular Expression) của Java thay vì bịa ra phương thức mới.
* Trả về mã nguồn Java hoàn chỉnh nằm trong khối code markdown.

---

## 3. Mã nguồn Java sinh ra từ Prompt mới

Ví dụ sử dụng API chính thức:

* Lớp: `java.util.regex.Pattern`
* Phương thức: `Pattern.compile()`
* Phương thức: `Matcher.find()`

Đây đều là API chính thức của Java Standard Library.

```java
import java.util.regex.Pattern;

public class StringValidator {

    // Ký tự đặc biệt: không phải chữ cái, số hoặc khoảng trắng
    private static final Pattern SPECIAL_CHARACTER_PATTERN =
            Pattern.compile("[^a-zA-Z0-9\\s]");

    public static boolean hasSpecialCharacter(String input) {
        if (input == null || input.isEmpty()) {
            return false;
        }

        return SPECIAL_CHARACTER_PATTERN.matcher(input).find();
    }

    public static void main(String[] args) {
        System.out.println(hasSpecialCharacter("HelloWorld"));      // false
        System.out.println(hasSpecialCharacter("Hello World"));     // false
        System.out.println(hasSpecialCharacter("Hello@World"));     // true
        System.out.println(hasSpecialCharacter("Java#17"));         // true
        System.out.println(hasSpecialCharacter("123456"));          // false
    }
}
```

### Cơ sở kiểm chứng API

Các API được sử dụng đều thuộc thư viện chuẩn Java:

* Java Platform Standard Edition `java.util.regex.Pattern`
* `Pattern.compile(String regex)`
* `Pattern.matcher(CharSequence input)`
* `Matcher.find()`

Theo tài liệu chính thức của Oracle:

* `Pattern.compile()` dùng để biên dịch biểu thức chính quy.
* `Matcher.find()` tìm kiếm xem có đoạn nào khớp với mẫu regex hay không.

Vì vậy giải pháp trên tránh hoàn toàn hiện tượng "bịa API", sử dụng các phương thức đã được kiểm chứng và tồn tại thực sự trong Java Standard Library.

