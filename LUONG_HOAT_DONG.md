# LUỒNG HOẠT ĐỘNG CÁC CHỨC NĂNG
## Website Quản Lý Tour

---

## 1. LUỒNG ĐĂNG NHẬP

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Truy cập trang đăng nhập | |
| | Hiển thị giao diện trang đăng nhập |
| Nhập email và mật khẩu | |
| Nhấn nút "Đăng nhập" | |
| | Nhận dữ liệu từ form POST |
| | Validate: Kiểm tra email và mật khẩu không rỗng |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với thông báo lỗi |
| | **Nếu hợp lệ** → Gọi `User::authenticate()` để kiểm tra trong database |
| | **Điểm quyết định: Đăng nhập thành công?** |
| | **Nếu thất bại** → Hiển thị lỗi "Email hoặc mật khẩu không đúng" |
| | **Nếu thành công** → Lưu thông tin user vào session |
| | Kiểm tra phân quyền (admin/hdv) |
| | Redirect về trang home tương ứng |
| Thấy trang home | |
| **Kết thúc** | |

---

## 2. LUỒNG QUẢN LÝ TOUR - TẠO TOUR MỚI

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào menu "Quản lý Tour" → "Thêm tour mới" | |
| | Kiểm tra quyền Admin |
| | Lấy danh sách danh mục từ database |
| | Hiển thị form tạo tour với danh sách danh mục |
| Điền thông tin: Tên tour, Danh mục, Mô tả, Giá, Trạng thái | |
| Thêm chính sách (có thể nhiều): Tên chính sách + Nội dung | |
| Thêm lịch trình (có thể nhiều): Số ngày + Điểm tham quan + Hoạt động | |
| Thêm nhà cung cấp (có thể nhiều): Tên + Loại + Liên hệ + Ghi chú | |
| Upload ảnh tour chính | |
| Upload ảnh chi tiết (có thể nhiều) | |
| Nhấn nút "Lưu" | |
| | Nhận dữ liệu POST |
| | Validate: Kiểm tra tên tour, danh mục, mô tả, giá > 0 |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với lỗi và dữ liệu cũ |
| | **Nếu hợp lệ**: |
| | - Upload ảnh tour chính → Lưu vào `uploads/tours/` |
| | - Upload ảnh chi tiết → Lưu vào `uploads/tours/` |
| | - Tạo record mới trong bảng `tour` |
| | - Lấy `tour_id` vừa tạo |
| | - Lưu chính sách vào bảng `tour_chinh_sach` |
| | - Lưu lịch trình vào bảng `tour_lich_trinh` |
| | - Lưu nhà cung cấp vào bảng `tour_nha_cung_cap` |
| | - Lưu ảnh chi tiết vào bảng `tour_anh` |
| | **Điểm quyết định: Lưu thành công?** |
| | **Nếu thất bại** → Lưu thông báo error vào session → Redirect về form tạo |
| | **Nếu thành công** → Lưu thông báo success vào session → Redirect về danh sách tour |
| Thấy danh sách tour với thông báo thành công | |
| **Kết thúc** | |

---

## 3. LUỒNG QUẢN LÝ TOUR - SỬA TOUR

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào danh sách tour | |
| Chọn tour cần sửa → Nhấn "Sửa" | |
| | Kiểm tra quyền Admin |
| | Lấy thông tin tour từ database theo ID |
| | Lấy danh sách chính sách, lịch trình, nhà cung cấp, ảnh chi tiết |
| | Hiển thị form với dữ liệu hiện có |
| Sửa thông tin cần thiết | |
| Có thể xóa chính sách, lịch trình, nhà cung cấp cũ | |
| Có thể thêm chính sách, lịch trình, nhà cung cấp mới | |
| Có thể xóa ảnh chi tiết (chọn checkbox) | |
| Có thể thêm ảnh chi tiết mới | |
| Nhấn nút "Cập nhật" | |
| | Nhận dữ liệu POST (có `id`) |
| | Validate dữ liệu |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với lỗi |
| | **Nếu hợp lệ**: |
| | - Nếu có upload ảnh mới → Upload và lưu |
| | - Nếu không → Giữ ảnh cũ |
| | - Cập nhật bảng `tour` |
| | - Xóa tất cả chính sách cũ → Lưu mới vào `tour_chinh_sach` |
| | - Xóa tất cả lịch trình cũ → Lưu mới vào `tour_lich_trinh` |
| | - Xóa tất cả nhà cung cấp cũ → Lưu mới vào `tour_nha_cung_cap` |
| | - Xóa ảnh chi tiết được chọn (từ `tour_anh`) |
| | - Thêm ảnh chi tiết mới (nếu có) |
| | **Điểm quyết định: Cập nhật thành công?** |
| | **Nếu thất bại** → Redirect về form sửa với thông báo lỗi |
| | **Nếu thành công** → Redirect về danh sách tour với thông báo thành công |
| Thấy danh sách tour với thông báo | |
| **Kết thúc** | |

