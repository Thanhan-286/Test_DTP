# Phân tích SLA đơn hàng nội thành / ngoại thành

## Mục tiêu
Đoạn code dùng để **phân tích SLA xử lý đơn hàng** dựa trên:
- Khu vực giao hàng: **nội thành** hoặc **ngoại thành**
- Thời điểm đặt đơn
- Thời gian hoàn thành từng bước xử lý đơn

Kết quả trả về là:
- Tổng số đơn
- Số đơn **trễ SLA**
- Phân loại theo từng nhóm điều kiện

---

##  Tư duy xử lý chính

### 1️ Xác định nội thành / ngoại thành
- Dựa vào **center** (mã trung tâm vận hành)
- Ánh xạ center → thành phố chính
- So sánh với **city** của đơn:
  - Trùng → **nội thành**
  - Khác → **ngoại thành**

---

### 2️ Phân loại đơn nội thành theo thời gian đặt
Đơn nội thành được chia thành 3 nhóm:

| Case | Thời gian đặt |
|------|---------------|
| inner_case1 | Trước 10:00 |
| inner_case2 | 10:00 – 16:00 |
| inner_case3 | Sau 16:00 |

Việc phân loại giúp áp SLA khác nhau cho từng nhóm.

---

### 3️ Kiểm tra SLA

####  Đơn nội thành
- Mỗi case có **mốc thời gian SLA cố định**
- So sánh **giờ + ngày** của:
  - Duyệt đơn
  - Đóng gói
  - Hoàn tất
- Những đơn nào không có giá trị packedAt, completeAt coi như không tính

####  Đơn ngoại thành
- Áp SLA theo **khoảng thời gian (timedelta)**:
  - Duyệt đơn ≤ 24h
  - Đóng gói ≤ 4h sau duyệt
  - Hoàn tất ≤ 24h sau đóng gói

---

### 4️ Đọc dữ liệu & thống kê
- Đọc file Excel bằng `openpyxl`
- Bỏ các dòng:
  - Trống
  - Thiếu dữ liệu
  - Không xác định được nội/ngoại thành
- Thống kê cho từng loại:
  - **Tổng số đơn**
  - **Số đơn trễ SLA**

---

##  Kết luận
Code được thiết kế theo hướng:
- Dễ mở rộng thêm:
  - Case SLA mới
  - City mới
  - Khung Quy tắc SLA mới
