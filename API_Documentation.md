# Tài liệu API - Hệ thống đặt lịch cắt tóc

## Giới thiệu

Tài liệu này mô tả các API endpoints của hệ thống đặt lịch cắt tóc được phát triển với Next.js và React.js. API được xây dựng sử dụng Next.js API Routes.

## Cấu trúc cơ bản

- Base URL: `/api`
- Format dữ liệu: JSON
- Authentication: JWT (JSON Web Token)

## Authentication

### Đăng ký tài khoản

**Request:**
- Method: `POST`
- Endpoint: `/api/auth/register`
- Body:
```json
{
  "name": "Nguyen Van A",
  "email": "example@gmail.com",
  "password": "password123",
  "phone": "0123456789"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Đăng ký tài khoản thành công",
  "user": {
    "id": "user_id",
    "name": "Nguyen Van A",
    "email": "example@gmail.com",
    "phone": "0123456789",
    "role": "customer"
  }
}
```

### Đăng nhập

**Request:**
- Method: `POST`
- Endpoint: `/api/auth/login`
- Body:
```json
{
  "email": "example@gmail.com",
  "password": "password123"
}
```

**Response thành công:**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user_id",
    "name": "Nguyen Van A",
    "email": "example@gmail.com",
    "role": "customer"
  }
}
```

### Đăng xuất

**Request:**
- Method: `POST`
- Endpoint: `/api/auth/logout`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "message": "Đăng xuất thành công"
}
```

### Lấy thông tin người dùng hiện tại

**Request:**
- Method: `GET`
- Endpoint: `/api/auth/me`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "user": {
    "id": "user_id",
    "name": "Nguyen Van A",
    "email": "example@gmail.com",
    "phone": "0123456789",
    "role": "customer",
    "avatar": "https://example.com/avatar.jpg"
  }
}
```

## Quản lý người dùng (User)

### Lấy danh sách người dùng (Admin only)

**Request:**
- Method: `GET`
- Endpoint: `/api/users`
- Headers:
  - Authorization: `Bearer {token}`
- Query parameters:
  - page: số trang (mặc định: 1)
  - limit: số lượng mỗi trang (mặc định: 10)
  - role: lọc theo vai trò (customer, staff, admin)

**Response thành công:**
```json
{
  "success": true,
  "users": [
    {
      "id": "user_id_1",
      "name": "Nguyen Van A",
      "email": "example1@gmail.com",
      "phone": "0123456789",
      "role": "customer"
    },
    {
      "id": "user_id_2",
      "name": "Nguyen Van B",
      "email": "example2@gmail.com",
      "phone": "0987654321",
      "role": "customer"
    }
  ],
  "pagination": {
    "totalItems": 50,
    "totalPages": 5,
    "currentPage": 1,
    "itemsPerPage": 10
  }
}
```

### Lấy thông tin người dùng theo ID (Admin only)

**Request:**
- Method: `GET`
- Endpoint: `/api/users/{id}`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "user": {
    "id": "user_id",
    "name": "Nguyen Van A",
    "email": "example@gmail.com",
    "phone": "0123456789",
    "role": "customer",
    "avatar": "https://example.com/avatar.jpg",
    "createdAt": "2023-08-01T10:30:00Z"
  }
}
```

### Cập nhật thông tin người dùng

**Request:**
- Method: `PUT`
- Endpoint: `/api/users/{id}`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "name": "Nguyen Van A Updated",
  "phone": "0123456789",
  "avatar": "https://example.com/new-avatar.jpg"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Cập nhật thông tin thành công",
  "user": {
    "id": "user_id",
    "name": "Nguyen Van A Updated",
    "email": "example@gmail.com",
    "phone": "0123456789",
    "role": "customer",
    "avatar": "https://example.com/new-avatar.jpg"
  }
}
```

### Đổi mật khẩu

**Request:**
- Method: `PUT`
- Endpoint: `/api/users/{id}/change-password`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "currentPassword": "password123",
  "newPassword": "newPassword123"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Đổi mật khẩu thành công"
}
```

## Quản lý nhân viên (Staff)

### Lấy danh sách nhân viên

**Request:**
- Method: `GET`
- Endpoint: `/api/staff`
- Query parameters:
  - page: số trang (mặc định: 1)
  - limit: số lượng mỗi trang (mặc định: 10)
  - isActive: lọc theo trạng thái (true/false)