---

## 4. LUỒNG QUẢN LÝ TOUR - XÓA TOUR

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào danh sách tour | |
| Chọn tour cần xóa → Nhấn "Xóa" | |
| | Kiểm tra quyền Admin |
| | Nhận POST request với `id` |
| | Kiểm tra tour có tồn tại không |
| | Kiểm tra tour có đang được sử dụng trong booking không |
| | **Điểm quyết định: Có thể xóa?** |
| | **Nếu không thể xóa** → Lưu thông báo lỗi "Không thể xóa tour này vì đang được sử dụng" |
| | **Nếu có thể xóa**: |
| | - Xóa tour trong bảng `tour` |
| | - Xóa các record liên quan (chính sách, lịch trình, nhà cung cấp, ảnh) |
| | - Lưu thông báo thành công |
| | Redirect về danh sách tour với thông báo |
| Thấy danh sách tour với thông báo | |
| **Kết thúc** | |

---

## 5. LUỒNG QUẢN LÝ BOOKING - TẠO BOOKING MỚI

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào menu "Quản lý Booking" → "Thêm booking mới" | |
| | Kiểm tra quyền Admin |
| | Lấy danh sách tour từ database |
| | Lấy danh sách HDV từ database |
| | Hiển thị form với dropdown tour và HDV |
| Điền form: Chọn tour, Loại khách, Tên người đặt, Số lượng, Thời gian tour, Liên hệ | |
| Thêm yêu cầu đặc biệt (nếu có) | |
| Phân công HDV (nếu có) | |
| Thêm khách hàng (có thể thêm sau) | |
| Thiết lập lịch khởi hành: Ngày giờ xuất phát, Điểm tập trung, Thời gian kết thúc (có thể thêm sau) | |
| Upload file Excel danh sách khách (tùy chọn) | |
| Nhấn nút "Lưu" | |
| | Nhận dữ liệu POST |
| | Validate: tour_id, tên người đặt, số lượng > 0, thời gian tour, liên hệ |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với lỗi |
| | **Nếu hợp lệ**: |
| | - Tạo record mới trong bảng `booking` |
| | - Lấy `booking_id` vừa tạo |
| | - Nếu có HDV → Lưu vào bảng `booking_hdv` |
| | - Nếu có khách → Lưu vào bảng `booking_khach` |
| | - Nếu có lịch khởi hành → Lưu vào bảng `lich_khoi_hanh` |
| | - Nếu có yêu cầu đặc biệt → Tạo dịch vụ trong `booking_dich_vu` |
| | - Nếu có file Excel → Upload và lưu vào `uploads/guest_lists/` |
| | **Điểm quyết định: Lưu thành công?** |
| | **Nếu thất bại** → Redirect về form tạo với thông báo lỗi |
| | **Nếu thành công** → Redirect về danh sách booking với thông báo thành công |
| Thấy danh sách booking với thông báo thành công | |
| **Kết thúc** | |

---

