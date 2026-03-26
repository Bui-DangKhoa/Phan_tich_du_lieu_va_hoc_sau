Phân loại rác thải bằng ResNet18 và PyTorch
Dự án này trình bày một giải pháp phân loại hình ảnh rác thải bằng cách sử dụng mô hình học sâu ResNet18 với thư viện PyTorch.
Công nghệ sử dụng
Các công nghệ và thư viện chính được sử dụng trong dự án này bao gồm:

Python: Ngôn ngữ lập trình chính.
PyTorch: Framework học sâu cho việc xây dựng và huấn luyện mô hình.
torchvision: Gói của PyTorch cung cấp các bộ dữ liệu, mô hình và biến đổi hình ảnh phổ biến.
ResNet18: Một kiến trúc mạng nơ-ron tích chập (CNN) được sử dụng làm mô hình nền tảng (backbone) đã được huấn luyện trước trên tập dữ liệu ImageNet.
Kagglehub: Để tải và quản lý tập dữ liệu.
Matplotlib: Để trực quan hóa hình ảnh và kết quả.
Numpy: Để xử lý số học và các phép toán trên mảng.
Optimizer AdamW: Thuật toán tối ưu hóa được sử dụng để điều chỉnh trọng số của mô hình.
CosineAnnealingLR: Lịch trình điều chỉnh tốc độ học (learning rate scheduler) giúp cải thiện hiệu suất huấn luyện.
Mixed Precision Training: Sử dụng torch.cuda.amp.autocast và GradScaler để huấn luyện nhanh hơn và hiệu quả hơn về bộ nhớ trên GPU.
Cách hoạt động
Giải pháp này tuân theo một quy trình học sâu tiêu chuẩn cho phân loại hình ảnh:

Tải và tiền xử lý tập dữ liệu: Tập dữ liệu phân loại rác thải được tải xuống từ Kaggle. Các biến đổi hình ảnh được áp dụng, bao gồm thay đổi kích thước ngẫu nhiên, lật ngang, nhiễu màu, xoay ngẫu nhiên và chuẩn hóa để tăng cường dữ liệu và chuẩn bị cho mô hình.

Tạo Dataloader cân bằng: Tập dữ liệu được chia thành tập huấn luyện và tập kiểm tra. Để giải quyết vấn đề mất cân bằng lớp (nếu có), WeightedRandomSampler được sử dụng trong DataLoader của tập huấn luyện, đảm bảo các lớp ít gặp hơn cũng được lấy mẫu đủ.

Thiết lập mô hình: Một mô hình ResNet18 đã được huấn luyện trước (trên ImageNet) được khởi tạo. Các lớp đầu tiên của mô hình được đóng băng để sử dụng các tính năng học được, trong khi lớp cuối cùng (fc) được thay thế bằng một lớp tuyến tính mới để phù hợp với số lượng lớp phân loại rác thải cụ thể của tập dữ liệu này. Mô hình được chuyển đến thiết bị GPU (nếu có).

Cấu hình Huấn luyện: Hàm mất mát CrossEntropyLoss được chọn để phân loại đa lớp. Bộ tối ưu hóa AdamW với tốc độ học và giảm trọng số cụ thể được cấu hình để chỉ cập nhật các tham số không bị đóng băng. CosineAnnealingLR được sử dụng để điều chỉnh tốc độ học trong quá trình huấn luyện. GradScaler được sử dụng cho huấn luyện độ chính xác hỗn hợp để tăng tốc độ và giảm mức sử dụng bộ nhớ.

Vòng lặp huấn luyện và đánh giá: Mô hình được huấn luyện trong một số epoch đã định. Trong mỗi epoch:

Mô hình được đặt ở chế độ huấn luyện (model.train()).
Dữ liệu được tải theo lô thông qua train_loader.
Lan truyền tiến (forward pass) được thực hiện với autocast để tận dụng huấn luyện độ chính xác hỗn hợp.
Mất mát được tính toán và lan truyền ngược (backward pass) được thực hiện, sau đó bộ tối ưu hóa cập nhật trọng số.
Sau mỗi epoch, tốc độ học được điều chỉnh bằng bộ lập lịch.
Mô hình được đánh giá trên test_loader bằng cách sử dụng độ chính xác để theo dõi hiệu suất. Kết quả mất mát huấn luyện và độ chính xác kiểm tra được in ra cho mỗi epoch.
