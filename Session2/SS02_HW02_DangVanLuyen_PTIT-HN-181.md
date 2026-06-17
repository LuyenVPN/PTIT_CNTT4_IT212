### Prompt sau khi tối ưu

Hãy viết cho tôi class `VNPayPaymentService` bằng Java để thực hiện thanh toán trực tuyến qua VNPay.

Yêu cầu bảo mật bắt buộc:

* Tuyệt đối không hardcode API Key, Secret Key, Access Token hoặc bất kỳ thông tin nhạy cảm nào trong mã nguồn.
* Khóa bí mật VNPay phải được nạp từ biến môi trường bằng `System.getenv("VNPAY_HASH_SECRET")`.
* Nếu biến môi trường không tồn tại, có giá trị `null` hoặc chuỗi rỗng thì phải ném ra ngoại lệ `IllegalStateException` với thông báo rõ ràng.
* Mã nguồn phải tuân thủ nguyên tắc bảo mật, không ghi log hoặc hiển thị Secret Key ra màn hình.
* Tạo phương thức lấy Secret Key an toàn và phương thức tạo chữ ký HMAC SHA512 cho dữ liệu thanh toán.
* Sử dụng Java chuẩn, viết mã dễ đọc, có chú thích ngắn gọn cho các phần quan trọng.

### Mã nguồn Java hoàn chỉnh, an toàn

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.nio.charset.StandardCharsets;

public class VNPayPaymentService {

    private static final String ENV_SECRET_KEY = "VNPAY_HASH_SECRET";

    /**
     * Lấy Secret Key từ biến môi trường.
     * Nếu không tồn tại hoặc rỗng thì dừng hệ thống để tránh chạy sai cấu hình.
     */
    private String getHashSecret() {
        String secret = System.getenv(ENV_SECRET_KEY);

        if (secret == null || secret.trim().isEmpty()) {
            throw new IllegalStateException(
                "Missing required environment variable: " + ENV_SECRET_KEY
            );
        }

        return secret;
    }

    /**
     * Tạo chữ ký HMAC SHA512 cho dữ liệu VNPay.
     *
     * @param data Chuỗi dữ liệu cần ký
     * @return Chuỗi hash dạng hex
     */
    public String generateSecureHash(String data) {
        try {
            String secretKey = getHashSecret();

            Mac hmac512 = Mac.getInstance("HmacSHA512");
            SecretKeySpec keySpec = new SecretKeySpec(
                    secretKey.getBytes(StandardCharsets.UTF_8),
                    "HmacSHA512"
            );

            hmac512.init(keySpec);

            byte[] hashBytes = hmac512.doFinal(
                    data.getBytes(StandardCharsets.UTF_8)
            );

            StringBuilder result = new StringBuilder();

            for (byte b : hashBytes) {
                result.append(String.format("%02x", b));
            }

            return result.toString();

        } catch (Exception e) {
            throw new RuntimeException(
                "Failed to generate VNPay secure hash",
                e
            );
        }
    }

    /**
     * Ví dụ tạo URL thanh toán.
     * Thực tế có thể bổ sung thêm các tham số VNPay theo tài liệu chính thức.
     */
    public String createPaymentSignature(String paymentData) {
        return generateSecureHash(paymentData);
    }
}
```

### Ví dụ cấu hình biến môi trường

Linux / macOS:

```bash
export VNPAY_HASH_SECRET=your_vnpay_secret_key
```

Windows CMD:

```cmd
set VNPAY_HASH_SECRET=your_vnpay_secret_key
```

Windows PowerShell:

```powershell
$env:VNPAY_HASH_SECRET="your_vnpay_secret_key"
```

Cách này tuân thủ nguyên tắc bảo mật vì khóa bí mật không xuất hiện trong mã nguồn, không bị commit lên Git và có kiểm tra an toàn khi hệ thống khởi động.