**Response thành công:**
```json
{
  "success": true,
  "staff": [
    {
      "id": "staff_id_1",
      "userId": "user_id_1",
      "name": "Le Thi C",
      "specialization": "Cắt tóc nam",
      "avatar": "https://example.com/avatar1.jpg",
      "isActive": true
    },
    {
      "id": "staff_id_2",
      "userId": "user_id_2",
      "name": "Pham Van D",
      "specialization": "Nhuộm tóc",
      "avatar": "https://example.com/avatar2.jpg",
      "isActive": true
    }
  ],
  "pagination": {
    "totalItems": 8,
    "totalPages": 1,
    "currentPage": 1,
    "itemsPerPage": 10
  }
}
```

### Lấy thông tin nhân viên theo ID

**Request:**
- Method: `GET`
- Endpoint: `/api/staff/{id}`

**Response thành công:**
```json
{
  "success": true,
  "staff": {
    "id": "staff_id_1",
    "userId": "user_id_1",
    "name": "Le Thi C",
    "email": "staff1@gmail.com",
    "phone": "0123456789",
    "specialization": "Cắt tóc nam",
    "avatar": "https://example.com/avatar1.jpg",
    "isActive": true
  }
}
```

### Thêm nhân viên mới (Admin only)

**Request:**
- Method: `POST`
- Endpoint: `/api/staff`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "name": "Le Thi E",
  "email": "staff3@gmail.com",
  "phone": "0123456789",
  "password": "password123",
  "specialization": "Uốn tóc",
  "avatar": "https://example.com/avatar3.jpg"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Thêm nhân viên thành công",
  "staff": {
    "id": "staff_id_3",
    "userId": "user_id_3",
    "name": "Le Thi E",
    "specialization": "Uốn tóc",
    "avatar": "https://example.com/avatar3.jpg",
    "isActive": true
  }
}
```

### Cập nhật thông tin nhân viên (Admin only)

**Request:**
- Method: `PUT`
- Endpoint: `/api/staff/{id}`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "specialization": "Uốn và nhuộm tóc",
  "isActive": true
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Cập nhật thông tin nhân viên thành công",
  "staff": {
    "id": "staff_id_3",
    "userId": "user_id_3",
    "name": "Le Thi E",
    "specialization": "Uốn và nhuộm tóc",
    "avatar": "https://example.com/avatar3.jpg",
    "isActive": true
  }
}
```

## Quản lý dịch vụ (Service)

### Lấy danh sách dịch vụ

**Request:**
- Method: `GET`
- Endpoint: `/api/services`
- Query parameters:
  - page: số trang (mặc định: 1)
  - limit: số lượng mỗi trang (mặc định: 10)
  - categoryId: lọc theo danh mục

**Response thành công:**
```json
{
  "success": true,
  "services": [
    {
      "id": "service_id_1",
      "name": "Cắt tóc nam",
      "description": "Dịch vụ cắt tóc nam cơ bản",
      "price": 100000,
      "duration": 30,
      "image": "https://example.com/service1.jpg",
      "categoryId": "category_id_1"
    },
    {
      "id": "service_id_2",
      "name": "Uốn tóc",
      "description": "Dịch vụ uốn tóc",
      "price": 500000,
      "duration": 120,
      "image": "https://example.com/service2.jpg",
      "categoryId": "category_id_2"
    }
  ],
  "pagination": {
    "totalItems": 15,
    "totalPages": 2,
    "currentPage": 1,
    "itemsPerPage": 10
  }
}
```

### Lấy thông tin dịch vụ theo ID

**Request:**
- Method: `GET`
- Endpoint: `/api/services/{id}`

**Response thành công:**
```json
{
  "success": true,
  "service": {
    "id": "service_id_1",
    "name": "Cắt tóc nam",
    "description": "Dịch vụ cắt tóc nam cơ bản",
    "price": 100000,
    "duration": 30,
    "image": "https://example.com/service1.jpg",
    "categoryId": "category_id_1",
    "category": {
      "id": "category_id_1",
      "name": "Dịch vụ cắt tóc"
    }
  }
}
```

### Thêm dịch vụ mới (Admin only)

