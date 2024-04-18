
<style>
  table {
    width: auto; /* Tự động điều chỉnh kích thước bảng */
    max-width: 100%; /* Độ rộng tối đa là 100% của kích thước hiển thị */
  }
  th, td {
    padding: 8px; /* Thêm khoảng cách giữa dòng và cột */
    text-align: left; /* Canh lề trái cho nội dung trong cột */
  }
</style>

# The Goal of Feature Engineering
* Mục tiêu của kỹ thuật tính năng chỉ đơn giản là làm cho dữ liệu của bạn phù hợp hơn với vấn đề 
trong tầm tay.

Hãy xem xét các biện pháp "nhiệt độ biểu kiến" như chỉ số nhiệt và gió lạnh. Những đại lượng này cố gắng  đo nhiệt độ cảm nhận được đối với con người dựa trên nhiệt độ không khí, độ ẩm và tốc độ gió, những thứ mà chúng ta có thể đo trực tiếp. Bạn có thể nghĩ về nhiệt độ biểu kiến là kết quả của một loại kỹ thuật tính năng, một nỗ lực để làm cho dữ liệu quan sát được phù hợp hơn với những gì chúng ta thực sự quan tâm: cảm giác thực sự bên ngoài như thế nào!
Bạn có thể thực hiện kỹ thuật tính năng để:
1.	Cải thiện hiệu suất dự đoán của mô hình
2.	Giảm nhu cầu tính toán hoặc dữ liệu
3.	cải thiện khả năng diễn giải kết quả
## A Guiding Principle of Feature Engineering
* Để một tính năng trở nên hữu ích, nó phải có mối quan hệ với mục tiêu mà mô hình của bạn có thể học được. Ví dụ, các mô hình tuyến tính chỉ có thể học các mối quan hệ tuyến tính. Vì vậy, khi sử dụng mô hình tuyến tính, mục tiêu của bạn là chuyển đổi các tính năng để làm cho mối quan hệ của chúng với tuyến tính đích.

