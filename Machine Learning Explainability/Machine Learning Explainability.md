# What Types of Insights Are Possible¶
* Nhiều người nói rằng các mô hình học máy là "hộp đen", theo nghĩa là chúng có thể đưa ra dự đoán tốt nhưng bạn không thể hiểu logic đằng sau những dự đoán đó. Tuyên bố này đúng theo nghĩa là hầu hết các nhà khoa học dữ liệu chưa biết cách trích xuất thông tin chi tiết từ các mô hình.

Tuy nhiên, khóa học vi mô này sẽ dạy cho bạn các kỹ thuật để trích xuất những hiểu biết sau đây từ các mô hình học máy tinh vi.
1.	Những tính năng nào trong dữ liệu mà mô hình nghĩ là quan trọng nhất?
2.	Đối với bất kỳ dự đoán đơn lẻ nào từ một mô hình, mỗi tính năng trong dữ liệu ảnh hưởng đến dự đoán cụ thể đó như thế nào?
3.	Làm thế nào để mỗi tính năng ảnh hưởng đến dự đoán của mô hình theo nghĩa lớn (hiệu ứng điển hình của nó là gì khi được xem xét trên một số lượng lớn các dự đoán có thể)?
Why Are These Insights Valuable
Những thông tin chi tiết này có nhiều công dụng, bao gồm
1.	Gỡ lỗi
2.	Thông báo kỹ thuật tính năng
3.	Chỉ đạo thu thập dữ liệu trong tương lai
4.	Thông báo cho việc ra quyết định của con người
5.	Xây dựng niềm tin
#### Debugging
* Thế giới có rất nhiều dữ liệu không đáng tin cậy, vô tổ chức và nói chung là bẩn. Bạn thêm một nguồn lỗi tiềm ẩn khi bạn viết mã tiền xử lý. Thêm vào tiềm năng cho target leakage, Và đó là tiêu chuẩn chứ không phải là ngoại lệ để có lỗi tại một số điểm trong một dự án khoa học dữ liệu thực sự.

Với tần suất và hậu quả tai hại tiềm tàng của lỗi, gỡ lỗi là một trong những kỹ năng có giá trị nhất trong khoa học dữ liệu. Hiểu được các mẫu mà một mô hình đang tìm kiếm sẽ giúp bạn xác định khi nào chúng mâu thuẫn với kiến thức của bạn về thế giới thực và đây thường là bước đầu tiên trong việc theo dõi lỗi.
#### Informing Feature Engineering
* Feature engineering thường là cách hiệu quả nhất để cải thiện độ chính xác của mô hình. Kỹ thuật tính năng thường liên quan đến việc liên tục tạo các tính năng mới bằng cách sử dụng các chuyển đổi dữ liệu thô hoặc các tính năng bạn đã tạo trước đó.

Đôi khi bạn có thể trải qua quá trình này mà không sử dụng gì ngoài trực giác về chủ đề cơ bản. Nhưng bạn sẽ cần nhiều định hướng hơn khi bạn có 100 tính năng thô hoặc khi bạn thiếu kiến thức nền tảng về chủ đề bạn đang làm việc.

Một cuộc thi Kaggle để predict loan defaults đưa ra một ví dụ cực đoan. Cuộc thi này có 100 tính năng thô. Vì lý do riêng tư, các tính năng có tên như f1, f2, f3  thay vì tên tiếng Anh thông thường. Điều này mô phỏng một kịch bản mà bạn có ít trực giác về dữ liệu thô.

Một đối thủ cạnh tranh nhận thấy rằng sự khác biệt giữa hai trong số các tính năng, cụ thể là f527 - f528, đã tạo ra một tính năng mới rất mạnh mẽ. Các mô hình bao gồm sự khác biệt đó như một tính năng tốt hơn nhiều so với các mô hình không có nó. Nhưng làm thế nào bạn có thể nghĩ đến việc tạo biến này khi bạn bắt đầu với hàng trăm biến?

Các kỹ thuật bạn sẽ học trong khóa học vi mô này sẽ làm cho nó minh bạch rằng  f527 và f528  là những tính năng quan trọng và vai trò của chúng bị vướng víu chặt chẽ. Điều này sẽ hướng bạn xem xét các phép biến đổi của hai biến này và có thể tìm thấy "tính năng vàng" của f527 - f528.

Khi ngày càng có nhiều bộ dữ liệu bắt đầu với 100 hoặc 1000 tính năng thô, cách tiếp cận này ngày càng trở nên quan trọng.
#### Directing Future Data Collection
* Bạn không có quyền kiểm soát các bộ dữ liệu mà bạn tải xuống trực tuyến. Nhưng nhiều doanh nghiệp và tổ chức sử dụng khoa học dữ liệu có cơ hội mở rộng loại dữ liệu họ thu thập. Thu thập các loại dữ liệu mới có thể tốn kém hoặc bất tiện, vì vậy họ chỉ muốn làm điều này nếu họ biết nó sẽ đáng giá. Thông tin chi tiết dựa trên mô hình giúp bạn hiểu rõ về giá trị của các tính năng bạn hiện có, điều này sẽ giúp bạn suy luận về những giá trị mới nào có thể hữu ích nhất.
#### Informing Human Decision-Making
* Một số quyết định được đưa ra tự động bởi các mô hình. Amazon không có con người (hoặc yêu tinh) chạy để quyết định những gì sẽ hiển thị cho bạn bất cứ khi nào bạn truy cập trang web của họ. Nhưng nhiều quyết định quan trọng được đưa ra bởi con người. Đối với những quyết định này, thông tin chi tiết có thể có giá trị hơn dự đoán.
#### Building Trust
* Nhiều người sẽ không cho rằng họ có thể tin tưởng mô hình của bạn cho các quyết định quan trọng mà không xác minh một số sự kiện cơ bản. Đây là một biện pháp phòng ngừa thông minh với tần suất lỗi dữ liệu. Trong thực tế, việc thể hiện những hiểu biết sâu sắc phù hợp với hiểu biết chung của họ về vấn đề sẽ giúp xây dựng lòng tin, ngay cả trong số những người có ít kiến thức sâu về khoa học dữ liệu.
## Permutation Importance
* Một trong những câu hỏi cơ bản nhất mà chúng ta có thể hỏi về một mô hình là: Những tính năng nào có tác động lớn nhất đến dự đoán? Khái niệm này được gọi là feature importance.