**Request:**
- Method: `POST`
- Endpoint: `/api/services`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "name": "Nhuộm tóc highlight",
  "description": "Dịch vụ nhuộm tóc highlight",
  "price": 700000,
  "duration": 180,
  "image": "https://example.com/service3.jpg",
  "categoryId": "category_id_2"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Thêm dịch vụ thành công",
  "service": {
    "id": "service_id_3",
    "name": "Nhuộm tóc highlight",
    "description": "Dịch vụ nhuộm tóc highlight",
    "price": 700000,
    "duration": 180,
    "image": "https://example.com/service3.jpg",
    "categoryId": "category_id_2"
  }
}
```

### Cập nhật thông tin dịch vụ (Admin only)

**Request:**
- Method: `PUT`
- Endpoint: `/api/services/{id}`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "price": 750000,
  "duration": 200,
  "description": "Dịch vụ nhuộm tóc highlight cao cấp"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Cập nhật dịch vụ thành công",
  "service": {
    "id": "service_id_3",
    "name": "Nhuộm tóc highlight",
    "description": "Dịch vụ nhuộm tóc highlight cao cấp",
    "price": 750000,
    "duration": 200,
    "image": "https://example.com/service3.jpg",
    "categoryId": "category_id_2"
  }
}
```

### Xóa dịch vụ (Admin only)

**Request:**
- Method: `DELETE`
- Endpoint: `/api/services/{id}`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "message": "Xóa dịch vụ thành công"
}
```

## Quản lý danh mục (Category)

### Lấy danh sách danh mục

**Request:**
- Method: `GET`
- Endpoint: `/api/categories`

**Response thành công:**
```json
{
  "success": true,
  "categories": [
    {
      "id": "category_id_1",
      "name": "Dịch vụ cắt tóc",
      "description": "Các dịch vụ cắt tóc cơ bản"
    },
    {
      "id": "category_id_2",
      "name": "Dịch vụ uốn và nhuộm",
      "description": "Các dịch vụ uốn và nhuộm tóc"
    }
  ]
}
```

### CRUD danh mục (Admin only)

Các endpoints tương tự như Service:
- `POST /api/categories`: Thêm danh mục mới
- `GET /api/categories/{id}`: Lấy thông tin danh mục theo ID
- `PUT /api/categories/{id}`: Cập nhật thông tin danh mục
- `DELETE /api/categories/{id}`: Xóa danh mục

## Quản lý đặt lịch (Appointment)

### Lấy danh sách các khung giờ trống

**Request:**
- Method: `GET`
- Endpoint: `/api/appointments/available-slots`
- Query parameters:
  - date: ngày cần kiểm tra (YYYY-MM-DD)
  - staffId: ID nhân viên (tùy chọn)
  - serviceId: ID dịch vụ (cần thiết để tính thời gian)

**Response thành công:**
```json
{
  "success": true,
  "availableSlots": [
    {
      "staffId": "staff_id_1",
      "staffName": "Le Thi C",
      "slots": [
        {
          "startTime": "09:00",
          "endTime": "09:30"
        },
        {
          "startTime": "10:00",
          "endTime": "10:30"
        }
      ]
    },
    {
      "staffId": "staff_id_2",
      "staffName": "Pham Van D",
      "slots": [
        {
          "startTime": "09:30",
          "endTime": "10:00"
        },
        {
          "startTime": "10:30",
          "endTime": "11:00"
        }
      ]
    }
  ]
}
```

### Đặt lịch mới

**Request:**
- Method: `POST`
- Endpoint: `/api/appointments`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "serviceId": "service_id_1",
  "staffId": "staff_id_1",
  "date": "2023-08-10",
  "startTime": "10:00",
  "notes": "Tôi muốn cắt kiểu mohawk"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Đặt lịch thành công",
  "appointment": {
    "id": "appointment_id_1",
    "serviceId": "service_id_1",
    "serviceName": "Cắt tóc nam",
    "staffId": "staff_id_1",
    "staffName": "Le Thi C",
    "date": "2023-08-10",
    "startTime": "10:00",
    "endTime": "10:30",
    "status": "pending",
    "notes": "Tôi muốn cắt kiểu mohawk",
    "totalPrice": 100000
  }
}
```

### Lấy danh sách lịch hẹn của người dùng

**Request:**
- Method: `GET`
- Endpoint: `/api/appointments/my-appointments`
- Headers:
  - Authorization: `Bearer {token}`
- Query parameters:
  - status: lọc theo trạng thái (pending, confirmed, completed, canceled)
  - from: ngày bắt đầu (YYYY-MM-DD)
  - to: ngày kết thúc (YYYY-MM-DD)

**Response thành công:**
```json
{
  "success": true,
  "appointments": [
    {
      "id": "appointment_id_1",
      "serviceId": "service_id_1",
      "serviceName": "Cắt tóc nam",
      "staffId": "staff_id_1",
      "staffName": "Le Thi C",
      "date": "2023-08-10",
      "startTime": "10:00",
      "endTime": "10:30",
      "status": "confirmed",
      "totalPrice": 100000
    }
  ]
}
```

