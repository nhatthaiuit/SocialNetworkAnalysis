# Social Network Analysis - Author Collaborator Finder

## 📋 Mô tả dự án (Project Description)

Dự án phân tích mạng lưới cộng tác tác giả khoa học (Author Collaboration Network Analysis) sử dụng dữ liệu từ ArXiv. Mục tiêu là đề xuất các đồng tác giả tiềm năng trong một lĩnh vực nghiên cứu dựa trên:

- **Dataset**: ca-* collaboration graphs (e.g., ca-HepTh) từ Stanford Network Analysis Project
- **Goal**: Gợi ý các đồng tác giả tiềm năng (Suggest potential co-authors)
- **Methods**: 
  - Link prediction algorithms (Common Neighbors, Adamic-Adar, Resource Allocation, Preferential Attachment)
  - Community detection (Louvain algorithm)
  - Hybrid methods combining topology and community features
- **Deliverables**: Danh sách gợi ý + đường dẫn giải thích (suggestion list + justification paths)

## 📁 Cấu trúc thư mục (Project Structure)

```
SocialNetworkAnalysis/
├── Code/
│   ├── CleanData.ipynb      # Làm sạch và chuẩn hóa dữ liệu thô
│   ├── DataMining.ipynb     # Khai thác và phân tích dữ liệu
│   └── MainCode.ipynb       # Code chính: xây dựng mô hình và đánh giá
├── FinalDataset/
│   ├── authors.csv          # Danh sách tác giả
│   ├── papers.csv           # Danh sách bài báo
│   ├── paper_authors.csv    # Quan hệ bài báo - tác giả
│   └── coauthor_edges.csv   # Các cạnh đồng tác giả (edges)
├── RawData/                 # Dữ liệu gốc từ ArXiv
├── Report/                  # Báo cáo khoa học
├── Slide/                   # Slide thuyết trình
├── Link/                    # Link tới các tài nguyên như slide, report, code trên Google Colab
└── README.md               # File này

```

## 🔧 Yêu cầu hệ thống (Requirements)

### Python Version
- Python 3.7 trở lên

### Thư viện cần thiết (Required Libraries)
```bash
pandas
numpy
networkx
matplotlib
scikit-learn
python-louvain
gradio
```

## 📥 Hướng dẫn cài đặt (Installation Guide)

### Bước 1: Clone repository
```bash
git clone <repository-url>
cd SocialNetworkAnalysis
```

### Bước 2: Cài đặt thư viện
```bash
pip install pandas numpy networkx matplotlib scikit-learn python-louvain gradio
```

Hoặc nếu chạy trên **Google Colab**, chỉ cần chạy cell đầu tiên trong notebook:
```python
!pip install python-louvain gradio -q
```

## 🚀 Hướng dẫn chạy (How to Run)

### Phương án 1: Chạy trên Google Colab (Khuyến nghị)

1. Upload các file notebook trong thư mục `Code/` lên Google Colab
2. Upload thư mục `FinalDataset/` lên Colab hoặc mount Google Drive
3. Chạy các notebook theo thứ tự:

#### a) CleanData.ipynb
- **Mục đích**: Làm sạch dữ liệu thô từ ArXiv
- **Input**: Dữ liệu thô trong `RawData/`
- **Output**: Dữ liệu đã làm sạch trong `FinalDataset/`

#### b) DataMining.ipynb
- **Mục đích**: Khai thác và phân tích dữ liệu
- **Input**: Dữ liệu từ `FinalDataset/`
- **Output**: Các phân tích thống kê và visualization

#### c) MainCode.ipynb (Main Analysis)
- **Mục đích**: Xây dựng và đánh giá mô hình link prediction
- **Input**: `coauthor_edges.csv` và `authors.csv` từ `FinalDataset/`
- **Output**: 
  - Kết quả đánh giá các thuật toán (AUC, AP scores)
  - Giao diện Gradio để gợi ý đồng tác giả

