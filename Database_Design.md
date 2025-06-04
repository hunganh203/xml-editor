# Thiết Kế Cơ Sở Dữ Liệu - Hệ Thống Đặt Lịch Cắt Tóc

## 1. Mô hình Entity Relationship Diagram (ERD)

```
+---------------+       +---------------+       +---------------+
|    User       |       | Appointment   |       |    Service    |
+---------------+       +---------------+       +---------------+
| id            |       | id            |       | id            |
| email         |       | userId        |------>| name          |
| password      |       | staffId       |------>| description   |
| name          |       | serviceId     |------>| price         |
| phone         |       | date          |       | duration      |
| role          |       | startTime     |       | image         |
| avatar        |       | endTime       |       | categoryId    |------>
| createdAt     |       | status        |       | createdAt     |
| updatedAt     |<------| notes         |       | updatedAt     |
+------^--------+       | totalPrice    |       +---------------+
       |                | createdAt     |
       |                | updatedAt     |
       |                +---------------+
       |
       |                +---------------+       +---------------+
       |                |    Staff      |       |   Category    |
       |                +---------------+       +---------------+
       +----------------| id            |       | id            |
                        | userId        |       | name          |
                        | specialization|       | description   |
                        | isActive      |       | createdAt     |
                        | createdAt     |       | updatedAt     |
                        | updatedAt     |       +------^--------+
                        +---------------+              |
                                                      |
+---------------+       +---------------+       +---------------+
|   Review      |       |  WorkingHour  |       |   Payment     |
+---------------+       +---------------+       +---------------+
| id            |       | id            |       | id            |
| userId        |------>| staffId       |------>| appointmentId |------>
| appointmentId |------>| dayOfWeek     |       | amount        |
| rating        |       | startTime     |       | method        |
| comment       |       | endTime       |       | status        |
| createdAt     |       | isAvailable   |       | transactionId |
| updatedAt     |       | createdAt     |       | createdAt     |
+---------------+       | updatedAt     |       | updatedAt     |
                        +---------------+       +---------------+

                        +---------------+
                        | Notification  |
                        +---------------+
                        | id            |
                        | userId        |------>
                        | type          |
                        | content       |
                        | isRead        |
                        | createdAt     |
                        | updatedAt     |
                        +---------------+
```

## 2. Chi tiết các bảng

### 2.1. Bảng User

**Mô tả**: Lưu trữ thông tin người dùng (khách hàng, nhân viên, quản lý)

| Tên trường | Kiểu dữ liệu | Mô tả                                      |
|------------|--------------|-------------------------------------------|
| id         | ObjectId     | ID duy nhất của người dùng                |
| email      | String       | Email của người dùng (duy nhất)           |
| password   | String       | Mật khẩu đã được mã hóa                   |
| name       | String       | Tên đầy đủ của người dùng                 |
| phone      | String       | Số điện thoại của người dùng              |
| role       | String       | Vai trò: "customer", "staff", "admin"     |
| avatar     | String       | URL hình đại diện                        |
| createdAt  | DateTime     | Thời gian tạo tài khoản                   |
| updatedAt  | DateTime     | Thời gian cập nhật thông tin gần nhất     |

### 2.2. Bảng Staff

**Mô tả**: Lưu trữ thông tin bổ sung của nhân viên

| Tên trường     | Kiểu dữ liệu | Mô tả                                       |
|----------------|--------------|---------------------------------------------|
| id             | ObjectId     | ID duy nhất của nhân viên                   |
| userId         | ObjectId     | Tham chiếu đến User (khóa ngoại)           |
| specialization | String       | Chuyên môn của nhân viên                    |
| isActive       | Boolean      | Trạng thái hoạt động của nhân viên          |
| createdAt      | DateTime     | Thời gian tạo                               |
| updatedAt      | DateTime     | Thời gian cập nhật gần nhất                 |

### 2.3. Bảng Service

**Mô tả**: Lưu trữ thông tin các dịch vụ của salon

| Tên trường  | Kiểu dữ liệu | Mô tả                                     |
|-------------|--------------|-------------------------------------------|
| id          | ObjectId     | ID duy nhất của dịch vụ                   |
| name        | String       | Tên dịch vụ                               |
| description | String       | Mô tả chi tiết về dịch vụ                 |
| price       | Decimal      | Giá dịch vụ                               |
| duration    | Integer      | Thời gian thực hiện (phút)                |
| image       | String       | URL hình ảnh dịch vụ                      |
| categoryId  | ObjectId     | Tham chiếu đến Category (khóa ngoại)      |
| createdAt   | DateTime     | Thời gian tạo                             |
| updatedAt   | DateTime     | Thời gian cập nhật gần nhất               |

