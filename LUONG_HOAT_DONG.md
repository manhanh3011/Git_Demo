# LUỒNG HOẠT ĐỘNG CÁC CHỨC NĂNG
## Website Quản Lý Tour

---

## 1. LUỒNG ĐĂNG NHẬP

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Truy cập trang đăng nhập | |
| 2. Nhập email và mật khẩu | |
| 3. Nhấn nút "Đăng nhập" | 4. Nhận dữ liệu từ form POST |
| | 5. Validate: Kiểm tra email và mật khẩu không rỗng |
| | 6. **Nếu có lỗi** → Hiển thị form với thông báo lỗi → Quay lại bước 2 |
| | 7. **Nếu hợp lệ** → Gọi `User::authenticate()` để kiểm tra trong database |
| | 8. **Nếu sai** → Hiển thị lỗi "Email hoặc mật khẩu không đúng" → Quay lại bước 2 |
| | 9. **Nếu đúng** → Lưu thông tin user vào session |
| | 10. Kiểm tra phân quyền (admin/hdv) |
| | 11. Redirect về trang home tương ứng |
| 12. Thấy trang home | |

---

## 2. LUỒNG QUẢN LÝ TOUR - TẠO TOUR MỚI

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào menu "Quản lý Tour" → "Thêm tour mới" | |
| 2. Hệ thống hiển thị form tạo tour | 2. Kiểm tra quyền Admin |
| | 3. Lấy danh sách danh mục từ database |
| | 4. Hiển thị form với danh sách danh mục |
| 3. Điền thông tin: Tên tour, Danh mục, Mô tả, Giá, Trạng thái | |
| 4. Thêm chính sách (có thể nhiều): Tên chính sách + Nội dung | |
| 5. Thêm lịch trình (có thể nhiều): Số ngày + Điểm tham quan + Hoạt động | |
| 6. Thêm nhà cung cấp (có thể nhiều): Tên + Loại + Liên hệ + Ghi chú | |
| 7. Upload ảnh tour chính | |
| 8. Upload ảnh chi tiết (có thể nhiều) | |
| 9. Nhấn nút "Lưu" | 10. Nhận dữ liệu POST |
| | 11. Validate: Kiểm tra tên tour, danh mục, mô tả, giá > 0 |
| | 12. **Nếu có lỗi** → Hiển thị form với lỗi và dữ liệu cũ → Quay lại bước 3 |
| | 13. **Nếu hợp lệ**: |
| | - Upload ảnh tour chính → Lưu vào `uploads/tours/` |
| | - Upload ảnh chi tiết → Lưu vào `uploads/tours/` |
| | - Tạo record mới trong bảng `tour` |
| | - Lấy `tour_id` vừa tạo |
| | - Lưu chính sách vào bảng `tour_chinh_sach` |
| | - Lưu lịch trình vào bảng `tour_lich_trinh` |
| | - Lưu nhà cung cấp vào bảng `tour_nha_cung_cap` |
| | - Lưu ảnh chi tiết vào bảng `tour_anh` |
| | 14. **Thành công** → Lưu thông báo success vào session → Redirect về danh sách tour |
| | 15. **Thất bại** → Lưu thông báo error → Redirect về form tạo |
| 10. Thấy danh sách tour với thông báo thành công | |

---

