* Phân cụm đơn giản có nghĩa là gán các điểm dữ liệu cho các nhóm dựa trên mức độ tương tự của các điểm với nhau. Có thể nói, một thuật toán phân cụm làm cho "những con chim cùng lông có thể tụ tập lại với nhau".

Ví dụ: khi được sử dụng cho feature engineering, chúng tôi có thể cố gắng khám phá các nhóm khách hàng đại diện cho một phân khúc thị trường hoặc các khu vực địa lý có chung kiểu thời tiết tương tự. Việc thêm tính năng của nhãn cụm có thể giúp các mô hình học máy gỡ rối các mối quan hệ phức tạp về không gian hoặc khoảng cách.

## Cluster Labels as a Feature
* Được áp dụng cho một đối tượng có giá trị thực duy nhất, việc phân cụm hoạt động giống như một phép biến đổi "tạo nhóm" hoặc "rời rạc" truyền thống. Trên nhiều tính năng, nó giống như "tạo nhóm đa chiều" (đôi khi được gọi là lượng tử hóa vectơ)
![alt text](.\img\image.png)
 
Ví dụ : phân cụm một tính năng bên trái , và nhiều tính năng bên phải 

| Longitude | Latitude | Cluster |
|-----------|----------|---------|
| -93.619   | 42.054   |    3    |
| -93.619   | 42.053   |    3    |
| -93.638   | 42.060   |    1    |
| -93.602   | 41.988   |    0    |

Điều quan trọng cần nhớ là tính năng Cụm này mang tính phân loại. Ở đây, nó được hiển thị với mã hóa nhãn (nghĩa là dưới dạng một chuỗi các số nguyên) như một thuật toán phân cụm thông thường sẽ tạo ra; tùy thuộc vào kiểu máy của bạn, mã hóa một nóng có thể phù hợp hơn.

Ý tưởng thúc đẩy việc thêm nhãn cụm là các cụm sẽ chia nhỏ các mối quan hệ phức tạp giữa các tính năng thành các phần đơn giản hơn. Sau đó, mô hình của chúng tôi có thể học từng phần đơn giản hơn thay vì phải học toàn bộ phần phức tạp cùng một lúc. Đó là chiến lược “chia để trị”.
![alt text](.\img\image-1.png) 
Clustering the YearBuilt feature helps this linear model learn its relationship to SalePrice.
Hình này cho thấy cách phân cụm có thể cải thiện một mô hình tuyến tính đơn giản. Mối quan hệ cong giữa YearBuilt và SalePrice quá phức tạp đối với loại mô hình này -- nó không phù hợp. Tuy nhiên, trên các phần nhỏ hơn, mối quan hệ gần như tuyến tính và mô hình có thể học dễ dàng.
## k-Means Clustering
 * Phân cụm K-mean đo lường độ tương tự bằng cách sử dụng khoảng cách đường thẳng thông thường (nói cách khác là khoảng cách Euclide). Nó tạo ra các cụm bằng cách đặt một số điểm, gọi là trọng tâm, bên trong không gian đặc trưng. Mỗi điểm trong tập dữ liệu được gán cho cụm của bất kỳ tâm nào gần nhất với nó. "k" trong "k-means" là số lượng centroid (nghĩa là cụm) mà nó tạo ra. Bạn tự xác định k.  

![alt text](.\img\image-2.png)

Bạn có thể tưởng tượng mỗi tâm điểm chụp các điểm thông qua một chuỗi các vòng tròn tỏa ra. Khi tập hợp các vòng tròn từ các tâm cạnh tranh chồng lên nhau, chúng sẽ tạo thành một đường thẳng. Kết quả là cái được gọi là Tessall Voronoi. Tessallation cho bạn biết dữ liệu trong tương lai sẽ được chỉ định theo cụm nào; tessallation về cơ bản là những gì k-mean học được từ dữ liệu huấn luyện của nó.

Việc phân cụm trên tập dữ liệu Ames ở trên là phân cụm k-means. Đây là 
hình tương tự với tesallation và centroid được hiển thị.

![alt text](.\img\image-3.png)
 
Hãy xem xét cách thuật toán k-means tìm hiểu các cụm và điều đó có ý nghĩa gì đối với kỹ thuật tính năng. Chúng ta sẽ tập trung vào ba tham số trong quá trình triển khai scikit-learn: n_clusters, max_iter và n_init.

Đó là một quá trình hai bước đơn giản. Thuật toán bắt đầu bằng cách khởi tạo ngẫu nhiên một số số (n_clusters) centroid được xác định trước. Sau đó nó lặp lại hai thao tác sau:

1.gán điểm cho tâm cụm gần nhất

![alt text](.\img\image-4.png)

2.di chuyển từng tâm để giảm thiểu khoảng cách đến các điểm của nó

![alt text](.\img\image-5.png)

Nó lặp lại hai bước này cho đến khi trọng tâm không di chuyển nữa hoặc cho đến khi vượt qua số lần lặp tối đa (max_iter).

Điều thường xảy ra là vị trí ngẫu nhiên ban đầu của các tâm kết thúc ở một cụm kém. Vì lý do này, thuật toán lặp lại một số lần (n_init) và trả về phân cụm có tổng khoảng cách nhỏ nhất giữa mỗi điểm và trọng tâm của nó, phân cụm tối ưu.

Hoạt ảnh dưới đây cho thấy thuật toán đang hoạt động. Nó minh họa sự phụ thuộc của kết quả vào trọng tâm ban đầu và tầm quan trọng của việc lặp lại cho đến khi hội tụ.
 
![alt text](.\img\image-6.png)

Bạn có thể cần tăng max_iter cho số lượng lớn cụm hoặc n_init cho tập dữ liệu phức tạp. Thông thường, tham số duy nhất bạn cần tự chọn là n_clusters (nghĩa là k). Cách phân vùng tốt nhất cho một tập hợp các tính năng tùy thuộc vào kiểu máy bạn đang sử dụng và những gì bạn đang cố gắng dự đoán, vì vậy tốt nhất bạn nên điều chỉnh nó giống như bất kỳ siêu tham số nào (chẳng hạn như thông qua xác thực chéo).


