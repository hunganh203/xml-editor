# Cấu trúc dự án đặt lịch cắt tóc với Next.js và React.js

## Cấu trúc thư mục

```
hair-salon-booking/
├── .github/                   # GitHub workflows
├── .next/                     # Next.js build output (generated)
├── components/                # Các components React tái sử dụng
│   ├── common/                # Components dùng chung
│   │   ├── Button.jsx
│   │   ├── Input.jsx
│   │   ├── Modal.jsx
│   │   └── ...
│   ├── layout/                # Components liên quan đến layout
│   │   ├── Footer.jsx
│   │   ├── Header.jsx
│   │   ├── Sidebar.jsx
│   │   └── ...
│   ├── ui/                    # UI components
│   │   ├── Calendar.jsx
│   │   ├── ServiceCard.jsx
│   │   ├── StaffCard.jsx
│   │   └── ...
│   ├── forms/                 # Form components
│   │   ├── BookingForm.jsx
│   │   ├── LoginForm.jsx
│   │   ├── RegisterForm.jsx
│   │   └── ...
│   └── pages/                 # Page-specific components
│       ├── home/
│       ├── booking/
│       ├── admin/
│       └── ...
├── config/                    # Các file cấu hình
│   ├── routes.js              # Cấu hình routes
│   └── constants.js           # Các hằng số
├── context/                   # React Context
│   ├── AuthContext.jsx
│   ├── BookingContext.jsx
│   └── ...
├── hooks/                     # Custom React hooks
│   ├── useAuth.js
│   ├── useBooking.js
│   └── ...
├── lib/                       # Thư viện và utilities
│   ├── api.js                 # API client
│   ├── firebase.js            # Firebase config
│   ├── helpers.js             # Helper functions
│   └── ...
├── models/                    # Định nghĩa models
│   ├── User.js
│   ├── Service.js
│   ├── Appointment.js
│   └── ...
├── pages/                     # Pages của Next.js
│   ├── _app.js
│   ├── _document.js
│   ├── index.js               # Trang chủ
│   ├── booking/               # Trang đặt lịch
│   │   ├── index.js
│   │   ├── [id].js
│   │   └── confirmation.js
│   ├── services/              # Trang dịch vụ
│   │   ├── index.js
│   │   └── [id].js
│   ├── profile/               # Trang hồ sơ người dùng
│   │   ├── index.js
│   │   └── appointments.js
│   ├── login.js               # Trang đăng nhập
│   ├── register.js            # Trang đăng ký
│   ├── admin/                 # Trang quản trị
│   │   ├── index.js
│   │   ├── appointments/
│   │   ├── services/
│   │   ├── staff/
│   │   └── settings/
│   └── api/                   # API routes
│       ├── auth/
│       ├── appointments/
│       ├── services/
│       ├── users/
│       └── ...
├── public/                    # Tài nguyên tĩnh
│   ├── favicon.ico
│   ├── logo.svg
│   └── images/
├── styles/                    # Styles CSS/SCSS
│   ├── globals.css
│   └── ...
├── utils/                     # Các hàm utility
│   ├── auth.js
│   ├── date.js
│   ├── validation.js
│   └── ...
├── .env.local                 # Environment variables
├── .gitignore
├── jest.config.js             # Cấu hình Jest cho testing
├── next.config.js             # Cấu hình Next.js
├── package.json
├── README.md
└── tailwind.config.js         # Cấu hình Tailwind CSS (nếu sử dụng)
```

## Mô tả chi tiết

### 1. Components

Folder này chứa tất cả các React components có thể tái sử dụng trong ứng dụng. Được tổ chức thành các nhóm:

- **common**: Các components cơ bản như Button, Input, Modal được sử dụng rộng rãi trong ứng dụng.
- **layout**: Components liên quan đến layout như Header, Footer, Sidebar.
- **ui**: Các UI components phức tạp hơn như Calendar, ServiceCard.
- **forms**: Components liên quan đến forms như BookingForm, LoginForm.
- **pages**: Components cụ thể cho từng trang.

### 2. Config

Chứa các file cấu hình và constants:

- **routes.js**: Định nghĩa các routes trong ứng dụng.
- **constants.js**: Các hằng số được sử dụng trong ứng dụng.

### 3. Context

Chứa các React Context cho state management:

- **AuthContext.jsx**: Quản lý trạng thái đăng nhập/đăng xuất.
- **BookingContext.jsx**: Quản lý trạng thái đặt lịch.

### 4. Hooks

Chứa các custom React hooks:

- **useAuth.js**: Hook xử lý xác thực người dùng.
- **useBooking.js**: Hook xử lý logic đặt lịch.

### 5. Lib

Chứa các thư viện và utilities:

- **api.js**: Client gọi API.
- **firebase.js**: Cấu hình Firebase (nếu sử dụng).
- **helpers.js**: Các hàm helper.

### 6. Models

Chứa các định nghĩa models:

- **User.js**: Model cho người dùng.
- **Service.js**: Model cho dịch vụ.
- **Appointment.js**: Model cho cuộc hẹn.

### 7. Pages

Chứa các trang của Next.js:

- **index.js**: Trang chủ.
- **booking/**: Các trang liên quan đến đặt lịch.
- **services/**: Các trang hiển thị dịch vụ.
- **profile/**: Các trang liên quan đến hồ sơ người dùng.
- **admin/**: Các trang quản trị.
- **api/**: API routes của Next.js.

### 8. Public

Chứa các tài nguyên tĩnh như hình ảnh, favicon, etc.

### 9. Styles

Chứa các file CSS/SCSS:

- **globals.css**: CSS toàn cục.

### 10. Utils

Chứa các hàm utility:

- **auth.js**: Các hàm liên quan đến xác thực.
- **date.js**: Các hàm xử lý ngày tháng.
- **validation.js**: Các hàm xác thực form.

## Công nghệ đề xuất

### Frontend
- **React.js**: Thư viện UI
- **Next.js**: Framework React
- **Tailwind CSS**: Styling
- **React Hook Form**: Form handling
- **SWR/React Query**: Data fetching và caching
- **Zustand/Redux Toolkit**: State management (nếu cần)
- **date-fns**: Xử lý ngày tháng
- **react-day-picker**: Calendar UI
- **react-toastify**: Thông báo

### Backend (Next.js API Routes)
- **Prisma/Mongoose**: ORM/ODM
- **NextAuth.js**: Xác thực
- **jsonwebtoken**: JWT
- **bcrypt**: Mã hóa mật khẩu
- **nodemailer/SendGrid**: Gửi email
- **Twilio**: Gửi SMS

### Database
- **MongoDB/PostgreSQL**: Cơ sở dữ liệu
- **Supabase/Firebase**: Backend as a Service (tùy chọn)

### Deployment
- **Vercel**: Hosting
- **GitHub Actions**: CI/CD
- **Sentry**: Error tracking