## 3. LUỒNG QUẢN LÝ TOUR - SỬA TOUR

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào danh sách tour | |
| 2. Chọn tour cần sửa → Nhấn "Sửa" | 3. Kiểm tra quyền Admin |
| | 4. Lấy thông tin tour từ database theo ID |
| | 5. Lấy danh sách chính sách, lịch trình, nhà cung cấp, ảnh chi tiết |
| | 6. Hiển thị form với dữ liệu hiện có |
| 4. Sửa thông tin cần thiết | |
| 5. Có thể xóa chính sách, lịch trình, nhà cung cấp cũ | |
| 6. Có thể thêm chính sách, lịch trình, nhà cung cấp mới | |
| 7. Có thể xóa ảnh chi tiết (chọn checkbox) | |
| 8. Có thể thêm ảnh chi tiết mới | |
| 9. Nhấn nút "Cập nhật" | 10. Nhận dữ liệu POST (có `id`) |
| | 11. Validate dữ liệu |
| | 12. **Nếu có lỗi** → Hiển thị form với lỗi → Quay lại bước 4 |
| | 13. **Nếu hợp lệ**: |
| | - Nếu có upload ảnh mới → Upload và lưu |
| | - Nếu không → Giữ ảnh cũ |
| | - Cập nhật bảng `tour` |
| | - Xóa tất cả chính sách cũ → Lưu mới vào `tour_chinh_sach` |
| | - Xóa tất cả lịch trình cũ → Lưu mới vào `tour_lich_trinh` |
| | - Xóa tất cả nhà cung cấp cũ → Lưu mới vào `tour_nha_cung_cap` |
| | - Xóa ảnh chi tiết được chọn (từ `tour_anh`) |
| | - Thêm ảnh chi tiết mới (nếu có) |
| | 14. **Thành công** → Redirect về danh sách tour |
| | 15. **Thất bại** → Redirect về form sửa |
| 10. Thấy danh sách tour với thông báo | |

---

## 4. LUỒNG QUẢN LÝ TOUR - XÓA TOUR

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào danh sách tour | |
| 2. Chọn tour cần xóa → Nhấn "Xóa" | 3. Kiểm tra quyền Admin |
| | 4. Nhận POST request với `id` |
| 3. Xác nhận xóa (trong popup) | 5. Kiểm tra tour có tồn tại không |
| | 6. Kiểm tra tour có đang được sử dụng trong booking không |
| | 7. **Nếu có** → Trả về lỗi "Không thể xóa tour này vì đang được sử dụng" |
| | 8. **Nếu không**: |
| | - Xóa tour trong bảng `tour` |
| | - Xóa các record liên quan (chính sách, lịch trình, nhà cung cấp, ảnh) |
| | 9. Redirect về danh sách tour với thông báo |
| 4. Thấy danh sách tour với thông báo | |

---

## 5. LUỒNG QUẢN LÝ BOOKING - TẠO BOOKING MỚI

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào menu "Quản lý Booking" → "Thêm booking mới" | |
| 2. Hệ thống hiển thị form | 2. Kiểm tra quyền Admin |
| | 3. Lấy danh sách tour từ database |
| | 4. Lấy danh sách HDV từ database |
| | 5. Hiển thị form với dropdown tour và HDV |
| 3. Điền form: Chọn tour, Loại khách, Tên người đặt, Số lượng, Thời gian tour, Liên hệ | |
| 4. Thêm yêu cầu đặc biệt (nếu có) | |
| 5. Phân công HDV (nếu có) | |
| 6. Thêm khách hàng (có thể thêm sau) | |
| 7. Thiết lập lịch khởi hành: Ngày giờ xuất phát, Điểm tập trung, Thời gian kết thúc (có thể thêm sau) | |
| 8. Upload file Excel danh sách khách (tùy chọn) | |
| 9. Nhấn nút "Lưu" | 10. Nhận dữ liệu POST |
| | 11. Validate: tour_id, tên người đặt, số lượng > 0, thời gian tour, liên hệ |
| | 12. **Nếu có lỗi** → Hiển thị form với lỗi → Quay lại bước 3 |
| | 13. **Nếu hợp lệ**: |
| | - Tạo record mới trong bảng `booking` |
| | - Lấy `booking_id` vừa tạo |
| | - Nếu có HDV → Lưu vào bảng `booking_hdv` |
| | - Nếu có khách → Lưu vào bảng `booking_khach` |
| | - Nếu có lịch khởi hành → Lưu vào bảng `lich_khoi_hanh` |
| | - Nếu có yêu cầu đặc biệt → Tạo dịch vụ trong `booking_dich_vu` |
| | - Nếu có file Excel → Upload và lưu vào `uploads/guest_lists/` |
| | 14. **Thành công** → Redirect về danh sách booking |
| | 15. **Thất bại** → Redirect về form tạo |
| 10. Thấy danh sách booking với thông báo | |

