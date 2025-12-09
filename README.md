# BÁO CÁO DỰ ÁN
## Website Quản Lý Tour

---

## 📋 MỤC LỤC

1. [Tổng quan dự án](#1-tổng-quan-dự-án)
2. [Lý do chọn đề tài và mục tiêu](#2-lý-do-chọn-đề-tài-và-mục-tiêu)
   - 2.1. [Lý do chọn đề tài](#21-lý-do-chọn-đề-tài)
   - 2.2. [Mục tiêu của đề tài](#22-mục-tiêu-của-đề-tài)
   - 2.3. [Ý nghĩa của đề tài](#23-ý-nghĩa-của-đề-tài)
3. [Công nghệ và công cụ sử dụng](#3-công-nghệ-và-công-cụ-sử-dụng)
4. [Kiến trúc hệ thống](#4-kiến-trúc-hệ-thống)
5. [Cơ sở dữ liệu](#5-cơ-sở-dữ-liệu)
6. [Chức năng chính](#6-chức-năng-chính)
7. [Phân quyền người dùng](#7-phân-quyền-người-dùng)
8. [Giao diện người dùng](#8-giao-diện-người-dùng)
9. [Kết luận và hướng phát triển](#9-kết-luận-và-hướng-phát-triển)

---

## 1. TỔNG QUAN DỰ ÁN

### 1.1. Giới thiệu
**Website Quản Lý Tour** là một hệ thống quản lý tour du lịch được xây dựng bằng PHP thuần, áp dụng mô hình MVC (Model-View-Controller) tối giản phục vụ mục đích học tập. Hệ thống cho phép quản lý toàn bộ quy trình từ tạo tour, đặt tour, đến vận hành tour với sự tham gia của nhiều vai trò khác nhau.

### 1.2. Đặc điểm nổi bật
- ✅ Hệ thống quản lý tour đầy đủ chức năng CRUD
- ✅ Phân quyền rõ ràng giữa Admin và Hướng dẫn viên
- ✅ Quản lý booking và khách hàng chi tiết
- ✅ Module vận hành tour cho hướng dẫn viên
- ✅ Giao diện sử dụng AdminLTE 4.0
- ✅ Cấu trúc code rõ ràng, dễ bảo trì

---

## 2. LÝ DO CHỌN ĐỀ TÀI VÀ MỤC TIÊU

### 2.1. Lý do chọn đề tài

#### 2.1.1. Lý do về mặt thực tiễn

**a) Nhu cầu thực tế của ngành du lịch**

Ngành du lịch Việt Nam đang phát triển mạnh mẽ và trở thành một trong những ngành kinh tế mũi nhọn của đất nước. Theo số liệu thống kê, ngành du lịch đóng góp đáng kể vào GDP và tạo ra nhiều cơ hội việc làm. Tuy nhiên, việc quản lý tour du lịch tại nhiều công ty du lịch vẫn còn gặp nhiều khó khăn:

- **Quản lý thủ công**: Nhiều công ty vẫn sử dụng phương pháp quản lý truyền thống bằng sổ sách, Excel, dẫn đến mất thời gian, dễ sai sót và khó theo dõi.

- **Thiếu hệ thống tập trung**: Thông tin về tour, booking, khách hàng, hướng dẫn viên được lưu trữ rải rác, khó truy xuất và quản lý.

- **Khó khăn trong phối hợp**: Việc phối hợp giữa các bộ phận (quản lý tour, booking, hướng dẫn viên) gặp nhiều trở ngại do thiếu công cụ hỗ trợ hiệu quả.

- **Theo dõi vận hành tour**: Việc theo dõi quá trình vận hành tour, điểm danh khách, nhật ký tour chưa được số hóa một cách hệ thống.

**b) Xu hướng số hóa trong quản lý**

Trong bối cảnh cách mạng công nghiệp 4.0, việc số hóa các quy trình quản lý là xu hướng tất yếu. Các hệ thống quản lý tour hiện đại giúp:

- Tăng hiệu quả quản lý và giảm chi phí vận hành
- Cải thiện chất lượng dịch vụ khách hàng
- Tăng tính minh bạch và khả năng theo dõi
- Hỗ trợ ra quyết định dựa trên dữ liệu

#### 2.1.2. Lý do về mặt học thuật

**a) Áp dụng kiến thức đã học**

Đề tài này cho phép áp dụng và củng cố các kiến thức đã được học trong chương trình:

- **Lập trình Web**: Sử dụng PHP để xây dựng ứng dụng web động
- **Cơ sở dữ liệu**: Thiết kế và quản lý database MySQL với các quan hệ phức tạp
- **Kiến trúc phần mềm**: Áp dụng mô hình MVC để tổ chức code một cách có hệ thống
- **Giao diện người dùng**: Xây dựng giao diện web responsive và thân thiện với người dùng
- **Bảo mật**: Xử lý xác thực người dùng, phân quyền và bảo vệ dữ liệu

**b) Phát triển kỹ năng thực hành**

Thông qua việc thực hiện đề tài, sinh viên có cơ hội:

- **Kỹ năng phân tích**: Phân tích yêu cầu nghiệp vụ và thiết kế hệ thống phù hợp
- **Kỹ năng lập trình**: Viết code PHP thuần, xử lý form, session, file upload
- **Kỹ năng thiết kế database**: Thiết kế schema database với nhiều bảng và quan hệ
- **Kỹ năng debug và xử lý lỗi**: Tìm và sửa lỗi trong quá trình phát triển
- **Kỹ năng quản lý dự án**: Tổ chức code, quản lý version với Git

**c) Tính phù hợp với mục tiêu học tập**

- **Độ phức tạp vừa phải**: Đề tài đủ phức tạp để thể hiện kiến thức nhưng không quá khó để hoàn thành trong thời gian học tập
- **Tính thực tế cao**: Hệ thống có thể áp dụng vào thực tế, giúp sinh viên hiểu rõ hơn về quy trình nghiệp vụ
- **Có thể mở rộng**: Hệ thống có thể phát triển thêm nhiều tính năng trong tương lai

#### 2.1.3. Lý do về mặt kỹ thuật

**a) Công nghệ phù hợp**

- **PHP**: Ngôn ngữ phổ biến, dễ học, có nhiều tài liệu và cộng đồng hỗ trợ
- **MySQL**: Hệ quản trị cơ sở dữ liệu quan hệ mạnh mẽ, phù hợp với dữ liệu có cấu trúc
- **MVC Pattern**: Giúp tổ chức code rõ ràng, dễ bảo trì và mở rộng
- **AdminLTE**: Framework giao diện admin chuyên nghiệp, tiết kiệm thời gian phát triển UI

**b) Môi trường phát triển thuận lợi**

- Có thể phát triển trên môi trường local với Laragon/XAMPP
- Không cần cấu hình phức tạp
- Dễ dàng test và debug

#### 2.1.4. Lý do về mặt cá nhân

- **Sở thích**: Quan tâm đến lĩnh vực du lịch và công nghệ thông tin
- **Định hướng nghề nghiệp**: Muốn phát triển kỹ năng lập trình web để phục vụ công việc tương lai
- **Thách thức**: Muốn thử sức với một dự án có tính thực tế và phức tạp vừa phải

---

### 2.2. Mục tiêu của đề tài

#### 2.2.1. Mục tiêu tổng quát

Xây dựng một **hệ thống quản lý tour du lịch** hoàn chỉnh, hỗ trợ các công ty du lịch quản lý toàn bộ quy trình từ tạo tour, đặt tour, đến vận hành tour một cách hiệu quả và chuyên nghiệp. Hệ thống được xây dựng bằng PHP thuần với kiến trúc MVC, phục vụ mục đích học tập và có thể áp dụng vào thực tế.

#### 2.2.2. Mục tiêu cụ thể

**a) Mục tiêu về chức năng**

1. **Quản lý Tour**
   - Xây dựng module quản lý tour với đầy đủ chức năng CRUD (Create, Read, Update, Delete)
   - Quản lý thông tin chi tiết tour: mô tả, giá, ảnh, chính sách, lịch trình, nhà cung cấp
   - Phân loại tour theo danh mục (Tour Trong Nước, Tour Quốc Tế, Tour Yêu Cầu)
   - Quản lý trạng thái tour (Hoạt động/Không hoạt động)

2. **Quản lý Booking**
   - Xử lý đặt tour của khách hàng
   - Quản lý thông tin khách hàng trong booking
   - Import danh sách khách từ file Excel
   - Quản lý lịch khởi hành cụ thể cho từng booking
   - Quản lý dịch vụ bổ sung
   - Phân công hướng dẫn viên cho booking
   - Xuất danh sách khách ra file Excel

3. **Quản lý Người dùng**
   - Quản lý tài khoản Admin và Hướng dẫn viên
   - Hệ thống đăng nhập/đăng xuất an toàn
   - Phân quyền rõ ràng giữa các vai trò

4. **Module Vận hành Tour (dành cho HDV)**
   - HDV xem danh sách booking được phân công
   - Điểm danh khách trong tour
   - Cập nhật yêu cầu đặc biệt
   - Quản lý nhật ký tour

5. **Quản lý Danh mục và Hướng dẫn viên**
   - CRUD danh mục tour
   - CRUD thông tin hướng dẫn viên

**b) Mục tiêu về kỹ thuật**

1. **Kiến trúc hệ thống**
   - Áp dụng mô hình MVC để tổ chức code một cách có hệ thống
   - Tách biệt rõ ràng giữa Model (xử lý dữ liệu), View (giao diện), Controller (logic nghiệp vụ)
   - Xây dựng hệ thống routing linh hoạt và dễ mở rộng

2. **Cơ sở dữ liệu**
   - Thiết kế database hợp lý với 16 bảng chính
   - Thiết lập đầy đủ các quan hệ (foreign key) giữa các bảng
   - Đảm bảo tính toàn vẹn dữ liệu
   - Sử dụng encoding UTF8MB4 để hỗ trợ đầy đủ tiếng Việt

3. **Bảo mật**
   - Xử lý xác thực người dùng an toàn (hash mật khẩu bằng bcrypt)
   - Phân quyền rõ ràng giữa Admin và HDV
   - Bảo vệ các route quan trọng
   - Xử lý an toàn dữ liệu đầu vào (SQL injection, XSS)

4. **Giao diện người dùng**
   - Xây dựng giao diện chuyên nghiệp sử dụng AdminLTE 4.0
   - Responsive design, hỗ trợ đầy đủ trên desktop, tablet, mobile
   - UX tốt với breadcrumb, thông báo, confirmation dialogs

**c) Mục tiêu về học tập**

1. **Nắm vững kiến thức**
   - Hiểu rõ và áp dụng được mô hình MVC trong thực tế
   - Thành thạo lập trình PHP thuần
   - Nắm vững cách làm việc với MySQL database
   - Hiểu về session, authentication, authorization

2. **Phát triển kỹ năng**
   - Kỹ năng phân tích và thiết kế hệ thống
   - Kỹ năng lập trình và debug
   - Kỹ năng làm việc với database
   - Kỹ năng xây dựng giao diện web

3. **Kinh nghiệm thực tế**
   - Trải nghiệm quy trình phát triển một dự án web hoàn chỉnh
   - Hiểu về quy trình nghiệp vụ trong ngành du lịch
   - Rèn luyện tư duy giải quyết vấn đề

**d) Mục tiêu về chất lượng**

1. **Code chất lượng**
   - Code rõ ràng, dễ đọc, dễ hiểu
   - Có comment và documentation đầy đủ
   - Tuân thủ các best practices của PHP
   - Dễ bảo trì và mở rộng

2. **Hệ thống ổn định**
   - Xử lý đầy đủ các trường hợp lỗi
   - Validation dữ liệu đầu vào
   - Xử lý edge cases

3. **Tài liệu đầy đủ**
   - README với hướng dẫn cài đặt và sử dụng
   - Documentation về cấu trúc code
   - Báo cáo chi tiết về dự án

#### 2.2.3. Phạm vi dự án

**a) Phạm vi chức năng**

