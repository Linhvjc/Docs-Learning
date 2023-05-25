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
Đây là kỹ thuật mà chúng ta sử dụng kết quả mà các mô hình dự đoán để tạo ra một mô hình mới bằng cách học cách kết hợp đầu ra của các mô hình đơn lẻ đó. Quá trình này giúp cải thiện mô hình cuối cùng bằng cách cân bằng những ưu và nhược điểm của các mô hình khác.
