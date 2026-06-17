# BÀI 5: Thiết kế Quy trình & Prompt Kiểm chứng Đầu ra (AI Verifier)

## 1. Bối cảnh và ý đồ thiết kế quy trình 2 bước

Trong thực tế, AI có thể sinh ra mã nguồn chạy được nhưng vẫn tồn tại lỗi logic, lỗi xử lý dữ liệu biên hoặc các vấn đề liên quan đến ngày tháng.

Vì vậy, thay vì chỉ sử dụng một lần AI để sinh code, quy trình được thiết kế gồm:

### Bước 1 – Code Generation

Yêu cầu AI đóng vai trò lập trình viên Java tạo lớp `TicketValidator`.

Mục tiêu:

* Sinh mã nguồn theo đúng yêu cầu nghiệp vụ.
* Xử lý đầy đủ các trường hợp biên.
* Sử dụng API hiện đại của Java.

### Bước 2 – AI Auditing

Yêu cầu một AI khác hoặc cùng AI trong vai trò độc lập.

Mục tiêu:

* Không tin tưởng mã nguồn ở Bước 1.
* Tìm lỗi logic tiềm ẩn.
* Phản biện như một kỹ sư kiểm thử hoặc code reviewer.
* Đề xuất cải tiến.

Mô hình:

```text
Yêu cầu nghiệp vụ
        ↓
Bước 1: AI Code Generator
        ↓
Sinh TicketValidator.java
        ↓
Bước 2: AI Auditor
        ↓
Phát hiện lỗi
        ↓
Sửa mã nguồn
        ↓
Phiên bản cuối cùng
```

---

## 2. Prompt sinh mã nguồn (Bước 1)

Bạn là một Senior Java Developer.

Hãy viết lớp TicketValidator bằng Java để kiểm tra tính hợp lệ của mã vé xe khách GreenBus.

Quy tắc:

1. Mã vé phải bắt đầu bằng tiền tố "BUS-".
2. Tiếp theo là mã tỉnh/thành phố gồm đúng 2 ký tự chữ in hoa.
3. Tiếp theo là dấu "-" và 6 chữ số theo định dạng YYMMDD.
4. Ngày trong mã vé phải là ngày hợp lệ.
5. Ngày đi không được nằm trong quá khứ.
6. Phải xử lý các trường hợp:

    * null
    * chuỗi rỗng
    * khoảng trắng
    * mã sai định dạng
    * ngày không tồn tại (ví dụ 321332)
    * năm nhuận
7. Không được phát sinh NullPointerException.
8. Sử dụng thư viện java.time nếu có thể.
9. Viết kèm hàm main minh họa.
10. Giải thích ngắn gọn cách hoạt động của thuật toán.

Trả về mã nguồn Java hoàn chỉnh.

---

## 3. Prompt kiểm chứng độc lập (Bước 2)

Bạn là một Software Auditor và Security Reviewer độc lập.

Nhiệm vụ:

Phân tích đoạn mã Java dưới đây với thái độ phản biện.

Yêu cầu:

1. Không giả định code là đúng.
2. Tìm tất cả lỗi logic tiềm ẩn.
3. Kiểm tra:

    * NullPointerException
    * Sai định dạng Regex
    * Lỗi xử lý ngày tháng
    * Năm nhuận
    * Ngày 32 tháng 13
    * Vé ngày quá khứ
    * Chuyển giao năm mới
    * Múi giờ hệ thống
    * Lỗi parse YYMMDD
    * Lỗi bảo trì về sau
4. Đưa ra ví dụ đầu vào làm chương trình sai nếu có.
5. Đề xuất cách sửa.
6. Sinh lại phiên bản tốt hơn nếu phát hiện lỗi.

Đây là mã nguồn cần kiểm tra:

[PASTE CODE HERE]

---

## 4. Minh chứng hội thoại (Text Log)

### Bước 1 – AI sinh mã nguồn lần đầu

**User**

```text
Hãy viết lớp TicketValidator kiểm tra mã vé GreenBus.
```

**AI**

```java
import java.text.SimpleDateFormat;
import java.util.Date;

public class TicketValidator {

    public static boolean isValid(String ticketCode) {

        if (ticketCode == null) {
            return false;
        }

        String regex = "^BUS-[A-Z]{2}-\\d{6}$";

        if (!ticketCode.matches(regex)) {
            return false;
        }

        try {

            String datePart = ticketCode.substring(7);

            SimpleDateFormat sdf =
                    new SimpleDateFormat("yyMMdd");

            Date travelDate =
                    sdf.parse(datePart);

            return travelDate.after(new Date());

        } catch (Exception e) {
            return false;
        }
    }
}
```

---

### Bước 2 – AI Auditor phát hiện lỗi

**User**

```text
Hãy kiểm toán đoạn mã trên.
```

**AI Auditor**

```text
Phát hiện các vấn đề:

1. SimpleDateFormat mặc định lenient=true.

Ví dụ:

321332

vẫn có thể parse thành một ngày hợp lệ khác.

=> Sai nghiệp vụ.

------------------------------------------------

2. travelDate.after(new Date())

Yêu cầu nghiệp vụ:

Ngày đi >= ngày hiện tại.

Nhưng đoạn code chỉ cho phép:

Ngày đi > ngày hiện tại.

Vé của chính ngày hôm nay bị từ chối.

------------------------------------------------

3. Không xử lý rõ múi giờ hệ thống.

Nếu hệ thống chạy gần thời điểm chuyển ngày
có thể xảy ra sai lệch.

------------------------------------------------

4. API java.util.Date và SimpleDateFormat
đã cũ.

Nên sử dụng java.time.LocalDate.

------------------------------------------------

5. Sử dụng substring cứng.

Nếu format thay đổi trong tương lai
sẽ khó bảo trì.
```

---

## 5. Mã nguồn cuối cùng sau kiểm duyệt

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.time.format.ResolverStyle;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class TicketValidator {

    private static final Pattern TICKET_PATTERN =
            Pattern.compile("^BUS-([A-Z]{2})-(\\d{6})$");

    private static final DateTimeFormatter DATE_FORMATTER =
            DateTimeFormatter.ofPattern("uuMMdd")
                    .withResolverStyle(ResolverStyle.STRICT);

    public static boolean isValid(String ticketCode) {

        if (ticketCode == null || ticketCode.isBlank()) {
            return false;
        }

        Matcher matcher =
                TICKET_PATTERN.matcher(ticketCode.trim());

        if (!matcher.matches()) {
            return false;
        }

        String datePart = matcher.group(2);

        try {

            LocalDate travelDate =
                    LocalDate.parse(datePart, DATE_FORMATTER);

            LocalDate today =
                    LocalDate.now();

            return !travelDate.isBefore(today);

        } catch (DateTimeParseException ex) {
            return false;
        }
    }

    public static void main(String[] args) {

        System.out.println(
                isValid("BUS-HN-260615"));

        System.out.println(
                isValid("BUS-SG-321332"));

        System.out.println(
                isValid("BUS-DN-260229"));

        System.out.println(
                isValid(null));

        System.out.println(
                isValid(""));
    }
}
```

### Điểm cải tiến của phiên bản cuối

* Sử dụng `java.time.LocalDate` hiện đại.
* Sử dụng `DateTimeFormatter` với `ResolverStyle.STRICT`.
* Chặn ngày không hợp lệ như `321332`.
* Không phát sinh `NullPointerException`.
* Chấp nhận ngày hiện tại (`>= today`).
* Regex kiểm tra chính xác cấu trúc mã vé.
* Dễ bảo trì và phù hợp chuẩn Java hiện đại.