### Lấy thông tin chi tiết lịch hẹn

**Request:**
- Method: `GET`
- Endpoint: `/api/appointments/{id}`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "appointment": {
    "id": "appointment_id_1",
    "userId": "user_id_1",
    "userName": "Nguyen Van A",
    "userPhone": "0123456789",
    "serviceId": "service_id_1",
    "serviceName": "Cắt tóc nam",
    "staffId": "staff_id_1",
    "staffName": "Le Thi C",
    "date": "2023-08-10",
    "startTime": "10:00",
    "endTime": "10:30",
    "status": "confirmed",
    "notes": "Tôi muốn cắt kiểu mohawk",
    "totalPrice": 100000,
    "createdAt": "2023-08-01T15:30:00Z"
  }
}
```

### Cập nhật trạng thái lịch hẹn (Staff/Admin only)

**Request:**
- Method: `PUT`
- Endpoint: `/api/appointments/{id}/status`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "status": "confirmed"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Cập nhật trạng thái lịch hẹn thành công",
  "appointment": {
    "id": "appointment_id_1",
    "status": "confirmed"
  }
}
```

### Hủy lịch hẹn

**Request:**
- Method: `PUT`
- Endpoint: `/api/appointments/{id}/cancel`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "message": "Hủy lịch hẹn thành công",
  "appointment": {
    "id": "appointment_id_1",
    "status": "canceled"
  }
}
```

## Quản lý lịch làm việc (WorkingHour)

### Lấy lịch làm việc của nhân viên

**Request:**
- Method: `GET`
- Endpoint: `/api/working-hours/staff/{staffId}`
- Headers:
  - Authorization: `Bearer {token}` (for staff/admin only)

**Response thành công:**
```json
{
  "success": true,
  "workingHours": [
    {
      "id": "working_hour_id_1",
      "dayOfWeek": 1,
      "startTime": "09:00",
      "endTime": "17:00",
      "isAvailable": true
    },
    {
      "id": "working_hour_id_2",
      "dayOfWeek": 2,
      "startTime": "09:00",
      "endTime": "17:00",
      "isAvailable": true
    }
  ]
}
```

### Cập nhật lịch làm việc (Staff/Admin only)

**Request:**
- Method: `PUT`
- Endpoint: `/api/working-hours/{id}`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "startTime": "10:00",
  "endTime": "18:00",
  "isAvailable": true
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Cập nhật lịch làm việc thành công",
  "workingHour": {
    "id": "working_hour_id_1",
    "dayOfWeek": 1,
    "startTime": "10:00",
    "endTime": "18:00",
    "isAvailable": true
  }
}
```

## Quản lý đánh giá (Review)

### Gửi đánh giá sau khi sử dụng dịch vụ

