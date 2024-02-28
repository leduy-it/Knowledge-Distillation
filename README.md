# Knowledge-Distillation

### Tổng quan
  - Knowledge Distillation (KD) là một kỹ thuật trong lĩnh vực học máy và trí tuệ nhân tạo, nhằm mục đích chuyển giao kiến thức từ một mô hình lớn (teacher model) sang một mô hình nhỏ hơn (student model)
  - Mục tiêu của kỹ thuật này là tạo ra một mô hình nhỏ gọn hơn có khả năng thực hiện các nhiệm vụ tương tự như mô hình lớn, nhưng với hiệu suất tính toán thấp hơn như trong các thiết bị di động hoặc các hệ thống nhúng, tối ưu hóa việc sử dụng tài nguyên và tăng khả năng triển khai mô hình trong các ứng dụng thực tế như xe không người lái, hệ thống giao thông thông minh,...
### Ý tưởng:

<p> Như trong Hình. 1 thông tin được chuyển từ teacher model sang student model thông qua quá trình huấn luyện. Student model không chỉ học từ dữ liệu đánh nhãn mà còn học cách mô phỏng cách mà teacher model đưa ra dự đoán. Điều này thường được thực hiện bằng cách sử dụng đầu ra của teacher model (ví dụ, xác suất dự đoán (logits) của các lớp) làm mục tiêu “mềm” trong quá trình huấn luyện của student model thông qua Distillation Loss như trong phương trình 1 và 2. </p>

![distillation](https://github.com/leduy-it/Knowledge-Distillation/assets/85160629/24cb37da-cf49-4926-b188-edbc36eae492)
