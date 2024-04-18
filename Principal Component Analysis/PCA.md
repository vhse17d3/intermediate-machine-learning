# Principal Component Analysis

* Các feature vectors trong các bài toán thực tế có thể có số chiều rất lớn, tới vài nghìn. Ngoài ra, số lượng các điểm dữ liệu cũng thường rất lớn. Nếu thực hiện lưu trữ và tính toán trực tiếp trên dữ liệu có số chiều cao này thì sẽ gặp khó khăn cả về việc lưu trữ và tốc độ tính toán. Vì vậy, giảm số chiều dữ liệu là một bước quan trọng trong nhiều bài toán. Đây cũng được coi là một phương pháp nén dữ liệu.

Phân tích thành phần chính (PCA). Giống như phân cụm là phân vùng tập dữ liệu dựa trên mức độ gần nhau, bạn có thể coi PCA là phân vùng của biến thể trong dữ liệu. PCA là một công cụ tuyệt vời giúp bạn khám phá các mối quan hệ quan trọng trong dữ liệu và cũng có thể được sử dụng để tạo ra nhiều tính năng mang tính thông tin hơn.

(Lưu ý kỹ thuật: PCA thường được áp dụng cho dữ liệu được tiêu chuẩn hóa. Với dữ liệu được tiêu chuẩn hóa, "biến thể" có nghĩa là "tương quan". Với dữ liệu không được tiêu chuẩn hóa, "biến thể" có nghĩa là "hiệp phương sai". Tất cả dữ liệu trong khóa học này sẽ được tiêu chuẩn hóa trước khi áp dụng PCA.)
#### Principal Component Analysis
* Trong bộ dữ liệu Abalone là các phép đo vật lý được lấy từ hàng nghìn con bào ngư Tasmania. (Bào ngư là một sinh vật biển giống như nghêu hoặc hàu.) Bây giờ chúng ta sẽ chỉ xem xét một số đặc điểm: 'Height' and 'Diameter'(chiều cao và đường kính ) của vỏ của chúng. 

Bạn có thể tưởng tượng rằng trong dữ liệu này có các "trục biến thiên" mô tả cách bào ngư có xu hướng khác nhau. Về mặt hình ảnh, các trục này xuất hiện dưới dạng các đường vuông góc chạy dọc theo các kích thước tự nhiên của dữ liệu, một trục cho mỗi đặc điểm ban đầu.
 
![alt text](.\img\image.png)

Thông thường, chúng ta có thể đặt tên cho các trục biến thiên này. Trục dài hơn mà chúng ta có thể gọi là thành phần " Size": chiều cao nhỏ và đường kính nhỏ (phía dưới bên trái) tương phản với chiều cao lớn và đường kính lớn (phía trên bên phải). Trục ngắn hơn chúng ta có thể gọi là thành phần " Shape": chiều cao nhỏ và đường kính lớn (hình phẳng) tương phản với chiều cao lớn và đường kính nhỏ (hình tròn).

Lưu ý rằng thay vì mô tả bào ngư bằng ‘Height' and 'Diameter', chúng ta cũng có thể mô tả chúng bằng 'Size' and 'Shape' .Trên thực tế, đây là toàn bộ ý tưởng của PCA: thay vì mô tả dữ liệu bằng các đặc điểm ban đầu, chúng tôi mô tả dữ liệu bằng các trục biến đổi của nó. Các trục biến đổi trở thành các tính năng mới. 

![alt text](.\img\image-1.png)

The principal components become the new features by a rotation of the dataset in the feature space.

Cấu trúc PCA của các tính năng mới thực chất chỉ là sự kết hợp tuyến tính (tổng có trọng số) của các tính năng ban đầu:
```python
df["Size"] = 0.707 * X["Height"] + 0.707 * X["Diameter"]
df["Shape"] = 0.707 * X["Height"] - 0.707 * X["Diameter"]
```
Những tính năng mới này được gọi là principal components of the data. Bản thân các trọng lượng được gọi là loadings. Sẽ có nhiều thành phần chính giống như các tính năng trong tập dữ liệu gốc: nếu chúng tôi sử dụng mười tính năng thay vì hai, thì cuối cùng chúng tôi sẽ có mười thành phần.
Tải trọng của một thành phần cho chúng ta biết sự biến đổi mà nó thể hiện thông qua các dấu hiệu và độ lớn:
| Features/Components | Size (PC1) | Shape (PC2) | 
|----------|------------|------------|
| Height   | 0.707      | 0.707      |             
| Diameter | 0.707      | -0.707     |             