**Request:**
- Method: `POST`
- Endpoint: `/api/reviews`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "appointmentId": "appointment_id_1",
  "rating": 5,
  "comment": "Dịch vụ rất tốt, nhân viên nhiệt tình"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Gửi đánh giá thành công",
  "review": {
    "id": "review_id_1",
    "appointmentId": "appointment_id_1",
    "rating": 5,
    "comment": "Dịch vụ rất tốt, nhân viên nhiệt tình"
  }
}
```

### Lấy đánh giá theo nhân viên

**Request:**
- Method: `GET`
- Endpoint: `/api/reviews/staff/{staffId}`
- Query parameters:
  - page: số trang (mặc định: 1)
  - limit: số lượng mỗi trang (mặc định: 10)

**Response thành công:**
```json
{
  "success": true,
  "reviews": [
    {
      "id": "review_id_1",
      "userId": "user_id_1",
      "userName": "Nguyen Van A",
      "appointmentId": "appointment_id_1",
      "rating": 5,
      "comment": "Dịch vụ rất tốt, nhân viên nhiệt tình",
      "createdAt": "2023-08-11T10:30:00Z"
    }
  ],
  "averageRating": 4.8,
  "pagination": {
    "totalItems": 5,
    "totalPages": 1,
    "currentPage": 1,
    "itemsPerPage": 10
  }
}
```

## Thống kê và báo cáo (Admin only)

### Thống kê doanh thu

**Request:**
- Method: `GET`
- Endpoint: `/api/reports/revenue`
- Headers:
  - Authorization: `Bearer {token}`
- Query parameters:
  - from: ngày bắt đầu (YYYY-MM-DD)
  - to: ngày kết thúc (YYYY-MM-DD)
  - groupBy: nhóm theo (day, week, month, year)

**Response thành công:**
```json
{
  "success": true,
  "revenue": [
    {
      "period": "2023-08-01",
      "amount": 1500000
    },
    {
      "period": "2023-08-02",
      "amount": 1200000
    }
  ],
  "totalRevenue": 2700000
}
```

### Thống kê lịch hẹn

**Request:**
- Method: `GET`
- Endpoint: `/api/reports/appointments`
- Headers:
  - Authorization: `Bearer {token}`
- Query parameters:
  - from: ngày bắt đầu (YYYY-MM-DD)
  - to: ngày kết thúc (YYYY-MM-DD)

**Response thành công:**
```json
{
  "success": true,
  "statistics": {
    "total": 50,
    "byStatus": {
      "pending": 10,
      "confirmed": 15,
      "completed": 20,
      "canceled": 5
    },
    "successRate": 0.8
  }
}
```

## Quản lý thông báo (Notification)

### Lấy danh sách thông báo của người dùng

**Request:**
- Method: `GET`
- Endpoint: `/api/notifications`
- Headers:
  - Authorization: `Bearer {token}`
- Query parameters:
  - isRead: lọc theo trạng thái đã đọc (true/false)

**Response thành công:**
```json
{
  "success": true,
  "notifications": [
    {
      "id": "notification_id_1",
      "type": "appointment_confirmation",
      "content": "Lịch hẹn của bạn đã được xác nhận",
      "isRead": false,
      "createdAt": "2023-08-05T14:30:00Z"
    },
    {
      "id": "notification_id_2",
      "type": "appointment_reminder",
      "content": "Nhắc nhở: Bạn có lịch hẹn vào ngày mai",
      "isRead": true,
      "createdAt": "2023-08-06T09:00:00Z"
    }
  ],
  "unreadCount": 1
}
```

### Đánh dấu thông báo đã đọc

**Request:**
- Method: `PUT`
- Endpoint: `/api/notifications/{id}/read`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "message": "Đánh dấu thông báo đã đọc thành công"
}
```

### Đánh dấu tất cả thông báo đã đọc

**Request:**
- Method: `PUT`
- Endpoint: `/api/notifications/read-all`
- Headers:
  - Authorization: `Bearer {token}`

**Response thành công:**
```json
{
  "success": true,
  "message": "Đánh dấu tất cả thông báo đã đọc thành công"
}
```

## Quản lý thanh toán (Payment)

### Tạo thanh toán mới

**Request:**
- Method: `POST`
- Endpoint: `/api/payments`
- Headers:
  - Authorization: `Bearer {token}`
- Body:
```json
{
  "appointmentId": "appointment_id_1",
  "amount": 100000,
  "method": "credit_card"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Tạo thanh toán thành công",
  "payment": {
    "id": "payment_id_1",
    "appointmentId": "appointment_id_1",
    "amount": 100000,
    "method": "credit_card",
    "status": "pending",
    "paymentUrl": "https://payment-gateway.com/checkout/xyz123"
  }
}
```

### Cập nhật trạng thái thanh toán (Webhook)

**Request:**
- Method: `POST`
- Endpoint: `/api/payments/webhook`
- Headers:
  - Authorization: `Bearer {api_key}`
- Body:
```json
{
  "paymentId": "payment_id_1",
  "transactionId": "trans_123456",
  "status": "completed"
}
```

**Response thành công:**
```json
{
  "success": true,
  "message": "Cập nhật trạng thái thanh toán thành công"
}
```

## Xử lý lỗi

Tất cả các lỗi sẽ được trả về với format sau:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Mô tả lỗi"
  }
}
```

### Các mã lỗi phổ biến

- `UNAUTHORIZED`: Không có quyền truy cập
- `INVALID_CREDENTIALS`: Thông tin đăng nhập không hợp lệ
- `RESOURCE_NOT_FOUND`: Không tìm thấy tài nguyên
- `VALIDATION_ERROR`: Lỗi xác thực dữ liệu đầu vào
- `CONFLICT`: Xung đột dữ liệu
- `INTERNAL_ERROR`: Lỗi hệ thống

### Ví dụ lỗi

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Email không hợp lệ",
    "fields": {
      "email": "Email không đúng định dạng"
    }
  }
}
```

## Bảo mật

- Tất cả các endpoints cần xác thực sẽ yêu cầu JWT token trong header `Authorization`
- Token có thời hạn 24 giờ
- Các endpoints chỉ dành cho admin sẽ kiểm tra vai trò của người dùng
- Tất cả các giao tiếp API phải được mã hóa qua HTTPS