### 2.4. Bảng Category

**Mô tả**: Lưu trữ các danh mục dịch vụ

| Tên trường  | Kiểu dữ liệu | Mô tả                                     |
|-------------|--------------|-------------------------------------------|
| id          | ObjectId     | ID duy nhất của danh mục                  |
| name        | String       | Tên danh mục                              |
| description | String       | Mô tả về danh mục                         |
| createdAt   | DateTime     | Thời gian tạo                             |
| updatedAt   | DateTime     | Thời gian cập nhật gần nhất               |

### 2.5. Bảng Appointment

**Mô tả**: Lưu trữ thông tin các cuộc hẹn

| Tên trường  | Kiểu dữ liệu | Mô tả                                     |
|-------------|--------------|-------------------------------------------|
| id          | ObjectId     | ID duy nhất của cuộc hẹn                  |
| userId      | ObjectId     | Tham chiếu đến User (khách hàng)          |
| staffId     | ObjectId     | Tham chiếu đến Staff (nhân viên thực hiện)|
| serviceId   | ObjectId     | Tham chiếu đến Service (dịch vụ)          |
| date        | Date         | Ngày hẹn                                  |
| startTime   | Time         | Thời gian bắt đầu                         |
| endTime     | Time         | Thời gian kết thúc                        |
| status      | String       | Trạng thái: "pending", "confirmed", "completed", "canceled" |
| notes       | String       | Ghi chú bổ sung                           |
| totalPrice  | Decimal      | Tổng giá tiền                             |
| createdAt   | DateTime     | Thời gian tạo lịch hẹn                    |
| updatedAt   | DateTime     | Thời gian cập nhật gần nhất               |

### 2.6. Bảng WorkingHour

**Mô tả**: Lưu trữ lịch làm việc của nhân viên

| Tên trường   | Kiểu dữ liệu | Mô tả                                     |
|--------------|--------------|-------------------------------------------|
| id           | ObjectId     | ID duy nhất của lịch làm việc             |
| staffId      | ObjectId     | Tham chiếu đến Staff                      |
| dayOfWeek    | Integer      | Ngày trong tuần (1-7, 1 là Thứ Hai)       |
| startTime    | Time         | Thời gian bắt đầu ca làm việc             |
| endTime      | Time         | Thời gian kết thúc ca làm việc            |
| isAvailable  | Boolean      | Trạng thái khả dụng                       |
| createdAt    | DateTime     | Thời gian tạo                             |
| updatedAt    | DateTime     | Thời gian cập nhật gần nhất               |

### 2.7. Bảng Review

**Mô tả**: Lưu trữ đánh giá của khách hàng

| Tên trường    | Kiểu dữ liệu | Mô tả                                     |
|---------------|--------------|-------------------------------------------|
| id            | ObjectId     | ID duy nhất của đánh giá                  |
| userId        | ObjectId     | Tham chiếu đến User (người đánh giá)      |
| appointmentId | ObjectId     | Tham chiếu đến Appointment                |
| rating        | Integer      | Điểm đánh giá (1-5)                       |
| comment       | String       | Nội dung đánh giá                         |
| createdAt     | DateTime     | Thời gian tạo                             |
| updatedAt     | DateTime     | Thời gian cập nhật gần nhất               |

### 2.8. Bảng Payment

**Mô tả**: Lưu trữ thông tin thanh toán

| Tên trường    | Kiểu dữ liệu | Mô tả                                     |
|---------------|--------------|-------------------------------------------|
| id            | ObjectId     | ID duy nhất của thanh toán                |
| appointmentId | ObjectId     | Tham chiếu đến Appointment                |
| amount        | Decimal      | Số tiền thanh toán                        |
| method        | String       | Phương thức: "cash", "credit_card", "momo", "vnpay" |
| status        | String       | Trạng thái: "pending", "completed", "failed", "refunded" |
| transactionId | String       | ID giao dịch từ cổng thanh toán (nếu có)  |
| createdAt     | DateTime     | Thời gian tạo                             |
| updatedAt     | DateTime     | Thời gian cập nhật gần nhất               |

### 2.9. Bảng Notification

**Mô tả**: Lưu trữ thông báo cho người dùng

| Tên trường | Kiểu dữ liệu | Mô tả                                     |
|------------|--------------|-------------------------------------------|
| id         | ObjectId     | ID duy nhất của thông báo                 |
| userId     | ObjectId     | Tham chiếu đến User (người nhận)          |
| type       | String       | Loại thông báo                            |
| content    | String       | Nội dung thông báo                        |
| isRead     | Boolean      | Đã đọc hay chưa                           |
| createdAt  | DateTime     | Thời gian tạo                             |
| updatedAt  | DateTime     | Thời gian cập nhật gần nhất               |