---

## 6. LUỒNG QUẢN LÝ BOOKING - IMPORT KHÁCH TỪ EXCEL

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào trang sửa booking | |
| 2. Chọn tab "Danh sách khách" | |
| 3. Chọn file Excel (định dạng: Họ tên, Giới tính, Năm sinh, Số giấy tờ, Yêu cầu) | |
| 4. Nhấn nút "Import" | 5. Nhận POST request với `booking_id` và file |
| | 6. Kiểm tra file có tồn tại và hợp lệ không (CSV, XLS, XLSX) |
| | 7. **Nếu không hợp lệ** → Hiển thị lỗi → Quay lại bước 3 |
| | 8. **Nếu hợp lệ**: |
| | - Upload file tạm |
| | - Đọc file Excel bằng PHPSpreadsheet (bỏ dòng header, bắt đầu từ dòng 2) |
| | 9. **Với mỗi dòng trong file**: |
| | - Lấy: Họ tên, Giới tính, Năm sinh, Số giấy tờ, Yêu cầu |
| | - Validate: Họ tên không được rỗng |
| | - **Nếu hợp lệ** → Tạo record trong `booking_khach` → Đếm thành công |
| | - **Nếu không hợp lệ** → Ghi lại lỗi → Đếm thất bại |
| | 10. Xóa file tạm |
| | 11. **Nếu có thành công** → Lưu thông báo "Import thành công X khách hàng" |
| | 12. **Nếu có lỗi** → Lưu thông báo lỗi chi tiết |
| | 13. Redirect về trang chi tiết booking |
| 5. Thấy danh sách khách đã được import | |

---

## 7. LUỒNG QUẢN LÝ BOOKING - XUẤT EXCEL ĐIỂM DANH

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào trang chi tiết booking | |
| 2. Chọn tab "Điểm danh" | |
| 3. Nhấn nút "Xuất Excel" | 4. Lấy danh sách khách từ `booking_khach` theo `booking_id` |
| | 5. Lấy thông tin điểm danh từ `diem_danh_khach` |
| | 6. Tạo file Excel bằng PHPSpreadsheet: |
| | - Header: STT, Họ tên, Giới tính, Năm sinh, Số giấy tờ, Trạng thái điểm danh |
| | - Dữ liệu: Mỗi khách một dòng với thông tin tương ứng |
| | 7. Trả về file Excel để download |
| 4. File Excel được tải về máy | |

---

## 8. LUỒNG HDV - XEM DANH SÁCH BOOKING

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| 1. Đăng nhập với tài khoản HDV | |
| 2. Vào menu "Booking của tôi" | 3. Kiểm tra đăng nhập và quyền HDV |
| | 4. Lấy `user_id` từ session |
| | 5. Tìm `hdv_id` từ bảng `hdv` theo `tai_khoan_id` |
| | 6. Query booking từ `booking_hdv` với `hdv_id` này |
| | 7. Lấy thông tin tour, lịch khởi hành cho mỗi booking |
| | 8. Hiển thị danh sách booking |
| 3. Thấy danh sách booking được phân công | |

---

