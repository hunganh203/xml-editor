# Software Requirements Specification (SRS)
# Hệ Thống Đặt Lịch Cắt Tóc

## 1. Giới thiệu

### 1.1 Mục đích
Tài liệu này mô tả các yêu cầu chức năng và phi chức năng cho hệ thống đặt lịch cắt tóc trực tuyến được phát triển bằng Next.js và React.js. Hệ thống này giúp khách hàng đặt lịch cắt tóc với salon và giúp salon quản lý các cuộc hẹn.

### 1.2 Phạm vi
Hệ thống bao gồm các chức năng đặt lịch, quản lý lịch hẹn, quản lý nhân viên, quản lý dịch vụ và thông báo cho khách hàng. Hệ thống cũng cung cấp giao diện quản trị cho salon và giao diện đặt lịch cho khách hàng.

### 1.3 Định nghĩa và từ viết tắt
- **SRS**: Software Requirements Specification (Đặc tả yêu cầu phần mềm)
- **UI**: User Interface (Giao diện người dùng)
- **API**: Application Programming Interface (Giao diện lập trình ứng dụng)
- **CRUD**: Create, Read, Update, Delete (Tạo, Đọc, Cập nhật, Xóa)

### 1.4 Tổng quan
Phần còn lại của tài liệu này mô tả chi tiết các chức năng, yêu cầu phi chức năng, giao diện người dùng và các yêu cầu kỹ thuật khác của hệ thống. Tài liệu cũng bao gồm các yêu cầu về bảo mật, hiệu suất và khả năng mở rộng.

## 2. Mô tả tổng quan

### 2.1 Viễn cảnh của sản phẩm
Hệ thống đặt lịch cắt tóc trực tuyến nhằm mục đích mang lại sự tiện lợi cho khách hàng trong việc đặt lịch hẹn với salon mà không cần gọi điện hoặc đến trực tiếp. Salon có thể quản lý lịch hẹn, nhân viên và dịch vụ một cách hiệu quả.

### 2.2 Chức năng của sản phẩm
Hệ thống có các chức năng chính sau:
- Đăng ký và đăng nhập cho khách hàng và nhân viên salon
- Quản lý thông tin cá nhân của khách hàng và nhân viên
- Đặt lịch, hủy lịch, và theo dõi lịch hẹn
- Quản lý dịch vụ và giá cả
- Quản lý thời gian làm việc của nhân viên
- Hệ thống thông báo (email, SMS)
- Đánh giá và phản hồi sau khi sử dụng dịch vụ

### 2.3 Đối tượng người dùng
- **Khách hàng**: Người sử dụng dịch vụ cắt tóc, có thể đặt lịch và quản lý lịch hẹn của họ
- **Nhân viên salon**: Thợ cắt tóc, có thể xem lịch làm việc và các cuộc hẹn được giao
- **Quản lý salon**: Người quản lý salon, có thể quản lý nhân viên, dịch vụ và xem báo cáo
- **Quản trị viên hệ thống**: Người quản lý toàn bộ hệ thống, có toàn quyền truy cập

### 2.4 Các ràng buộc
- Hệ thống phải hoạt động trên các trình duyệt web phổ biến
- Hệ thống phải có giao diện thân thiện với người dùng và đáp ứng (responsive)
- Hệ thống phải đảm bảo tính bảo mật cho thông tin người dùng
- Hệ thống phải xử lý được nhiều cuộc hẹn cùng lúc

### 2.5 Giả định và phụ thuộc
- Người dùng có kết nối internet ổn định
- Salon có thể cung cấp thông tin chính xác về dịch vụ và thời gian làm việc
- Hệ thống có thể tích hợp với các dịch vụ email và SMS để gửi thông báo

## 3. Yêu cầu chức năng

### 3.1 Quản lý người dùng

#### 3.1.1 Đăng ký tài khoản
- Hệ thống phải cho phép khách hàng đăng ký tài khoản với thông tin: tên, email, số điện thoại, mật khẩu
- Hệ thống phải xác thực email hoặc số điện thoại của khách hàng
- Hệ thống phải cho phép đăng ký bằng tài khoản Google, Facebook

#### 3.1.2 Đăng nhập
- Hệ thống phải cho phép đăng nhập bằng email/số điện thoại và mật khẩu
- Hệ thống phải cho phép đăng nhập bằng tài khoản Google, Facebook
- Hệ thống phải có chức năng khôi phục mật khẩu

#### 3.1.3 Quản lý thông tin cá nhân
- Người dùng có thể xem và cập nhật thông tin cá nhân
- Khách hàng có thể xem lịch sử đặt lịch
- Người dùng có thể thay đổi mật khẩu

### 3.2 Quản lý đặt lịch