Có nhiều cách để đo lường tầm quan trọng của tính năng. Một số cách tiếp cận trả lời các phiên bản khác nhau một cách tinh tế của câu hỏi trên. Các cách tiếp cận khác đã ghi nhận những thiếu sót.
 
So với hầu hết các cách tiếp cận khác, tầm quan trọng hoán vị là:
1.	nhanh chóng để tính toán,
2.	được sử dụng và hiểu rộng rãi, và
3.	Phù hợp với các thuộc tính, chúng tôi muốn có một thước đo tầm quan trọng của tính năng.
#### How It Works
* Tầm quan trọng hoán vị sử dụng các mô hình khác với bất cứ điều gì bạn đã thấy cho đến nay và nhiều người thấy nó khó hiểu lúc đầu. Vì vậy, chúng tôi sẽ bắt đầu với một ví dụ để làm cho nó cụ thể hơn.
Xem xét dữ liệu với định dạng sau:
 
![alt text](.\img\image.png)

Chúng tôi muốn dự đoán chiều cao của một người khi họ 20 tuổi, sử dụng dữ liệu có sẵn ở tuổi 10.
Dữ liệu của chúng tôi bao gồm các tính năng hữu ích (chiều cao ở tuổi 10), các tính năng có ít khả năng dự đoán (sở hữu tất), cũng như một số tính năng khác mà chúng tôi sẽ không tập trung vào trong phần giải thích này.

Tầm quan trọng hoán vị được tính toán sau khi một mô hình đã được trang bị.Vì vậy, chúng tôi  sẽ không thay đổi mô hình hoặc thay đổi những dự đoán mà chúng tôi sẽ nhận được cho một giá trị nhất định về chiều cao, số lượng tất, v.v.

Thay vào đó, chúng tôi sẽ hỏi câu hỏi sau: Nếu tôi xáo trộn ngẫu nhiên một cột duy nhất của dữ liệu xác thực, để mục tiêu và tất cả các cột khác tại chỗ, điều đó sẽ ảnh hưởng đến độ chính xác của các dự đoán trong dữ liệu hiện đang xáo trộn đó như thế nào?
![alt text](.\img\image-1.png) 
Việc sắp xếp lại ngẫu nhiên một cột sẽ gây ra các dự đoán kém chính xác hơn, vì dữ liệu kết quả không còn tương ứng với bất cứ điều gì được quan sát trong thế giới thực. Độ chính xác của mô hình đặc biệt bị ảnh hưởng nếu chúng ta xáo trộn một cột mà mô hình phụ thuộc rất nhiều vào các dự đoán. Trong trường hợp này, xáo trộn chiều cao ở tuổi 10 sẽ gây ra những dự đoán khủng khiếp. Nếu chúng ta xáo trộn  tất sở hữu thay thế, các dự đoán kết quả sẽ không bị ảnh hưởng nhiều như vậy.

Với cái nhìn sâu sắc này, quá trình như sau:
1.	Nhận một mô hình được đào tạo.
2.	Xáo trộn các giá trị trong một cột, đưa ra dự đoán bằng cách sử dụng tập dữ liệu kết quả. Sử dụng các dự đoán này và các giá trị mục tiêu thực sự để tính toán hàm tổn thất bị xáo trộn bao nhiêu. Sự suy giảm hiệu suất đó đo lường tầm quan trọng của biến bạn vừa xáo trộn.

Trả dữ liệu về thứ tự ban đầu (hoàn tác xáo trộn từ bước 2). Bây giờ lặp lại bước 2 với cột tiếp theo trong tập dữ liệu, cho đến khi bạn đã tính toán tầm quan trọng của từng cột. 
#### Code Example
* Ví dụ của chúng tôi sẽ sử dụng một mô hình dự đoán liệu một đội bóng đá / bóng đá sẽ có người chiến thắng "Người đàn ông của trò chơi" dựa trên số liệu thống kê của đội. Giải thưởng "Người đàn ông của trò chơi" được trao cho người chơi xuất sắc nhất trong trò chơi. Xây dựng mô hình không phải là trọng tâm hiện tại của chúng tôi, vì vậy ô bên dưới tải dữ liệu và xây dựng một mô hình thô sơ.

In [1]:
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

data = pd.read_csv('../input/fifa-2018-match-statistics/FIFA 2018 Statistics.csv')
y = (data['Man of the Match'] == "Yes")  # Convert from string "Yes"/"No" to binary
feature_names = [i for i in data.columns if data[i].dtype in [np.int64]]
X = data[feature_names]
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)
my_model = RandomForestClassifier(n_estimators=100,
                                  random_state=0).fit(train_X, train_y)