## 9. LUỒNG HDV - CHECK-IN KHÁCH

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| 1. Vào chi tiết booking được phân công | |
| 2. Chọn tab "Điểm danh" | |
| 3. Chọn khách cần check-in | |
| 4. Chọn trạng thái: Đã đến / Vắng / Vắng mặt / Trễ | |
| 5. Nhập ghi chú (nếu có) | |
| 6. Nhấn nút "Lưu điểm danh" | 7. Nhận POST request: `booking_id`, `lich_khoi_hanh_id`, `booking_khach_id`, `trang_thai`, `ghi_chu` |
| | 8. Kiểm tra quyền HDV và booking có thuộc HDV này không |
| | 9. **Nếu không có quyền** → Hiển thị lỗi → Quay lại bước 1 |
| | 10. Validate: `booking_id`, `lich_khoi_hanh_id`, `booking_khach_id`, `trang_thai` hợp lệ |
| | 11. **Nếu chưa có `lich_khoi_hanh_id`** → Tạo mới trong `lich_khoi_hanh` |
| | 12. Gọi `Booking::upsertDiemDanh()`: |
| | - Kiểm tra đã có điểm danh chưa (trong `diem_danh_khach`) |
| | - **Nếu có** → Cập nhật record |
| | - **Nếu chưa** → Tạo mới record |
| | 13. **Thành công** → Lưu thông báo success → Redirect về trang chi tiết booking |
| | 14. **Thất bại** → Lưu thông báo error → Redirect về trang chi tiết booking |
| 7. Thấy trang chi tiết booking với thông báo | |

---

## 10. LUỒNG HDV - TẠO NHẬT KÝ TOUR

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| 1. Vào chi tiết booking | |
| 2. Chọn "Nhật ký tour" | |
| 3. Nhấn nút "Thêm nhật ký" | 4. Kiểm tra quyền HDV |
| | 5. Lấy thông tin booking |
| | 6. Hiển thị form tạo nhật ký |
| 4. Điền form: Ngày giờ, Nội dung, Đánh giá HDV | |
| 5. Nhấn nút "Lưu" | 6. Nhận POST request: `booking_id`, `ngay_gio`, `noi_dung`, `danh_gia_hdv` |
| | 7. Kiểm tra quyền HDV |
| | 8. Validate: `noi_dung` không được rỗng |
| | 9. **Nếu có lỗi** → Hiển thị form với lỗi → Quay lại bước 4 |
| | 10. **Nếu `ngay_gio` rỗng** → Lấy thời gian hiện tại |
| | 11. Tạo record mới trong `nhat_ky_tour` |
| | 12. **Thành công** → Redirect về danh sách nhật ký |
| | 13. **Thất bại** → Redirect về form tạo với lỗi |
| 6. Thấy danh sách nhật ký với thông báo | |

---

## 11. LUỒNG HDV - SỬA NHẬT KÝ TOUR

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| 1. Vào danh sách nhật ký tour | |
| 2. Chọn nhật ký cần sửa → Nhấn "Sửa" | 3. Kiểm tra quyền HDV |
| | 4. Lấy thông tin nhật ký từ database theo ID |
| | 5. Hiển thị form với dữ liệu hiện có |
| 3. Sửa nội dung nhật ký | |
| 4. Nhấn nút "Cập nhật" | 5. Nhận POST request với `id` |
| | 6. Validate: `noi_dung` không được rỗng |
| | 7. **Nếu có lỗi** → Hiển thị form với lỗi → Quay lại bước 3 |
| | 8. **Nếu hợp lệ** → Cập nhật record trong `nhat_ky_tour` |
| | 9. **Thành công** → Redirect về danh sách nhật ký |
| | 10. **Thất bại** → Redirect về form sửa với lỗi |
| 5. Thấy danh sách nhật ký với thông báo | |

---

## 12. LUỒNG HDV - XÓA NHẬT KÝ TOUR

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| 1. Vào danh sách nhật ký tour | |
| 2. Chọn nhật ký cần xóa → Nhấn "Xóa" | 3. Kiểm tra quyền HDV |
| | 4. Nhận POST request với `id` |
| 3. Xác nhận xóa (trong popup) | 5. Lấy nhật ký từ database |
| | 6. Xóa record trong `nhat_ky_tour` |
| | 7. Redirect về danh sách nhật ký với thông báo |
| 4. Thấy danh sách nhật ký với thông báo | |

---