#### 3.2.1 Đặt lịch
- Khách hàng có thể xem danh sách dịch vụ và giá cả
- Khách hàng có thể chọn dịch vụ, ngày, giờ và nhân viên mong muốn
- Hệ thống phải kiểm tra và hiển thị thời gian còn trống
- Khách hàng có thể xác nhận đặt lịch và nhận thông báo xác nhận

#### 3.2.2 Quản lý lịch hẹn
- Khách hàng có thể xem, hủy hoặc đổi lịch hẹn
- Nhân viên salon có thể xem lịch làm việc của mình
- Quản lý salon có thể xem tất cả các cuộc hẹn
- Hệ thống phải gửi thông báo nhắc nhở trước cuộc hẹn

#### 3.2.3 Xác nhận và hủy lịch
- Salon có thể xác nhận hoặc từ chối yêu cầu đặt lịch
- Hệ thống phải thông báo cho khách hàng khi lịch hẹn được xác nhận hoặc từ chối
- Hệ thống phải cập nhật trạng thái lịch hẹn khi có thay đổi

### 3.3 Quản lý dịch vụ

#### 3.3.1 CRUD dịch vụ
- Quản lý salon có thể thêm, sửa, xóa, xem dịch vụ
- Mỗi dịch vụ bao gồm: tên, mô tả, giá, thời gian thực hiện, hình ảnh

#### 3.3.2 Phân loại dịch vụ
- Quản lý salon có thể tạo và quản lý các danh mục dịch vụ
- Dịch vụ có thể được gắn với một hoặc nhiều danh mục

### 3.4 Quản lý nhân viên

#### 3.4.1 Thêm và quản lý nhân viên
- Quản lý salon có thể thêm, sửa, xóa thông tin nhân viên
- Thông tin nhân viên bao gồm: tên, số điện thoại, email, chuyên môn, hình ảnh

#### 3.4.2 Lịch làm việc của nhân viên
- Quản lý salon có thể thiết lập thời gian làm việc cho từng nhân viên
- Nhân viên có thể xem và yêu cầu thay đổi lịch làm việc của mình

### 3.5 Thống kê và báo cáo

#### 3.5.1 Báo cáo doanh thu
- Hệ thống phải tạo báo cáo doanh thu theo ngày, tuần, tháng, năm
- Báo cáo doanh thu theo từng dịch vụ, nhân viên

#### 3.5.2 Thống kê lịch hẹn
- Hệ thống phải thống kê số lượng lịch hẹn theo trạng thái (đã đặt, đã xác nhận, đã hoàn thành, đã hủy)
- Hệ thống phải thống kê tỷ lệ đặt lịch thành công và thất bại

### 3.6 Hệ thống thông báo

#### 3.6.1 Thông báo qua email
- Hệ thống phải gửi email xác nhận khi khách hàng đặt lịch, hủy lịch, hoặc thay đổi lịch
- Hệ thống phải gửi email nhắc nhở trước cuộc hẹn

#### 3.6.2 Thông báo qua SMS
- Hệ thống có thể gửi SMS xác nhận và nhắc nhở cho khách hàng (tùy chọn)

#### 3.6.3 Thông báo trong hệ thống
- Hệ thống phải hiển thị thông báo trong ứng dụng cho người dùng

### 3.7 Đánh giá và phản hồi

#### 3.7.1 Đánh giá dịch vụ
- Khách hàng có thể đánh giá và viết nhận xét sau khi sử dụng dịch vụ
- Đánh giá bao gồm số sao (1-5) và nhận xét văn bản

#### 3.7.2 Quản lý đánh giá
- Quản lý salon có thể xem và phản hồi đánh giá của khách hàng

## 4. Yêu cầu phi chức năng

### 4.1 Hiệu suất
- Trang web phải tải trong vòng 3 giây
- Hệ thống phải xử lý được ít nhất 100 người dùng đồng thời
- Thời gian phản hồi API không quá 1 giây

### 4.2 Bảo mật
- Mật khẩu người dùng phải được mã hóa
- Dữ liệu người dùng phải được bảo vệ theo quy định của GDPR
- Hệ thống phải có bảo vệ chống tấn công XSS, CSRF, và SQL Injection
- API phải được bảo vệ bằng token xác thực

### 4.3 Khả năng sử dụng
- Giao diện người dùng phải trực quan và dễ sử dụng
- Giao diện phải đáp ứng (responsive) trên các thiết bị (máy tính, máy tính bảng, điện thoại)
- Hệ thống phải hỗ trợ ít nhất hai ngôn ngữ: Tiếng Việt và Tiếng Anh

### 4.4 Khả năng mở rộng
- Hệ thống phải dễ dàng mở rộng để thêm tính năng mới
- Kiến trúc phải cho phép tích hợp với các dịch vụ bên thứ ba

### 4.5 Độ tin cậy
- Hệ thống phải có tính khả dụng cao (uptime > 99%)
- Hệ thống phải có cơ chế sao lưu dữ liệu định kỳ
- Hệ thống phải có khả năng phục hồi sau sự cố