## 6. LUỒNG QUẢN LÝ BOOKING - IMPORT KHÁCH TỪ EXCEL

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào trang sửa booking | |
| Chọn tab "Danh sách khách" | |
| Chọn file Excel (định dạng: Họ tên, Giới tính, Năm sinh, Số giấy tờ, Yêu cầu) | |
| Nhấn nút "Import" | |
| | Nhận POST request với `booking_id` và file |
| | Kiểm tra file có tồn tại và hợp lệ không (CSV, XLS, XLSX) |
| | **Điểm quyết định: File hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị lỗi "File không hợp lệ" |
| | **Nếu hợp lệ**: |
| | - Upload file tạm |
| | - Đọc file Excel bằng PHPSpreadsheet (bỏ dòng header, bắt đầu từ dòng 2) |
| | **Vòng lặp: Với mỗi dòng trong file**: |
| | - Lấy: Họ tên, Giới tính, Năm sinh, Số giấy tờ, Yêu cầu |
| | - Validate: Họ tên không được rỗng |
| | - **Nếu hợp lệ** → Tạo record trong `booking_khach` → Đếm thành công |
| | - **Nếu không hợp lệ** → Ghi lại lỗi → Đếm thất bại |
| | - Xóa file tạm |
| | - **Nếu có thành công** → Lưu thông báo "Import thành công X khách hàng" |
| | - **Nếu có lỗi** → Lưu thông báo lỗi chi tiết |
| | Redirect về trang chi tiết booking |
| Thấy danh sách khách đã được import | |
| **Kết thúc** | |

---

## 7. LUỒNG QUẢN LÝ BOOKING - XUẤT EXCEL ĐIỂM DANH

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào trang chi tiết booking | |
| Chọn tab "Điểm danh" | |
| Nhấn nút "Xuất Excel" | |
| | Lấy danh sách khách từ `booking_khach` theo `booking_id` |
| | Lấy thông tin điểm danh từ `diem_danh_khach` |
| | Tạo file Excel bằng PHPSpreadsheet: |
| | - Header: STT, Họ tên, Giới tính, Năm sinh, Số giấy tờ, Trạng thái điểm danh |
| | - Dữ liệu: Mỗi khách một dòng với thông tin tương ứng |
| | Trả về file Excel để download |
| File Excel được tải về máy | |
| **Kết thúc** | |

---

## 8. LUỒNG HDV - XEM DANH SÁCH BOOKING

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| **Bắt đầu** | |
| Đăng nhập với tài khoản HDV | |
| Vào menu "Booking của tôi" | |
| | Kiểm tra đăng nhập và quyền HDV |
| | Lấy `user_id` từ session |
| | Tìm `hdv_id` từ bảng `hdv` theo `tai_khoan_id` |
| | Query booking từ `booking_hdv` với `hdv_id` này |
| | Lấy thông tin tour, lịch khởi hành cho mỗi booking |
| | Hiển thị danh sách booking |
| Thấy danh sách booking được phân công | |
| **Kết thúc** | |

---

## 9. LUỒNG HDV - CHECK-IN KHÁCH

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| **Bắt đầu** | |
| Vào chi tiết booking được phân công | |
| Chọn tab "Điểm danh" | |
| Chọn khách cần check-in | |
| Chọn trạng thái: Đã đến / Vắng / Vắng mặt / Trễ | |
| Nhập ghi chú (nếu có) | |
| Nhấn nút "Lưu điểm danh" | |
| | Nhận POST request: `booking_id`, `lich_khoi_hanh_id`, `booking_khach_id`, `trang_thai`, `ghi_chu` |
| | Kiểm tra quyền HDV và booking có thuộc HDV này không |
| | **Điểm quyết định: Có quyền?** |
| | **Nếu không có quyền** → Hiển thị lỗi "Không có quyền truy cập" |
| | **Nếu có quyền**: |
| | - Validate: `booking_id`, `lich_khoi_hanh_id`, `booking_khach_id`, `trang_thai` hợp lệ |
| | - **Nếu chưa có `lich_khoi_hanh_id`** → Tạo mới trong `lich_khoi_hanh` |
| | - Gọi `Booking::upsertDiemDanh()`: |
| |   - Kiểm tra đã có điểm danh chưa (trong `diem_danh_khach`) |
| |   - **Nếu có** → Cập nhật record |
| |   - **Nếu chưa** → Tạo mới record |
| | **Điểm quyết định: Lưu thành công?** |
| | **Nếu thất bại** → Lưu thông báo error → Redirect về trang chi tiết booking |
| | **Nếu thành công** → Lưu thông báo success → Redirect về trang chi tiết booking |
| Thấy trang chi tiết booking với thông báo | |
| **Kết thúc** | |

