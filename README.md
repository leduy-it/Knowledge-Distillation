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
- **Feature-based Knowledge Distillation:** Được mô tả trong Hình 3a, kiến thức được chuyển giao từ teacher model sang student model thông qua các đặc trưng (features) mà teacher model học được. Mục tiêu là làm cho các đặc trưng của student model tương tự như teacher model, thông qua việc giảm thiểu sự khác biệt giữa các đặc trưng của hai mô hình nhờ vào Distillation Loss. Điều này có thể bao gồm việc so sánh các feature maps hoặc các intermediate layers giữa hai mô hình. Phương pháp này giúp student model không chỉ học cách dự đoán đầu ra mà còn học cách trích xuất và xử lý thông tin giống như teacher model.
- **Logit-based Knowledge Distillation:** Phương pháp này tập trung vào việc chuyển giao kiến thức từ các logits như được minh họa trong Hình 3b. Logits thường chứa thông tin ngữ nghĩa cao vì chúng bảo toàn nhiều thông tin về mức độ tự tin và mối quan hệ giữa các lớp của đầu ra. Mục tiêu là làm cho logits của student model gần với logits của teacher model nhất có thể. Điều này thường được thực hiện bằng cách giảm thiểu sự khác biệt (ví dụ qua hàm loss như KL divergence ) giữa logits của hai mô hình.
![Screenshot 2024-02-28 at 22 45 54](https://github.com/leduy-it/Knowledge-Distillation/assets/85160629/02b9c727-ab2c-4f40-b37d-ba033f683d4c)
---------



```
| Dataset Name            | Samples | Accuracy (05/12) | Accuracy (12/12) | Accuracy (19/12) | Accuracy (26/12) | Accuracy (02/01) | NED (05/12) | NED (12/12) | NED (19/12) | NED (26/12) | NED (02/01) |
|-------------------------|----------|------------------|------------------|------------------|------------------|------------------|-------------|-------------|-------------|-------------|-------------|
| RKKCS_address          | 740      | 0.894737        | 0.9230          | 0.9378          | 0.9392          | **0.9514**      | 0.991923    | 0.9931      | 0.9952      | 0.9954      | **0.9961**  |
| RKKCS_building_name    | 740      | 0.763441        | 0.8113          | 0.8962          | 0.9016          | **0.9284**      | 0.955724    | 0.9660      | 0.9813      | 0.9816      | **0.9874**  |
| RKKCS_first_name_kanji | 1854     | 0.936961        | 0.9461          | **0.9639**      | 0.9612          | 0.9601          | 0.969783    | 0.9725      | **0.9810**  | 0.9804      | 0.9800      |
| RKKCS_last_name_kanji  | 1853     | 0.952561        | 0.9520          | 0.9676          | 0.9665          | **0.9682**      | 0.977000    | 0.9762      | 0.9839      | 0.9833      | **0.9840**  |
| RKKCS_name_hira        | 3667     | 0.900402        | 0.9266          | 0.9596          | 0.9643          | **0.9659**      | 0.969749    | 0.9780      | 0.9881      | 0.9897      | **0.9901**  |
| SRA_2                  | 1249     | 0.776006        | 0.8998          | 0.9319          | **0.9399**      | 0.9351          | 0.965842    | 0.9858      | 0.9892      | 0.9895      | **0.9897**  |
| SRA_customer           | 62       | 0.893939        | 0.9355          | 0.9839          | **1.0000**      | **1.0000**      | 0.986340    | 0.9972      | 0.9995      | **1.0000**  | **1.0000**  |
| number_1               | 369      | **0.953930**    | 0.9404          | 0.9458          | 0.9485          | 0.9458          | **0.995565** | 0.9943      | 0.9946      | 0.9948      | 0.9946      |
| number_2               | 369      | 0.937669        | **0.9485**      | 0.9431          | 0.9404          | **0.9485**      | 0.994108    | **0.9948**  | 0.9944      | 0.9941      | **0.9948**  |
| number_3               | 369      | 0.943089        | 0.9404          | **0.9539**      | 0.9566          | **0.9539**      | 0.994354    | 0.9941      | 0.9956      | **0.9958**  | **0.9958**  |
| number_4               | 369      | 0.927891        | 0.9350          | 0.9458          | 0.9377          | 0.9350          | 0.992971    | 0.9939      | **0.9944**  | 0.9939      | 0.9936      |
| number_5               | 369      | 0.943089        | 0.9485          | **0.9512**      | 0.9458          | **0.9539**      | 0.993636    | 0.9946      | 0.9944      | 0.9944      | **0.9951**  |
| number_6               | 261      | 0.874552        | 0.8736          | 0.8697          | 0.8736          | **0.8774**      | 0.957885    | 0.9587      | 0.9559      | **0.9583**  | **0.9583**  |
| number_7               | 306      | 0.957055        | **0.9673**      | 0.9608          | 0.9542          | 0.9575          | 0.980061    | **0.9891**  | 0.9842      | 0.9831      | 0.9842      |
| **Overall Average (Weighted)** | **11,578** | **0.8995** | **0.9258** | **0.9502** | **0.9519** | **0.9547** | **0.9746** | **0.9802** | **0.9868** | **0.9872** | **0.9878** |
```
