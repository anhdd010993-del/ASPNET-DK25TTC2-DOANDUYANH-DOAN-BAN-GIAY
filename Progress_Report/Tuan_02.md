# BÁO CÁO TIẾN ĐỘ ĐỒ ÁN - TUẦN 2

- **Trọng tâm công việc:** Phân tích thiết kế hệ thống và Cơ sở dữ liệu

## 1. Nội dung công việc
- Khảo sát thực tế nhu cầu của hệ thống cửa hàng thương mại điện tử.
- Xác định chi tiết các yêu cầu chức năng (các Use Case cốt lõi như Đăng nhập, Đăng ký, Quản lý quyền, Quản lý tài khoản, Tra cứu sản phẩm, Đặt hàng, Quản lý danh mục, Quản lý nhập xuất) và các yêu cầu phi chức năng phục vụ vận hành.
- Vẽ sơ đồ Use Case tổng quát (Mức chính) và sơ đồ Use Case chi tiết cho từng phân hệ.
- Thiết kế mô hình quan hệ dữ liệu hệ thống (UML Database) trên SQL Server.

## 2. Tài liệu liên quan
- Tài liệu phân tích yêu cầu phần mềm và đặc tả chức năng hệ thống.
- Tài liệu hướng dẫn quản trị cơ sở dữ liệu và chiến lược Database First với MSSQL Server.
- Đặc tả cấu trúc hệ thống bảng cơ sở dữ liệu: bảng phân quyền thành viên (`ThanhVien`, `LoaiThanhVien`, `Quyen`, `LoaiThanhVien_Quyen`) và các bảng nghiệp vụ bán hàng (`SanPham`, `LoaiSanPham`, `NhaSanXuat`, `NhaCungCap`, `DonDatHang`, `ChiTietDonHang`, `PhieuNhap`, `ChiTietPhieuNhap`, `BinhLuan`).

## 3. Khó khăn gặp phải
- Thiết kế các mối quan hệ ràng buộc, khóa chính (PK) và khóa ngoại (FK) chặt chẽ giữa các bảng thực thể nghiệp vụ phức tạp như `SanPham`, `LoaiSanPham`, `NhaSanXuat` và `NhaCungCap`.
- Đồng bộ cơ chế quản lý tài khoản và phân quyền của hệ thống sao cho khớp với các Actor đặc thù (Admin, Staff, Customer).

## 4. Kết quả đạt được
- Xây dựng xong danh sách các bảng chi tiết và sơ đồ cơ sở dữ liệu UML hoàn chỉnh.
- Hoàn thành biểu đồ Class Diagram cho hệ thống ứng dụng và sơ đồ cấu trúc màn hình chức năng.
