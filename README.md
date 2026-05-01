# datathon_vinuni

1. Exploratory Data Analysis (EDA)

Thực hiện trong Vin_graph.ipynb:
- Phân tích xu hướng theo thời gian
- Phát hiện các pattern quan trọng:
    + Seasonality rất mạnh theo quý (Q2 cao nhất, Q4 thấp nhất)
    + Thứ tự các tháng gần như ổn định qua nhiều năm
    + Có sự thay đổi level (trend shift) giữa các năm

➡️ Insight quan trọng: Dữ liệu không ngẫu nhiên mà có cấu trúc lặp lại rõ ràng → có thể khai thác bằng feature engineering thay vì chỉ dùng lag

2. Feature Engineering
- Tập trung vào các feature mang tính giải thích (explanatory features):
    + Time-based features
    + Month
    + Quarter
    + Trend (time index)
    + External features
    + Promotion (promo) → feature quan trọng nhất
    + Thử nghiệm (nhưng không ưu tiên)
    + Lag features
    + Rolling statistics

=> Lag/rolling không cải thiện nhiều → ưu tiên model đơn giản nhưng đúng signal

3. Modeling Strategy
Sử dụng các model tree-based:
  - LightGBM
  - CatBoost
Lý do:
  - Xử lý tốt dữ liệu tabular
  - Bắt được nonlinear relationship
  - Không cần scaling
  - Chiến lược chính:
  - Không overfit bằng cách thêm quá nhiều feature
  - Tập trung vào:
  - Trend
  - Seasonality (gián tiếp qua month/quarter)
  - Promotion

4. Hyperparameter Optimization
Sử dụng Optuna để:
  - Tune các tham số của model
  - Tự động tìm cấu hình tối ưu
Ví dụ:
  + learning rate
  + num leaves
  + depth
  + regularization
=>  Giúp cải thiện performance mà không cần thay đổi pipeline

5. Validation Strategy
  - Sử dụng time-based split
  - Không shuffle dữ liệu
  - Đảm bảo model học đúng theo thứ tự thời gian

6. Pipeline Huấn luyện & Submission
Thực hiện trong: final-submission-upgraded-report.ipynb (Kaggle)
Bao gồm:
  - Data preprocessing
  - Feature engineering
  - Training model
  - Prediction
  - Generate file submission
📈 Insight quan trọng
    + Dữ liệu có seasonality cực mạnh → yếu tố quyết định
    + Promotion có ảnh hưởng lớn đến doanh số
    + Model đơn giản + feature tốt > model phức tạp
