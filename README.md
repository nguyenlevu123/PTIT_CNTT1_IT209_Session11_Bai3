# Bài 3: Tối ưu tốc độ CI bằng Gradle Dependency Caching

## Mục tiêu
- Cấu hình cơ chế lưu cache tự động cho các gói thư viện phụ thuộc của Gradle.
- Giảm thiểu thời gian thực thi của luồng CI trong các lần commit tiếp theo.
- So sánh thời gian chạy thực tế giữa hai lần build: Không có cache (Cache Miss) và Có cache (Cache Hit).

---

## 1. Cấu trúc Dự án
```text
ss11/b3/
├── .github/
│   └── workflows/
│       └── ci-caching.yml      # Pipeline CI có cấu hình cache: 'gradle'
├── gradle/wrapper/
├── src/
│   ├── main/java/com/example/demo/DemoApplication.java
│   └── test/java/com/example/demo/DemoApplicationTests.java
├── build.gradle
├── settings.gradle
├── gradlew
├── report.md                   # Báo cáo so sánh số liệu thực nghiệm
└── README.md
```

---

## 2. Thiết lập Caching
Tại `.github/workflows/ci-caching.yml`:
```yaml
- name: Set up JDK 17 with Gradle Caching
  uses: actions/setup-java@v4
  with:
    java-version: '17'
    distribution: 'temurin'
    cache: 'gradle'
```

---

## 3. Tóm tắt Kết quả Đo lường
- **Chạy lần đầu (Cache Miss)**: 2m 12s.
- **Chạy lần thứ hai (Cache Hit)**: 31s.
- **Hiệu năng cải thiện**: Tốc độ tăng hơn **4.2 lần**.

Chi tiết xem tại báo cáo đầy đủ: 📄 [report.md](report.md).