```
Dưới đây là cách tính toán và thể hiện tầm quan trọng với eli5 library:

In [2]:
```python
import eli5
from eli5.sklearn import PermutationImportance

perm = PermutationImportance(my_model, random_state=1).fit(val_X, val_y)
eli5.show_weights(perm, feature_names = val_X.columns.tolist())
```
Out[2]:
| Weight        | Feature             |
|---------------|---------------------|
| 0.1750 ± 0.0848 | Goal Scored           |
| 0.0500 ± 0.0637 | Distance Covered (Kms)|
| 0.0437 ± 0.0637 | Yellow Card           |
| 0.0187 ± 0.0500 | Off-Target            |
| 0.0187 ± 0.0637 | Free Kicks            |
| 0.0187 ± 0.0637 | Fouls Committed       |
| 0.0125 ± 0.0637 | Pass Accuracy %       |
| 0.0125 ± 0.0306 | Blocked               |
| 0.0063 ± 0.0612 | Saves                 |
| 0.0063 ± 0.0250 | Ball Possession %     |
| 0 ± 0.0000      | Red                   |
| 0 ± 0.0000      | Yellow & Red          |
| 0.0000 ± 0.0559 | On-Target             |
| -0.0063 ± 0.0729| Offsides              |
| -0.0063 ± 0.0919| Corners               |
| -0.0063 ± 0.0250| Goals in PSO          |
| -0.0187 ± 0.0306| Attempts              |
| -0.0500 ± 0.0637| Passes                |


#### Interpreting Permutation Importances
* Các giá trị hướng về phía trên cùng là các tính năng quan trọng nhất và các giá trị hướng tới đáy ít quan trọng nhất.

Số đầu tiên trong mỗi hàng cho thấy hiệu suất mô hình giảm bao nhiêu khi xáo trộn ngẫu nhiên (trong trường hợp này, sử dụng "độ chính xác" làm chỉ số hiệu suất).

Giống như hầu hết mọi thứ trong khoa học dữ liệu, có một số ngẫu nhiên đối với sự thay đổi hiệu suất chính xác từ việc xáo trộn một cột. Chúng tôi đo lường lượng ngẫu nhiên trong tính toán tầm quan trọng hoán vị của chúng tôi bằng cách lặp lại quá trình với nhiều xáo trộn. Con số sau ±  đo lường hiệu suất thay đổi như thế nào từ cải tổ này sang cải tổ tiếp theo.

Đôi khi bạn sẽ thấy các giá trị âm cho tầm quan trọng hoán vị. Trong những trường hợp đó, các dự đoán về dữ liệu bị xáo trộn (hoặc nhiễu) xảy ra chính xác hơn dữ liệu thực. Điều này xảy ra khi tính năng không quan trọng (lẽ ra phải có tầm quan trọng gần bằng 0), nhưng cơ hội ngẫu nhiên khiến các dự đoán về dữ liệu xáo trộn chính xác hơn. Điều này phổ biến hơn với các bộ dữ liệu nhỏ, như trong ví dụ này, bởi vì có nhiều chỗ cho may mắn / cơ hội hơn.

Trong ví dụ của chúng tôi, tính năng quan trọng nhất là Mục tiêu ghi được. Điều đó có vẻ hợp lý. Người hâm mộ bóng đá có thể có một số trực giác về việc liệu thứ tự của các biến khác có đáng ngạc nhiên hay không.

## Partial Dependence Plots
*Mặc dù tầm quan trọng của tính năng cho thấy biến nào ảnh hưởng nhiều nhất đến dự đoán, biểu đồ phụ thuộc một phần cho thấy tính năng ảnh hưởng đến dự đoán như thế nào.

Điều này rất hữu ích để trả lời các câu hỏi như:
1.	Kiểm soát tất cả các tính năng nhà khác, kinh độ và vĩ độ có tác động gì đến giá nhà? Để nói lại điều này, những ngôi nhà có kích thước tương tự sẽ được định giá như thế nào ở các khu vực khác nhau?
2.	Sự khác biệt về sức khỏe được dự đoán giữa hai nhóm là do sự khác biệt trong chế độ ăn uống của họ, hay do một số yếu tố khác?

Nếu bạn đã quen thuộc với các mô hình hồi quy tuyến tính hoặc logistic, các biểu đồ phụ thuộc một phần có thể được diễn giải tương tự như các hệ số trong các mô hình đó. Mặc dù, các biểu đồ phụ thuộc một phần vào các mô hình phức tạp có thể nắm bắt các mẫu phức tạp hơn các hệ số từ các mô hình đơn giản. Nếu bạn không quen thuộc với hồi quy tuyến tính hoặc logistic, đừng lo lắng về sự so sánh này.

Chúng tôi sẽ đưa ra một vài ví dụ, giải thích cách giải thích các ô này và sau đó xem lại mã để tạo các ô này.
#### How it Works
*Giống như tầm quan trọng hoán vị, các biểu đồ phụ thuộc một phần được tính toán sau khi một mô hình đã được phù hợp. Mô hình này phù hợp với dữ liệu thực chưa bị thao túng giả tạo theo bất kỳ cách nào.

Trong ví dụ bóng đá của chúng tôi, các đội có thể khác nhau theo nhiều cách. Họ thực hiện bao nhiêu đường chuyền, những cú sút họ thực hiện, những bàn thắng họ ghi được, v.v. Thoạt nhìn, có vẻ khó để gỡ rối hiệu ứng của các tính năng này.

Để xem các biểu đồ từng phần phân tách hiệu ứng của từng tính năng như thế nào, chúng ta bắt đầu bằng cách xem xét một hàng dữ liệu duy nhất. Ví dụ: hàng dữ liệu đó có thể đại diện cho một đội có bóng 50% thời gian, thực hiện 100 đường chuyền, thực hiện 10 cú sút và ghi được 1 bàn thắng.

Chúng tôi sẽ sử dụng mô hình được trang bị để dự đoán kết quả của chúng tôi (xác suất cầu thủ của họ giành được "người đàn ông của trận đấu"). Nhưng chúng tôi liên tục thay đổi giá trị cho một biến để đưa ra một loạt các dự đoán. Chúng tôi có thể dự đoán kết quả nếu đội chỉ có bóng 40% thời gian. Sau đó, chúng tôi dự đoán với việc họ có bóng 50% thời gian. Sau đó dự đoán lại cho 60%. Và như vậy. Chúng tôi theo dõi các kết quả dự đoán (trên trục dọc) khi chúng tôi chuyển từ các giá trị sở hữu bóng nhỏ sang các giá trị lớn (trên trục ngang).

Trong mô tả này, chúng tôi chỉ sử dụng một hàng dữ liệu duy nhất. Tương tác giữa các đối tượng địa lý có thể khiến cốt truyện cho một hàng không điển hình. Vì vậy, chúng tôi lặp lại thí nghiệm tinh thần đó với nhiều hàng từ tập dữ liệu ban đầu và chúng tôi vẽ kết quả dự đoán trung bình trên trục dọc.
#### Code Example
* Xây dựng mô hình không phải là trọng tâm của chúng tôi, vì vậy chúng tôi sẽ không tập trung vào việc khám phá dữ liệu hoặc mã xây dựng mô hình.

In [1]:
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.tree import DecisionTreeClassifier

data = pd.read_csv('../input/fifa-2018-match-statistics/FIFA 2018 Statistics.csv')
y = (data['Man of the Match'] == "Yes")  # Convert from string "Yes"/"No" to binary
feature_names = [i for i in data.columns if data[i].dtype in [np.int64]]
X = data[feature_names]
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)
tree_model = DecisionTreeClassifier(random_state=0, max_depth=5, min_samples_split=5).fit(train_X, train_y)
```
Ví dụ đầu tiên của chúng tôi sử dụng cây quyết định, bạn có thể thấy bên dưới. Trong thực tế, bạn sẽ sử dụng nhiều mô hình ngụy biện hơn cho các ứng dụng trong thế giới thực.

