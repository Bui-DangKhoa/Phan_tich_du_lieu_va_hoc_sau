1. Công nghệ sử dụng
Ngôn ngữ: Python
Thư viện chính:
nltk (Natural Language Toolkit): Thư viện chính để xử lý ngôn ngữ tự nhiên, tách từ, loại bỏ stop words, và huấn luyện mô hình phân loại.
BeautifulSoup (bs4): Sử dụng để bóc tách nội dung văn bản từ các định dạng HTML.
urllib: Dùng để tải dữ liệu từ các URL (Project Gutenberg, BBC News).
random & string: Hỗ trợ xử lý dữ liệu và xáo trộn tập tin.
2. Cách hoạt động
Quy trình xử lý trong notebook bao gồm các bước chính sau:

A. Thu thập và Tiền xử lý dữ liệu
Dữ liệu mẫu: Sử dụng các tác phẩm từ kho lưu trữ gutenberg (như Macbeth) và dữ liệu từ web.
Tokenization: Chia văn bản thành danh sách các từ hoặc câu.
Lọc dữ liệu: Loại bỏ dấu câu và các từ dừng (stop words) để tập trung vào các từ mang ý nghĩa nội dung.
B. Phân tích thống kê
Tần suất từ (Frequency Distribution): Xác định các từ xuất hiện nhiều nhất.
N-grams: Tìm kiếm các cặp từ (bigrams) hoặc nhóm 3 từ (trigrams) thường đi cùng nhau.
Concordance & Similarity: Tìm kiếm ngữ cảnh xuất hiện của từ và các từ có cách sử dụng tương tự.
C. Phân loại cảm xúc (Sentiment Analysis)
Dataset: Sử dụng kho ngữ liệu movie_reviews.
Trích xuất đặc trưng (Feature Extraction): Xây dựng bộ đặc trưng dựa trên sự xuất hiện của các từ phổ biến trong văn bản.
Huấn luyện mô hình: Sử dụng thuật toán NaiveBayesClassifier để học cách phân biệt đánh giá tích cực (pos) và tiêu cực (neg).
Đánh giá: Tính toán độ chính xác của mô hình trên tập kiểm thử và hiển thị các đặc trưng có sức ảnh hưởng lớn nhất (Most Informative Features).
