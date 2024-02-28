# Knowledge-Distillation

## Tổng quan
  - Knowledge Distillation (KD) là một kỹ thuật trong lĩnh vực học máy và trí tuệ nhân tạo, nhằm mục đích chuyển giao kiến thức từ một mô hình lớn (teacher model) sang một mô hình nhỏ hơn (student model)
  - Mục tiêu của kỹ thuật này là tạo ra một mô hình nhỏ gọn hơn có khả năng thực hiện các nhiệm vụ tương tự như mô hình lớn, nhưng với hiệu suất tính toán thấp hơn như trong các thiết bị di động hoặc các hệ thống nhúng, tối ưu hóa việc sử dụng tài nguyên và tăng khả năng triển khai mô hình trong các ứng dụng thực tế như xe không người lái, hệ thống giao thông thông minh,...
### Ý tưởng:
<p> Như trong Hình. 1 thông tin được chuyển từ teacher model sang student model thông qua quá trình huấn luyện. Student model không chỉ học từ dữ liệu đánh nhãn mà còn học cách mô phỏng cách mà teacher model đưa ra dự đoán. Điều này thường được thực hiện bằng cách sử dụng đầu ra của teacher model (ví dụ, xác suất dự đoán (logits) của các lớp) làm mục tiêu “mềm” trong quá trình huấn luyện của student model thông qua Distillation Loss như trong phương trình 1 và 2. </p>

![distillation](https://github.com/leduy-it/Knowledge-Distillation/assets/85160629/2d23be51-aa12-4b4f-8181-aafbf8c9615f)

---
## So sánh Transfer learning và Knowledge Distillation

#### Bảng 1: So sánh giữa Transfer Learning và Knowledge Distillation 
|       Tiêu chí       |      Transfer learning        | Knowledge Distillation     |
| :------------:|:-------------:|:-----:|
|    Mục đích như trong Hình. 2          |      Chuyển giao kiến thức (copy weights) từ mô hình đào tạo sẵn        |  Chuyển giao kiến thức từ mô hình lớn sang mô hình nhỏ   |
|     Mô hình nguồn         |     Mô hình được huấn luyện trước    |  Mô hình lớn (teacher model)   |
|    Mô hình đích         | Mô hình mới cần được tinh chỉnh           |    Mô hình nhỏ hơn (student model)  |
| Phương pháp | Tinh chỉnh các lớp của mô hình | Sử dụng đầu ra của mô hình teacher để huấn luyện mô hình student |
| Ứng dụng | NLP, Computer Vision, v.v. | Nén mô hình, tăng hiệu suất | 

---
#### Hình 2: Sự khác biệt về kiến trúc giữa Transfer Learning và Knowledge Distillation

![Screenshot 2024-02-28 at 22 19 55](https://github.com/leduy-it/Knowledge-Distillation/assets/85160629/30807e5b-6cdc-4501-9c4b-a720780a7b2e)

---------
## Các cơ chế Knowledge Distillation
Trong Knowledge Distillation có hai cơ chế chính Feature-based và Logit-based:
- ** Feature-based Knowledge Distillation: **Được mô tả trong Hình 3a, kiến thức được chuyển giao từ teacher model sang student model thông qua các đặc trưng (features) mà teacher model học được. Mục tiêu là làm cho các đặc trưng của student model tương tự như teacher model, thông qua việc giảm thiểu sự khác biệt giữa các đặc trưng của hai mô hình nhờ vào Distillation Loss. Điều này có thể bao gồm việc so sánh các feature maps hoặc các intermediate layers giữa hai mô hình. Phương pháp này giúp student model không chỉ học cách dự đoán đầu ra mà còn học cách trích xuất và xử lý thông tin giống như teacher model.
- ** Logit-based Knowledge Distillation: **: Phương pháp này tập trung vào việc chuyển giao kiến thức từ các logits như được minh họa trong Hình 3b. Logits thường chứa thông tin ngữ nghĩa cao vì chúng bảo toàn nhiều thông tin về mức độ tự tin và mối quan hệ giữa các lớp của đầu ra. Mục tiêu là làm cho logits của student model gần với logits của teacher model nhất có thể. Điều này thường được thực hiện bằng cách giảm thiểu sự khác biệt (ví dụ qua hàm loss như KL divergence ) giữa logits của hai mô hình.
![Screenshot 2024-02-28 at 22 45 54](https://github.com/leduy-it/Knowledge-Distillation/assets/85160629/02b9c727-ab2c-4f40-b37d-ba033f683d4c)