In [2]:
```python
from sklearn import tree
import graphviz

tree_graph = tree.export_graphviz(tree_model, out_file=None, feature_names=feature_names)
graphviz.Source(tree_graph)
```
Out[2]:
![alt text](.\img\image-2.png)
 
 Theo hướng dẫn để đọc cây:
1.	Lá có nhánh con hiển thị tiêu chí tách của chúng trên đầu
2.	Cặp giá trị ở dưới cùng hiển thị số lượng giá trị False và giá trị True cho mục tiêu tương ứng, của các điểm dữ liệu trong nút đó của cây.
Đây là code để tạo Partial Dependence Plot bằng thư viện scikit-learn.

In [3]:
```python
from matplotlib import pyplot as plt
from sklearn.inspection import PartialDependenceDisplay

# Create and plot the data
disp1 = PartialDependenceDisplay.from_estimator(tree_model, val_X, ['Goal Scored'])
plt.show()
``` 
![alt text](.\img\image-3.png)

Trục y được hiểu là sự thay đổi trong dự đoán  từ những gì nó sẽ được dự đoán ở giá trị cơ sở hoặc ngoài cùng bên trái.
Từ biểu đồ cụ thể này, chúng ta thấy rằng ghi bàn thắng làm tăng đáng kể cơ hội chiến thắng "Người đàn ông của trận đấu". Nhưng các mục tiêu bổ sung ngoài đó dường như ít ảnh hưởng đến dự đoán.
Here's another example storyline:
In [4]:
```python
feature_to_plot = 'Distance Covered (Kms)'
disp2 = PartialDependenceDisplay.from_estimator(tree_model, val_X, [feature_to_plot])
plt.show()
``` 
![alt text](.\img\image-4.png)

Biểu đồ này có vẻ quá đơn giản để đại diện cho thực tế. Nhưng đó là bởi vì mô hình rất đơn giản. Bạn sẽ có thể thấy từ cây quyết định ở trên rằng điều này đại diện cho chính xác cấu trúc của mô hình.
Bạn có thể dễ dàng so sánh cấu trúc hoặc ý nghĩa của các mô hình khác nhau. Đây là cốt truyện tương tự với mô hình Rừng ngẫu nhiên.

In [5]:
```python
# Build Random Forest model
rf_model = RandomForestClassifier(random_state=0).fit(train_X, train_y)

disp3 = PartialDependenceDisplay.from_estimator(rf_model, val_X, [feature_to_plot])
plt.show()
``` 
![alt text](.\img\image-5.png) 

Mô hình này cho rằng bạn có nhiều khả năng giành được Man of the Match hơn nếu người chơi của bạn chạy tổng cộng 100km trong suốt trò chơi. Mặc dù chạy nhiều hơn gây ra dự đoán thấp hơn.
Nhìn chung, hình dạng mượt mà của đường cong này có vẻ hợp lý hơn so với hàm bước từ mô hình Cây quyết định. Mặc dù tập dữ liệu này đủ nhỏ để chúng tôi sẽ cẩn thận trong cách diễn giải bất kỳ mô hình nào.
#### 2D Partial Dependence Plots
* Nếu bạn tò mò về sự tương tác giữa các tính năng, các ô phụ thuộc một phần 2D cũng hữu ích. Một ví dụ có thể làm rõ điều này.