Ý tưởng chính ở đây là một chuyển đổi bạn áp dụng cho một tính năng về bản chất trở thành một phần của chính mô hình. Giả sử bạn đang cố gắng dự đoán Price của các ô vuông đất từ Length của một phía. Lắp mô hình tuyến tính trực tiếp vào Length Cho kết quả kém: mối quan hệ không phải là tuyến tính.
![alt text](https://storage.googleapis.com/kaggle-media/learn/images/5D1z24N.png )

A linear model fits poorly with only Length as feature.


Nếu chúng ta bình phương Length Tính năng để có được'Area', tuy nhiên, chúng ta tạo ra một mối quan hệ tuyến tính. Thêm Area vào bộ tính năng có nghĩa là mô hình tuyến tính này giờ đây có thể phù hợp với một parabol. Nói cách khác, bình phương một tính năng đã cho mô hình tuyến tính khả năng phù hợp với các tính năng bình phương.
 

![alt text](https://storage.googleapis.com/kaggle-media/learn/images/BLRsYOK.png )
<center>Trái: Sự phù hợp với Khu vực tốt hơn nhiều. Phải: Điều này làm cho độ vừa vặn với Chiều dài cũng tốt hơn.
</center>

Điều này sẽ cho bạn thấy lý do tại sao có thể có lợi tức cao về thời gian đầu tư vào kỹ thuật tính năng. Bất cứ mối quan hệ nào mà mô hình của bạn không thể học được, bạn có thể cung cấp cho mình thông qua các biến đổi. Khi bạn phát triển bộ tính năng của mình, hãy suy nghĩ về thông tin mà mô hình của bạn có thể sử dụng để đạt được hiệu suất tốt nhất.
## Mutual Information
* Lần đầu tiên gặp phải một tập dữ liệu mới đôi khi có thể cảm thấy quá sức. Bạn có thể được trình bày với hàng trăm hoặc hàng ngàn tính năng mà không cần mô tả để đi qua. Bạn thậm chí bắt đầu từ đâu?

Bước đầu tiên tuyệt vời là xây dựng thứ hạng với số liệu tiện ích tính năng, một chức năng đo lường mối liên hệ giữa một tính năng và mục tiêu. Sau đó, bạn có thể chọn một bộ nhỏ hơn các tính năng hữu ích nhất để phát triển ban đầu và tự tin hơn rằng thời gian của bạn sẽ được sử dụng tốt.

Số liệu chúng ta sẽ sử dụng được gọi là "thông tin lẫn nhau". Thông tin lẫn nhau rất giống mối tương quan ở chỗ nó đo lường mối quan hệ giữa hai đại lượng. Ưu điểm của thông tin lẫn nhau là nó có thể  phát hiện bất kỳ loại mối quan hệ nào  , trong khi mối tương quan chỉ phát hiện các mối quan hệ tuyến tính.

Thông tin lẫn nhau là một số liệu có mục đích chung tuyệt vời và đặc biệt hữu ích khi bắt đầu phát triển tính năng khi bạn có thể chưa biết mình muốn sử dụng mô hình nào. Đó là:
1.	dễ sử dụng và giải thích,
2.	hiệu quả tính toán,
3.	về mặt lý thuyết có cơ sở,
4.	chống lại overfitting, và,
5.	có thể phát hiện bất kỳ loại mối quan hệ nào
#### Mutual Information and What it Measures
* Thông tin lẫn nhau mô tả các mối quan hệ dưới dạng không chắc chắn. Thông tin lẫn nhau (MI) giữa hai đại lượng là thước đo mức độ hiểu biết về một đại lượng làm giảm sự không chắc chắn về đại lượng kia. Nếu bạn biết giá trị của một tính năng, bạn sẽ tự tin hơn bao nhiêu về mục tiêu?
Dưới đây là một ví dụ từ  dữ liệu Nhà ở Ames. Con số này cho thấy mối quan hệ giữa chất lượng bên ngoài của một ngôi nhà và giá mà nó được bán. Mỗi điểm đại diện cho một ngôi nhà.
![alt text](https://storage.googleapis.com/kaggle-media/learn/images/X12ARUK.png )
<center>Biết chất lượng bên ngoài của một ngôi nhà làm giảm sự không chắc chắn về giá bán của nó.
</center> 

Từ hình vẽ, chúng ta có thể thấy rằng việc biết giá trị  của ExterQual  sẽ giúp bạn chắc chắn hơn về SalePrice tương ứng  - mỗi danh mục của ExterQual có xu hướng tập trung SalePrice vào một phạm vi nhất định. Thông tin lẫn nhau mà  ExterQual  có với  SalePrice  là mức giảm trung bình sự không chắc chắn trong SalePrice được thực hiện trên bốn giá trị của ExterQual. Vì  Fair  xảy ra ít thường xuyên  hơn Typical, ví dụ, Fair nhận được ít trọng số hơn trong điểm MI.

(Lưu ý kỹ thuật: Cái mà chúng ta gọi là sự không chắc chắn được đo bằng cách sử dụng một đại lượng từ lý thuyết thông tin được gọi là "entropy". Entropy của một biến có nghĩa đại khái: "trung bình bạn cần bao nhiêu câu hỏi có hoặc không để mô tả sự xuất hiện của biến đó." Bạn càng phải hỏi nhiều câu hỏi, bạn càng phải không chắc chắn về biến số. Thông tin lẫn nhau là số lượng câu hỏi bạn mong đợi tính năng trả lời về mục tiêu.)
#### Interpreting Mutual Information Scores
* Thông tin lẫn nhau ít nhất có thể giữa các đại lượng là 0,0. Khi MI bằng 0, các đại lượng là độc lập: không ai có thể cho bạn biết bất cứ điều gì về cái kia. Ngược lại, về lý thuyết, không có giới hạn trên đối với MI có thể là gì. Trong thực tế, mặc dù các giá trị trên 2.0 hoặc hơn là không phổ biến. (Thông tin lẫn nhau là một đại lượng logarit, vì vậy nó tăng rất chậm.)

Hình tiếp theo sẽ cung cấp cho bạn ý tưởng về cách các giá trị MI tương ứng với loại và mức độ liên kết mà một tính năng có với mục tiêu.
![alt text](https://storage.googleapis.com/kaggle-media/learn/images/Dt75E1f.png  )
<center>Trái: Thông tin lẫn nhau tăng lên khi sự phụ thuộc giữa tính năng và mục tiêu trở nên chặt chẽ hơn. Phải: Thông tin lẫn nhau có thể nắm bắt bất kỳ loại liên kết nào (không chỉ tuyến tính, như tương quan.)
</center> 

Dưới đây là một số điều cần nhớ khi áp dụng thông tin lẫn nhau:
1.	MI có thể giúp bạn hiểu tiềm  năng tương đối của một tính năng như một yếu tố dự đoán mục tiêu, được xem xét bởi chính nó.
2.	Một tính năng có thể rất nhiều thông tin khi tương tác với các tính năng khác, nhưng không quá nhiều thông tin. MI không thể phát hiện tương tác giữa các tính năng. Nó là một  số liệu đơn biến.
3.	Tính  hữu dụng thực tế của một  tính năng phụ thuộc vào kiểu máy bạn sử dụng tính năng đó. Một tính năng chỉ hữu ích khi mối quan hệ của nó với mục tiêu là mối quan hệ mà mô hình của bạn có thể tìm hiểu. Chỉ vì một tính năng có điểm MI cao không có nghĩa là mô hình của bạn sẽ có thể làm bất cứ điều gì với thông tin đó. Trước tiên, bạn có thể cần phải chuyển đổi tính năng để hiển thị liên kết.

#### Ví Dụ - 1985 Automobiles
* The Automobile Bộ dữ liệu bao gồm 193 chiếc xe từ năm mô hình 1985. Mục tiêu của bộ dữ liệu này là dự đoán giá của một chiếc xe  (mục tiêu) từ 23 tính năng của chiếc xe, chẳng hạn như kiểu dáng, body_style và mã lực. Trong ví dụ này, chúng tôi sẽ xếp hạng các tính năng có thông tin lẫn nhau và điều tra kết quả bằng cách trực quan hóa dữ liệu.

In [1]:
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

plt.style.use("seaborn-whitegrid")

df = pd.read_csv("../input/fe-course-data/autos.csv")
df.head()
```
Out[1]:
| symboling | make        | fuel_type | aspiration | num_of_doors | body_style | drive_wheels | engine_location | wheel_base | length | ... | engine_size | fuel_system | bore | stroke | compression_ratio | horsepower | peak_rpm | city_mpg | highway_mpg | price |
|-----------|-------------|-----------|------------|--------------|------------|--------------|-----------------|------------|--------|-----|-------------|-------------|------|--------|-------------------|------------|----------|----------|--------------|-------|
| 3         | alfa-romero | gas       | std        | 2            | convertible| rwd          | front           | 88.6       | 168.8  | ... | 130         | mpfi        | 3.47 | 2.68   |                   | 111        | 5000     | 21       | 27           | 13495 |
| 3         | alfa-romero | gas       | std        | 2            | convertible| rwd          | front           | 88.6       | 168.8  | ... | 130         | mpfi        | 3.47 | 2.68   | 9                 | 111        | 5000     | 21       | 27           | 16500 |
| 1         | alfa-romero | gas       | std        | 2            | hatchback  | rwd          | front           | 94.5       | 171.2  | ... | 152         | mpfi        | 2.68 | 3.47   | 9                 | 154        | 5000     | 19       | 26           | 16500 |
| 2         | audi        | gas       | std        | 4            | sedan      | fwd          | front           | 99.8       | 176.6  | ... | 109         | mpfi        | 3.19 | 3.40   | 10                | 102        | 5500     | 24       | 30           | 13950 |
| 2         | audi        | gas       | std        | 4            | sedan      | 4wd          | front           | 99.4       | 176.6  | ... | 136         | mpfi        | 3.19 | 3.40   | 8                 | 115        | 5500     | 18       | 22           | 17450 |

5 rows × 25 columns
Thuật toán scikit-learn cho MI xử lý các tính năng rời rạc khác với các tính năng liên tục. Do đó, bạn cần cho nó biết đó là cái nào. Theo nguyên tắc thông thường, bất cứ thứ gì phải có  kiểu phao không rời  rạc. Categoricals (đối tượng hoặc phân loại dtype) có thể được coi là rời rạc bằng cách cung cấp cho họ một mã hóa nhãn. (Bạn có thể xem lại mã hóa nhãn trong Categorical Variables lesson.)

In [2]:
```python
X = df.copy()
y = X.pop("price")

# Label encoding for categoricals
for colname in X.select_dtypes("object"):
    X[colname], _ = X[colname].factorize()

# All discrete features should now have integer dtypes (double-check this before using MI!)
discrete_features = X.dtypes == int
```
Thuật toán scikit-learn cho MI xử lý các tính năng rời rạc khác với các tính năng liên tục. Do đó, bạn cần cho nó biết đó là cái nào. Theo nguyên tắc thông thường, bất cứ thứ gì phải có  kiểu phao không rời  rạc. Categoricals (đối tượng hoặc phân loại dtype) có thể được coi là rời rạc bằng cách cung cấp cho họ một mã hóa nhãn. 

In [3]:
```python
from sklearn.feature_selection import mutual_info_regression

def make_mi_scores(X, y, discrete_features):
mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)
mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
mi_scores = mi_scores.sort_values(ascending=False)
return mi_scores

mi_scores = make_mi_scores(X, y, discrete_features)
mi_scores[::3]  # show a few features with their MI scores
```
Out[3]:
| Feature            | Coefficient |
|--------------------|-------------|
| curb_weight        | 1.540126    |
| highway_mpg        | 0.951700    |
| length             | 0.621566    |
| fuel_system        | 0.485085    |
| stroke             | 0.389321    |
| num_of_cylinders   | 0.330988    |
| compression_ratio  | 0.133927    |
| fuel_type          | 0.048139    |

Name: MI Scores, dtype: float64

Và bây giờ một biểu đồ thanh để so sánh dễ dàng hơn:

In [4]:
```python
def plot_mi_scores(scores):
    scores = scores.sort_values(ascending=True)
    width = np.arange(len(scores))
    ticks = list(scores.index)
    plt.barh(width, scores)
    plt.yticks(width, ticks)
    plt.title("Mutual Information Scores")


plt.figure(dpi=100, figsize=(8, 5))
plot_mi_scores(mi_scores)
``` 
![alt text](./img%20Feature%20Engineering/image.png)

<center>Data visualization is a great follow-up to a utility ranking. Let's take a closer look at a couple of these.
</center> 

 
Như chúng ta có thể mong đợi, tính năng curb_weight điểm cao  thể hiện mối quan hệ chặt chẽ với giá cả, mục tiêu.

In [5]:
```python
sns.relplot(x="curb_weight", y="price", data=df);
 ```    
 ![alt text](image-1.png)
 
Tính  năng fuel_type có  điểm MI khá thấp, nhưng như chúng ta có thể thấy từ hình, nó phân tách rõ ràng hai  quần thể giá với các xu hướng khác nhau trong  tính năng mã lực. Điều này chỉ ra rằng fuel_type đóng góp một hiệu ứng tương tác và có thể không quan trọng sau tất cả. Trước khi quyết định một tính năng không quan trọng từ điểm MI của nó, bạn nên điều tra bất kỳ hiệu ứng tương tác nào có thể xảy ra - kiến thức về miền có thể cung cấp rất nhiều hướng dẫn ở đây.

In [6]:
```python
sns.lmplot(x="horsepower", y="price", hue="fuel_type", data=df);
 ```
![alt text](./img%20Feature%20Engineering/image-2.png)


## Creating Features


* Khi bạn đã xác định được một tập hợp các tính năng có tiềm năng, đã đến lúc bắt đầu phát triển chúng. Trong bài học này, bạn sẽ tìm hiểu một số biến đổi phổ biến mà bạn có thể thực hiện hoàn toàn trong Pandas. Nếu bạn cảm thấy gỉ, chúng tôi đã có một tuyệt vời course on Pandas.



In [1]:
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

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

accidents = pd.read_csv("../input/fe-course-data/accidents.csv")
autos = pd.read_csv("../input/fe-course-data/autos.csv")
concrete = pd.read_csv("../input/fe-course-data/concrete.csv")
customer = pd.read_csv("../input/fe-course-data/customer.csv")
```
Mẹo khám phá các tính năng mới
1.	Hiểu các tính năng. Tham khảo  tài liệu dữ liệu của tập dữ liệu của bạn, nếu có.
2.	Nghiên cứu miền vấn đề để có được kiến thức về miền. Nếu vấn đề của bạn là dự đoán giá nhà, hãy thực hiện một số nghiên cứu về bất động sản chẳng hạn. Wikipedia có thể là một điểm khởi đầu tốt, nhưng sách và bài báo thường sẽ có thông tin tốt nhất.
3.	Nghiên cứu công việc trước đây. Viết giải pháp từ các cuộc thi Kaggle trước đây là một nguồn tài nguyên tuyệt vời.
4.	Sử dụng trực quan hóa dữ liệu. Hình dung có thể tiết lộ các bệnh lý trong việc phân phối một tính năng hoặc các mối quan hệ phức tạp có thể được đơn giản hóa. Đảm bảo trực quan hóa tập dữ liệu của bạn khi bạn làm việc thông qua quy trình kỹ thuật tính năng.
Mathematical Transforms ( biến đổi toán học )

Mối quan hệ giữa các tính năng số thường được thể hiện thông qua các công thức toán học, mà bạn sẽ thường xuyên bắt gặp như một phần của nghiên cứu tên miền của mình. Trong Pandas, bạn có thể áp dụng các phép toán số học cho các cột giống như thể chúng là các số thông thường.
Trong  bộ dữ liệu ô tô là các tính năng mô tả động cơ ô tô. Nghiên cứu mang lại nhiều công thức khác nhau để tạo ra các tính năng mới hữu ích tiềm năng. Ví dụ, "tỷ lệ hành trình" là thước đo mức độ hiệu quả của động cơ so với hiệu suất:

In [2]:
```python
autos["stroke_ratio"] = autos.stroke / autos.bore

autos[["stroke", "bore", "stroke_ratio"]].head()
```
Out[2]:
| stroke | bore | stroke_ratio |
|--------|------|--------------|
| 2.68   | 3.47 | 0.772334     |
| 2.68   | 3.47 | 0.772334     |
| 3.47   | 2.68 | 1.294776     |
| 3.40   | 3.19 | 1.065831     |
| 3.40   | 3.19 | 1.065831     |

Sự kết hợp càng phức tạp, mô hình sẽ càng khó học, như công thức này cho "sự dịch chuyển" của động cơ, một thước đo sức mạnh của nó:

In [3]:
```python
autos["displacement"] = (
    np.pi * ((0.5 * autos.bore) ** 2) * autos.stroke * autos.num_of_cylinders
)
```
Trực quan hóa dữ liệu có thể gợi ý các phép biến đổi, thường là "định hình lại" một đối tượng địa lý thông qua lũy thừa hoặc logarit. Ví dụ, sự phân bố của WindSpeed trong các vụ tai nạn ở Hoa Kỳ rất sai lệch. Trong trường hợp này, logarit có hiệu quả trong việc chuẩn hóa nó:

In [4]:
```python
# If the feature has 0.0 values, use np.log1p (log(1+x)) instead of np.log
accidents["LogWindSpeed"] = accidents.WindSpeed.apply(np.log1p)

# Plot a comparison
fig, axs = plt.subplots(1, 2, figsize=(8, 4))
sns.kdeplot(accidents.WindSpeed, shade=True, ax=axs[0])
sns.kdeplot(accidents.LogWindSpeed, shade=True, ax=axs[1]);
```
/opt/conda/lib/python3.7/site-packages/ipykernel_launcher.py:6: FutureWarning: 

`shade` is now deprecated in favor of `fill`; setting `fill=True`.
This will become an error in seaborn v0.14.0; please update your code.

  
/opt/conda/lib/python3.7/site-packages/ipykernel_launcher.py:7: FutureWarning: 

`shade` is now deprecated in favor of `fill`; setting `fill=True`.
This will become an error in seaborn v0.14.0; please update your code.

  import sys
 
 ![alt text](./img%20Feature%20Engineering/image-3.png)

Kiểm tra bài học của chúng tôi  về chuẩn hóa  trong Làm sạch dữ liệu,  nơi bạn cũng sẽ tìm hiểu về chuyển đổi Box-Cox, một loại chuẩn hóa rất chung.
#### Counts
* Các tính năng mô tả sự hiện diện hay vắng mặt của một cái gì đó thường đi theo bộ, tập hợp các yếu tố nguy cơ của một căn bệnh, nói. Bạn có thể tổng hợp các tính năng như vậy bằng cách tạo số lượng.

Các tính năng này sẽ là nhị phân (1 cho  Hiện tại, 0 cho Vắng mặt)  hoặc boolean (Đúng hoặc Sai). Trong Python, booleans có thể được cộng lại giống như thể chúng là số nguyên.
Trong Tai nạn giao thông là một số  đặc điểm cho biết liệu một số đối tượng trên đường có ở gần vụ tai nạn hay không. Thao tác này sẽ tạo ra tổng số tính năng đường bộ gần đó bằng  phương pháp tổng:

In [5]:
```python
roadway_features = ["Amenity", "Bump", "Crossing", "GiveWay",
    "Junction", "NoExit", "Railway", "Roundabout", "Station", "Stop",
    "TrafficCalming", "TrafficSignal"]
accidents["RoadwayFeatures"] = accidents[roadway_features].sum(axis=1)

accidents[roadway_features + ["RoadwayFeatures"]].head(10)
```
Out[5]:
| Amenity | Bump | Crossing | GiveWay | Junction | NoExit | Railway | Roundabout | Station | Stop | TrafficCalming | TrafficSignal | RoadwayFeatures |
|---------|------|----------|---------|----------|--------|---------|------------|---------|------|----------------|---------------|-----------------|
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |
| False   | False| False    | False   | True     | False  | False   | False      | False   | False| False          | False         | 1               |
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |
| False   | False| True     | False   | False    | False  | False   | False      | False   | False| False          | True          | 2               |
| False   | False| True     | False   | False    | False  | False   | False      | False   | False| False          | True          | 2               |
| False   | False| False    | False   | False    | False  | False   | False      | False   | False| False          | False         | 0               |



Bạn cũng có thể sử dụng các phương thức tích hợp sẵn của khung dữ liệu để tạo các giá trị boolean. Trong  tập dữ liệu Bê tông là số lượng các thành phần trong một công thức cụ thể. Nhiều công thức thiếu một hoặc nhiều thành phần (nghĩa là thành phần có giá trị bằng 0). Điều này sẽ đếm có bao nhiêu thành phần trong một công thức với phương thức lớn hơn gt được tích hợp sẵn của khung dữ liệu  :

In [6]:
```python
components = [ "Cement", "BlastFurnaceSlag", "FlyAsh", "Water",
               "Superplasticizer", "CoarseAggregate", "FineAggregate"]
concrete["Components"] = concrete[components].gt(0).sum(axis=1)

concrete[components + ["Components"]].head(10)
```
Out[6]:
| Cement | BlastFurnaceSlag | FlyAsh | Water | Superplasticizer | CoarseAggregate | FineAggregate | Components |
|--------|-------------------|--------|-------|------------------|-----------------|---------------|------------|
| 540.0  | 0.0               | 0.0    | 162.0 | 2.5              | 1040.0          | 676.0         | 5          |
| 540.0  | 0.0               | 0.0    | 162.0 | 2.5              | 1055.0          | 676.0         | 5          |
| 332.5  | 142.5             | 0.0    | 228.0 | 0.0              | 932.0           | 594.0         | 5          |
| 332.5  | 142.5             | 0.0    | 228.0 | 0.0              | 932.0           | 594.0         | 5          |
| 198.6  | 132.4             | 0.0    | 192.0 | 0.0              | 978.4           | 825.5         | 5          |
| 266.0  | 114.0             | 0.0    | 228.0 | 0.0              | 932.0           | 670.0         | 5          |
| 380.0  | 95.0              | 0.0    | 228.0 | 0.0              | 932.0           | 594.0         | 5          |
| 380.0  | 95.0              | 0.0    | 228.0 | 0.0              | 932.0           | 594.0         | 5          |
| 266.0  | 114.0             | 0.0    | 228.0 | 0.0              | 932.0           | 670.0         | 5          |
| 475.0  | 0.0               | 0.0    | 228.0 | 0.0              | 932.0           | 594.0         | 4          |

#### Building-Up and Breaking-Down Features
* Thường thì bạn sẽ có các chuỗi phức tạp có thể được chia thành các phần đơn giản hơn. Một số ví dụ phổ biến:

1.	ID numbers: '123-45-6789'
2.	Phone numbers: '(999) 555-0123'
3.	Street addresses: '8241 Kaggle Ln., Goose City, NV'
4.	Internet addresses: 'http://www.kaggle.com
5.	Product codes: '0 36000 29145 2'
6.	Dates and times: 'Mon Sep 30 07:06:05 2013'

Các tính năng như thế này thường sẽ có một số loại cấu trúc mà bạn có thể sử dụng. Ví dụ: số điện thoại Hoa Kỳ có mã vùng  (phần '(999)') cho bạn biết vị trí của người gọi. Như mọi khi, một số nghiên cứu có thể trả hết ở đây.

Trình  truy cập str cho phép bạn áp dụng các phương thức chuỗi như tách trực tiếp vào các cột. Bộ  dữ liệu Giá trị trọn đời của khách hàng  chứa các tính năng mô tả khách hàng của một công ty bảo hiểm. Từ  tính năng Chính sách, chúng tôi có thể tách Loại khỏi Cấp độ bảo hiểm:

In [7]:
```python
customer[["Type", "Level"]] = (  # Create two new features
    customer["Policy"]           # from the Policy feature
    .str                         # through the string accessor
    .split(" ", expand=True)     # by splitting on " "
                                 # and expanding the result into separate columns
)

customer[["Policy", "Type", "Level"]].head(10)
```
Out[7]:
| Policy       | Type      | Level |
|--------------|-----------|-------|
| Corporate L3 | Corporate | L3    |
| Personal L3  | Personal  | L3    |
| Personal L3  | Personal  | L3    |
| Corporate L2 | Corporate | L2    |
| Personal L1  | Personal  | L1    |
| Personal L3  | Personal  | L3    |
| Corporate L3 | Corporate | L3    |
| Corporate L3 | Corporate | L3    |
| Corporate L3 | Corporate | L3    |
| Special L2   | Special   | L2    |

Bạn cũng có thể kết hợp các tính năng đơn giản thành một tính năng sáng tác nếu bạn có lý do để tin rằng có một số tương tác trong sự kết hợp:

In [8]:
```python
autos["make_and_style"] = autos["make"] + "_" + autos["body_style"]
autos[["make", "body_style", "make_and_style"]].head()
```
Out[8]:
| make        | body_style   | make_and_style        |
|-------------|--------------|-----------------------|
| alfa-romero | convertible  | alfa-romero_convertible |
| alfa-romero | convertible  | alfa-romero_convertible |
| alfa-romero | hatchback    | alfa-romero_hatchback |
| audi        | sedan        | audi_sedan            |
| audi        | sedan        | audi_sedan            |

Ở những nơi khác trên Kaggle Learn Có một vài loại dữ liệu khác mà chúng tôi chưa nói đến ở đây đặc biệt giàu thông tin. May mắn thay, chúng tôi đã giúp bạn!
1.	Để biết ngày và giờ, hãy xem Phân tích Ngày từ khóa học Làm sạch Dữ liệu của chúng tôi.
2.	Để biết vĩ độ và kinh độ, hãy xem  khóa học Phân tích không gian địa lý của chúng tôi.
## Group Transforms
* Cuối cùng, chúng ta có Group transforms, tổng hợp thông tin trên nhiều hàng được nhóm theo một số danh mục. Với chuyển đổi nhóm, bạn có thể tạo các tính năng như: "thu nhập trung bình của tiểu bang cư trú của một người" hoặc "tỷ lệ phim được phát hành vào một ngày trong tuần, theo thể loại". Nếu bạn đã phát hiện ra một tương tác thể loại, một nhóm biến đổi trên categry đó có thể là một cái gì đó tốt để điều tra.

Sử dụng hàm tổng hợp, biến đổi nhóm kết hợp hai tính năng: một tính năng phân loại cung cấp nhóm và một tính năng khác có giá trị bạn muốn tổng hợp. Đối với "thu nhập trung bình theo tiểu bang", bạn sẽ chọn Tiểu bang cho tính năng nhóm, trung bình cho  chức năng tổng hợp và Thu nhập cho tính năng  tổng hợp. Để tính toán điều này trong Pandas, chúng ta sử dụng các  phương thức groupby và transform:

In [9]:
```python
customer["AverageIncome"] = (
    customer.groupby("State")  # for each state
    ["Income"]                 # select the income
    .transform("mean")         # and compute its mean
)

customer[["State", "Income", "AverageIncome"]].head(10)
```
Out[9]:
| State      | Income | AverageIncome |
|------------|--------|---------------|
| Washington | 56274  | 38122.733083  |
| Arizona    | 0      | 37405.402231  |
| Nevada     | 48767  | 38369.605442  |
| California | 0      | 37558.946667  |
| Washington | 43836  | 38122.733083  |
| Oregon     | 62902  | 37557.283353  |
| Oregon     | 55350  | 37557.283353  |
| Arizona    | 0      | 37405.402231  |
| Oregon     | 14072  | 37557.283353  |
| Oregon     | 28812  | 37557.283353  |

Hàm mean là một phương thức khung dữ liệu tích hợp, có nghĩa là chúng ta có thể truyền nó dưới dạng một chuỗi để biến đổi. Các phương pháp tiện dụng khác bao gồm max, min, median, var  ,  std và count. Dưới đây là cách bạn có thể tính toán tần suất mà mỗi trạng thái xảy ra trong tập dữ liệu:

In [10]:
```python
customer["StateFreq"] = (
    customer.groupby("State")
    ["State"]
    .transform("count")
    / customer.State.count()
)

customer[["State", "StateFreq"]].head(10)
```
Out[10]:
| State      | StateFreq |
|------------|-----------|
| Washington | 0.087366  |
| Arizona    | 0.186446  |
| Nevada     | 0.096562  |
| California | 0.344865  |
| Washington | 0.087366  |
| Oregon     | 0.284760  |
| Oregon     | 0.284760  |
| Arizona    | 0.186446  |
| Oregon     | 0.284760  |
| Oregon     | 0.284760  |

Bạn có thể sử dụng một biến đổi như thế này để tạo ra một "mã hóa tần số" cho một tính năng phân loại.

Nếu bạn đang sử dụng phần tách đào tạo và xác thực, để duy trì tính độc lập của chúng, tốt nhất bạn nên tạo một tính năng được nhóm chỉ bằng tập hợp đào tạo và sau đó kết hợp tính năng đó với nhóm xác thực. Chúng ta có thể sử dụng  phương thức merge của validation set  sau khi tạo một tập hợp các giá trị duy nhất với drop_duplicates trên training set:

In [11]:
```python
# Create splits
df_train = customer.sample(frac=0.5)
df_valid = customer.drop(df_train.index)

# Create the average claim amount by coverage type, on the training set
df_train["AverageClaim"] = df_train.groupby("Coverage")["ClaimAmount"].transform("mean")

# Merge the values into the validation set
df_valid = df_valid.merge(
    df_train[["Coverage", "AverageClaim"]].drop_duplicates(),
    on="Coverage",
    how="left",
)

df_valid[["Coverage", "AverageClaim"]].head(10)
```
Out[11]:
| Coverage | AverageClaim |
|----------|--------------|
| Premium  | 671.603973   |
| Basic    | 375.455516   |
| Basic    | 375.455516   |
| Basic    | 375.455516   |
| Basic    | 375.455516   |
| Basic    | 375.455516   |
| Basic    | 375.455516   |
| Basic    | 375.455516   |
| Extended | 474.483232   |
| Basic    | 375.455516   |


Mẹo tạo tính năng bạn nên ghi nhớ điểm mạnh và điểm yếu của mô hình khi tạo tính năng. Dưới đây là một số nguyên tắc:
1.	Các mô hình tuyến tính học tổng và sự khác biệt một cách tự nhiên, nhưng không thể học bất cứ điều gì phức tạp hơn.
2.	Tỷ lệ dường như khó khăn đối với hầu hết các mô hình. Kết hợp tỷ lệ thường dẫn đến một số tăng hiệu suất dễ dàng.
3.	Các mô hình tuyến tính và mạng lưới thần kinh thường hoạt động tốt hơn với các tính năng chuẩn hóa. Mạng lưới thần kinh đặc biệt cần các tính năng được thu nhỏ theo các giá trị không quá xa 0. Các mô hình dựa trên cây (như rừng ngẫu nhiên và XGBoost) đôi khi có thể được hưởng lợi từ việc chuẩn hóa, nhưng thường ít hơn nhiều.
4.	Các mô hình cây có thể học cách xấp xỉ hầu hết mọi sự kết hợp của các tính năng, nhưng khi sự kết hợp đặc biệt quan trọng, chúng vẫn có thể hưởng lợi từ việc tạo nó một cách rõ ràng, đặc biệt là khi dữ liệu bị hạn chế.
5.	Số lượng đặc biệt hữu ích cho các mô hình cây, vì các mô hình này không có cách tổng hợp thông tin tự nhiên trên nhiều tính năng cùng một lúc.		                                                                                    
