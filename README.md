# 🛍️ Đồ Án Website Bán Giày Dép (WebsiteBanHang)

Đồ án môn học — website thương mại điện tử bán **giày dép** (và một số mặt hàng khác như laptop, phụ kiện) được xây dựng bằng **ASP.NET MVC 5** + **Entity Framework 6 (Database First)** + **SQL Server**.

---

## 📋 Mục lục
- [Giới thiệu đồ án](#-giới-thiệu-đồ-án)
- [Công nghệ sử dụng](#-công-nghệ-sử-dụng)
- [Cấu trúc thư mục](#-cấu-trúc-thư-mục)
- [Hướng dẫn cài đặt qua SSMS](#-hướng-dẫn-cài-đặt-qua-ssms)
- [Chạy project bằng Visual Studio](#-chạy-project-bằng-visual-studio)
- [Tài khoản Admin & Người dùng](#-tài-khoản-admin--người-dùng)
- [Các link quan trọng](#-các-link-quan-trọng)
- [Danh sách chức năng](#-danh-sách-chức-năng)
- [Danh sách Map (Route) của đồ án](#-danh-sách-map-route-của-đồ-án)
- [Lỗi thường gặp & Cách khắc phục](#-lỗi-thường-gặp--cách-khắc-phục)

---

## 🎯 Giới thiệu đồ án

**WebsiteBanHang** là hệ thống thương mại điện tử cho phép:

- **Khách hàng** (không cần đăng nhập): xem sản phẩm, tìm kiếm, xem chi tiết, thêm vào giỏ hàng, đặt hàng, bình luận.
- **Thành viên**: đăng ký/đăng nhập, đặt hàng với thông tin đã lưu.
- **Nhân viên (Quản lý)**: quản lý sản phẩm, đơn hàng, loại sản phẩm, nhà sản xuất, nhập hàng.
- **Admin (Quản trị viên)**: toàn quyền — thêm/quản lý thành viên, phân quyền, xem thống kê doanh thu.

Đồ án phục vụ mục đích học tập, minh họa mô hình **MVC + Repository + Entity Framework Database First**, hệ thống phân quyền bằng **Forms Authentication + Role-based**.

---

## 🛠️ Công nghệ sử dụng

| Hạng mục | Chi tiết |
|---|---|
| Ngôn ngữ | C# |
| Framework | ASP.NET MVC 5 (.NET Framework 4.7.2) |
| ORM | Entity Framework 6 (Database First — EDMX) |
| CSDL | SQL Server (mặc định `.\SQLEXPRESS`, DB: `QuanLyBanHang`) |
| Front-end | Bootstrap 3, jQuery, SB Admin 2 template |
| Authentication | Forms Authentication (custom, role-based) |
| IDE | Visual Studio 2017/2019/2022 |

---

## 📂 Cấu trúc thư mục

```
Websitegiaydep/
├── WebsiteBanHang.sln                 # Solution file
├── WebsiteBanHang/                    # Project chính (MVC)
│   ├── App_Start/                     # RouteConfig, BundleConfig, FilterConfig
│   ├── Content/                       # CSS, HinhAnhSP/, slider images
│   ├── Controllers/                   # 13 controller
│   ├── Models/                        # EDMX + entities + Metadata + ViewModel
│   ├── Views/                         # Razor views (57 file .cshtml)
│   ├── Scripts/                       # jQuery, Bootstrap JS
│   ├── App_Data/                      # 
│   ├── Web.config                     # Connection string
│   └── packages.config                # NuGet packages
├── Hinh/                              # Hình ảnh tài liệu
├── scriptgiay.sql                     # Script tạo DB + seed data (~888 dòng)
└── README.md                          # File này
```

---

## 💾 Hướng dẫn cài đặt qua SSMS

### Yêu cầu trước khi cài
- Đã cài **SQL Server** (Express hoặc Developer) và **SQL Server Management Studio (SSMS)**.
- Cấu hình mặc định trong project: `data source=.\SQLEXPRESS`, DB: `QuanLyBanHang`, dùng **Windows Authentication**.

### Bước 1 — Mở SSMS
1. Mở **SQL Server Management Studio**.
2. Server name gõ: `.\SQLEXPRESS` (hoặc tên SQL Server của bạn).
3. Authentication chọn **Windows Authentication** → nhấn **Connect**.

### Bước 2 — Chạy script tạo Database
1. Trên thanh menu: **File → Open → File…** (phím tắt `Ctrl + O`).
2. Chọn file `scriptgiay.sql` nằm trong thư mục gốc đồ án.
3. Đảm bảo database master đang chọn (gõ `USE master; GO` nếu cần).
4. Nhấn **Execute** (phím tắt `F5`) để chạy toàn bộ script.

Script sẽ tự động:
- Tạo database `QuanLyBanHang`.
- Tạo **15 bảng** (SanPham, LoaiSanPham, NhaSanXuat, NhaCungCap, ThanhVien, LoaiThanhVien, Quyen, LoaiThanhVien_Quyen, KhachHang, DonDatHang, ChiTietDonDatHang, PhieuNhap, ChiTietPhieuNhap, BinhLuan).
- Thêm các **ràng buộc khóa ngoại** (FK).
- Insert dữ liệu mẫu (khoảng 134 sản phẩm, 16 khách hàng, 6 tài khoản, 16 nhà sản xuất...).

### Bước 3 — Kiểm tra Database
Trong SSMS, mở rộng **Databases → QuanLyBanHang → Tables**. Bạn sẽ thấy đầy đủ các bảng và dữ liệu.

### Bước 4 — Cấu hình SQL Server cho phép kết nối
Mặc định project dùng `.\SQLEXPRESS` + **Windows Authentication**, nên không cần tạo login mới. Nếu gặp lỗi kết nối, kiểm tra:
- SQL Server service đang chạy (mở **Services** → `SQL Server (SQLEXPRESS)` → Start).
- Trong **SQL Server Configuration Manager**, bật **TCP/IP** protocol.

### Bước 5 (tuỳ chọn) — Nếu muốn dùng SQL Authentication
Mở `Web.config` trong project, sửa connection string:
```xml
<add name="QuanLyBanHangEntities"
     connectionString="metadata=res://*/Models.QuanLyBanHangModel.csdl|res://*/Models.QuanLyBanHangModel.ssdl|res://*/Models.QuanLyBanHangModel.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=.\SQLEXPRESS;initial catalog=QuanLyBanHang;user id=sa;password=YourPassword;MultipleActiveResultSets=True;App=EntityFramework&quot;"
     providerName="System.Data.EntityClient" />
```

---

## ▶️ Chạy project bằng Visual Studio

### Bước 1 — Mở Solution
- Mở **Visual Studio** (khuyến nghị 2019 hoặc 2022).
- **File → Open → Project/Solution** → chọn `WebsiteBanHang.sln`.

### Bước 2 — Restore NuGet Packages
- Chuột phải lên **Solution** → **Restore NuGet Packages**.
- Nếu dùng VS2017 trở lên, VS sẽ tự động restore khi build. Nếu thiếu package, mở **Package Manager Console** và gõ:
```
Update-Package -reinstall
```

### Bước 3 — Kiểm tra Connection String
Mở `Web.config` → `<connectionStrings>` đảm bảo đúng:
```
data source=.\SQLEXPRESS;initial catalog=QuanLyBanHang;integrated security=True
```
Trỏ đúng `data source` nếu bạn dùng tên SQL Server khác.

### Bước 4 — Build & Run
- Chọn cấu hình `Debug` và nhấn **IIS Express** (mặc định).
- Nhấn **F5** (Start Debugging) hoặc **Ctrl + F5** (Start Without Debugging).
- Trình duyệt sẽ mở trang chủ `http://localhost:xxxx/`.

### Bước 5 — Đăng nhập
- Truy cập `http://localhost:xxxx/ThongKe` để vào trang **Admin** (đăng nhập bằng tài khoản admin).
- Hoặc nhấn **Đăng nhập** trên header để đăng nhập người dùng thường.

---

## 👤 Tài khoản Admin & Người dùng

### 🔐 Tài khoản Admin (Quản trị viên — `MaLoaiTV = 1`)

| Tài khoản | Mật khẩu | Họ tên | Quyền |
|---|---|---|---|
| `admin` | `123456` | Quan tri vien | **QuanTriWeb** — Toàn quyền |

> Truy cập: `/ThongKe` (Admin Dashboard) — đăng nhập tại đây.

### 🛒 Tài khoản Nhân viên / Quản lý (`MaLoaiTV = 2`)

| Tài khoản | Mật khẩu | Họ tên | Quyền |
|---|---|---|---|
| `staff1` | `123456` | Nhan vien 1 | **QuanLy** |
| `staff2` | `123456` | nhan vien 2 | **QuanLy** |
| `staff3` | `123456` | nhan vien 3 | **QuanLy** |

> Quản lý: sản phẩm, đơn hàng, loại SP, nhà SX, phiếu nhập (KHÔNG được quản lý thành viên & phân quyền).

### 👥 Tài khoản Người dùng (Khách hàng — `MaLoaiTV = 3`)

| Tài khoản | Mật khẩu | Họ tên |
|---|---|---|
| `asida118` | `123` | Le Gia Huy |
| `asida111` | `123` | ho thi nhu loan |
| `asida111123` | `123` | ad |

> Ngoài ra có thể **Đăng ký** tài khoản mới ngay trên trang chủ.

### 🆕 Đăng ký Admin mới
Truy cập `/ThongKe/DangkyAdmin` để tạo tài khoản Admin mới (mặc định `MaLoaiTV = 2`).

> ⚠️ **Lưu ý bảo mật**: Mật khẩu trong đồ án đang được lưu **plain text** (chưa hash). Nếu dùng cho môi trường thực tế cần bổ sung hash (SHA256/BCrypt).

---

## 🔗 Các link quan trọng

| Đường dẫn | Mô tả |
|---|---|
| `/` hoặc `/Home/Index` | Trang chủ — danh sách sản phẩm mới |
| `/SanPham/SanPham?MaLoaiSP=...&MaNSX=...` | Danh sách sản phẩm (lọc theo loại & NSX) |
| `/SanPham/XemChiTiet/{id}` | Xem chi tiết sản phẩm |
| `/TimKiem/KQTimKiem?sTuKhoa=...` | Tìm kiếm sản phẩm |
| `/GioHang/XemGioHang` | Xem giỏ hàng |
| `/GioHang/DatHang` | Đặt hàng (checkout) |
| `/Home/DangKy` | Đăng ký tài khoản mới |
| `/Home/DangNhap` | Đăng nhập người dùng |
| `/ThongKe` | **Admin Dashboard** (doanh thu, đơn hàng…) |
| `/ThongKe/DangkyAdmin` | Đăng ký tài khoản Admin |
| `/QuanLySanPham` | Quản lý sản phẩm (CRUD) |
| `/QuanLyDonHang` | Quản lý đơn hàng |
| `/QuanLyThanhVien` | Quản lý thành viên (**Admin**) |
| `/QuanLyLoai` | Quản lý loại sản phẩm |
| `/QuanLyNhaSX` | Quản lý nhà sản xuất |
| `/QuanLyPhieuNhap` | Quản lý phiếu nhập hàng |
| `/QuanLyQuyen` | Quản lý quyền (**Admin**) |
| `/PhanQuyen` | Phân quyền cho loại thành viên (**Admin**) |
| `/Home/LoiPhanQuyen` | Trang thông báo lỗi phân quyền |

---

## ✅ Danh sách chức năng

### 👤 Phía Khách hàng / Người dùng
- ✅ Xem danh sách sản phẩm theo loại, theo nhà sản xuất
- ✅ Xem chi tiết sản phẩm (URL thân thiện SEO: `/ten-san-pham-id`)
- ✅ Tìm kiếm sản phẩm theo tên (có phân trang)
- ✅ Đăng ký tài khoản (có Captcha + câu hỏi bảo mật)
- ✅ Đăng nhập / Đăng xuất (Forms Authentication)
- ✅ Thêm / Sửa / Xóa sản phẩm trong giỏ hàng (Session-based)
- ✅ Đặt hàng (checkout) — tạo KhachHang + DonDatHang + ChiTietDonDatHang
- ✅ Bình luận sản phẩm

### 🛠️ Phía Quản lý (QuanLy + QuanTriWeb)
- ✅ Quản lý sản phẩm: thêm, sửa, xóa, upload nhiều hình ảnh (tối đa 5 ảnh)
- ✅ Quản lý đơn hàng: duyệt đơn, đánh dấu đã thanh toán / đã giao
- ✅ Quản lý loại sản phẩm (CRUD)
- ✅ Quản lý nhà sản xuất (CRUD)
- ✅ Quản lý nhập hàng: tạo phiếu nhập, nhập nhiều sản phẩm, tự động cộng `SoLuongTon`
- ✅ Xem danh sách sản phẩm sắp hết hàng (`SoLuongTon <= 5`)
- ✅ Xem thống kê: tổng doanh thu, doanh thu theo tháng, số đơn hàng, số thành viên, khách trực tuyến

### 🔐 Phía Admin (QuanTriWeb)
- ✅ Tất cả chức năng của Quản lý
- ✅ Quản lý thành viên (CRUD)
- ✅ Quản lý quyền (CRUD)
- ✅ Phân quyền cho loại thành viên (mapping `LoaiThanhVien ↔ Quyen`)
- ✅ Đăng ký tài khoản Admin mới

---

## 🗺️ Danh sách Map (Route) của đồ án

### Routes đã khai báo trong `App_Start/RouteConfig.cs`

| Tên route | URL pattern | Controller / Action | Mô tả |
|---|---|---|---|
| `XemChiTiet` | `{tensp}-{id}` | `SanPham/XemChiTiet/{id}` | Trang chi tiết SP (SEO-friendly) |
| `Default` | `{controller}/{action}/{id}` | `Home/Index` | Route mặc định |

### Map URL → Controller/Action chính

| URL | Controller | Action | Quyền |
|---|---|---|---|
| `/` | `Home` | `Index` | Anonymous |
| `/Home/DangKy` | `Home` | `DangKy` | Anonymous |
| `/Home/DangNhap` (POST) | `Home` | `DangNhap` | Anonymous |
| `/Home/DangXuat` | `Home` | `DangXuat` | Anonymous |
| `/Home/LoiPhanQuyen` | `Home` | `LoiPhanquyen` | Anonymous |
| `/SanPham/XemChiTiet/{id}` | `SanPham` | `XemChiTiet` | Anonymous |
| `/SanPham/SanPham` | `SanPham` | `SanPham` | Anonymous |
| `/SanPham/LoaiSanPham` | `SanPham` | `LoaiSanPham` | Anonymous |
| `/TimKiem/KQTimKiem` | `TimKiem` | `KQTimKiem` | Anonymous |
| `/GioHang/XemGioHang` | `GioHang` | `XemGioHang` | Anonymous |
| `/GioHang/ThemGioHang/{MaSP}` | `GioHang` | `ThemGioHang` | Anonymous |
| `/GioHang/SuaGioHang/{MaSP}` | `GioHang` | `SuaGioHang` | Anonymous |
| `/GioHang/XoaGioHang/{MaSP}` | `GioHang` | `XoaGioHang` | Anonymous |
| `/GioHang/DatHang` | `GioHang` | `DatHang` | Anonymous |
| `/ThongKe` | `ThongKe` | `Index` | QuanTriWeb |
| `/ThongKe/DangkyAdmin` | `ThongKe` | `DangkyAdmin` | AllowAnonymous (nhưng set `MaLoaiTV=2`) |
| `/ThongKe/DangNhapAdmin` (POST) | `ThongKe` | `DangNhapAdmin` | AllowAnonymous |
| `/ThongKe/DangXuatAdmin` | `ThongKe` | `DangXuatAdmin` | QuanTriWeb |
| `/QuanLySanPham` | `QuanLySanPham` | `Index` | QuanLy, QuanTriWeb |
| `/QuanLySanPham/TaoMoi` | `QuanLySanPham` | `TaoMoi` | QuanLy, QuanTriWeb |
| `/QuanLySanPham/ChinhSua/{id}` | `QuanLySanPham` | `ChinhSua` | QuanLy, QuanTriWeb |
| `/QuanLySanPham/Xoa/{id}` | `QuanLySanPham` | `Xoa` | QuanLy, QuanTriWeb |
| `/QuanLySanPham/UploadHinh/{id}` | `QuanLySanPham` | `UploadHinh` | QuanLy, QuanTriWeb |
| `/QuanLyDonHang/ChuaThanhToan` | `QuanLyDonHang` | `ChuaThanhToan` | QuanLy, QuanTriWeb |
| `/QuanLyDonHang/ChuaGiao` | `QuanLyDonHang` | `ChuaGiao` | QuanLy, QuanTriWeb |
| `/QuanLyDonHang/DaGiaoDaThanhToan` | `QuanLyDonHang` | `DaGiaoDaThanhToan` | QuanLy, QuanTriWeb |
| `/QuanLyDonHang/DuyetDonHang/{id}` | `QuanLyDonHang` | `DuyetDonHang` | QuanLy, QuanTriWeb |
| `/QuanLyThanhVien` | `QuanLyThanhVien` | `Index` | QuanTriWeb |
| `/QuanLyThanhVien/TaoMoi` | `QuanLyThanhVien` | `TaoMoi` | QuanTriWeb |
| `/QuanLyThanhVien/ChinhSua/{id}` | `QuanLyThanhVien` | `ChinhSua` | QuanTriWeb |
| `/QuanLyThanhVien/Xoa/{id}` | `QuanLyThanhVien` | `Xoa` | QuanTriWeb |
| `/QuanLyLoai` | `QuanLyLoai` | `Index` | QuanLy, QuanTriWeb |
| `/QuanLyLoai/TaoMoi` | `QuanLyLoai` | `TaoMoi` | QuanLy, QuanTriWeb |
| `/QuanLyLoai/ChinhSua/{id}` | `QuanLyLoai` | `ChinhSua` | QuanLy, QuanTriWeb |
| `/QuanLyLoai/Xoa/{id}` | `QuanLyLoai` | `Xoa` | QuanLy, QuanTriWeb |
| `/QuanLyNhaSX` | `QuanLyNhaSX` | `Index` | QuanLy, QuanTriWeb |
| `/QuanLyNhaSX/TaoMoi` | `QuanLyNhaSX` | `TaoMoi` | QuanLy, QuanTriWeb |
| `/QuanLyNhaSX/ChinhSua/{id}` | `QuanLyNhaSX` | `ChinhSua` | QuanLy, QuanTriWeb |
| `/QuanLyNhaSX/Xoa/{id}` | `QuanLyNhaSX` | `Xoa` | QuanLy, QuanTriWeb |
| `/QuanLyPhieuNhap` | `QuanLyPhieuNhap` | `NhapHang` | QuanLy, QuanTriWeb |
| `/QuanLyPhieuNhap/NhapHangDon/{id}` | `QuanLyPhieuNhap` | `NhapHangDon` | QuanLy, QuanTriWeb |
| `/QuanLyPhieuNhap/DSSPHetHang` | `QuanLyPhieuNhap` | `DSSPHetHang` | QuanLy, QuanTriWeb |
| `/QuanLyQuyen` | `QuanLyQuyen` | `Index` | QuanTriWeb |
| `/QuanLyQuyen/TaoMoi` | `QuanLyQuyen` | `TaoMoi` | QuanTriWeb |
| `/QuanLyQuyen/ChinhSua/{id}` | `QuanLyQuyen` | `ChinhSua` | QuanTriWeb |
| `/QuanLyQuyen/Xoa/{id}` | `QuanLyQuyen` | `Xoa` | QuanTriWeb |
| `/PhanQuyen` | `PhanQuyen` | `Index` | QuanTriWeb |
| `/PhanQuyen/PhanQuyen/{id}` | `PhanQuyen` | `PhanQuyen` | QuanTriWeb |

---

## ⚠️ Lỗi thường gặp & Cách khắc phục

### 1. ❌ Lỗi kết nối: `Cannot open database "QuanLyBanHang" requested by the login`
**Nguyên nhân**: Chưa chạy script tạo database, hoặc tên DB / server sai.

**Cách khắc phục**:
- Mở SSMS, kiểm tra database `QuanLyBanHang` đã tồn tại chưa.
- Nếu chưa, mở file `scriptgiay.sql` → nhấn **F5** để chạy.
- Kiểm tra `data source` trong `Web.config` khớp với SQL Server của bạn (mặc định `.\SQLEXPRESS`).

### 2. ❌ Lỗi: `A network-related or instance-specific error occurred while establishing a connection to SQL Server`
**Nguyên nhân**: SQL Server service chưa chạy hoặc TCP/IP chưa bật.

**Cách khắc phục**:
- Mở **Services** (`services.msc`) → tìm `SQL Server (SQLEXPRESS)` → **Start**.
- Mở **SQL Server Configuration Manager** → **SQL Server Network Configuration** → **Protocols for SQLEXPRESS** → bật **TCP/IP** → Restart SQL Server.

### 3. ❌ Lỗi: `The entity type <Tên> is not part of the model for the current context`
**Nguyên nhân**: Model EDMX bị lỗi tham chiếu sau khi thay đổi DB.

**Cách khắc phục**:
- Mở file `Models/QuanLyBanHangModel.edmx` → chuột phải → **Update Model from Database**.
- Hoặc build lại project: **Build → Rebuild Solution**.

### 4. ❌ Lỗi 500.19 khi chạy trên IIS Express
**Nguyên nhân**: Sai phiên bản .NET Framework hoặc thiếu application pool.

**Cách khắc phục**:
- Đảm bảo đã cài **.NET Framework 4.7.2** Developer Pack.
- Trong `Web.config`, kiểm tra `<httpRuntime targetFramework="4.7.2" />`.
- Đổi sang **IIS Express** thay vì Local IIS: chuột phải project → **Properties → Web → Use IIS Express**.

### 5. ❌ Không upload được hình ảnh sản phẩm
**Nguyên nhân**: Thiếu thư mục `Content/HinhAnhSP/` hoặc thiếu quyền ghi.

**Cách khắc phục**:
- Tạo thư mục `WebsiteBanHang/Content/HinhAnhSP/` (nếu chưa có).
- Chuột phải thư mục → **Properties → Security** → đảm bảo user `IIS_IUSRS` và `IUSR` có quyền **Modify**.
- Trong IIS Express, đảm bảo đã bật `requestLimits maxAllowedContentLength` (đã có sẵn trong `Web.config`).

### 6. ❌ Lỗi: `Login failed for user 'IIS APPPOOL\...'`
**Nguyên nhân**: IIS AppPool không có quyền truy cập SQL Server.

**Cách khắc phục**:
- Đổi sang **IIS Express** (đơn giản nhất).
- Hoặc trong IIS → **Application Pools** → chọn pool đang dùng → **Advanced Settings** → **Identity** → đổi sang `NetworkService` hoặc `LocalSystem`.

### 7. ❌ Session timeout quá nhanh / bị đăng xuất liên tục
**Nguyên nhân**: `<sessionState timeout>` và `<forms timeout>` quá thấp.

**Cách khắc phục**: Mở `Web.config`, sửa:
```xml
<sessionState timeout="60"></sessionState>   <!-- phút -->
<forms loginUrl="~/Home/LoiPhanQuyen" timeout="2880"></forms>   <!-- phút, mặc định 2880 = 2 ngày -->
```

### 8. ❌ Lỗi: `The model backing the <Context> context has changed since the database was created`
**Nguyên nhân**: Schema DB khác với EDMX.

**Cách khắc phục**:
- Nếu DB do bạn sửa thủ công → cập nhật EDMX.
- Nếu muốn EF tự động tạo lại DB khi model đổi, thêm vào `Global.asax.cs` (Application_Start):
```csharp
Database.SetInitializer(new DropCreateDatabaseIfModelChanges<QuanLyBanHangEntities>());
```
> ⚠️ Lệnh này sẽ **xóa toàn bộ dữ liệu**, chỉ dùng cho dev.

### 9. ❌ Captcha không hiển thị / luôn báo sai
**Nguyên nhân**: Mất session hoặc Session quá timeout.

**Cách khắc phục**:
- Tăng `sessionState timeout` trong `Web.config`.
- Tắt các extension chặn cookie của Chrome (ví dụ `SameSite` mặc định).

### 10. ❌ Không xóa được sản phẩm / nhà sản xuất / loại sản phẩm
**Nguyên nhân**: Đang có ràng buộc khóa ngoại (sản phẩm đã phát sinh đơn hàng, phiếu nhập…).

**Cách khắc phục**:
- Hệ thống sẽ chuyển sang trang `/QuanLySanPham/KhongTheXoa`. Bạn cần **xóa dữ liệu liên quan** (đơn hàng, bình luận, phiếu nhập) trước, hoặc dùng thao tác **mềm** (set `DaXoa = true`).

### 11. ❌ Lỗi thiếu NuGet package khi build
**Cách khắc phục**:
- Mở **Tools → NuGet Package Manager → Package Manager Console** → gõ:
```
Update-Package -reinstall
```
- Ho��c click phải Solution → **Restore NuGet Packages**.

### 12. ❌ Lỗi: `Could not load file or assembly 'EntityFramework'`
**Cách khắc phục**:
- Mở `packages.config` đảm bảo có `<package id="EntityFramework" version="6.x.x" />`.
- Build lại project: **Build → Rebuild Solution**.

### 13. ❌ Mất định dạng CSS / giao diện lộn xộn
**Cách khắc phục**:
- Mở `App_Start/BundleConfig.cs` kiểm tra bundle CSS đang hoạt động.
- Trong Layout, kiểm tra `@Styles.Render("~/Content/css")` đã gọi đúng bundle.
- Xóa cache trình duyệt (`Ctrl + Shift + Delete`) hoặc nhấn `Ctrl + F5` (hard reload).

### 14. ❌ Truy cập `/QuanLyThanhVien` bị redirect về trang lỗi phân quyền
**Nguyên nhân**: Đăng nhập bằng tài khoản `staff1/2/3` (role `QuanLy`) — không có quyền `QuanTriWeb`.

**Cách khắc phục**:
- Đăng nhập bằng `admin / 123456` để có quyền `QuanTriWeb`.
- Hoặc vào `/PhanQuyen` để gán quyền cho loại thành viên `MaLoaiTV = 2`.

### 15. ❌ Lỗi font tiếng Việt trong Database
**Cách khắc phục**:
- Khi tạo DB, đảm bảo collation là `Vietnamese_CI_AS` hoặc `SQL_Latin1_General_CP1_CI_AS`.
- Các trường `nvarchar` đã set sẵn trong script nên hỗ trợ Unicode đầy đủ.

---

## 📝 Ghi chú

- Đồ án này được xây dựng cho **mục đích học tập**.
- Mật khẩu đang lưu **plain text** — KHÔNG dùng cho production.
- Phân quyền dựa trên **Forms Authentication** + **Role string**, không phải ASP.NET Identity.
- Một số `[ValidateInput(false)]` trong quản lý sản phẩm cho phép nhập HTML, cần lọc kỹ nếu dùng thực tế.

---

## 👨‍💻 Tác giả
Đồ án môn học — Website Bán Giày Dép — ASP.NET MVC 5