# Phân loại nguy cơ Ung thư Cổ tử cung bằng Học Máy (Cervical Cancer Prediction)

## Tổng quan

Dự án được thực hiện trong khuôn khổ bài tập lớn môn Học Máy [Mã môn học - Tên Trường], nhằm xây dựng mô hình học máy để dự đoán nguy cơ mắc ung thư cổ tử cung (Nhãn 0 - Khỏe mạnh, Nhãn 1 - Có dấu hiệu) dựa trên các yếu tố rủi ro. Các bước chính trong dự án bao gồm:

* **Tiền xử lý dữ liệu:** Xử lý giá trị thiếu (thay `?` bằng `NaN`, điền bằng trung vị), chuẩn hóa dữ liệu (StandardScaler) và đặc biệt sử dụng **SMOTE** để giải quyết triệt để vấn đề mất cân bằng dữ liệu giữa hai lớp.
* **Giảm chiều dữ liệu:** Áp dụng PCA (giữ 95% phương sai, giảm còn 18 chiều) và LDA (giảm xuống 1 chiều) để trích xuất đặc trưng và trực quan hóa.
* **Mô hình phân loại:** Sử dụng tìm kiếm lưới (Grid Search) với Cross-Validation để tối ưu hóa:
    * **K-Nearest Neighbors (KNN):** Tìm được K=3 tối ưu.
    * **Logistic Regression:** Tìm được C=10, solver='liblinear'.
* **Đánh giá:** Đánh giá chéo hiệu suất của 2 mô hình trên 3 không gian dữ liệu (Gốc, PCA, LDA). Tập trung phân tích vào chỉ số **Recall (Độ nhạy)** vì đây là chỉ số quan trọng nhất trong sàng lọc y tế.
* **Kết quả:** Logistic Regression kết hợp không gian LDA cho hiệu năng tốt nhất (Accuracy: 94.2%, Recall lớp bệnh: 82%, F1-Score: 0.65).

## Dữ liệu: Cervical Cancer (Risk Factors) Data Set

Bộ dữ liệu Cervical Cancer Risk Factors được thu thập tại Bệnh viện Đại học Caracas (Venezuela). Tập dữ liệu bao gồm 858 bệnh nhân với 36 thuộc tính là các đặc trưng về nhân khẩu học, thói quen sinh hoạt (hút thuốc), tiền sử bệnh lý (STDs) và các phương pháp tránh thai. Biến mục tiêu được sử dụng để phân loại là kết quả sinh thiết (`Biopsy`).

* Thông tin chi tiết và tải dataset gốc tại: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/383/cervical+cancer+risk+factors)

## Thông tin thêm

* **Giảng viên hướng dẫn:** Cao Văn Chung
* **Sinh viên thực hiện:**
    * Nguyễn Thị Ngọc Hân - 23000118
    * Lại Thị Huế - 23000122
    * Mẫn Thị Ngân An - 23000088

* **Phân chia công việc:**
    * Tiền xử lý dữ liệu, xây dựng mô hình Logistic Regression, blàm slide báo cáo: **Mẫn Thị Ngân An**
    * Viết báo cáo, tổng hợp nội dung, Làm slide, Xây dựng mô hình KNN: **Nguyễn Thị Ngọc Hân**
    * Cài đặt thuật toán PCA, LDA và trực quan hóa dữ liệu: **Lại Thị Huế**
## Cấu trúc thư mục

```text
project/
├── src/                    # Mã nguồn
│   └── main_model.ipynb    # Mã nguồn đầy đủ của dự án (chạy trên Jupyter/Colab)
├── data/                   # Thư mục dữ liệu 
│   └── risk_factors_cervical_cancer.csv # Dữ liệu gốc
├── results/                # Kết quả thực nghiệm
│   └── figures/            # Các biểu đồ trực quan hóa
│       ├── pca_2d.jpg      # Biểu đồ phân tán PCA
│       └── lda_1d.png      # Biểu đồ phân tách LDA
├── docs/                   # Tài liệu nộp
│   ├── report.pdf          # Báo cáo tiểu luận chi tiết (3 chương)
│   └── Huong_dan.docx      # Tổ chức nhân sự và kịch bản thực nghiệm
├── requirements.txt        # Danh sách thư viện cần thiết
├── README.md               # Hướng dẫn tổng quan
└── .gitignore              # Tệp bỏ qua các tệp không cần đẩy lên GitHub
