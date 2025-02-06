# README: So sánh PCA, t-SNE, UMAP, DBSCAN, HDBSCAN và K-Means

## 1. So sánh t-SNE, UMAP và PCA

### 1.1 PCA (Principal Component Analysis)
- **Mục đích:** Giảm chiều tuyến tính, giữ lại nhiều phương sai nhất.
- **Cách hoạt động:**
  - Tính ma trận hiệp phương sai.
  - Tìm vector riêng và giá trị riêng.
  - Chuyển đổi dữ liệu theo trục chính.
- **Kết quả:** Biểu diễn dữ liệu trong không gian ít chiều hơn.
- **Ưu điểm:**
  - Nhanh, đơn giản.
  - Bảo toàn cấu trúc tuyến tính.
- **Nhược điểm:**
  - Không bảo toàn tốt cấu trúc phi tuyến.
  - Chỉ hữu dụng khi cấu trúc dữ liệu tuyến tính.

### 1.2 t-SNE (t-Distributed Stochastic Neighbor Embedding)
- **Mục đích:** Giảm chiều phi tuyến, bảo toàn cấu trúc cục bộ.
- **Cách hoạt động:**
  - Xây dựng phân phối xác suất giữa các điểm.
  - Tối ưu hóa sự khác biệt giữa hai phân phối.
- **Kết quả:** Giữ lại sự tương đồng cục bộ giữa các điểm.
- **Ưu điểm:**
  - Hiển thị tốt các cụm dữ liệu.
  - Giúp phát hiện cấu trúc ngầm trong dữ liệu phức tạp.
- **Nhược điểm:**
  - Chậm, không ổn định.
  - Không bảo toàn cấu trúc tổng thể.

### 1.3 UMAP (Uniform Manifold Approximation and Projection)
- **Mục đích:** Tương tự t-SNE, nhưng nhanh hơn và bảo toàn cả cấu trúc cục bộ và tổng thể.
- **Cách hoạt động:**
  - Xây dựng đồ thị quan hệ cục bộ.
  - Giảm chiều dựa trên nhúng đa tạp.
- **Kết quả:** Giữ lại cả cấu trúc cục bộ và tổng thể.
- **Ưu điểm:**
  - Nhanh hơn t-SNE.
  - Kết quả ổn định.
  - Có thể áp dụng cho dữ liệu lớn.
- **Nhược điểm:**
  - Phức tạp hơn PCA.
  - Cần điều chỉnh tham số phù hợp.

---

## 2. So sánh DBSCAN, HDBSCAN và K-Means

| Thuật toán  | Loại cụm                 | Xử lý dữ liệu nhiễu | Cần số cụm trước | Độ phức tạp | Ứng dụng phù hợp |
|------------|-------------------------|----------------------|-----------------|-------------|-----------------|
| K-Means   | Hình cầu (centroid-based) | Nhạy cảm với nhiễu   | ✅ Cần số cụm k  | O(nk)       | Dữ liệu có cấu trúc rõ ràng, cụm kích thước tương đồng |
| DBSCAN    | Mật độ (density-based)    | ✅ Tốt với dữ liệu nhiễu | ❌ Không cần số cụm trước | O(n log n) | Phát hiện cụm phi tuyến, dữ liệu có nhiễu |
| HDBSCAN   | Mật độ phân cấp           | ✅ Tốt hơn DBSCAN với dữ liệu nhiễu | ❌ Không cần số cụm trước | O(n log n) | Cụm phức tạp, tự động chọn số cụm, phát hiện outlier tốt hơn DBSCAN |

### 2.1 K-Means
- **Cách hoạt động:**
  - Chọn k tâm cụm ngẫu nhiên.
  - Gán mỗi điểm vào cụm gần nhất.
  - Cập nhật tâm cụm bằng trung bình các điểm trong cụm.
  - Lặp lại đến khi hội tụ.
- **Ưu điểm:**
  - Đơn giản, nhanh, dễ triển khai.
  - Hiệu quả trên dữ liệu lớn có cụm hình cầu.
- **Nhược điểm:**
  - Phải chọn trước số cụm k.
  - Không hoạt động tốt với cụm có hình dạng phức tạp.
  - Nhạy cảm với outlier.

### 2.2 DBSCAN (Density-Based Spatial Clustering of Applications with Noise)
- **Cách hoạt động:**
  - Xác định điểm lõi (core point) dựa trên số điểm lân cận trong bán kính ε.
  - Kết nối điểm lõi với điểm lân cận để tạo cụm.
  - Điểm nhiễu (outlier) không thuộc cụm nào.
- **Ưu điểm:**
  - Không cần chọn số cụm trước.
  - Xử lý tốt dữ liệu nhiễu và cụm có hình dạng bất kỳ.
- **Nhược điểm:**
  - Nhạy cảm với tham số ε và minPts.
  - Không hoạt động tốt khi mật độ cụm không đồng đều.

### 2.3 HDBSCAN (Hierarchical DBSCAN)
- **Cách hoạt động:**
  - Mở rộng DBSCAN bằng cách xây dựng cây phân cấp theo mật độ.
  - Tự động chọn số cụm tối ưu dựa trên phân cấp.
- **Ưu điểm:**
  - Xử lý dữ liệu có mật độ cụm không đồng đều tốt hơn DBSCAN.
  - Tự động chọn số cụm.
  - Phát hiện outlier tốt hơn.
- **Nhược điểm:**
  - Chậm hơn DBSCAN trên dữ liệu lớn.

### 2.4 Khi nào dùng thuật toán nào?
- **Dùng K-Means** khi dữ liệu có cụm hình cầu và bạn biết trước số cụm.
- **Dùng DBSCAN** khi dữ liệu có nhiễu và cụm có hình dạng bất kỳ.
- **Dùng HDBSCAN** nếu dữ liệu có mật độ không đồng đều và bạn muốn số cụm tự động được xác định.

Nếu bạn có dữ liệu phức tạp, **HDBSCAN** thường là lựa chọn tốt nhất do khả năng tự động xác định số cụm và xử lý nhiễu tốt hơn.

