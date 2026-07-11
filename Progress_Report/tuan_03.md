# BÁO CÁO TIẾN ĐỘ ĐỒ ÁN - TUẦN 3

- **Khoảng thời gian:** 06/07/2026 - 12/07/2026
- **Trọng tâm công việc:** Hiện thực hóa code chức năng cốt lõi (Phía Khách hàng)

## 1. Nội dung công việc
- Cấu hình kết nối cơ sở dữ liệu SQL Server và áp dụng công nghệ Entity Framework để ánh xạ dữ liệu thành các thực thể hướng đối tượng.
- Triển khai lập trình giao diện và xử lý logic cho phía Khách hàng (User Website):
  + Màn hình Trang chủ hiển thị danh sách sản phẩm mới theo các style khác nhau.
  + Trang Danh sách sản phẩm và bộ lọc tìm kiếm theo Chủng loại / Nhà sản xuất / Từ khóa.
  + Trang Chi tiết sản phẩm hiển thị thông tin mô tả, thông số kỹ thuật, giá bán và lượt xem.
  + Lập trình logic Giỏ hàng: cho phép người dùng thêm sản phẩm, cập nhật số lượng, xóa sản phẩm và tự động tính tổng tiền.
  + Xử lý luồng Đặt hàng trực tuyến đối với cả Guest (điền form thông tin khi mua hàng) và Customer (không cần điền lại form).

## 2. Tài liệu liên quan
- Tài liệu kỹ thuật điều hướng hệ thống và xử lý Action trong mô hình ASP.NET MVC 5.
- Cơ chế lưu trữ thông tin trạng thái giỏ hàng tạm thời (`GioHang`) và truyền tải dữ liệu giữa View và Controller.

## 3. Khó khăn gặp phải
- Xử lý đồng bộ dữ liệu giỏ hàng, cập nhật tổng tiền và số lượng tức thời khi người dùng tương tác trực tiếp tại giao diện front-end mà không cần tải lại toàn bộ trang nhằm tối ưu trải nghiệm người dùng.

## 4. Kết quả đạt được
- Vận hành ổn định toàn bộ luồng mua hàng phía giao diện khách hàng từ xem danh sách đến đặt hàng thành công.
- Dữ liệu đơn đặt hàng (`DonDatHang`) và chi tiết đơn hàng được lưu trữ chính xác vào database sau khi người dùng xác nhận đặt hàng.