Chúng ta sẽ lại sử dụng mô hình Cây quyết định cho biểu đồ này. Nó sẽ tạo ra một cốt truyện cực kỳ đơn giản, nhưng bạn sẽ có thể khớp những gì bạn thấy trong cốt truyện với chính cái cây.
In [6]:
```python
fig, ax = plt.subplots(figsize=(8, 6))
f_names = [('Goal Scored', 'Distance Covered (Kms)')]
# Similar to previous PDP plot except we use tuple of features instead of single feature
disp4 = PartialDependenceDisplay.from_estimator(tree_model, val_X, f_names, ax=ax)
plt.show()
``` 
![alt text](.\img\image-6.png) 

Biểu đồ này hiển thị các dự đoán cho bất kỳ sự kết hợp nào giữa Số bàn thắng ghi được và Khoảng cách được bảo hiểm.

Ví dụ, chúng ta thấy những dự đoán cao nhất khi một đội ghi ít nhất 1 bàn thắng và họ chạy tổng quãng đường gần 100km. Nếu họ ghi 0 bàn, khoảng cách bao phủ không thành vấn đề. Bạn có thể thấy điều này bằng cách truy tìm thông qua cây quyết định với 0 mục tiêu?

Nhưng khoảng cách có thể ảnh hưởng đến dự đoán nếu họ ghi bàn. Hãy chắc chắn rằng bạn có thể thấy điều này từ biểu đồ phụ thuộc một phần 2D
## SHAP Values
* Bạn đã thấy (và sử dụng) các kỹ thuật để trích xuất thông tin chi tiết chung từ mô hình học máy. Nhưng nếu bạn muốn chia nhỏ cách mô hình hoạt động cho một dự đoán riêng lẻ thì sao?

Giá trị SHAP (từ viết tắt của SHapley Additive exPlanations) chia nhỏ dự đoán để hiển thị tác động của từng tính năng. Bạn có thể sử dụng cái này ở đâu?
1.	Một mô hình nói rằng một ngân hàng không nên cho ai đó vay tiền và ngân hàng được yêu cầu về mặt pháp lý để giải thích cơ sở cho mỗi lần từ chối cho vay
2.	Một nhà cung cấp dịch vụ chăm sóc sức khỏe muốn xác định những yếu tố nào đang thúc đẩy nguy cơ mắc một số bệnh của mỗi bệnh nhân để họ có thể trực tiếp giải quyết các yếu tố nguy cơ đó bằng các can thiệp sức khỏe có mục tiêu

Bạn sẽ sử dụng Giá trị SHAP để giải thích các dự đoán riêng lẻ trong bài học này. Trong bài học tiếp theo, bạn sẽ thấy cách chúng có thể được tổng hợp thành thông tin chi tiết mạnh mẽ ở cấp độ mô hình.
#### How They Work
* Giá trị SHAP diễn giải tác động của việc có một giá trị nhất định cho một tính năng nhất định so với dự đoán mà chúng tôi sẽ đưa ra nếu tính năng đó lấy một số giá trị cơ sở.

Một ví dụ rất hữu ích, và chúng ta sẽ tiếp tục ví dụ bóng đá / bóng đá từ tầm quan trọng hoán vị và các bài học về biểu đồ phụ thuộc một phần.


Chúng tôi có thể hỏi:
1.	Bao nhiêu là một dự đoán được thúc đẩy bởi thực tế là đội đã ghi được 3 bàn thắng?
Nhưng sẽ dễ dàng hơn để đưa ra một câu trả lời cụ thể, bằng số nếu chúng ta trình bày lại điều này là:
2.	Bao nhiêu là một dự đoán được thúc đẩy bởi thực tế là đội đã ghi được 3  bàn thắng, thay vì một số bàn thắng cơ bản.

Tất nhiên, mỗi đội có nhiều tính năng. Vì vậy, nếu chúng tôi trả lời câu hỏi này  cho số lượng mục tiêu, chúng tôi có thể lặp lại quy trình cho tất cả các tính năng khác.

Giá trị SHAP làm điều này theo cách đảm bảo một tài sản đẹp. Cụ thể, bạn phân tách một dự đoán bằng phương trình sau:
* **sum(SHAP values for all features) = pred_for_team - pred_for_baseline_values**
 
Đó là, các giá trị SHAP của tất cả các tính năng tổng hợp lại để giải thích tại sao dự đoán của tôi khác với đường cơ sở. Điều này cho phép chúng ta phân tách một dự đoán trong một biểu đồ như thế này:
 
![alt text](.\img\image-7.png) 

giải thích thế nào về điều này?

Chúng tôi dự đoán 0,7, trong khi base_value là 0,4979. Các giá trị đối tượng địa lý gây ra dự đoán tăng có màu hồng và kích thước hình ảnh của chúng cho thấy mức độ hiệu ứng của đối tượng. Các giá trị tính năng giảm dự đoán có màu xanh lam. Tác động lớn nhất đến từ bàn thắng ghi được là 2. Mặc dù giá trị sở hữu bóng có tác dụng có ý nghĩa làm giảm dự đoán.

Nếu bạn trừ đi chiều dài của các thanh màu xanh lam khỏi chiều dài của các thanh màu hồng, nó bằng khoảng cách từ giá trị cơ sở đến đầu ra.

