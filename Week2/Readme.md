# Lab 2 - Phân tích dữ liệu xét tuyển đại học

## Mô tả

Dự án phân tích và khám phá dữ liệu (EDA) về thông tin xét tuyển đại học của sinh viên, bao gồm điểm các môn học, giới tính, khu vực, đối tượng ưu tiên và kết quả xét tuyển.

---

## Công nghệ sử dụng

| Công nghệ            | Phiên bản | Mục đích                                          |
| -------------------- | --------- | ------------------------------------------------- |
| **Python**           | 3.x       | Ngôn ngữ lập trình chính                          |
| **Pandas**           | -         | Xử lý và phân tích dữ liệu dạng bảng              |
| **NumPy**            | -         | Tính toán số học và xử lý mảng                    |
| **Matplotlib**       | -         | Trực quan hóa dữ liệu (biểu đồ cột, biểu đồ tròn) |
| **Seaborn**          | -         | Trực quan hóa dữ liệu nâng cao                    |
| **SciPy**            | -         | Tính toán thống kê (Skewness, Kurtosis)           |
| **Jupyter Notebook** | -         | Môi trường phát triển tương tác                   |

---

## Cách hoạt động

### 1. Tải và đọc dữ liệu

- Đọc file CSV `processed_dulieuxettuyendaihoc.csv` chứa thông tin xét tuyển đại học
- Dữ liệu bao gồm các cột: STT, điểm các môn (T1, L1, H1, S1, V1, X1, D1, N1, T2,...), TBM1, TBM2, TBM3, GT (Giới tính), KV (Khu vực), DT (Đối tượng), DH1, DH2, DH3 (Điểm đại học)

### 2. Phân tích thống kê mô tả

- Tính các chỉ số thống kê: count, sum, mean, median, min, max, std (độ lệch chuẩn)
- Tính các phân vị (Q1, Q2, Q3)
- Phân tích theo nhóm (groupby) dựa trên giới tính, khu vực, đối tượng

### 3. Phân tích phân phối dữ liệu

- Tính độ lệch (Skewness) để đánh giá sự đối xứng của phân phối
- Tính độ nhọn (Kurtosis) để đánh giá hình dạng phân phối
- Sử dụng thư viện `scipy.stats` cho các phép tính thống kê nâng cao

### 4. Trực quan hóa dữ liệu

- **Biểu đồ cột (Bar Chart)**: So sánh số lượng theo giới tính, khu vực, đối tượng
- **Biểu đồ tròn (Pie Chart)**: Thể hiện tỷ lệ phần trăm các nhóm
- **Biểu đồ phân tích kết quả xét tuyển**: So sánh kết quả theo khu vực và khối thi

### 5. Phân tích đa chiều

- Pivot table để phân tích chéo giữa các biến
- So sánh kết quả xét tuyển theo khu vực (KV) và khối thi (KT)
- Phân tích tương quan giữa điểm số và kết quả xét tuyển

---

## Kết quả

### Phân tích thống kê cơ bản

- **Phân phối điểm T1**:
  - Mean: ~5.85
  - Min: 2.4, Max: 9.3
  - Độ lệch (Skewness): -0.1782 (hơi lệch trái)
  - Độ nhọn (Kurtosis): -0.4801 (phân phối hơi phẳng)

### Phân tích theo nhóm

- Thống kê số lượng sinh viên theo giới tính (GT)
- Phân bố sinh viên nam theo đối tượng ưu tiên (DT)
- Phân tích sinh viên theo khu vực (KV)

### Trực quan hóa

- Biểu đồ cột và biểu đồ tròn thể hiện phân bố theo giới tính
- Biểu đồ so sánh kết quả xét tuyển giữa các khu vực
- Biểu đồ phân tích mối quan hệ giữa khối thi và kết quả

### Bảng thống kê đa chiều

- Pivot table phân tích theo KV, DT với các chỉ số: count, sum, mean, median, min, max, std, Q1, Q2, Q3
- So sánh điểm trung bình và kết quả xét tuyển giữa các nhóm

---

## Cấu trúc thư mục

```
Lab2/
├── Lab2.ipynb                           # Jupyter Notebook chính
├── processed_dulieuxettuyendaihoc.csv   # Dữ liệu đã xử lý
└── README.md                            # File hướng dẫn
```

---

## Hướng dẫn chạy

1. Cài đặt các thư viện cần thiết:

```bash
pip install pandas numpy matplotlib seaborn scipy
```

2. Mở Jupyter Notebook:

```bash
jupyter notebook Lab2.ipynb
```

3. Chạy từng cell theo thứ tự để xem kết quả phân tích

---

## Ghi chú

- Dữ liệu đã được tiền xử lý (processed) trước khi phân tích
- Các biểu đồ được tạo bằng Matplotlib với kích thước phù hợp để hiển thị rõ ràng
- Kết quả phân tích có thể được sử dụng để đưa ra các quyết định về chính sách tuyển sinh
