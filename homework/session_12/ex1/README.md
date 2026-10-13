
## Thiết kế

Workflow kích hoạt khi push vào `main`. Job `test-matrix` có `strategy.matrix.java-version: ['17', '21']`, tạo hai job độc lập.

Mỗi job checkout bằng `actions/checkout@v5`, thiết lập Temurin bằng `actions/setup-java@v5`, bật `cache: 'gradle'`, rồi chạy Gradle test.

Project biên dịch mã nguồn với toolchain Java 17 để JAR vẫn tương thích Java 17. Task `test` chọn JVM thông qua thuộc tính `testJavaVersion`, vì vậy các test thực sự chạy trên JVM 17 hoặc 21 tương ứng với ma trận.

```bash
./gradlew test -PtestJavaVersion=17
./gradlew test -PtestJavaVersion=21
```

`fail-fast: false` cho phép job còn lại chạy tiếp nếu một phiên bản thất bại.

## Minh chứng

Sau khi push, mở GitHub Actions → Java Matrix Tests. Chụp hai job `test-matrix (17)` và `test-matrix (21)` đều xanh, lưu vào `homework/session_12/ex1/matrix-success.png`.

Chưa ghi nhận kết quả thực tế trên GitHub Actions cho workflow mới. Bổ sung ảnh sau khi hai job hoàn tất thành công.
