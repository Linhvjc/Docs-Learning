# Ensemble learning

## 1. Giới thiệu 
Ensemble learning là một kỹ thuật học máy kết hợp những mô hình đơn lẻ (mô hình yếu) để tạo ra một mô hình mạnh hơn. Mô hình yếu là mô hình có thể là có bias hoặc variance quá cao. Ý tưởng của phương pháp này là mỗi mô hình sẽ có các dự đoán độc lập với nhau, sau đó kết hợp những dự đoán này lại để đưa ra dự đoán cuối cùng

## 2. Kỹ thuật Ensemble đơn giản
### 2.1 Max voting
Kỹ thuật này là phương pháp đưa ra dự đoán dựa trên kết quả có số lần xuất hiện nhiều nhất. Ví dụ: Có 7 người review cho nhà hàng hải sản, trong đó có 3 người dự đưa ra đánh giá 4*, 2 người đánh giá 2*, 2 người đánh giá 5*. Sau khi có được 7 đánh giá trên, chúng ta thấy có 3 người dự đoán 4*, số lượng người lớn hơn so với 2* và 5*. Vậy nên đánh giá chung cho cửa hàng này sẽ có kết quả là 4*

### 2.2 Averaging
Kỹ thuật này là kỹ thuật sử dụng phương pháp tính trung bình tất cả các kết quả đã nhận được. Nếu áp dụng với ví dụ ở phần trên, chúng ta sẽ có được kết quả đánh giá cho nhà hàng này là (3x4 + 2x2 + 2x5)/7 = 3.7*

### 2.3 Weighted average
Kỹ thuật này là kỹ thuật sử dụng phương pháp tính trung bình dựa vào độ ưu tiên của mỗi kết quả. Đối với ví dụ phía trên có 5 người không biết gì về hải sản, 2 người là chuyên gia về hải sản. Vậy nên đối với các đánh giá của chuyên gia sẽ có độ ưu tiên để đánh giá nhiều hơn, nói cách khác thì weighted sẽ nhiều hơn.

## 3. Kỹ thuật Ensemble nâng cao
### 3.1 Staking
Đây là kỹ thuật mà chúng ta sử dụng kết quả mà các mô hình (các mô hình thường khác nhau) dự đoán để tạo ra một mô hình mới bằng cách học cách kết hợp đầu ra của các mô hình đơn lẻ đó. Quá trình này giúp cải thiện mô hình cuối cùng bằng cách cân bằng những ưu và nhược điểm của các mô hình khác.

**Ví dụ cụ thể:**
Chúng ta có 2 mô hình base, sau đó chúng ta sẽ cho hai mô hình học trên tập training và sau đó dự đoán trên chính tập training đó. Cuối cùng chúng ta sẽ sử dụng kết quả dự đoán của hai mô hình đó để mô hình chính của chúng ta (meta-model) học. Qua quá trình trên chúng ta đã có được mô hình meta-model là sự kết hợp giữa hai mô hình base. Tuy nhiên khi thực hiện dự đoán dữ liệu mới thì chúng ta cũng phải cần model base đưa ra kết quả dự đoán của chúng, sau đó meta model mới thực hiện dự đoán được. Nó khiến cho chương trình tốn thời gian và bộ nhớ.

### 3.2 Blending
Đây là kỹ thuật cũng tương tự như với Stacking, tuy nhiên thay vì chúng ta training và dự đoán trên chính tập training thì chúng ta sẽ chia tập training ra thành tập train và valid. Sau đó các mô hình base sẽ tiến hành training trên tập train và dự đoán trên tập valid, sau đó sẽ lấy kết quả đó làm tập training cho meta-model. Blending cũng có nhược điểm tương tự như Stacking

### 3.3 Bagging
Đây là kỹ thuật mà chúng ta sẽ biến dữ liệu training gốc thành n dữ liệu có kích thước bằng với dữ liệu gốc. Chúng ta sẽ đưa các mô hình base training trên các tập dữ liệu đó, mỗi mô hình sẽ training trên mỗi tập dữ liệu khác nhau. Sau đó chúng ta lưu lại toàn bộ các mô hình trên, khi mà muốn dự đoán tập test, chúng ta sẽ thực hiện lấy toàn bộ mô hình đó ra và dự đoán, sau đó dự đoán và dựa theo các phương pháp sau để lấy ra kết quả cuối cùng
- Phương pháp voting, kết quả cuối cùng sẽ là kết quả được nhiều mô hình đưa ra nhất
- Phương pháp lấy ra kết quả trung bình
- Phương pháp lấy trung bình trọng số
**Lưu ý:** Việc chia dữ liệu có thể gây ra sự khó hiểu, vậy nên hãy theo dói ví dụ sau, chúng ta có tập dữ liệu gồm [1,2,3,4], chúng ta sẽ thực hiện biến đổi dữ liệu thành các dữ liệu có kích thước giống dữ liệu gốc, tập dữ liệu mới sẽ có thể là [1,1,1,1], [1,3,4,1], [2,2,3,3], [4,3,2,1], [2,1,1,4], .....

### 3.4 Bootsting
Đây là kỹ thuật mà chúng ta sẽ tạo mô hình đầu tiên sau đó huấn luyện trên tập con ngẫu nhiên và dự đoán trên toàn bộ tập dữ liệu, những điểm dữ liệu có kết quả dự đoán sai sẽ được gán trọng số lớn. Chúng ta sẽ tiếp tục khởi tạo mô hình tiếp theo và thực hiện training trên tập con và dự đoán trên toàn bộ dữ liệu, mô hình này sẽ cố gắng dự đoán đúng trên các dữ liệu đã sai ở mô hình trước đó, chúng ta sẽ tiếp tục như vậy và sau đó kết hợp tất cả các mô hình đó thành một mô hình cuối cùng

### 3.5 AdaBoost
Đây là kỹ thuật mà chúng ta đầu tiên sẽ gán trọng số cho tất cả các sample bằng nhau, bởi vì lần đầu training chúng ta sẽ không biết là sample nào quan trọng hơn. Tiếp theo chúng ta sẽ khởi tạo một mô hình yếu để tiến hành dự đoán, mô hình yếu có nghĩa rằng nó chỉ hơn mô hình phân loại ngẫu nhiên một tí thôi, ở đây người ta thường dùng mô hình 'gốc cây' - Mô hình DecisionTree chỉ có 2 nốt và dept = 1. Chúng ta sẽ thực hiện training trên dữ liệu này và tiến hành dự đoán trên dữ liệu này, sau đó những sample được dự đoán đúng sẽ có trọng số giảm đi, những sample dự đoán sai sẽ có trọng số tăng lên. Tiếp tục chúng ta sẽ tạo tập dữ liệu mới dựa trên trọng số, các sample có trọng số cao sẽ được xuất hiện nhiều hơn trong tập dữ liệu này và sử dụng mô hình 'gốc cây' khác để thực hiện training và dự đoán. Quá trình này sẽ được lặp lại cho đến khi sai số đến ngưỡng mà chúng ta định nghĩa hoặc có số lần lặp như chúng ta muốn.