**Lưu ý quan trọng**: Đảm bảo đường dẫn đến file CSV đúng:
```python
df_edges = pd.read_csv("coauthor_edges.csv")
df_authors = pd.read_csv("authors.csv")
```

Nếu file nằm trong thư mục khác, cập nhật đường dẫn:
```python
df_edges = pd.read_csv("FinalDataset/coauthor_edges.csv")
df_authors = pd.read_csv("FinalDataset/authors.csv")
```

### Phương án 2: Chạy trên Jupyter Notebook (Local)

1. Mở terminal/command prompt
2. Di chuyển đến thư mục dự án:
```bash
cd /Users/tuongvi2407/SocialNetworkAnalysis
```

3. Khởi động Jupyter Notebook:
```bash
jupyter notebook
```

4. Mở và chạy các notebook trong thư mục `Code/` theo thứ tự như trên

### Phương án 3: Chạy từng cell trong notebook

Trong `MainCode.ipynb`, chạy các cell theo thứ tự:

1. **Cell 1**: Cài đặt thư viện
2. **Cell 2**: Load dữ liệu và kiểm tra
3. **Cell 3**: Xây dựng đồ thị và thống kê cơ bản
4. **Cell 4**: Chia dữ liệu train/test theo thời gian (temporal split)
5. **Cell 5-6**: Định nghĩa các hàm đánh giá và thuật toán
6. **Cell 7**: Phát hiện community bằng Louvain
7. **Cell 8**: Tạo hybrid methods
8. **Cell 9**: Đánh giá các phương pháp cơ bản
9. **Cell 10**: Đánh giá các phương pháp hybrid
10. **Các cell tiếp theo**: Visualization và Gradio interface

## 📊 Kết quả mong đợi (Expected Results)

Sau khi chạy `MainCode.ipynb`, bạn sẽ thấy:

### 1. Thống kê đồ thị (Graph Statistics)
```
Nodes: 13003
Edges: 23847
Avg degree: 3.67
Connected components: 2158
Global clustering coefficient: 0.24
```

### 2. Kết quả đánh giá Link Prediction
```
Method      AUC     AP
CN          0.5209  0.5205
AA          0.5209  0.5209
RA          0.5209  0.5208
PA          0.1942  0.4991
Louvain     0.5256  0.5213
```

### 3. Kết quả Hybrid Methods
```
Method      AUC     AP
HYB_CN      0.5301  0.5294
HYB_AA      0.5301  0.5296
HYB_RA      0.5301  0.5296
HYB_PA      0.1962  0.5006
```

### 4. Giao diện Gradio
- Giao diện web để nhập tên tác giả và nhận gợi ý đồng tác giả tiềm năng

## 🔍 Giải thích các phương pháp (Methods Explanation)

- **CN (Common Neighbors)**: Số lượng hàng xóm chung
- **AA (Adamic-Adar)**: Trọng số hàng xóm chung theo độ hiếm
- **RA (Resource Allocation)**: Phân bổ tài nguyên qua hàng xóm chung
- **PA (Preferential Attachment)**: Tích số bậc của hai node
- **Louvain**: Phát hiện community và gợi ý trong cùng community
- **HYB_X**: Kết hợp phương pháp X với thông tin community

## 📚 Tài liệu tham khảo (References)

- Stanford Network Analysis Data: https://snap.stanford.edu/data
- Dataset: ca-HepTh (High Energy Physics - Theory collaboration network)

## 👥 Tác giả (Authors)

- Ha Nhat Thai - Nguyen Khanh Tuan
- Project: Social Network Analysis - Author Collaborator Finder

## 📝 Lưu ý (Notes)

- Dữ liệu được chia theo thời gian: train (≤ 1998), test (> 1998)
- Có thể điều chỉnh `SPLIT_YEAR` trong code để thay đổi cách chia dữ liệu
- Tham số `alpha` trong hybrid methods có thể điều chỉnh để cân bằng giữa topology và community features

---

**Last Updated**: January 2026