---

## 10. LUỒNG HDV - TẠO NHẬT KÝ TOUR

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| **Bắt đầu** | |
| Vào chi tiết booking | |
| Chọn "Nhật ký tour" | |
| Nhấn nút "Thêm nhật ký" | |
| | Kiểm tra quyền HDV |
| | Lấy thông tin booking |
| | Hiển thị form tạo nhật ký |
| Điền form: Ngày giờ, Nội dung, Đánh giá HDV | |
| Nhấn nút "Lưu" | |
| | Nhận POST request: `booking_id`, `ngay_gio`, `noi_dung`, `danh_gia_hdv` |
| | Kiểm tra quyền HDV |
| | Validate: `noi_dung` không được rỗng |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với lỗi |
| | **Nếu hợp lệ**: |
| | - **Nếu `ngay_gio` rỗng** → Lấy thời gian hiện tại |
| | - Tạo record mới trong `nhat_ky_tour` |
| | **Điểm quyết định: Lưu thành công?** |
| | **Nếu thất bại** → Redirect về form tạo với lỗi |
| | **Nếu thành công** → Redirect về danh sách nhật ký với thông báo thành công |
| Thấy danh sách nhật ký với thông báo | |
| **Kết thúc** | |

---

## 11. LUỒNG HDV - SỬA NHẬT KÝ TOUR

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| **Bắt đầu** | |
| Vào danh sách nhật ký tour | |
| Chọn nhật ký cần sửa → Nhấn "Sửa" | |
| | Kiểm tra quyền HDV |
| | Lấy thông tin nhật ký từ database theo ID |
| | Hiển thị form với dữ liệu hiện có |
| Sửa nội dung nhật ký | |
| Nhấn nút "Cập nhật" | |
| | Nhận POST request với `id` |
| | Validate: `noi_dung` không được rỗng |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với lỗi |
| | **Nếu hợp lệ** → Cập nhật record trong `nhat_ky_tour` |
| | **Điểm quyết định: Cập nhật thành công?** |
| | **Nếu thất bại** → Redirect về form sửa với thông báo lỗi |
| | **Nếu thành công** → Redirect về danh sách nhật ký với thông báo thành công |
| Thấy danh sách nhật ký với thông báo | |
| **Kết thúc** | |

---

## 12. LUỒNG HDV - XÓA NHẬT KÝ TOUR

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| **Bắt đầu** | |
| Vào danh sách nhật ký tour | |
| Chọn nhật ký cần xóa → Nhấn "Xóa" | |
| | Kiểm tra quyền HDV |
| | Nhận POST request với `id` |
| Xác nhận xóa (trong popup) | |
| | Lấy nhật ký từ database |
| | Xóa record trong `nhat_ky_tour` |
| | **Điểm quyết định: Xóa thành công?** |
| | **Nếu thất bại** → Lưu thông báo lỗi |
| | **Nếu thành công** → Lưu thông báo thành công |
| | Redirect về danh sách nhật ký với thông báo |
| Thấy danh sách nhật ký với thông báo | |
| **Kết thúc** | |

---

## 13. LUỒNG HDV - CẬP NHẬT YÊU CẦU ĐẶC BIỆT

| **HDV** | **HỆ THỐNG** |
|---------|--------------|
| **Bắt đầu** | |
| Vào chi tiết booking | |
| Tìm phần "Yêu cầu đặc biệt" | |
| Sửa nội dung | |
| Nhấn nút "Cập nhật" | |
| | Nhận POST request: `booking_id`, `yeu_cau_dac_biet` |
| | Kiểm tra quyền HDV và booking có thuộc HDV này không |
| | **Điểm quyết định: Có quyền?** |
| | **Nếu không có quyền** → Hiển thị lỗi "Không có quyền truy cập" |
| | **Nếu có quyền**: |
| | - Lấy booking từ database |
| | - Cập nhật trường `yeu_cau_dac_biet` trong bảng `booking` |
| | **Điểm quyết định: Cập nhật thành công?** |
| | **Nếu thất bại** → Redirect về trang chi tiết booking với lỗi |
| | **Nếu thành công** → Redirect về trang chi tiết booking với thông báo thành công |
| Thấy trang chi tiết booking với thông báo | |
| **Kết thúc** | |

