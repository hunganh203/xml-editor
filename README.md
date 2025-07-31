# Hệ Thống Đặt Lịch Cắt Tóc (Hair Salon Booking System)

Một ứng dụng web hiện đại cho phép khách hàng đặt lịch cắt tóc trực tuyến và giúp salon quản lý các cuộc hẹn một cách hiệu quả.

## 🚀 Tính năng chính

- **Đặt lịch trực tuyến**: Khách hàng có thể dễ dàng đặt lịch cắt tóc qua web
- **Quản lý lịch hẹn**: Xem, sửa đổi và hủy các lịch hẹn
- **Quản lý nhân viên**: Theo dõi và phân công nhân viên
- **Quản lý dịch vụ**: Cập nhật và quản lý các dịch vụ salon
- **Hệ thống thông báo**: Nhắc nhở và xác nhận lịch hẹn
- **Giao diện quản trị**: Dashboard cho salon quản lý toàn bộ hệ thống

## 🛠️ Công nghệ sử dụng

- **Frontend**: Next.js, React.js
- **Styling**: CSS Modules / Tailwind CSS (tùy theo cấu hình)
- **Database**: [Cần xác định dựa trên Database_Design.md]
- **Authentication**: JWT / NextAuth.js
- **Deployment**: Vercel / Netlify

## 📋 Yêu cầu hệ thống

- Node.js 16.0 hoặc cao hơn
- npm hoặc yarn
- Database (MySQL/PostgreSQL/MongoDB)

## 🔧 Cài đặt và chạy dự án

### 1. Clone repository

```bash
git clone [repository-url]
cd xml-editor
```

### 2. Cài đặt dependencies

```bash
npm install
# hoặc
yarn install
```

### 3. Cấu hình môi trường

Tạo file `.env.local` và thêm các biến môi trường cần thiết:

```env
DATABASE_URL=your_database_url
NEXTAUTH_SECRET=your_secret_key
NEXTAUTH_URL=http://localhost:3000
```

### 4. Chạy ứng dụng

```bash
npm run dev
# hoặc
yarn dev
```

Truy cập `http://localhost:3000` để xem ứng dụng.

## 📚 Tài liệu

- [Software Requirements Specification](./SRS_Hair_Salon_Appointment_System.md)
- [Cấu trúc dự án](./Project_Structure.md)
- [Tài liệu API](./API_Documentation.md)
- [Thiết kế Database](./Database_Design.md)

## 🔐 Các vai trò người dùng

### Khách hàng

- Đăng ký/Đăng nhập tài khoản
- Đặt lịch cắt tóc
- Xem lịch sử đặt lịch
- Hủy/Sửa đổi lịch hẹn
- Đánh giá dịch vụ

### Nhân viên Salon

- Xem lịch làm việc cá nhân
- Cập nhật trạng thái cuộc hẹn
- Quản lý thông tin cá nhân

### Quản trị viên

- Quản lý toàn bộ hệ thống
- Quản lý nhân viên
- Quản lý dịch vụ và giá cả
- Xem báo cáo thống kê
- Cấu hình hệ thống

## 🚀 Deployment

### Vercel (Khuyến nghị)

1. Push code lên GitHub
2. Kết nối repository với Vercel
3. Cấu hình biến môi trường trên Vercel
4. Deploy tự động

### Manual Deployment

```bash
npm run build
npm start
```

## 🤝 Đóng góp

1. Fork dự án
2. Tạo branch mới (`git checkout -b feature/amazing-feature`)
3. Commit thay đổi (`git commit -m 'Add some amazing feature'`)
4. Push lên branch (`git push origin feature/amazing-feature`)
5. Tạo Pull Request

## 📄 License

Dự án này được phân phối dưới giấy phép [MIT License](LICENSE).

## 📞 Liên hệ

- **Email**: [your-email@example.com]
- **GitHub**: [your-github-username]
- **Website**: [your-website.com]

## 🙏 Acknowledgments

- Cảm ơn tất cả những người đã đóng góp cho dự án này
- Sử dụng các thư viện mã nguồn mở tuyệt vời từ cộng đồng React/Next.js
