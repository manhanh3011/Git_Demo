# Phân Tích Luồng Dự Án Website Quản Lý Tour

## 📋 Tổng Quan Dự Án

Website Quản Lý Tour là một hệ thống quản lý tour du lịch được xây dựng bằng PHP thuần, sử dụng kiến trúc MVC (Model-View-Controller) với cơ chế routing tùy chỉnh. Dự án được thiết kế để phục vụ việc quản lý các tour du lịch, bao gồm quản lý tài khoản, tour, booking, hướng dẫn viên và báo cáo thống kê.

### 🛠 Công Nghệ Sử Dụng

- **Backend**: PHP 8.x (thuần, không dùng framework)
- **Database**: MySQL với PDO
- **Frontend**: HTML5, CSS3, JavaScript (ES6+), Bootstrap 5
- **Admin Template**: AdminLTE 3
- **Package Manager**: Composer
- **External Libraries**:
  - PHPSpreadsheet (đọc/xử lý file Excel)
  - Bootstrap 5 (UI components)
  - Font Awesome (icons)

---

## 🏗 Kiến Trúc Tổng Quan

### Cấu Trúc Thư Mục

```
website_quan_ly_tour/
├── composer.json                    # Quản lý dependencies
├── index.php                        # Entry point & routing
├── config/
│   └── config.php                   # Cấu hình database & constants
├── src/
│   ├── controllers/                 # Logic xử lý nghiệp vụ
│   ├── models/                      # Xử lý dữ liệu & database
│   └── helpers/                     # Hàm tiện ích
├── views/                           # Templates & UI
│   ├── layouts/                     # Layouts & blocks
│   ├── admin/                       # Giao diện admin
│   ├── auth/                        # Giao diện đăng nhập
│   └── guide/                       # Giao diện HDV
├── public/                          # Tài nguyên tĩnh
│   ├── css/                         # Stylesheets
│   ├── js/                          # JavaScript files
│   ├── dist/                        # Compiled assets
│   └── uploads/                     # File uploads
└── docs/                            # Tài liệu hướng dẫn
```

---

## 🔄 Luồng Xử Lý Request

### 1. Entry Point (`index.php`)

**Quy trình xử lý:**

```php
// 1. Nạp cấu hình
$config = require 'config/config.php';

// 2. Nạp helpers
require_once 'src/helpers/helpers.php';
require_once 'src/helpers/database.php';

// 3. Nạp models & controllers
require_once 'src/models/*.php';
require_once 'src/controllers/*.php';

// 4. Khởi tạo controllers
$controllers = [...];

// 5. Xác định route từ $_GET['act']
$act = $_GET['act'] ?? '/';

// 6. Xử lý route đặc biệt (có tham số)
if (strpos($act, 'tours/edit/') === 0) {
    $id = str_replace('tours/edit/', '', $act);
    $tourController->edit($id);
    exit;
}

// 7. Route matching với match() expression
match ($act) {
    '/' => $homeController->welcome(),
    'login' => $authController->login(),
    'tours' => $tourController->index(),
    // ... các route khác
    default => $homeController->notFound()
};
```

### 2. Cơ Chế Authentication

**Session-based Authentication:**

```php
// Kiểm tra đăng nhập
function isLoggedIn() {
    return isset($_SESSION['user_id']);
}

// Lấy thông tin user hiện tại
function getCurrentUser() {
    if (!isLoggedIn()) return null;
    return new User([
        'id' => $_SESSION['user_id'],
        'name' => $_SESSION['user_name'],
        'role' => $_SESSION['user_role']
    ]);
}

// Phân quyền
function isAdmin() { /* kiểm tra role admin */ }
function isGuide() { /* kiểm tra role hướng dẫn viên */ }

// Bảo vệ route
function requireLogin() { /* redirect về login */ }
function requireAdmin() { /* yêu cầu quyền admin */ }
```

### 3. MVC Pattern Implementation

#### Model Layer

**Cấu trúc Model cơ bản:**
```php
class User {
    public $id, $name, $email, $role, $status;

    // CRUD operations
    public static function find($id) { /* SELECT */ }
    public static function create(User $user) { /* INSERT */ }
    public static function update(User $user) { /* UPDATE */ }
    public static function delete($id) { /* DELETE */ }

    // Business logic
    public function isAdmin() { return $this->role === 'admin'; }
    public function isGuide() { return $this->role === 'huong_dan_vien'; }
}
```

#### Controller Layer