**Chức năng được thực hiện:**
- ✅ Quản lý Tour (CRUD đầy đủ)
- ✅ Quản lý Danh mục Tour
- ✅ Quản lý Booking và Khách hàng
- ✅ Quản lý Tài khoản người dùng
- ✅ Quản lý Hướng dẫn viên
- ✅ Module vận hành tour cho HDV
- ✅ Nhật ký tour
- ✅ Import/Export Excel

**Chức năng chưa thực hiện (có thể phát triển sau):**
- ⏳ Module thanh toán online
- ⏳ Gửi email thông báo tự động
- ⏳ Module báo cáo thống kê chi tiết
- ⏳ Module đánh giá tour của khách hàng
- ⏳ API cho mobile app
- ⏳ Real-time notifications

**b) Phạm vi đối tượng sử dụng**

- **Admin**: Quản lý toàn bộ hệ thống (tour, booking, tài khoản, HDV)
- **Hướng dẫn viên**: Vận hành tour được phân công (xem booking, điểm danh, nhật ký)

**c) Phạm vi kỹ thuật**

- **Backend**: PHP 8.1+ thuần, không sử dụng framework
- **Database**: MySQL 8.0
- **Frontend**: HTML, CSS, JavaScript, AdminLTE 4.0
- **Server**: Apache (local development với Laragon)