Có một số phức tạp đối với kỹ thuật, để đảm bảo rằng đường cơ sở cộng với tổng các hiệu ứng riêng lẻ cộng lại với dự đoán (điều này không đơn giản như âm thanh). Chúng tôi sẽ không đi sâu vào chi tiết đó ở đây, vì nó không quan trọng đối với việc sử dụng kỹ thuật này. This blog post có một lời giải thích lý thuyết dài hơn.
## Code to Calculate SHAP Values
Chúng tôi tính toán các giá trị SHAP bằng cách sử dụng tuyệt vời Shap library.
Trong ví dụ này, chúng tôi sẽ sử dụng lại mô hình bạn đã thấy với dữ liệu Bóng đá.
In [1]:
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

data = pd.read_csv('../input/fifa-2018-match-statistics/FIFA 2018 Statistics.csv')
y = (data['Man of the Match'] == "Yes")  # Convert from string "Yes"/"No" to binary
feature_names = [i for i in data.columns if data[i].dtype in [np.int64, np.int64]]
X = data[feature_names]
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)
my_model = RandomForestClassifier(random_state=0).fit(train_X, train_y)
```
Chúng tôi sẽ xem xét các giá trị SHAP cho một hàng của tập dữ liệu (chúng tôi tùy ý chọn hàng 5). Đối với ngữ cảnh, chúng ta sẽ xem xét các dự đoán thô trước khi xem xét các giá trị SHAP.
In [2]:
```python
row_to_show = 5
data_for_prediction = val_X.iloc[row_to_show]  # use 1 row of data here. Could use multiple rows if desired
data_for_prediction_array = data_for_prediction.values.reshape(1, -1)
```

Out[2]:
array([[0.29, 0.71]])
Đội có 70% khả năng có một cầu thủ giành được giải thưởng.
Bây giờ, chúng ta sẽ chuyển sang mã để lấy giá trị SHAP cho dự đoán duy nhất đó.
In [3]:
```python
import shap  # package used to calculate Shap values

# Create object that can calculate shap values
explainer = shap.TreeExplainer(my_model)

# Calculate Shap values
shap_values = explainer.shap_values(data_for_prediction)
```
Đối  tượng shap_values ở trên là một danh sách có hai mảng. Mảng đầu tiên là các giá trị SHAP cho kết quả tiêu cực (không giành được giải thưởng) và mảng thứ hai là danh sách các giá trị SHAP cho kết quả tích cực (giành giải thưởng). Chúng ta thường nghĩ về các dự đoán theo dự đoán về một kết quả tích cực, vì vậy chúng ta sẽ rút ra các giá trị SHAP cho kết quả tích cực (rút ra shap_values[1]).

Thật cồng kềnh để xem xét các mảng thô, nhưng gói shap có một cách hay để hình dung kết quả.
```python
In [4]:
shap.initjs()
shap.force_plot(explainer.expected_value[1], shap_values[1], data_for_prediction)
``` 
![alt text](.\img\image-8.png)

Nếu bạn nhìn kỹ vào code nơi chúng ta đã tạo ra các giá trị SHAP, bạn sẽ nhận thấy chúng ta tham chiếu đến Trees in shap. TreeExplainer(my_model). Nhưng gói SHAP có giải thích cho mọi loại mô hình.
1.	shap.DeepExplainer hoạt động với các mô hình Deep Learning.
1.	shap.KernelExplainer hoạt động với tất cả các mô hình, mặc dù nó chậm hơn các Trình giải thích khác và nó cung cấp giá trị gần đúng thay vì giá trị Shap chính xác.

Dưới đây là một ví dụ sử dụng KernelExplainer để có được kết quả tương tự. Kết quả không giống nhau vì KernelExplainer cho kết quả gần đúng. Nhưng kết quả cũng cho thấy câu chuyện tương tự.

In [5]:
```python
# use Kernel SHAP to explain test set predictions
k_explainer = shap.KernelExplainer(my_model.predict_proba, train_X)
k_shap_values = k_explainer.shap_values(data_for_prediction)
shap.force_plot(k_explainer.expected_value[1], k_shap_values[1], data_for_prediction)
```
X does not have valid feature names, but RandomForestClassifier was fitted with feature names
X does not have valid feature names, but RandomForestClassifier was fitted with feature names
X does not have valid feature names, but RandomForestClassifier was fitted with feature names
The default of 'normalize' will be set to False in version 1.2 and deprecated in version 1.4.

Nếu bạn muốn thay đổi quy mô dữ liệu, hãy sử dụng Pipeline với StandardScaler trong giai đoạn tiền xử lý. Để tái tạo hành vi trước đó:
```python
from sklearn.pipeline import make_pipeline

model = make_pipeline(StandardScaler(with_mean=False), LassoLarsIC())
```
Nếu bạn muốn truyền một tham số sample_weight, bạn cần truyền nó dưới dạng tham số phù hợp cho mỗi bước của quy trình như sau:
```python
kwargs = {s[0] + '__sample_weight': sample_weight for s in model.steps}
model.fit(X, y, **kwargs)

Set parameter alpha to: original_alpha * np.sqrt(n_samples). 
```
The default of 'normalize' will be set to False in version 1.2 and deprecated in version 1.4.
If you wish to scale the data, use Pipeline with a StandardScaler in a preprocessing stage. To reproduce the previous behavior:
```python
from sklearn.pipeline import make_pipeline