---

## 14. LUỒNG QUẢN LÝ BOOKING - SỬA BOOKING

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào danh sách booking | |
| Chọn booking cần sửa → Nhấn "Sửa" | |
| | Kiểm tra quyền Admin |
| | Lấy thông tin booking từ database theo ID |
| | Lấy danh sách tour, HDV, khách, lịch khởi hành, điểm danh |
| | Hiển thị form với dữ liệu hiện có |
| Sửa thông tin booking | |
| Cập nhật HDV (nếu có) | |
| Cập nhật danh sách khách | |
| Cập nhật lịch khởi hành | |
| Cập nhật điểm danh (nếu có) | |
| Cập nhật dịch vụ | |
| Nhấn nút "Cập nhật" | |
| | Nhận dữ liệu POST với `id` |
| | Validate dữ liệu |
| | **Điểm quyết định: Dữ liệu hợp lệ?** |
| | **Nếu không hợp lệ** → Hiển thị form với lỗi |
| | **Nếu hợp lệ**: |
| | - Cập nhật bảng `booking` |
| | - Đồng bộ HDV (xóa cũ, thêm mới nếu có) |
| | - Đồng bộ khách (cập nhật hoặc thêm mới) |
| | - Cập nhật lịch khởi hành |
| | - Cập nhật điểm danh |
| | - Đồng bộ dịch vụ (xóa cũ, thêm mới) |
| | **Điểm quyết định: Cập nhật thành công?** |
| | **Nếu thất bại** → Redirect về form sửa với thông báo lỗi |
| | **Nếu thành công** → Redirect về danh sách booking với thông báo thành công |
| Thấy danh sách booking với thông báo | |
| **Kết thúc** | |

---

## 15. LUỒNG QUẢN LÝ BOOKING - XÓA BOOKING

| **ADMIN** | **HỆ THỐNG** |
|-----------|--------------|
| **Bắt đầu** | |
| Vào danh sách booking | |
| Chọn booking cần xóa → Nhấn "Xóa" | |
| | Kiểm tra quyền Admin |
| | Nhận POST request với `id` |
| Xác nhận xóa (trong popup) | |
| | Kiểm tra booking có tồn tại không |
| | Xóa booking trong bảng `booking` |
| | Xóa các record liên quan (khách, HDV, lịch khởi hành, điểm danh, dịch vụ, nhật ký) |
| | Xóa file Excel danh sách khách (nếu có) |
| | **Điểm quyết định: Xóa thành công?** |
| | **Nếu thất bại** → Lưu thông báo lỗi |
| | **Nếu thành công** → Lưu thông báo thành công |
| | Redirect về danh sách booking với thông báo |
| Thấy danh sách booking với thông báo | |
| **Kết thúc** | |

---

## GHI CHÚ VỀ BIỂU ĐỒ

### Cấu trúc:
- **2 Swimlanes (Làn bơi):** Admin/HDV và Hệ thống
- **Bắt đầu:** Nút tròn đen đặc (Initial Node) trong làn bơi Admin/HDV
- **Kết thúc:** Nút tròn đen có viền (Final Node) sau hoạt động cuối cùng

### Các thành phần:
1. **Hoạt động (Activity):** Các bước thực hiện trong mỗi làn bơi
2. **Điểm quyết định (Decision Node):** Hình thoi với các nhánh:
   - Thành công / Thất bại
   - Hợp lệ / Không hợp lệ
   - Có quyền / Không có quyền
3. **Vòng lặp (Loop):** Xử lý từng dòng trong file Excel
4. **Luồng (Flow):** Mũi tên nối các hoạt động, thể hiện thứ tự thực hiện

### Quy tắc:
- Mỗi hành động của Admin/HDV sẽ kích hoạt phản hồi tương ứng từ Hệ thống
- Hệ thống luôn kiểm tra quyền và validate dữ liệu trước khi xử lý
- Có các điểm quyết định rõ ràng để xử lý các trường hợp thành công/thất bại
- Luồng có thể quay lại (loop) khi có lỗi validation