#### 2.2.4. Kết quả mong đợi

Sau khi hoàn thành đề tài, hệ thống sẽ:

1. **Hoạt động ổn định**: Tất cả các chức năng chính hoạt động đúng như thiết kế
2. **Dễ sử dụng**: Giao diện thân thiện, dễ sử dụng cho cả Admin và HDV
3. **Code chất lượng**: Code rõ ràng, có cấu trúc, dễ bảo trì
4. **Tài liệu đầy đủ**: Có đầy đủ documentation và báo cáo
5. **Có thể áp dụng**: Hệ thống có thể được sử dụng trong thực tế với một số điều chỉnh nhỏ

---

### 2.3. Ý nghĩa của đề tài

#### 2.3.1. Ý nghĩa về mặt học thuật

- Củng cố và áp dụng kiến thức đã học vào thực tế
- Phát triển kỹ năng phân tích, thiết kế và lập trình
- Tạo nền tảng để học các công nghệ nâng cao hơn

#### 2.3.2. Ý nghĩa về mặt thực tiễn

- Có thể áp dụng vào các công ty du lịch nhỏ và vừa
- Giúp số hóa quy trình quản lý tour
- Nâng cao hiệu quả quản lý và chất lượng dịch vụ

#### 2.3.3. Ý nghĩa về mặt xã hội