Bảng tải trọng này cho chúng ta biết rằng trong thành phần Size , Height and Diameter thay đổi theo cùng một hướng (cùng dấu), nhưng trong thành phần Hình dạng, chúng khác nhau theo hướng ngược lại (dấu ngược lại). Trong mỗi thành phần, các tải trọng đều có cùng độ lớn và do đó các đặc tính đóng góp như nhau ở cả hai thành phần. 

PCA cũng cho chúng ta biết mức độ biến đổi của từng thành phần. Từ các hình vẽ, chúng ta có thể thấy rằng có nhiều biến thể trong dữ liệu dọc theo thành phần Size hơn là dọc theo thành phần Hình dạng. PCA làm cho điều này trở nên chính xác thông qua percent of explained variance. 
Size chiếm khoảng 96% và shape chiếm khoảng 4% phương sai giữa Height and Diameter.

![alt text](.\img\image-2.png)


Thành phần siza nắm bắt phần lớn sự thay đổi giữa Height và Diameter . Tuy nhiên, điều quan trọng cần nhớ là lượng phương sai trong một thành phần không nhất thiết phải tương ứng với mức độ tốt của nó như một yếu tố dự đoán: nó phụ thuộc vào những gì bạn đang cố gắng dự đoán
#### PCA for Feature Engineering 
*  Các bước thực hiện PCA

Từ các suy luận phía trên, ta có thể tóm tắt lại các bước trong PCA như sau:
 
Note :
-	Phương sai lớn nhất có nghĩa nó sẽ chứa nhiều điểm nhất và chứa được nhiều thông tin nhất
-	Từ đó chọn được các trục vecto chính theo k chiều yêu cầu để ánh xạ vào không gian mới 

Có hai cách bạn có thể sử dụng PCA cho kỹ thuật tính năng.

Cách đầu tiên là sử dụng nó như một kỹ thuật mô tả. Vì các thành phần cho bạn biết về sự biến đổi, nên bạn có thể tính điểm MI cho các thành phần đó và xem loại biến thể nào có tính dự đoán tốt nhất cho mục tiêu của bạn. Điều đó có thể cung cấp cho bạn ý tưởng về các loại tính năng cần tạo -- một sản phẩm trong 'Height' and 'Diameter' nếu  'Size'  là quan trọng, hoặc một tỷ lệ của 'Height' and 'Diameter' nếu Shape quan trọng . Bạn thậm chí có thể thử phân cụm một hoặc nhiều thành phần có điểm cao.

Cách thứ hai là sử dụng chính các thành phần đó làm tính năng. Bởi vì các thành phần thể hiện trực tiếp cấu trúc biến đổi của dữ liệu nên chúng thường có thể mang lại nhiều thông tin hơn các tính năng ban đầu. Dưới đây là một số trường hợp sử dụng: 
•	Dimensionality reduction (Giảm kích thước): Khi các tính năng của bạn có mức độ dư thừa cao (cụ thể là đa cộng tuyến), PCA sẽ phân chia phần dư thừa thành một hoặc nhiều thành phần phương sai gần như bằng 0, sau đó bạn có thể loại bỏ vì chúng sẽ chứa ít hoặc không có thông tin.
•	Anomaly detection (Phát hiện bất thường): Sự biến đổi bất thường, không rõ ràng so với các đặc điểm ban đầu, thường sẽ xuất hiện ở các thành phần có phương sai thấp. Các thành phần này có thể mang lại nhiều thông tin trong nhiệm vụ phát hiện sự bất thường hoặc ngoại lệ.
•	Noise reduction (Giảm nhiễu): Một tập hợp các thông số đọc từ cảm biến thường sẽ có chung một số tiếng ồn xung quanh. PCA đôi khi có thể thu thập tín hiệu (có tính cung cấp thông tin) thành một số lượng tính năng nhỏ hơn trong khi chỉ để lại nhiễu, do đó tăng tỷ lệ tín hiệu trên nhiễu. 
•	Decorrelation (Giải mã): Một số thuật toán ML gặp khó khăn với các tính năng có mức độ tương quan cao. PCA chuyển đổi các tính năng tương quan thành các thành phần không tương quan, điều này có thể giúp thuật toán của bạn hoạt động dễ dàng hơn.
Về cơ bản, PCA cho phép bạn truy cập trực tiếp vào cấu trúc tương quan của dữ liệu. Chắc chắn bạn sẽ nghĩ ra những ứng dụng của riêng mình!

