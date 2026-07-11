# BÁO CÁO TIẾN ĐỘ ĐỒ ÁN - TUẦN 4

- **Khoảng thời gian:** 13/07/2026 - 19/07/2026
- **Trọng tâm công việc:** Hiện thực hóa code chức năng quản trị (Phía Admin) và bổ sung tính năng cải tiến

## 1. Nội dung công việc
- Tích hợp giao diện trang quản trị Admin để hiển thị số liệu thống kê của hệ thống.
- Phát triển các chức năng CRUD (Thêm, Sửa, Xóa, Xem) tại phân hệ Admin dành cho người quản trị:
  + Quản lý danh mục Sản phẩm, Loại sản phẩm và Nhà sản xuất.
  + Quản lý hệ thống phiếu nhập hàng, quản lý sản phẩm gần hết hàng để bổ sung số lượng tồn kho.
  + Quản lý và duyệt đơn đặt hàng theo các trạng thái thanh toán và giao hàng.
- Thiết lập giao diện Quản lý thành viên, danh sách quyền và thực hiện chức năng phân quyền cho từng loại tài khoản qua Checkbox.

## 2. Tài liệu liên quan
- Cơ chế quản lý tài khoản thành viên và phân quyền dựa trên các bảng dữ liệu `Quyen` và `LoaiThanhVien_Quyen` trong hệ thống.
- Cú pháp LINQ hỗ trợ trong việc truy vấn dữ liệu một cách dễ dàng hơn thông qua cơ chế ánh xạ của Entity Framework.

## 3. Khó khăn khi viết thêm chức năng
- Gặp trở ngại lớn khi nghiên cứu tích hợp các chức năng nâng cao theo đề xuất cải tiến: Thiết lập hệ tính năng thông báo nổi thời gian thực tại trang Admin khi hệ thống ghi nhận có đơn đặt hàng mới từ khách hàng nhằm tăng tính tương tác.
- Gặp khó khăn khi xây dựng logic gợi ý thông minh tự động kiểm tra trùng khớp thông tin số điện thoại/email khách hàng cũ để gợi ý liên kết dữ liệu hoặc tạo nhanh profile tại trang quản trị đơn hàng, cấu hình Realtime tiêu tốn nhiều thời gian thử nghiệm.

## 4. Kết quả đạt được
- Hoàn thiện toàn bộ hệ thống các màn hình CRUD của Admin đáp ứng đầy đủ các yêu cầu quản trị.
- Tích hợp thành công cơ chế phân quyền chức năng rõ ràng giữa các vai trò Admin, Staff và Customer.