- Góp phần phát triển ngành du lịch Việt Nam
- Tạo công cụ hỗ trợ các doanh nghiệp du lịch
- Thúc đẩy ứng dụng công nghệ thông tin trong các ngành nghề truyền thống

---

## 3. CÔNG NGHỆ VÀ CÔNG CỤ SỬ DỤNG

### 3.1. Backend
- **Ngôn ngữ**: PHP 8.1+
- **Cơ sở dữ liệu**: MySQL 8.0
- **Kiến trúc**: MVC (Model-View-Controller)
- **Server**: Apache (qua Laragon)

### 3.2. Frontend
- **Framework CSS**: AdminLTE 4.0 Beta 3
- **JavaScript**: Vanilla JavaScript
- **Thư viện**: PHPSpreadsheet (xuất Excel)

### 3.3. Công cụ phát triển
- **IDE**: Cursor / VS Code
- **Local Server**: Laragon
- **Version Control**: Git
- **Database Management**: phpMyAdmin

### 3.4. Thư viện PHP
- `phpoffice/phpspreadsheet`: ^1.29 (xuất file Excel)

---

## 4. KIẾN TRÚC HỆ THỐNG

### 4.1. Cấu trúc thư mục

```
website_quan_ly_tour/
├── index.php                 # Điểm vào chính, xử lý routing
├── config/
│   └── config.php            # Cấu hình chung và database
├── src/
│   ├── controllers/          # Các controller xử lý logic
│   │   ├── HomeController.php
│   │   ├── AuthController.php
│   │   ├── TourController.php
│   │   ├── BookingController.php
│   │   ├── AccountController.php
│   │   ├── DanhMucTourController.php
│   │   ├── HDVController.php
│   │   └── GuideTourController.php
│   ├── models/               # Các model đại diện cho dữ liệu
│   │   ├── User.php
│   │   ├── Tour.php
│   │   ├── Booking.php
│   │   ├── DanhMucTour.php
│   │   ├── HDV.php
│   │   └── NhatKyTour.php
│   └── helpers/              # Các hàm tiện ích
│       ├── helpers.php       # Hàm render view, asset, session
│       └── database.php      # Kết nối database
├── views/                    # Giao diện người dùng
│   ├── layouts/              # Layout chung
│   │   ├── AdminLayout.php
│   │   ├── GuideLayout.php
│   │   ├── AuthLayout.php
│   │   └── blocks/           # Header, Footer, Sidebar
│   ├── admin/                # Views cho Admin
│   │   ├── tours/
│   │   ├── bookings/
│   │   ├── accounts/
│   │   ├── categories/
│   │   └── hdvs/
│   ├── guide/                # Views cho Hướng dẫn viên
│   └── auth/                 # Views đăng nhập
├── public/                   # Tài nguyên tĩnh
│   ├── css/
│   ├── js/
│   └── images/
├── AdminLTE-4.0.0-beta3/     # Framework AdminLTE
└── .htaccess                 # Rewrite URL
```

### 4.2. Mô hình MVC

**Model (M):**
- Đại diện cho dữ liệu và logic nghiệp vụ
- Tương tác trực tiếp với database
- Các file trong `src/models/`

**View (V):**
- Hiển thị giao diện người dùng
- Nhận dữ liệu từ Controller
- Các file trong `views/`

**Controller (C):**
- Xử lý logic nghiệp vụ
- Nhận request từ người dùng
- Gọi Model để lấy/xử lý dữ liệu
- Truyền dữ liệu cho View
- Các file trong `src/controllers/`

### 4.3. Routing System

Hệ thống routing sử dụng:
- **File `.htaccess`**: Rewrite URL từ `/home` thành `index.php?act=home`
- **File `index.php`**: Xử lý routing bằng `match()` expression
- **Routes có tham số**: Xử lý riêng trước khi vào `match()`

**Ví dụ routing:**
```php
// Route đơn giản
'tours' => $tourController->index()
'tours/create' => $tourController->create()

// Route có tham số
'tours/edit/{id}' => Xử lý riêng trước match()
```

### 4.4. Helper Functions

**File `helpers.php`:**
- `view()`: Render view với layout
- `asset()`: Tạo đường dẫn đến file tĩnh
- `redirect()`: Chuyển hướng trang
- `session()`: Quản lý session
- `auth()`: Kiểm tra đăng nhập
- `requireAuth()`: Yêu cầu đăng nhập
- `requireAdmin()`: Yêu cầu quyền Admin

