# Lab 1: Phân Tích Dữ Liệu Xét Tuyển Đại Học

## Mô Tả Dự Án

Dự án này thực hiện phân tích và xử lý dữ liệu xét tuyển đại học của học sinh, bao gồm điểm số các môn học từ lớp 10 đến lớp 12, thông tin cá nhân và kết quả xét tuyển. Mục tiêu chính là làm sạch dữ liệu, tạo các biến phái sinh và dự đoán kết quả xét tuyển đại học.

## Công Nghệ Sử Dụng

### Ngôn ngữ lập trình

- Python 3.x

### Thư viện chính

- **Pandas**: Xử lý và phân tích dữ liệu dạng bảng
- **NumPy**: Tính toán số học và xử lý mảng
- **Jupyter Notebook**: Môi trường phát triển tương tác

### Kỹ thuật xử lý dữ liệu

- Làm sạch dữ liệu (Data Cleaning)
- Xử lý giá trị thiếu (Missing Values)
- Feature Engineering (Tạo biến phái sinh)
- Min-Max Normalization (Chuẩn hóa dữ liệu)
- Label Encoding (Mã hóa nhãn)

## Cấu Trúc Dữ Liệu

### Dữ liệu đầu vào

File `dulieuxettuyendaihoc.csv` chứa thông tin:

- **Điểm các môn học** (lớp 10, 11, 12): Toán (T), Lý (L), Hóa (H), Sinh (S), Văn (V), Sử (X), Địa (D), Ngoại ngữ (N)
- **Thông tin cá nhân**: Giới tính (GT), Dân tộc (DT), Khu vực (KV)
- **Điểm ưu tiên**: DH1, DH2, DH3
- **Khối thi**: KT (A, A1, B, C, D1, ...)

### Dữ liệu đầu ra

File `processed_dulieuxettuyendaihoc.csv` chứa dữ liệu đã xử lý với các biến mới

## Cách Hoạt Động

### 1. Tải và Khám Phá Dữ Liệu

```python
df = pd.read_csv('dulieuxettuyendaihoc.csv', index_col="STT")
df.head()
df.info()
df.describe()
```

### 2. Xử Lý Giá Trị Thiếu

- Xử lý cột `DT` (Dân tộc): Thay thế giá trị thiếu bằng `0.0`
- Loại bỏ các dòng có giá trị thiếu ở các cột khác

### 3. Tạo Các Biến Phát Sinh

#### a) Điểm Trung Bình Môn (TBM)

Tính điểm trung bình môn cho 3 năm học (lớp 10, 11, 12):

```
TBM = (T×2 + L + H + S + V×2 + X + D + N) / 10
```

- `TBM1`: Điểm trung bình lớp 10
- `TBM2`: Điểm trung bình lớp 11
- `TBM3`: Điểm trung bình lớp 12

#### b) Xếp Loại Học Lực (XL)

Dựa trên điểm trung bình môn:

- **Y (Yếu)**: TBM < 5.0
- **TB (Trung bình)**: 5.0 ≤ TBM < 6.5
- **K (Khá)**: 6.5 ≤ TBM < 8.0
- **G (Giỏi)**: 8.0 ≤ TBM < 9.0
- **XS (Xuất sắc)**: TBM ≥ 9.0

#### c) Chuyển Đổi Thang Điểm (US_TBM)

Chuyển điểm từ thang 10 (Việt Nam) sang thang 4 (Mỹ) sử dụng **Min-Max Normalization**:

```
US_TBM = ((TBM - min(TBM)) / (max(TBM) - min(TBM))) × 4
```

#### d) Kết Quả Xét Tuyển (KQXT)

Tính điểm xét tuyển dựa trên khối thi:

- **Khối A, A1**: Score = (DH1×2 + DH2 + DH3) / 4
- **Khối B**: Score = (DH1 + DH2×2 + DH3) / 4
- **Khối khác**: Score = (DH1 + DH2 + DH3) / 3

**Kết quả**:

- `KQXT = 1`: Đậu (Score ≥ 5.0)
- `KQXT = 0`: Rớt (Score < 5.0)

### 4. Xuất Dữ Liệu Đã Xử Lý

```python
df.to_csv('processed_dulieuxettuyendaihoc.csv')
```

## Kết Quả

### Thống kê dữ liệu

- **Tổng số học sinh**: 100
- **Số cột dữ liệu gốc**: ~52 cột
- **Số cột sau xử lý**: ~65 cột (bao gồm các biến mới)

### Các biến mới được tạo

1. **TBM1, TBM2, TBM3**: Điểm trung bình môn 3 năm
2. **XL1, XL2, XL3**: Xếp loại học lực 3 năm
3. **US_TBM1, US_TBM2, US_TBM3**: Điểm chuẩn hóa theo thang 4
4. **KQXT**: Kết quả xét tuyển (Đậu/Rớt)

### Phân bố kết quả xét tuyển

- Số lượng học sinh **đậu** (`KQXT = 1`)
- Số lượng học sinh **rớt** (`KQXT = 0`)

## Hướng Dẫn Chạy

### Yêu cầu

```bash
pip install pandas numpy jupyter
```

### Chạy notebook

```bash
jupyter notebook Lab1.ipynb
```

### Thứ tự thực hiện

1. Chạy các cell theo thứ tự từ trên xuống
2. Đảm bảo file `dulieuxettuyendaihoc.csv` nằm cùng thư mục
3. Kết quả sẽ được lưu vào file `processed_dulieuxettuyendaihoc.csv`

## Ghi Chú

- Dữ liệu được xử lý hoàn toàn bằng Python và Pandas
- Tất cả các biến phái sinh được tính toán dựa trên quy tắc rõ ràng
- Phương pháp chuẩn hóa Min-Max đảm bảo dữ liệu nằm trong khoảng [0, 4]
- Kết quả xét tuyển được tính dựa trên công thức chính thức của các khối thi

## Người làm

Bùi Đăng Khoa-2374802013428
Lab1 - Nhập môn Phân tích Dữ liệu và Học Sâu

## Ngày Cập Nhật

January 2026
