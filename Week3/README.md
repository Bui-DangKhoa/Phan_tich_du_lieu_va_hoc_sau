# Lab 3: Xử lý và Làm sạch Dữ liệu Nhịp tim Bệnh nhân

## Mô tả

Dự án này thực hiện quá trình làm sạch và xử lý dữ liệu nhịp tim bệnh nhân từ file CSV thô, giải quyết các vấn đề phổ biến trong dữ liệu thực tế.

---

## Công nghệ sử dụng

| Công nghệ            | Phiên bản | Mục đích                             |
| -------------------- | --------- | ------------------------------------ |
| **Python**           | 3.x       | Ngôn ngữ lập trình chính             |
| **Pandas**           | -         | Xử lý và phân tích dữ liệu dạng bảng |
| **NumPy**            | -         | Tính toán số học và xử lý mảng       |
| **Jupyter Notebook** | -         | Môi trường phát triển tương tác      |

---

## Cách hoạt động

### Quy trình xử lý dữ liệu (Data Cleaning Pipeline)

```
patient_heart_rate.csv → [Xử lý] → patient_heart_rate_clean.csv
```

### Các bước xử lý chi tiết:

#### 1. **Thêm Header cho DataFrame**

- Đọc file CSV và gán tên cột: `Id`, `Name`, `Age`, `Weight`, `m0006`, `m0612`, `m1218`, `f0006`, `f0612`, `f1218`

#### 2. **Tách cột Name**

- Tách cột `Name` thành `Firstname` và `Lastname`
- Xóa cột `Name` gốc

#### 3. **Chuẩn hóa đơn vị đo lường**

- Chuyển đổi cột `Weight` từ đơn vị `lbs` sang `kg`
- Công thức: `weight_kg = weight_lbs / 2.2`

#### 4. **Xóa dòng rỗng**

- Loại bỏ các dòng có tất cả giá trị là NaN

#### 5. **Xử lý dữ liệu trùng lặp**

- Loại bỏ các dòng trùng lặp dựa trên: `Firstname`, `Lastname`, `Age`, `Weight`

#### 6. **Xử lý ký tự Non-ASCII**

- Thay thế các ký tự không thuộc bảng mã ASCII

#### 7. **Xử lý Missing Values (Age, Weight)**

- Thống kê số lượng giá trị thiếu
- Xóa dòng thiếu cả `Age` và `Weight`
- Điền giá trị trung bình (mean) cho các giá trị còn thiếu

#### 8. **Phân rã cột phức hợp (Melt)**

- Chuyển đổi các cột `m0006`, `m0612`, `m1218`, `f0006`, `f0612`, `f1218` thành:
  - `sex`: Giới tính (m/f)
  - `Time`: Khoảng thời gian (00-06, 06-12, 12-18)
  - `PulseRate`: Giá trị nhịp tim

#### 9. **Xử lý Missing Values (PulseRate)**

Áp dụng theo thứ tự ưu tiên:

1. Trung bình giá trị liền trước và liền sau
2. Trung bình 2 giá trị liền trước
3. Trung bình 2 giá trị liền sau
4. Trung bình các giá trị của cùng bệnh nhân
5. Trung bình theo nhóm giới tính
6. Trung bình toàn bộ dữ liệu hoặc giá trị y học chuẩn (75 bpm)

#### 10. **Rút gọn và Reindex**

- Sắp xếp lại thứ tự cột
- Reset index
- Làm tròn giá trị số
- Lưu file CSV

---

## Kết quả

### File đầu ra

| File                           | Mô tả                               |
| ------------------------------ | ----------------------------------- |
| `patient_heart_rate_clean.csv` | Dữ liệu đã được làm sạch hoàn chỉnh |
| `outputcleanup.csv`            | File trung gian sau bước melt       |

### Cấu trúc dữ liệu sau xử lý

| Cột         | Kiểu dữ liệu | Mô tả                  |
| ----------- | ------------ | ---------------------- |
| `Id`        | int          | Mã định danh bệnh nhân |
| `Firstname` | string       | Tên                    |
| `Lastname`  | string       | Họ                     |
| `Age`       | float        | Tuổi                   |
| `Weight`    | float        | Cân nặng (kg)          |
| `sex`       | string       | Giới tính (m/f)        |
| `Time`      | string       | Khoảng thời gian đo    |
| `PulseRate` | float        | Nhịp tim (bpm)         |

### Các vấn đề đã xử lý

- Dữ liệu không có header
- Cột chứa nhiều thông tin (Name → Firstname, Lastname)
- Đơn vị đo lường không thống nhất (lbs → kg)
- Dòng dữ liệu rỗng
- Dữ liệu trùng lặp
- Ký tự non-ASCII
- Missing values (Age, Weight, PulseRate)
- Cột phức hợp cần phân rã

---

## Cấu trúc thư mục

```
Lab3/
├── Lab3.ipynb                    # Notebook chính
├── patient_heart_rate.csv        # Dữ liệu gốc
├── patient_heart_rate_clean.csv  # Dữ liệu đã làm sạch
├── outputcleanup.csv             # File trung gian
└── README.md                     # Tài liệu hướng dẫn
```

---

## Hướng dẫn sử dụng

1. Mở file `Lab3.ipynb` bằng Jupyter Notebook hoặc VS Code
2. Chạy tuần tự các cell từ đầu đến cuối
3. Kết quả sẽ được lưu vào file `patient_heart_rate_clean.csv`

---

## Tác giả

- **Môn học**: Nhập môn phân tích dữ liệu và học sâu
- **Bài thực hành**: Lab 3 - Data Cleaning