**File `database.php`:**
- `getConnection()`: Kết nối database
- Các hàm query database

---

## 5. CƠ SỞ DỮ LIỆU

### 5.1. Tổng quan
Hệ thống sử dụng MySQL với 16 bảng chính, được thiết kế để quản lý đầy đủ thông tin về tour, booking, khách hàng, và vận hành.

### 5.2. Các bảng chính

#### 5.2.1. Quản lý Tour
- **`tour`**: Thông tin tour (id, danh_muc_id, ten_tour, mo_ta, gia, trang_thai, anh_tour)
- **`danh_muc_tour`**: Danh mục tour (Tour Trong Nước, Tour Quốc Tế, Tour Yêu Cầu)
- **`tour_anh`**: Ảnh chi tiết của tour
- **`tour_chinh_sach`**: Chính sách tour (hủy tour, đặt tour, trẻ em, đổi lịch, hoàn tiền)
- **`tour_lich_trinh`**: Lịch trình tour theo từng ngày
- **`tour_nha_cung_cap`**: Nhà cung cấp dịch vụ (khách sạn, phương tiện, nhà hàng, HDV)

#### 5.2.2. Quản lý Booking
- **`booking`**: Thông tin booking (tai_khoan_id, tour_id, loai_khach, ten_nguoi_dat, so_luong, thoi_gian_tour, trang_thai)
- **`booking_khach`**: Danh sách khách trong booking (ho_ten, gioi_tinh, nam_sinh, so_giay_to, tinh_trang_thanh_toan)
- **`booking_dich_vu`**: Dịch vụ bổ sung cho booking
- **`booking_hdv`**: Phân công hướng dẫn viên cho booking
- **`lich_khoi_hanh`**: Lịch khởi hành cụ thể của booking

#### 5.2.3. Quản lý Người dùng
- **`tai_khoan`**: Tài khoản người dùng (ten_dang_nhap, mat_khau, ho_ten, email, sdt, phan_quyen, trang_thai)
- **`hdv`**: Thông tin hướng dẫn viên (tai_khoan_id, ngay_sinh, anh_dai_dien, lien_he, nhom, chuyen_mon)

#### 5.2.4. Vận hành Tour
- **`nhat_ky_tour`**: Nhật ký tour của HDV (booking_id, ngay_gio, noi_dung, danh_gia_hdv)
- **`diem_danh_khach`**: Điểm danh khách trong tour (booking_khach_id, lich_khoi_hanh_id, trang_thai)

#### 5.2.5. Báo cáo
- **`bao_cao_tong_hop_tour`**: Báo cáo tổng hợp tour (tour_id, ky_bao_cao, nam, doanh_thu, chi_phi, loi_nhuan)

### 5.3. Quan hệ giữa các bảng

```
tai_khoan (1) ──┬── (1) hdv
                │
                └── (1) ── booking ── (N) ── booking_khach
                              │
                              ├── (N) ── booking_dich_vu
                              ├── (N) ── booking_hdv ── (1) ── hdv
                              ├── (1) ── lich_khoi_hanh
                              └── (N) ── nhat_ky_tour

tour (1) ── (N) ── booking
  │
  ├── (N) ── tour_anh
  ├── (N) ── tour_chinh_sach
  ├── (N) ── tour_lich_trinh
  └── (N) ── tour_nha_cung_cap

danh_muc_tour (1) ── (N) ── tour
```

### 5.4. Thiết kế Database
- **Encoding**: UTF8MB4 (hỗ trợ đầy đủ tiếng Việt và emoji)
- **Engine**: InnoDB (hỗ trợ transaction và foreign key)
- **Indexing**: Primary key và foreign key được thiết lập đầy đủ

---

## 6. CHỨC NĂNG CHÍNH

### 6.1. Module Quản lý Tour (Admin)

#### 6.1.1. Danh sách Tour
- Hiển thị danh sách tất cả tour
- Hiển thị thông tin: Tên tour, Danh mục, Giá, Trạng thái
- Các thao tác: Xem chi tiết, Sửa, Xóa

#### 6.1.2. Tạo Tour mới
- Form nhập thông tin cơ bản:
  - Tên tour
  - Danh mục (dropdown)
  - Giá tour
  - Mô tả tour
  - Trạng thái (Hoạt động/Không hoạt động)
  - Ảnh tour chính
- Form nhập thông tin chi tiết:
  - **Chính sách tour**: Tên chính sách + Nội dung
  - **Lịch trình**: Số ngày + Điểm tham quan + Hoạt động
  - **Nhà cung cấp**: Tên + Loại + Liên hệ + Ghi chú
  - **Ảnh chi tiết**: Upload nhiều ảnh