model = make_pipeline(StandardScaler(with_mean=False), LassoLarsIC())
```
Nếu bạn muốn truyền một tham số sample_weight, bạn cần truyền nó dưới dạng tham số phù hợp cho mỗi bước của quy trình như sau:
```python
kwargs = {s[0] + '__sample_weight': sample_weight for s in model.steps}
model.fit(X, y, **kwargs)
```
Set parameter alpha to: original_alpha * np.sqrt(n_samples). 
 ![alt text](.\img\image-9.png)
## Advanced Uses of SHAP Values


* Chúng tôi bắt đầu bằng cách tìm hiểu về tầm quan trọng hoán vị và biểu đồ phụ thuộc một phần để có cái nhìn tổng quan về những gì mô hình đã học được.Sau đó, chúng tôi đã tìm hiểu về các giá trị SHAP để phá vỡ các thành phần của các dự đoán riêng lẻ.

Bây giờ chúng ta sẽ mở rộng các giá trị SHAP, xem cách tổng hợp nhiều giá trị SHAP có thể đưa ra các lựa chọn thay thế chi tiết hơn cho tầm quan trọng hoán vị và biểu đồ phụ thuộc một phần.
#### SHAP Values Review
* Giá trị Shap cho biết một đối tượng địa lý nhất định đã thay đổi dự đoán của chúng ta đến mức nào (so với việc chúng ta đưa ra dự đoán đó ở một số giá trị cơ sở của tính năng đó).
Ví dụ: hãy xem xét một mô hình cực kỳ đơn giản:
* **y=4∗x1+2∗x2**

Nếu  x1 lấy giá trị 2,  thay vì giá trị cơ sở là 0, thì giá trị SHAP của chúng ta cho x1 sẽ là 8 (từ 4 nhân với 2).
Đây là những khó khăn hơn để tính toán với các mô hình phức tạp mà chúng tôi sử dụng trong thực tế. Nhưng thông qua một số thuật toán thông minh, các giá trị Shap cho phép chúng ta phân tách bất kỳ dự đoán nào thành tổng các hiệu ứng của từng giá trị tính năng, mang lại một biểu đồ như thế này:
 
![alt text](.\img\image-10.png)

Ngoài sự cố tốt đẹp này cho mỗi dự đoán, các Shap library cung cấp hình ảnh trực quan tuyệt vời của các nhóm giá trị Shap. Chúng tôi sẽ tập trung vào hai trong số những hình dung này. Những hình dung này có sự tương đồng về khái niệm với tầm quan trọng hoán vị và biểu đồ phụ thuộc một phần. Vì vậy, nhiều chủ đề từ các bài tập trước sẽ kết hợp với nhau ở đây.
#### Summary Plots
Permutation importance là tuyệt vời vì nó tạo ra các số đo đơn giản để xem tính năng nào quan trọng đối với mô hình. Điều này đã giúp chúng tôi so sánh giữa các tính năng một cách dễ dàng và bạn có thể trình bày các biểu đồ kết quả cho các đối tượng phi kỹ thuật.

Nhưng nó không cho bạn biết mỗi tính năng quan trọng như thế nào. Nếu một đối tượng địa lý có tầm quan trọng hoán vị trung bình, điều đó có nghĩa là nó có
1.	một hiệu ứng lớn cho một vài dự đoán, nhưng không có tác dụng nói chung, hoặc
2.	một hiệu ứng trung bình cho tất cả các dự đoán.

Các cốt truyện tóm tắt SHAP cung cấp cho chúng ta cái nhìn toàn cảnh về tầm quan trọng của tính năng và điều gì đang thúc đẩy nó. Chúng ta sẽ đi qua một biểu đồ ví dụ cho dữ liệu bóng đá:
 
![alt text](.\img\image-11.png) 

Cốt truyện này được làm bằng nhiều dấu chấm. Mỗi dấu chấm có ba đặc điểm:
1.	Vị trí dọc cho biết tính năng mà nó đang mô tả
2.	Màu sắc cho biết tính năng đó cao hay thấp cho hàng đó của tập dữ liệu
3.	Vị trí nằm ngang cho biết ảnh hưởng của giá trị đó gây ra dự đoán cao hơn hay thấp hơn.
Ví dụ, điểm ở phía trên bên trái là dành cho một đội ghi được ít bàn thắng, giảm dự đoán xuống 0,25.

Một số điều bạn sẽ có thể dễ dàng chọn ra:
•	Mô hình bỏ qua Red and Yellow & Red Tính năng.
•	Thường Yellow Card không ảnh hưởng đến dự đoán, nhưng có một trường hợp cực đoan trong đó giá trị cao gây ra dự đoán thấp hơn nhiều.

Giá trị cao của Bàn thắng ghi được gây ra dự đoán cao hơn và giá trị thấp gây ra dự đoán thấp
Nếu bạn tìm kiếm đủ lâu, có rất nhiều thông tin trong biểu đồ này. Bạn sẽ phải đối mặt với một số câu hỏi để kiểm tra cách bạn đọc chúng trong bài tập.
#### Summary Plots in Code

In [1]:
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

data = pd.read_csv('../input/fifa-2018-match-statistics/FIFA 2018 Statistics.csv')
y = (data['Man of the Match'] == "Yes")  # Convert from string "Yes"/"No" to binary
feature_names = [i for i in data.columns if data[i].dtype in [np.int64, np.int64]]
X = data[feature_names]
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)
my_model = RandomForestClassifier(random_state=0).fit(train_X, train_y)
```
Chúng tôi nhận được các giá trị SHAP cho tất cả dữ liệu xác thực bằng mã sau. Nó đủ ngắn để chúng tôi giải thích nó trong các ý kiến.
In [2]:
```python
import shap  # package used to calculate Shap values

# Create object that can calculate shap values
explainer = shap.TreeExplainer(my_model)

# calculate shap values. This is what we will plot.
# Calculate shap_values for all of val_X rather than a single row, to have more data for plot.
shap_values = explainer.shap_values(val_X)

# Make plot. Index of [1] is explained in text below.
shap.summary_plot(shap_values[1], val_X)
 ```