**Cấu trúc Controller:**
```php
class TourController {
    public function index() {
        // 1. Lấy dữ liệu từ Model
        $tours = Tour::getAll();

        // 2. Xử lý logic nghiệp vụ
        $data = [
            'tours' => $tours,
            'title' => 'Danh sách Tour'
        ];

        // 3. Render view
        view('admin.tours.index', $data);
    }

    public function create() {
        // Hiển thị form tạo mới
        view('admin.tours.create', [
            'title' => 'Thêm Tour Mới'
        ]);
    }
}
```

#### View Layer

**Template Rendering với Output Buffering:**

```php
// Trong view (ví dụ: home.php)
<?php
ob_start(); // Bắt đầu capture output
?>

<h1>Trang Chủ</h1>
<p>Nội dung trang...</p>

<?php
$content = ob_get_clean(); // Lấy nội dung đã capture

// Truyền vào layout
view('layouts.AdminLayout', [
    'title' => 'Trang Chủ',
    'content' => $content
]);
?>
```

---

## 📊 Cơ Sở Dữ Liệu

### Các Bảng Chính

```sql
-- Tài khoản người dùng
tai_khoan (
    id, ho_ten, email, sdt, mat_khau,
    phan_quyen, trang_thai, ngay_tao, ngay_cap_nhat
)

-- Tour du lịch
tour (
    id, ten_tour, id_danh_muc, gia_tour, mo_ta,
    trang_thai, ngay_tao, ngay_cap_nhat
)

-- Booking/Đặt tour
booking (
    id, id_tour, id_hdv, ngay_khoi_hanh,
    so_luong_khach, tong_tien, trang_thai, ghi_chu
)

-- Hướng dẫn viên
huong_dan_vien (
    id, id_tai_khoan, ho_ten, sdt, kinh_nghiem,
    chung_chi, trang_thai
)

-- Danh mục tour
danh_muc_tour (
    id, ten_danh_muc, mo_ta, trang_thai
)

-- Nhật ký tour (cho HDV ghi nhận hoạt động)
nhat_ky_tour (
    id, id_booking, id_hdv, noi_dung,
    hinh_anh, ngay_tao
)
```

### Database Connection

**Singleton Pattern với PDO:**

```php
function getDB() {
    static $pdo = null;

    if ($pdo === null) {
        $config = require 'config/config.php';
        $dsn = "mysql:host={$config['host']};dbname={$config['name']};charset={$config['charset']}";

        $pdo = new PDO($dsn, $config['user'], $config['pass'], [
            PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
            PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC
        ]);
    }

    return $pdo;
}
```

---

## 👥 Hệ Thống Phân Quyền

### Các Vai Trò Người Dùng

1. **Admin (Quản trị viên)**
   - Quản lý toàn bộ hệ thống
   - CRUD tất cả entities
   - Xem báo cáo thống kê
   - Quản lý tài khoản

2. **Guide (Hướng dẫn viên)**
   - Xem danh sách booking được phân công
   - Ghi nhật ký tour
   - Cập nhật thông tin khách
   - Quản lý check-in/check-out

### Bảo Mật Route

```php
// Yêu cầu đăng nhập
function requireLogin() {
    if (!isLoggedIn()) {
        header('Location: ' . BASE_URL . '?act=login');
        exit;
    }
}

// Yêu cầu quyền admin
function requireAdmin() {
    requireLogin();
    if (!isAdmin()) {
        header('Location: ' . BASE_URL);
        exit;
    }
}

// Yêu cầu quyền HDV hoặc admin
function requireGuideOrAdmin() {
    requireLogin();
    if (!isGuide() && !isAdmin()) {
        header('Location: ' . BASE_URL);
        exit;
    }
}
```

---

## 🎨 Giao Diện & UX

### Layout System

**Cấu trúc Layout:**

```
views/layouts/
├── AdminLayout.php     # Layout cho admin
├── GuideLayout.php     # Layout cho HDV
├── AuthLayout.php      # Layout cho auth pages
└── blocks/
    ├── header.php      # Header chung
    ├── aside.php       # Sidebar menu
    └── footer.php      # Footer
```

**AdminLTE Integration:**

- Sử dụng AdminLTE 3 template
- Responsive design
- Dark/Light mode support
- Component library đầy đủ

### Asset Management

