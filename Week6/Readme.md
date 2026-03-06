Fashion MNIST Classification with PyTorch

Dự án này minh họa cách xây dựng và huấn luyện một mạng nơ-ron đơn giản bằng PyTorch để phân loại hình ảnh trong tập dữ liệu Fashion MNIST.

Notebook thực hiện nhiều thí nghiệm để đánh giá ảnh hưởng của các siêu tham số (hyperparameters) như:

Batch size

Optimizer (SGD và Adam)

Learning rate

đến hiệu suất của mô hình.

Công Nghệ Sử Dụng

Python: Ngôn ngữ lập trình chính.

PyTorch: Framework Deep Learning dùng để xây dựng và huấn luyện mạng nơ-ron.

torchvision: Thư viện hỗ trợ các tác vụ Computer Vision trong PyTorch, dùng để tải dataset Fashion MNIST.

NumPy: Thư viện tính toán số học và xử lý mảng.

Matplotlib: Dùng để trực quan hóa kết quả huấn luyện.

Google Colab: Môi trường chạy notebook, hỗ trợ GPU để tăng tốc quá trình training.

Cách Hoạt Động
1. Tải và Tiền Xử Lý Dữ Liệu

Tập dữ liệu Fashion MNIST được tải bằng:

torchvision.datasets.FashionMNIST

Mỗi ảnh có kích thước 28x28 pixel.
Trước khi đưa vào mô hình, ảnh được:

Chuyển thành tensor

Làm phẳng từ 28×28 → 784

Trong một số thí nghiệm, giá trị pixel được chuẩn hóa bằng cách chia cho 255

2. Dataset và DataLoader

Một class FMNISTDataset được tạo để:

Lấy dữ liệu ảnh

Lấy nhãn tương ứng

DataLoader được sử dụng để:

Chia dữ liệu thành batch

Duyệt dữ liệu trong quá trình training và validation

3. Xây Dựng Mô Hình

Mô hình là một Feed Forward Neural Network đơn giản được định nghĩa bằng:

torch.nn.Sequential

Cấu trúc mạng gồm:

Layer 1: Linear (784 → 1000)

Activation: ReLU

Layer 2: Linear (1000 → 10)

Trong đó 10 là số lớp phân loại của Fashion MNIST.

4. Hàm Loss và Optimizer

Loss Function

nn.CrossEntropyLoss

Phù hợp cho bài toán phân loại nhiều lớp.

Optimizers

Sử dụng hai thuật toán tối ưu:

torch.optim.SGD

torch.optim.Adam

5. Vòng Lặp Huấn Luyện (Training Loop)

Quá trình training được thực hiện qua nhiều epochs.

Trong mỗi epoch:

Dữ liệu được chia thành các batch

Batch được đưa qua mô hình

Hàm train_batch thực hiện:

Tính loss

Backpropagation

Cập nhật trọng số

Hàm accuracy tính tỷ lệ dự đoán đúng

6. Validation

Một tập validation được sử dụng để:

Đánh giá mô hình trên dữ liệu chưa từng thấy

Kiểm tra khả năng generalization của mô hình

7. Trực Quan Hóa Kết Quả

Các chỉ số sau được vẽ bằng matplotlib:

Training loss

Validation loss

Training accuracy

Validation accuracy