## 5. Thiết kế giao diện người dùng

### 5.1 Giao diện khách hàng

#### 5.1.1 Trang chủ
- Hiển thị thông tin giới thiệu salon
- Hiển thị dịch vụ nổi bật
- Hiển thị nút đặt lịch nhanh

#### 5.1.2 Trang đặt lịch
- Hiển thị các bước đặt lịch rõ ràng
- Cho phép chọn dịch vụ, ngày, giờ, và nhân viên
- Hiển thị tổng chi phí và thời gian dự kiến

#### 5.1.3 Trang tài khoản khách hàng
- Hiển thị thông tin cá nhân
- Hiển thị lịch sử đặt lịch
- Cho phép quản lý lịch hẹn

### 5.2 Giao diện quản lý salon

#### 5.2.1 Dashboard
- Hiển thị tổng quan về lịch hẹn trong ngày
- Hiển thị thống kê doanh thu
- Hiển thị các thông báo quan trọng

#### 5.2.2 Quản lý lịch hẹn
- Hiển thị lịch hẹn dưới dạng lịch hoặc danh sách
- Cho phép tìm kiếm, lọc và sắp xếp lịch hẹn
- Cho phép cập nhật trạng thái lịch hẹn

#### 5.2.3 Quản lý dịch vụ và nhân viên
- Giao diện CRUD dịch vụ
- Giao diện quản lý nhân viên
- Giao diện thiết lập lịch làm việc

## 6. Yêu cầu kỹ thuật

### 6.1 Công nghệ Frontend
- React.js 18.0 trở lên
- Next.js 13.0 trở lên
- HTML5, CSS3, JavaScript ES6+
- Thư viện UI: Material-UI hoặc Tailwind CSS
- State management: Redux Toolkit hoặc React Context API
- Form validation: React Hook Form hoặc Formik

### 6.2 Công nghệ Backend
- Node.js với Next.js API Routes
- Cơ sở dữ liệu: MongoDB hoặc PostgreSQL
- Authentication: NextAuth.js
- Upload file: Cloudinary hoặc AWS S3
- Email service: SendGrid hoặc Nodemailer
- SMS service: Twilio hoặc Nexmo

### 6.3 Kiến trúc
- Mô hình kiến trúc: Client-Server
- RESTful API hoặc GraphQL
- Serverless functions cho API endpoints

### 6.4 Môi trường triển khai
- Hosting: Vercel hoặc Netlify
- CI/CD: GitHub Actions
- Container: Docker (tùy chọn)
- Monitoring: Sentry hoặc LogRocket

## 7. Kế hoạch phát triển

### 7.1 Giai đoạn 1 - MVP
- Đăng ký, đăng nhập người dùng
- Chức năng đặt lịch cơ bản
- Quản lý dịch vụ và nhân viên cơ bản
- Thông báo qua email

### 7.2 Giai đoạn 2
- Thống kê và báo cáo
- Thông báo qua SMS
- Đánh giá và phản hồi
- Tối ưu hóa hiệu suất

### 7.3 Giai đoạn 3
- Tích hợp thanh toán trực tuyến
- Tích hợp mạng xã hội
- Ứng dụng di động (React Native)
- Tính năng marketing và khuyến mãi

## 8. Các yêu cầu bổ sung

### 8.1 Tích hợp thanh toán
- Hỗ trợ thanh toán trước hoặc đặt cọc qua thẻ tín dụng
- Tích hợp với các cổng thanh toán phổ biến (VNPay, MoMo, PayPal)

### 8.2 Tích hợp mạng xã hội
- Chia sẻ dịch vụ lên mạng xã hội
- Đăng nhập bằng tài khoản mạng xã hội

### 8.3 Quản lý kho hàng
- Quản lý sản phẩm và tồn kho
- Thông báo khi sản phẩm sắp hết

## 9. Phụ lục

### 9.1 Thuật ngữ
- **Cuộc hẹn (Appointment)**: Một lịch hẹn cụ thể giữa khách hàng và nhân viên salon
- **Dịch vụ (Service)**: Các dịch vụ mà salon cung cấp như cắt tóc, nhuộm tóc, làm móng, v.v.

### 9.2 Tài liệu tham khảo
- Tài liệu kỹ thuật Next.js: https://nextjs.org/docs
- Tài liệu kỹ thuật React.js: https://reactjs.org/docs

### 9.3 Luồng người dùng (User Flow)
- Luồng đặt lịch: Chọn dịch vụ -> Chọn nhân viên -> Chọn ngày giờ -> Xác nhận -> Nhận thông báo
- Luồng quản lý salon: Đăng nhập -> Xem lịch hẹn -> Xác nhận/Từ chối -> Thực hiện dịch vụ -> Hoàn thành