## 13. LUỒNG HDV - CẬP NHẬT YÊU CẦU ĐẶC BIỆT

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| 1. Vào chi tiết booking | |
| 2. Tìm phần "Yêu cầu đặc biệt" | |
| 3. Sửa nội dung | |
| 4. Nhấn nút "Cập nhật" | 5. Nhận POST request: `booking_id`, `yeu_cau_dac_biet` |
| | 6. Kiểm tra quyền HDV và booking có thuộc HDV này không |
| | 7. **Nếu không có quyền** → Hiển thị lỗi → Quay lại bước 1 |
| | 8. Lấy booking từ database |
| | 9. Cập nhật trường `yeu_cau_dac_biet` trong bảng `booking` |
| | 10. **Thành công** → Redirect về trang chi tiết booking |
| | 11. **Thất bại** → Redirect về trang chi tiết booking với lỗi |
| 5. Thấy trang chi tiết booking với thông báo | |

---

## 14. LUỒNG QUẢN LÝ BOOKING - SỬA BOOKING

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào danh sách booking | |
| 2. Chọn booking cần sửa → Nhấn "Sửa" | 3. Kiểm tra quyền Admin |
| | 4. Lấy thông tin booking từ database theo ID |
| | 5. Lấy danh sách tour, HDV, khách, lịch khởi hành, điểm danh |
| | 6. Hiển thị form với dữ liệu hiện có |
| 3. Sửa thông tin booking | |
| 4. Cập nhật HDV (nếu có) | |
| 5. Cập nhật danh sách khách | |
| 6. Cập nhật lịch khởi hành | |
| 7. Cập nhật điểm danh (nếu có) | |
| 8. Cập nhật dịch vụ | |
| 9. Nhấn nút "Cập nhật" | 10. Nhận dữ liệu POST với `id` |
| | 11. Validate dữ liệu |
| | 12. **Nếu có lỗi** → Hiển thị form với lỗi → Quay lại bước 3 |
| | 13. **Nếu hợp lệ**: |
| | - Cập nhật bảng `booking` |
| | - Đồng bộ HDV (xóa cũ, thêm mới nếu có) |
| | - Đồng bộ khách (cập nhật hoặc thêm mới) |
| | - Cập nhật lịch khởi hành |
| | - Cập nhật điểm danh |
| | - Đồng bộ dịch vụ (xóa cũ, thêm mới) |
| | 14. **Thành công** → Redirect về danh sách booking |
| | 15. **Thất bại** → Redirect về form sửa |
| 10. Thấy danh sách booking với thông báo | |

---

## 15. LUỒNG QUẢN LÝ BOOKING - XÓA BOOKING

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| 1. Vào danh sách booking | |
| 2. Chọn booking cần xóa → Nhấn "Xóa" | 3. Kiểm tra quyền Admin |
| | 4. Nhận POST request với `id` |
| 3. Xác nhận xóa (trong popup) | 5. Kiểm tra booking có tồn tại không |
| | 6. Xóa booking trong bảng `booking` |
| | 7. Xóa các record liên quan (khách, HDV, lịch khởi hành, điểm danh, dịch vụ, nhật ký) |
| | 8. Xóa file Excel danh sách khách (nếu có) |
| | 9. Redirect về danh sách booking với thông báo |
| 4. Thấy danh sách booking với thông báo | |

---

## GHI CHÚ

- Tất cả các luồng đều bắt đầu từ người dùng (Admin/HDV) thực hiện hành động
- Hệ thống luôn kiểm tra quyền trước khi xử lý
- Hệ thống luôn validate dữ liệu trước khi lưu vào database
- Có vòng lặp xử lý khi import Excel (xử lý từng dòng)
- Có điều kiện rẽ nhánh: thành công/thất bại, có lỗi/không lỗi
- Các thao tác database: SELECT, INSERT, UPDATE, DELETE
- Upload file: Kiểm tra định dạng → Upload → Lưu đường dẫn
- Session: Lưu thông báo success/error để hiển thị sau redirect