```php
// Hàm asset() tạo URL tới file tĩnh
function asset($path) {
    return BASE_URL . '/public/' . ltrim($path, '/');
}

// Sử dụng trong view
<link rel="stylesheet" href="<?= asset('css/adminlte.min.css') ?>">
<script src="<?= asset('js/adminlte.min.js') ?>"></script>
```

---

## 📁 File Upload System

### Upload Ảnh

**Các loại upload:**
- Ảnh tour (chính + chi tiết)
- Ảnh hướng dẫn viên
- File Excel cho import khách hàng

**Upload Functions:**

```php
// Upload single image
function uploadImage($file, $prefix = 'file', $uploadDir = 'uploads/general/')

// Upload multiple images
function uploadMultipleImages($files, $prefix = 'file', $uploadDir = 'uploads/general/')

// Validation:
- File type: image/jpeg, png, gif, webp
- File size: max 5MB
- Security: check extension + MIME type
```

### Import Excel

**PHPSpreadsheet Integration:**

```php
// Đọc file Excel/CSV
function readExcelFile($filePath, $startRow = 2) {
    // Support cả .xlsx, .xls, .csv
    // Parse data thành array
    // Handle encoding UTF-8
}
```

---

## 📊 Báo Cáo & Thống Kê

### Các Loại Báo Cáo

1. **Doanh thu theo tháng/quý/năm**
2. **Thống kê tour phổ biến**
3. **Tình hình booking**
4. **Hoạt động của HDV**

### Export Data

- Xuất danh sách khách hàng (Excel)
- Xuất báo cáo doanh thu (table view)
- Export dữ liệu booking

---

## 🔧 Tính Năng Nổi Bật

### 1. Quản Lý Tour Đầy Đủ
- CRUD tour với thông tin chi tiết
- Lịch trình theo ngày
- Chính sách tour (hủy, đặt, trẻ em, etc.)
- Nhà cung cấp dịch vụ
- Upload ảnh tour

### 2. Hệ Thống Booking
- Đặt tour với thông tin khách hàng
- Import danh sách khách từ Excel
- Quản lý trạng thái booking
- Phân công HDV

### 3. Quản Lý HDV
- Profile HDV
- Phân công tour
- Nhật ký hoạt động
- Check-in/check-out khách

### 4. Báo Cáo Thống Kê
- Dashboard tổng quan
- Báo cáo doanh thu
- Thống kê hiệu suất

---

## 🚀 Quy Trình Phát Triển

### Setup Development Environment

```bash
# 1. Clone project
git clone <repository-url>

# 2. Install dependencies
composer install

# 3. Setup database
# - Tạo database 'website_ql_tour'
# - Import schema từ file SQL

# 4. Configure web server
# - Document root: /path/to/project
# - URL rewrite cho clean URLs

# 5. Access application
# http://localhost/website_quan_ly_tour
```

### Coding Standards

- PSR-4 autoloading
- Consistent naming conventions
- Error handling với try-catch
- Input validation & sanitization
- CSRF protection (basic)
- SQL injection prevention với prepared statements

---

## 🔍 Điểm Mạnh & Điểm Cần Cải Thiện

### ✅ Điểm Mạnh

1. **Kiến trúc rõ ràng**: MVC pattern được implement tốt
2. **Tái sử dụng code**: Helper functions, layout system
3. **Security**: PDO prepared statements, password hashing
4. **UX tốt**: AdminLTE template, responsive design
5. **Tính năng đầy đủ**: CRUD operations cho tất cả entities
6. **File handling**: Upload images, import Excel

### 🔄 Điểm Cần Cải Thiện

1. **Validation**: Thêm form validation robust hơn
2. **Error Handling**: Centralized error handling system
3. **Caching**: Implement caching cho performance
4. **API**: Thêm REST API cho mobile app
5. **Testing**: Unit tests & integration tests
6. **Documentation**: API documentation với Swagger
7. **Security**: Thêm CSRF tokens, rate limiting

---

## 🎯 Kết Luận

Dự án Website Quản Lý Tour là một hệ thống quản lý tour du lịch hoàn chỉnh được xây dựng với PHP thuần. Với kiến trúc MVC rõ ràng, hệ thống phân quyền chặt chẽ và giao diện thân thiện, dự án đáp ứng được các nhu cầu cơ bản của việc quản lý tour du lịch.

Dự án thể hiện sự hiểu biết sâu sắc về phát triển web với PHP, từ routing, database design, security cho đến UX/UI. Đây là một dự án mẫu tốt để học tập và làm nền tảng cho các dự án web phức tạp hơn.