## 3. Mô hình Schema (MongoDB)

Nếu sử dụng MongoDB làm cơ sở dữ liệu, bạn có thể tham khảo các schema sau:

### User Schema

```javascript
const UserSchema = new Schema({
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  name: { type: String, required: true },
  phone: { type: String },
  role: { type: String, enum: ['customer', 'staff', 'admin'], default: 'customer' },
  avatar: { type: String },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Staff Schema

```javascript
const StaffSchema = new Schema({
  userId: { type: Schema.Types.ObjectId, ref: 'User', required: true },
  specialization: { type: String },
  isActive: { type: Boolean, default: true },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Service Schema

```javascript
const ServiceSchema = new Schema({
  name: { type: String, required: true },
  description: { type: String },
  price: { type: Number, required: true },
  duration: { type: Number, required: true }, // in minutes
  image: { type: String },
  categoryId: { type: Schema.Types.ObjectId, ref: 'Category' },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Category Schema

```javascript
const CategorySchema = new Schema({
  name: { type: String, required: true },
  description: { type: String },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Appointment Schema

```javascript
const AppointmentSchema = new Schema({
  userId: { type: Schema.Types.ObjectId, ref: 'User', required: true },
  staffId: { type: Schema.Types.ObjectId, ref: 'Staff', required: true },
  serviceId: { type: Schema.Types.ObjectId, ref: 'Service', required: true },
  date: { type: Date, required: true },
  startTime: { type: String, required: true },
  endTime: { type: String, required: true },
  status: { 
    type: String, 
    enum: ['pending', 'confirmed', 'completed', 'canceled'], 
    default: 'pending' 
  },
  notes: { type: String },
  totalPrice: { type: Number, required: true },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### WorkingHour Schema

```javascript
const WorkingHourSchema = new Schema({
  staffId: { type: Schema.Types.ObjectId, ref: 'Staff', required: true },
  dayOfWeek: { type: Number, required: true }, // 1-7, where 1 is Monday
  startTime: { type: String, required: true },
  endTime: { type: String, required: true },
  isAvailable: { type: Boolean, default: true },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Review Schema

```javascript
const ReviewSchema = new Schema({
  userId: { type: Schema.Types.ObjectId, ref: 'User', required: true },
  appointmentId: { type: Schema.Types.ObjectId, ref: 'Appointment', required: true },
  rating: { type: Number, required: true, min: 1, max: 5 },
  comment: { type: String },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Payment Schema

```javascript
const PaymentSchema = new Schema({
  appointmentId: { type: Schema.Types.ObjectId, ref: 'Appointment', required: true },
  amount: { type: Number, required: true },
  method: { 
    type: String, 
    enum: ['cash', 'credit_card', 'momo', 'vnpay'], 
    required: true 
  },
  status: { 
    type: String, 
    enum: ['pending', 'completed', 'failed', 'refunded'], 
    default: 'pending' 
  },
  transactionId: { type: String },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

### Notification Schema

```javascript
const NotificationSchema = new Schema({
  userId: { type: Schema.Types.ObjectId, ref: 'User', required: true },
  type: { type: String, required: true },
  content: { type: String, required: true },
  isRead: { type: Boolean, default: false },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
});
```

## 4. Mô hình Prisma Schema (PostgreSQL)

Nếu sử dụng PostgreSQL với Prisma, bạn có thể tham khảo schema sau:

```prisma
model User {
  id            String        @id @default(cuid())
  email         String        @unique
  password      String
  name          String
  phone         String?
  role          Role          @default(CUSTOMER)
  avatar        String?
  createdAt     DateTime      @default(now())
  updatedAt     DateTime      @updatedAt
  appointments  Appointment[]
  reviews       Review[]
  notifications Notification[]
  staff         Staff?
}

enum Role {
  CUSTOMER
  STAFF
  ADMIN
}

model Staff {
  id             String        @id @default(cuid())
  userId         String        @unique
  user           User          @relation(fields: [userId], references: [id])
  specialization String?
  isActive       Boolean       @default(true)
  createdAt      DateTime      @default(now())
  updatedAt      DateTime      @updatedAt
  appointments   Appointment[]
  workingHours   WorkingHour[]
}

model Service {
  id           String        @id @default(cuid())
  name         String
  description  String?
  price        Decimal
  duration     Int           // in minutes
  image        String?
  categoryId   String?
  category     Category?     @relation(fields: [categoryId], references: [id])
  createdAt    DateTime      @default(now())
  updatedAt    DateTime      @updatedAt
  appointments Appointment[]
}

model Category {
  id          String    @id @default(cuid())
  name        String
  description String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
  services    Service[]
}

model Appointment {
  id            String       @id @default(cuid())
  userId        String
  user          User         @relation(fields: [userId], references: [id])
  staffId       String
  staff         Staff        @relation(fields: [staffId], references: [id])
  serviceId     String
  service       Service      @relation(fields: [serviceId], references: [id])
  date          DateTime
  startTime     String
  endTime       String
  status        AppointmentStatus @default(PENDING)
  notes         String?
  totalPrice    Decimal
  createdAt     DateTime     @default(now())
  updatedAt     DateTime     @updatedAt
  reviews       Review[]
  payments      Payment[]
}

enum AppointmentStatus {
  PENDING
  CONFIRMED
  COMPLETED
  CANCELED
}

model WorkingHour {
  id          String   @id @default(cuid())
  staffId     String
  staff       Staff    @relation(fields: [staffId], references: [id])
  dayOfWeek   Int      // 1-7, where 1 is Monday
  startTime   String
  endTime     String
  isAvailable Boolean  @default(true)
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}

model Review {
  id            String     @id @default(cuid())
  userId        String
  user          User       @relation(fields: [userId], references: [id])
  appointmentId String
  appointment   Appointment @relation(fields: [appointmentId], references: [id])
  rating        Int
  comment       String?
  createdAt     DateTime   @default(now())
  updatedAt     DateTime   @updatedAt
}

model Payment {
  id            String       @id @default(cuid())
  appointmentId String
  appointment   Appointment  @relation(fields: [appointmentId], references: [id])
  amount        Decimal
  method        PaymentMethod
  status        PaymentStatus @default(PENDING)
  transactionId String?
  createdAt     DateTime     @default(now())
  updatedAt     DateTime     @updatedAt
}

enum PaymentMethod {
  CASH
  CREDIT_CARD
  MOMO
  VNPAY
}

enum PaymentStatus {
  PENDING
  COMPLETED
  FAILED
  REFUNDED
}

model Notification {
  id        String   @id @default(cuid())
  userId    String
  user      User     @relation(fields: [userId], references: [id])
  type      String
  content   String
  isRead    Boolean  @default(false)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

## 5. Quy tắc ràng buộc và quan hệ

### Quan hệ chính:

1. **User - Staff**: Một User có thể là một Staff (1:1)
2. **User - Appointment**: Một User có nhiều Appointment (1:N)
3. **Staff - Appointment**: Một Staff có nhiều Appointment (1:N)
4. **Service - Appointment**: Một Service được sử dụng trong nhiều Appointment (1:N)
5. **Category - Service**: Một Category có nhiều Service (1:N)
6. **Staff - WorkingHour**: Một Staff có nhiều WorkingHour (1:N)
7. **User - Review**: Một User viết nhiều Review (1:N)
8. **Appointment - Review**: Một Appointment có một Review (1:1)
9. **Appointment - Payment**: Một Appointment có một hoặc nhiều Payment (1:N)
10. **User - Notification**: Một User có nhiều Notification (1:N)

### Ràng buộc:

1. **Xóa User**: Khi xóa một User, cần xử lý các Appointment liên quan
2. **Xóa Service**: Khi xóa một Service, cần kiểm tra không có Appointment nào đang sử dụng
3. **Xóa Staff**: Khi xóa một Staff, cần kiểm tra không có Appointment nào trong tương lai
4. **Trạng thái Appointment**: Chỉ có thể chuyển từ "pending" sang "confirmed", "completed" hoặc "canceled"

## 6. Các truy vấn phổ biến

1. Tìm tất cả các cuộc hẹn của một khách hàng
2. Tìm tất cả các cuộc hẹn của một nhân viên trong một ngày cụ thể
3. Tìm tất cả các thời gian còn trống của một nhân viên trong một ngày
4. Tính tổng doanh thu trong một khoảng thời gian
5. Tìm các dịch vụ phổ biến nhất dựa trên số lượng đặt lịch
6. Tìm đánh giá trung bình của một nhân viên

## 7. Chỉ mục (Indexes)

Để tối ưu hiệu suất, nên tạo các chỉ mục sau:

1. User.email
2. Appointment.userId
3. Appointment.staffId
4. Appointment.date
5. Appointment.status
6. WorkingHour.staffId
7. WorkingHour.dayOfWeek
8. Payment.appointmentId
9. Review.appointmentId
10. Notification.userId