#### 6.1.3. Sửa Tour
- Form tương tự như tạo tour
- Load dữ liệu hiện có để chỉnh sửa
- Cập nhật thông tin vào database

#### 6.1.4. Xem chi tiết Tour
- Hiển thị đầy đủ thông tin tour
- Hiển thị các chính sách, lịch trình, nhà cung cấp
- Hiển thị ảnh tour

#### 6.1.5. Xóa Tour
- Xóa tour và các dữ liệu liên quan
- Có thể có kiểm tra ràng buộc với booking

### 6.2. Module Quản lý Danh mục Tour (Admin)

- **CRUD đầy đủ**: Tạo, Sửa, Xóa, Xem danh mục
- **Quản lý trạng thái**: Hoạt động/Không hoạt động
- **Danh mục mặc định**: Tour Trong Nước, Tour Quốc Tế, Tour Yêu Cầu

### 6.3. Module Quản lý Booking (Admin)

#### 6.3.1. Danh sách Booking
- Hiển thị danh sách booking
- Thông tin: Tên người đặt, Tour, Số lượng, Thời gian tour, Trạng thái
- Lọc và tìm kiếm booking

#### 6.3.2. Tạo Booking mới
- Form nhập thông tin booking:
  - Chọn tour
  - Loại khách (Cá nhân/Đoàn)
  - Tên người đặt
  - Số lượng
  - Thời gian tour
  - Liên hệ
  - Yêu cầu đặc biệt

#### 6.3.3. Quản lý Khách trong Booking
- **Import khách từ Excel**: Upload file Excel để import danh sách khách
- **Thêm khách thủ công**: Form nhập thông tin khách
- **Thông tin khách**: Họ tên, Giới tính, Năm sinh, Số giấy tờ, Tình trạng thanh toán, Yêu cầu cá nhân
- **Xem danh sách khách**: Hiển thị tất cả khách trong booking

#### 6.3.4. Quản lý Lịch khởi hành
- Thiết lập lịch khởi hành cụ thể cho booking
- Thông tin: Ngày giờ xuất phát, Điểm tập trung, Thời gian kết thúc, Ghi chú

#### 6.3.5. Quản lý Dịch vụ
- Thêm/sửa/xóa dịch vụ bổ sung cho booking
- Thông tin: Tên dịch vụ, Chi tiết

#### 6.3.6. Phân công Hướng dẫn viên
- Gán HDV cho booking
- Thông tin: HDV, Vai trò, Chi tiết

#### 6.3.7. Xuất Excel
- Xuất danh sách khách ra file Excel
- Bao gồm thông tin điểm danh

### 6.4. Module Quản lý Tài khoản (Admin)

- **CRUD đầy đủ**: Tạo, Sửa, Xóa, Xem tài khoản
- **Phân quyền**: Admin, HDV
- **Quản lý trạng thái**: Hoạt động/Ngừng hoạt động
- **Thông tin**: Tên đăng nhập, Mật khẩu (hash), Họ tên, Email, SĐT

### 6.5. Module Quản lý Hướng dẫn viên (Admin)

- **CRUD đầy đủ**: Tạo, Sửa, Xóa, Xem HDV
- **Thông tin**: Tài khoản liên kết, Ngày sinh, Ảnh đại diện, Liên hệ, Nhóm, Chuyên môn
- **Liên kết với tài khoản**: Mỗi HDV phải có tài khoản

### 6.6. Module Vận hành Tour (Hướng dẫn viên)

#### 6.6.1. Danh sách Booking của HDV
- Hiển thị các booking được phân công cho HDV
- Thông tin: Tour, Người đặt, Số lượng, Thời gian tour, Trạng thái

#### 6.6.2. Chi tiết Booking
- Xem thông tin chi tiết booking
- Xem danh sách khách
- Xem lịch khởi hành
- Xem dịch vụ

#### 6.6.3. Check-in Khách
- Điểm danh khách trong tour
- Cập nhật trạng thái: Có mặt/Vắng mặt
- Ghi chú cho từng khách

#### 6.6.4. Cập nhật Yêu cầu
- Cập nhật yêu cầu đặc biệt cho booking
- Cập nhật yêu cầu cho đoàn

#### 6.6.5. Nhật ký Tour
- **Tạo nhật ký**: Ghi lại các hoạt động trong tour
- **Sửa nhật ký**: Cập nhật nội dung nhật ký
- **Xóa nhật ký**: Xóa nhật ký không cần thiết
- **Danh sách nhật ký**: Xem tất cả nhật ký của booking
- **Thông tin**: Ngày giờ, Nội dung, Đánh giá HDV

### 6.7. Module Xác thực

#### 6.7.1. Đăng nhập
- Form đăng nhập: Tên đăng nhập, Mật khẩu
- Kiểm tra thông tin đăng nhập
- Tạo session khi đăng nhập thành công
- Phân biệt Admin và HDV để redirect đúng trang