Các phương pháp hay nhất về PCA: Có một số điều cần lưu ý khi áp dụng PCA:
-	PCA chỉ hoạt động với các tính năng số, như số lượng hoặc số đếm liên tục.
-	PCA rất nhạy cảm với quy mô. Bạn nên chuẩn hóa dữ liệu trước khi áp dụng PCA, trừ khi bạn biết mình có lý do chính đáng để không làm vậy.
-	Hãy cân nhắc việc loại bỏ hoặc hạn chế các giá trị ngoại lệ vì chúng có thể có ảnh hưởng không đáng có đến kết quả.

#### Example - 1985 Automobiles
Trong ví dụ này, chúng tôi sẽ quay lại tập dữ liệu Automobile và áp dụng PCA, sử dụng PCA làm kỹ thuật mô tả để khám phá các tính năng. Chúng ta sẽ xem xét các trường hợp sử dụng khác trong bài tập này.
Ô ẩn này tải dữ liệu và xác định các hàm plot_variance và make_mi_scores
```python 
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from IPython.display import display
from sklearn.feature_selection import mutual_info_regression


plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)


def plot_variance(pca, width=8, dpi=100):
    # Create figure
    fig, axs = plt.subplots(1, 2)
    n = pca.n_components_
    grid = np.arange(1, n + 1)
    # Explained variance
    evr = pca.explained_variance_ratio_
    axs[0].bar(grid, evr)
    axs[0].set(
        xlabel="Component", title="% Explained Variance", ylim=(0.0, 1.0)
    )
    # Cumulative Variance
    cv = np.cumsum(evr)
    axs[1].plot(np.r_[0, grid], np.r_[0, cv], "o-")
    axs[1].set(
        xlabel="Component", title="% Cumulative Variance", ylim=(0.0, 1.0)
    )
    # Set up figure
    fig.set(figwidth=8, dpi=100)
    return axs

def make_mi_scores(X, y, discrete_features):
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores


df = pd.read_csv("../input/fe-course-data/autos.csv")
```
Chúng tôi đã chọn bốn tính năng bao gồm một loạt các thuộc tính. Mỗi tính năng này cũng có điểm MI cao với mục tiêu, giá cả. Chúng tôi sẽ chuẩn hóa dữ liệu vì 
các tính năng này không tự nhiên trên cùng một quy mô.

In [2]:
```python
features = ["highway_mpg", "engine_size", "horsepower", "curb_weight"]

X = df.copy()
y = X.pop('price')
X = X.loc[:, features]

# Standardize
X_scaled = (X - X.mean(axis=0)) / X.std(axis=0)
```
Bây giờ chúng ta có thể phù hợp với công cụ ước tính PCA của scikit-learn  và tạo ra các thành phần chính. Bạn có thể thấy ở đây một vài hàng đầu tiên của tập dữ liệu đã chuyển đổi.

In [3]:
```python
from sklearn.decomposition import PCA

# Create principal components
pca = PCA()
X_pca = pca.fit_transform(X_scaled)

# Convert to dataframe
component_names = [f"PC{i+1}" for i in range(X_pca.shape[1])]
X_pca = pd.DataFrame(X_pca, columns=component_names)

X_pca.head()
```
Out[3]:
|    |      PC1 |      PC2 |      PC3 |      PC4 |
|---:|---------:|---------:|---------:|---------:|
|  0 | 0.382486 | -0.400222|  0.124122|  0.169539|
|  1 | 0.382486 | -0.400222|  0.124122|  0.169539|
|  2 | 1.550890 | -0.107175|  0.598361| -0.256081|
|  3 | -0.408859| -0.425947|  0.243335|  0.013920|
|  4 | 1.132749 | -0.814565| -0.202885|  0.224138|