![alt text](.\img\image-12.png)

Mã không quá phức tạp. Nhưng có một vài cảnh báo.
1.	Khi vẽ, chúng ta gọi shap_values[1]. Đối với các vấn đề phân loại, có một mảng riêng biệt các giá trị SHAP cho mỗi kết quả có thể xảy ra. Trong trường hợp này, chúng tôi lập chỉ mục để lấy các giá trị SHAP cho dự đoán "True".
2.	Tính toán các giá trị SHAP có thể chậm. Nó không phải là một vấn đề ở đây, bởi vì tập dữ liệu này là nhỏ. Nhưng bạn sẽ muốn cẩn thận khi chạy chúng để vẽ với các bộ dữ liệu có kích thước hợp lý. Ngoại lệ là khi sử dụng  mô hình xgboost, SHAP có một số tối ưu hóa và do đó nhanh hơn nhiều.

Điều này cung cấp một cái nhìn tổng quan tuyệt vời về mô hình, nhưng chúng ta có thể muốn đi sâu vào một tính năng duy nhất. Đó là nơi các âm mưu đóng góp phụ thuộc SHAP phát huy tác dụng.
#### SHAP Dependence Contribution Plots

* Trước đây, chúng tôi đã sử dụng Biểu đồ phụ thuộc một phần để cho thấy một tính năng duy nhất tác động đến các dự đoán như thế nào. Đây là những thông tin sâu sắc và phù hợp với nhiều trường hợp sử dụng trong thế giới thực. Thêm vào đó, với một chút nỗ lực, chúng có thể được giải thích cho khán giả phi kỹ thuật.

Nhưng có rất nhiều điều họ không thể hiện. Ví dụ, sự phân phối hiệu ứng là gì? Là hiệu ứng của việc có một giá trị nhất định khá ổn định, hoặc nó thay đổi rất nhiều tùy thuộc vào giá trị của các feaure khác. Các biểu đồ đóng góp phụ thuộc SHAP cung cấp một cái nhìn sâu sắc tương tự như PDP, nhưng chúng bổ sung thêm rất nhiều chi tiết.
 
![alt text](.\img\image-13.png) 

Bắt đầu bằng cách tập trung vào hình dạng, và chúng ta sẽ trở lại màu sắc sau một phút. Mỗi dấu chấm đại diện cho một hàng dữ liệu. Vị trí ngang là giá trị thực tế từ tập dữ liệu và vị trí dọc cho thấy giá trị đó đã làm gì với dự đoán. Thực tế điều này dốc lên trên nói rằng bạn càng sở hữu nhiều bóng, dự đoán của người mẫu càng cao để giành được  giải thưởng Người đàn ông của trận đấu.

Sự lây lan cho thấy rằng các tính năng khác phải tương tác với Sở hữu bóng. Ví dụ, ở đây chúng tôi đã nhấn mạnh hai điểm có giá trị sở hữu bóng tương tự. Giá trị đó khiến một dự đoán tăng lên và nó khiến dự đoán kia giảm.
 
![alt text](.\img\image-14.png) 

Để so sánh, một hồi quy tuyến tính đơn giản sẽ tạo ra các ô là những đường hoàn hảo, không có sự lan truyền này.
Điều này cho thấy chúng ta đi sâu vào các tương tác và các ô bao gồm mã hóa màu sắc để giúp làm điều đó. Mặc dù xu hướng chính là đi lên, bạn có thể kiểm tra trực quan xem điều đó có thay đổi theo màu chấm hay không.
Hãy xem xét ví dụ rất hẹp sau đây cho tính cụ thể.
 
![alt text](.\img\image-15.png) 

Hai điểm này nổi bật về mặt không gian là cách xa xu hướng tăng. Cả hai đều có màu tím, cho thấy đội đã ghi được một bàn thắng. Bạn có thể giải thích điều này để nói Nói chung, có bóng làm tăng cơ hội của một đội để cầu thủ của họ giành được giải thưởng. Nhưng nếu họ chỉ ghi được một bàn thắng, xu hướng đó sẽ đảo ngược và các trọng tài giải thưởng có thể phạt họ vì có bóng quá nhiều nếu họ ghi được ít bàn thắng đó.

Ngoài một vài ngoại lệ đó, sự tương tác được biểu thị bằng màu sắc không ấn tượng lắm ở đây. Nhưng đôi khi nó sẽ nhảy ra với bạn.
#### Dependence Contribution Plots in Code
* Chúng ta nhận được cốt truyện đóng góp phụ thuộc với mã sau. Dòng duy nhất khác với  dòng summary_plot là dòng cuối cùng.

In [3]:
```python
import shap  # package used to calculate Shap values

# Create object that can calculate shap values
explainer = shap.TreeExplainer(my_model)

# calculate shap values. This is what we will plot.
shap_values = explainer.shap_values(X)

# make plot.
shap.dependence_plot('Ball Possession %', shap_values[1], X, interaction_index="Goal Scored")
```  
![alt text](.\img\image-16.png)

Nếu bạn không cung cấp  một lập luận cho interaction_index, Shapley sử dụng một số logic để chọn một lập luận có thể thú vị.

Điều này không đòi hỏi phải viết nhiều mã. Nhưng bí quyết với các kỹ thuật này là suy nghĩ nghiêm túc về kết quả hơn là tự viết mã.