#### 6.7.2. Đăng xuất
- Xóa session
- Chuyển về trang welcome

#### 6.7.3. Bảo vệ Route
- Kiểm tra đăng nhập trước khi truy cập các trang
- Kiểm tra quyền Admin cho các chức năng quản lý
- Redirect về trang đăng nhập nếu chưa đăng nhập

---

## 7. PHÂN QUYỀN NGƯỜI DÙNG

### 7.1. Vai trò trong hệ thống

#### 7.1.1. Admin
**Quyền hạn:**
- ✅ Quản lý Tour (CRUD đầy đủ)
- ✅ Quản lý Danh mục Tour
- ✅ Quản lý Booking
- ✅ Quản lý Tài khoản
- ✅ Quản lý Hướng dẫn viên
- ✅ Vận hành Tour (có thể sử dụng module của HDV)

**Trang truy cập:**
- Trang chủ Admin (`/home`)
- Quản lý Tour (`/tours`)
- Quản lý Booking (`/bookings`)
- Quản lý Tài khoản (`/accounts`)
- Quản lý Danh mục (`/categories`)
- Quản lý HDV (`/hdvs`)

#### 7.1.2. Hướng dẫn viên (HDV)
**Quyền hạn:**
- ✅ Xem danh sách booking được phân công
- ✅ Xem chi tiết booking
- ✅ Check-in khách
- ✅ Cập nhật yêu cầu
- ✅ Quản lý nhật ký tour
- ❌ **KHÔNG** có quyền quản lý tour
- ❌ **KHÔNG** có quyền quản lý booking (tạo/sửa/xóa)
- ❌ **KHÔNG** có quyền quản lý tài khoản

**Trang truy cập:**
- Trang chủ HDV (`/home`)
- Danh sách booking của tôi (`/guide/my-bookings`)
- Chi tiết booking (`/guide/booking/{id}`)
- Check-in (`/guide/check-in`)
- Nhật ký tour (`/guide/diary/{booking_id}`)

### 7.2. Cơ chế phân quyền

**Kiểm tra đăng nhập:**
```php
requireAuth(); // Yêu cầu phải đăng nhập
```

**Kiểm tra quyền Admin:**
```php
requireAdmin(); // Yêu cầu phải là Admin
```

**Kiểm tra quyền HDV:**
```php
if (auth()['phan_quyen'] !== 'hdv') {
    redirect('/home');
}
```

### 7.3. Bảo vệ Route

Tất cả các route quản lý đều được bảo vệ:
- Route Admin: Sử dụng `requireAdmin()`
- Route HDV: Kiểm tra `phan_quyen === 'hdv'`
- Route công khai: Chỉ trang welcome và đăng nhập

---

## 8. GIAO DIỆN NGƯỜI DÙNG

### 8.1. Framework sử dụng
- **AdminLTE 4.0 Beta 3**: Framework admin template chuyên nghiệp
- **Bootstrap 5**: Framework CSS responsive
- **Font Awesome**: Icon library

### 8.2. Layout

#### 8.2.1. AdminLayout
- **Header**: Logo, thông tin người dùng, menu dropdown
- **Sidebar**: Menu điều hướng các chức năng
- **Content**: Nội dung chính của trang
- **Footer**: Thông tin footer

**Menu Sidebar Admin:**
- Trang chủ
- Quản lý Tour
- Quản lý Booking
- Quản lý Tài khoản
- Quản lý Danh mục
- Quản lý HDV
- Đăng xuất

#### 8.2.2. GuideLayout
- Layout tương tự AdminLayout
- Menu Sidebar khác nhau:
  - Trang chủ
  - Booking của tôi
  - Đăng xuất

#### 8.2.3. AuthLayout
- Layout đơn giản cho trang đăng nhập
- Không có sidebar và header phức tạp

### 8.3. Components

#### 8.3.1. Form Components
- Input text, textarea
- Select dropdown
- File upload
- Checkbox, radio
- Date picker

#### 8.3.2. Table Components
- DataTable cho danh sách
- Pagination
- Search và filter
- Action buttons (Xem, Sửa, Xóa)

#### 8.3.3. Card Components
- Card hiển thị thông tin
- Card form
- Card thống kê

### 8.4. Responsive Design
- Hỗ trợ đầy đủ trên desktop, tablet, mobile
- Sidebar tự động thu gọn trên mobile
- Table responsive với scroll ngang

### 8.5. UX Features
- Breadcrumb navigation
- Success/Error messages
- Loading states
- Confirmation dialogs
- Tooltips và help text

---

## 9. KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN

### 9.1. Kết quả đạt được