Sau khi lắp, phiên bản PCA chứa tải trong  thuộc tính components_ của nó  . (Thật không may, thuật ngữ cho PCA không nhất quán. Chúng ta đang tuân theo quy ước gọi các cột đã chuyển đổi trong X_pca các thành phần mà nếu không thì không có tên.) Chúng tôi sẽ kết thúc quá trình tải trong một khung dữ liệu.

In [4]:
```python
loadings = pd.DataFrame(
    pca.components_.T,  # transpose the matrix of loadings
    columns=component_names,  # so the columns are the principal components
    index=X.columns,  # and the rows are the original features
)
loadings
```
Out[4]:
|             |     PC1 |     PC2 |     PC3 |     PC4 |
|:------------|--------:|--------:|--------:|--------:|
| highway_mpg | -0.4923 |  0.7709 |  0.0701 | -0.3980 |
| engine_size |  0.5039 |  0.6267 |  0.0200 |  0.5941 |
| horsepower  |  0.5004 |  0.0138 |  0.7311 | -0.4635 |
| curb_weight |  0.5033 |  0.1130 | -0.6784 | -0.5232 |


Hãy nhớ lại rằng các dấu hiệu và cường độ tải của một thành phần cho chúng ta biết loại biến thể mà nó được nắm bắt. Thành phần đầu tiên (PC1) cho thấy sự tương phản giữa các phương tiện lớn, mạnh mẽ với khả năng tiết kiệm xăng kém và các phương tiện nhỏ hơn, tiết kiệm hơn với khả năng tiết kiệm xăng tốt. Chúng ta có thể gọi đây là trục "Sang trọng / Kinh tế". Hình tiếp theo cho thấy bốn tính năng được chọn của chúng tôi chủ yếu khác nhau dọc theo trục Luxury / Economy.

In [5]:
```python
# Look at explained variance
plot_variance(pca);
``` 
Chúng ta cũng hãy xem xét điểm MI của các thành phần. Không có gì đáng ngạc nhiên, PC1 có  nhiều thông tin, mặc dù các thành phần còn lại, mặc dù có sự khác biệt nhỏ, vẫn có mối quan hệ đáng kể với giá cả. Kiểm tra các thành phần đó có thể đáng giá để tìm các mối quan hệ không bị bắt bởi trục Xa xỉ / Kinh tế chính.

In [6]:
```python
mi_scores = make_mi_scores(X_pca, y, discrete_features=False)
mi_scores
```
Out[6]:
|      |        |
|:-----|-------:|
| PC1  | 1.0133 |
| PC2  | 0.3792 |
| PC3  | 0.3067 |
| PC4  | 0.2033 |

Name: MI Scores, dtype: float64
Thành phần thứ ba cho thấy sự tương phản giữa mã lực và curb_weight - có vẻ như xe thể thao so với toa xe.

In [7]:
```python
# Show dataframe sorted by PC3
idx = X_pca["PC3"].sort_values(ascending=False).index
cols = ["make", "body_style", "horsepower", "curb_weight"]
df.loc[idx, cols]
```
Out[7]:
| make          | body_style  | horsepower | curb_weight |
|---------------|-------------|------------|-------------|
| porsche       | hardtop     | 207        | 2756        |
| porsche       | hardtop     | 207        | 2756        |
| porsche       | convertible| 207        | 2800        |
| jaguar        | sedan       | 262        | 3950        |
| nissan        | hatchback  | 200        | 3139        |
| ...           | ...         | ...        | ...         |
| mercedes-benz | wagon      | 123        | 3750        |
| mercedes-benz | sedan      | 123        | 3770        |
| peugot        | wagon      | 95         | 3430        |
| peugot        | wagon      | 95         | 3485        |
| toyota        | wagon      | 62         | 3110        |

193 rows × 4 columns
Để thể hiện sự tương phản này, chúng ta hãy tạo một tính năng tỷ lệ mới:
In [8]:
```python
df["sports_or_wagon"] = X.curb_weight / X.horsepower
sns.regplot(x="sports_or_wagon", y='price', data=df, order=2);
```
![alt text](.\img\image-3.png)
