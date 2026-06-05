# LEGO WORLD STORE - PHP MVC PROJECT

Chào mừng bạn đến với dự án Website bán đồ chơi Lego được xây dựng bằng PHP theo mô hình MVC (Model-View-Controller). 

Dự án này được thực hiện trong khuôn khổ môn học **Chuyên đề thực tế 2**, với đề tài **"Sử dụng công cụ AI (Google Gemini) hỗ trợ xây dựng Website LEGO Shop"**. Dự án không chỉ tập trung vào trải nghiệm người dùng và quy trình quản lý kho hàng, mà còn ứng dụng AI làm trợ lý ảo để hỗ trợ viết code, phân tích cơ sở dữ liệu và tìm lỗi (debug) nhằm tăng tốc độ phát triển.

## Cấu trúc thư mục (Project Structure)
```plaintext
lego_shop_php/
├── app/                    # Thư mục chính chứa logic ứng dụng
│   ├── core/               # Các file hệ thống cốt lõi (`App.php`, `Controller.php`, `Database.php`)
│   ├── controllers/        # Xử lý logic và điều hướng (ví dụ: `HomeController`, `AccountController`)
│   ├── models/             # Tương tác với Database (ví dụ: `ProductModel`, `AccountModel`)
│   └── views/              # Giao diện hiển thị (HTML/PHP)
│       ├── user/           # Giao diện khách hàng (home, login, register,...)
│       ├── admin/          # Giao diện quản trị (dashboard, products,...)
│       └── components/     # Thành phần dùng chung (header, footer, sidebar)
├── public/                 # Thư mục công khai (truy cập từ trình duyệt)
│   ├── assets/             # Tài nguyên tĩnh
│   │   ├── css/
│   │   ├── js/
│   │   ├── images/
│   │   └── fonts/
│   └── .htaccess           # Cấu hình URL thân thiện
├── .htaccess               # Rewrite tất cả yêu cầu về `index.php`
├── index.php               # Entry point (gọi `session_start()` và khởi tạo `App`)
└── lego_shop.sql           # SQL schema để import vào MySQL
```

## Yêu cầu hệ thống (Prerequisites)

- XAMPP (PHP 7.4 hoặc 8.x)
- Trình duyệt: Chrome, Edge hoặc Firefox
- Công cụ quản lý DB: phpMyAdmin (hoặc MySQL client)

## Hướng dẫn cài đặt và chạy (Setup Instructions)

### Bước 1: Sao chép dự án
- Tải mã nguồn và giải nén vào thư mục `htdocs` của XAMPP (ví dụ `C:\xampp\htdocs`).
- Đặt tên thư mục là `lego_shop_php`.

### Bước 2: Import database
- Khởi động Apache và MySQL trên XAMPP.
- Mở `http://localhost/phpmyadmin`.
- Tạo database mới tên `lego_shop` (Khuyến nghị chọn Collation là `utf8mb4_unicode_ci`).
- Vào tab Import và chọn file `lego_shop.sql` ở thư mục gốc dự án để nạp dữ liệu.

### Bước 3: Cấu hình kết nối database
- Mở file `app/core/Database.php` và kiểm tra các biến kết nối:

```php
private $db_name = "lego_shop"; // Tên database
private $username = "root";     // Tên user DB
private $password = "";         // Mật khẩu DB (nếu có)
```

Chỉnh sửa nếu bạn dùng tên database hoặc thông tin kết nối khác trên máy tính của mình.

### Bước 4: Chạy ứng dụng và Tài khoản Test
- Mở trình duyệt và truy cập: `http://localhost/lego_shop_php/`
- **Tài khoản Admin (để truy cập trang quản trị):** - Email: `admin@legoworld.com` (hoặc `admin`)
  - Mật khẩu: `123456`
- **Tài khoản Khách hàng (để test mua hàng):**
  - Email: `test@gmail.com`
  - Mật khẩu: `123456`

## Các tính năng nổi bật & Ứng dụng AI

- **Kiến trúc MVC:** Tách biệt rõ ràng logic xử lý (Model/Controller) và giao diện (View), code dễ đọc và dễ bảo trì.
- **Quản lý quy trình toàn diện:** Hỗ trợ đầy đủ luồng mua sắm của khách (Giỏ hàng, Checkout) và luồng quản trị kho hàng của Admin (Nhập xuất tồn, quản lý đơn hàng).
- **Hỗ trợ từ AI (Google Gemini):** Dự án có sự can thiệp của AI trong việc sinh mã cơ bản (boilerplate code), viết các câu truy vấn MySQL phức tạp (ví dụ: thống kê báo cáo) và hỗ trợ tìm, sửa lỗi (debug) nhanh chóng trong quá trình phát triển.

## Lưu ý quan trọng

- Nếu gặp lỗi 404 khi chuyển trang, kiểm tra `mod_rewrite` trong Apache đã bật chưa và cấu hình `.htaccess` có hoạt động không.
- Đảm bảo hàm `session_start();` luôn được gọi ở dòng đầu tiên của `index.php` để giỏ hàng và chức năng đăng nhập hoạt động đúng.