✅ **Hoàn thành các chức năng chính:**
- Hệ thống quản lý tour đầy đủ CRUD
- Quản lý booking và khách hàng chi tiết
- Module vận hành tour cho HDV
- Phân quyền rõ ràng giữa Admin và HDV
- Giao diện chuyên nghiệp với AdminLTE

✅ **Chất lượng code:**
- Cấu trúc MVC rõ ràng
- Code dễ đọc, dễ bảo trì
- Tách biệt logic và presentation
- Sử dụng helper functions hiệu quả

✅ **Database:**
- Thiết kế database hợp lý
- Quan hệ giữa các bảng rõ ràng
- Hỗ trợ đầy đủ UTF8MB4

### 9.2. Điểm mạnh

1. **Cấu trúc rõ ràng**: MVC pattern giúp code dễ hiểu và bảo trì
2. **Phân quyền tốt**: Phân biệt rõ ràng giữa Admin và HDV
3. **Chức năng đầy đủ**: Cover đầy đủ các nghiệp vụ quản lý tour
4. **Giao diện đẹp**: Sử dụng AdminLTE tạo giao diện chuyên nghiệp
5. **Dễ học tập**: Code đơn giản, phù hợp cho người mới học PHP

### 9.3. Hạn chế

1. **Chưa có validation nâng cao**: Validation cơ bản, chưa có client-side validation
2. **Chưa có API**: Chưa có RESTful API cho mobile app
3. **Chưa có real-time**: Chưa có thông báo real-time
4. **Chưa có báo cáo**: Module báo cáo chưa được implement
5. **Chưa có thanh toán**: Chưa tích hợp cổng thanh toán

### 9.4. Hướng phát triển

#### 9.4.1. Ngắn hạn (1-2 tháng)
- ✅ Thêm validation nâng cao (client-side + server-side)
- ✅ Thêm tìm kiếm và filter cho danh sách
- ✅ Thêm pagination cho các danh sách dài
- ✅ Cải thiện UX với loading states và animations
- ✅ Thêm module báo cáo cơ bản

#### 9.4.2. Trung hạn (3-6 tháng)
- ✅ Tích hợp cổng thanh toán (VNPay, Momo)
- ✅ Gửi email thông báo cho khách hàng
- ✅ Upload ảnh lên cloud storage (AWS S3, Cloudinary)
- ✅ Thêm module đánh giá tour
- ✅ Thêm module thống kê và dashboard

#### 9.4.3. Dài hạn (6-12 tháng)
- ✅ Xây dựng RESTful API
- ✅ Xây dựng mobile app (React Native/Flutter)
- ✅ Thêm real-time notifications (WebSocket)
- ✅ Tích hợp AI để đề xuất tour
- ✅ Multi-language support (i18n)
- ✅ Nâng cấp lên framework (Laravel/Symfony)

### 9.5. Bài học kinh nghiệm

1. **Thiết kế database quan trọng**: Thiết kế database tốt giúp phát triển dễ dàng hơn
2. **MVC pattern hiệu quả**: Giúp tổ chức code một cách có hệ thống
3. **Phân quyền từ đầu**: Nên thiết kế phân quyền ngay từ đầu
4. **Code đơn giản**: Code đơn giản dễ bảo trì hơn code phức tạp
5. **Documentation**: Tài liệu rõ ràng giúp người khác hiểu code dễ hơn

### 9.6. Kết luận

Dự án **Website Quản Lý Tour** đã hoàn thành các mục tiêu ban đầu với hệ thống quản lý tour đầy đủ chức năng, cấu trúc code rõ ràng, và giao diện chuyên nghiệp. Dự án phù hợp cho mục đích học tập và có thể phát triển thêm nhiều tính năng trong tương lai.

Với nền tảng vững chắc hiện tại, dự án có thể dễ dàng mở rộng và nâng cấp để trở thành một hệ thống quản lý tour hoàn chỉnh và chuyên nghiệp.

---

## 📎 PHỤ LỤC

### A. Thông tin kỹ thuật

**Yêu cầu hệ thống:**
- PHP: 8.1+
- MySQL: 8.0+
- Apache: 2.4+
- Composer: 2.0+

**Cấu hình:**
- `config/config.php`: Cấu hình database và đường dẫn
- `.htaccess`: Rewrite URL

### B. Tài liệu tham khảo

- README.md: Hướng dẫn cơ bản về dự án
- KHUYEN_NGHI_THIET_KE.md: Khuyến nghị thiết kế
- DU_LIEU_TOUR_MAU.md: Dữ liệu mẫu để test
- HUONG_DAN_LAYOUT.md: Hướng dẫn sử dụng layout

### C. Liên hệ

Để biết thêm thông tin về dự án, vui lòng xem các file documentation trong thư mục gốc.

---

**Ngày hoàn thành báo cáo**: Tháng 12, 2025  
**Phiên bản**: 1.0

