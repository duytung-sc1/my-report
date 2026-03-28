---
title : "Vòng đời Triển khai"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 4.4.4. </b> "
---

## Tự động hóa việc triển khai Storage Stack cho các bucket S3 mới.

Trong bài tích hợp này, chúng ta sẽ triển khai một mẫu (template) CloudFormation để đảm bảo File Storage Security tự động giám sát bất kỳ bucket S3 mới nào được tạo ra. Ngoài ra, bất cứ khi nào một tài nguyên bucket S3 bị xóa, mẫu này cũng sẽ tự động gỡ bỏ tất cả các tài nguyên bảo mật liên quan đã được triển khai để giám sát bucket đó.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6b36a2df-ea3f-402c-9921-025fec2c965d" />

---

## Điều kiện tiên quyết

### 1. Lấy thông tin Region của tài khoản Cloud One.
* Đăng nhập vào **Cloud One**.
* Chọn **Account Settings**.
* Sao chép lại thông tin **Region**: ví dụ `us-1`.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/58769d11-9a16-45fd-99bc-422f8b3c812d" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/574d2a10-cd42-4254-abd1-871c7c409896" />

### 2. Tạo một API Key mới trong Cloud One.
* Trong mục **Account Settings** của Cloud One, chọn **API Keys** từ menu bên trái.
* Nhấp vào **New**.
* **API Key Alias**: `immersion_day`
* **Description**: (Tùy chọn).
* **Role**: `Full Access`
* **Language**: Ngôn ngữ ưu tiên của bạn.
* **Timezone**: Múi giờ ưu tiên của bạn.
* Nhấp **Next**.
* **Sao chép API Key** của bạn và lưu trữ ở nơi an toàn.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/c6fc1793-82df-4033-aab8-c98172dba78e" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/02e715fc-6bd0-4aa9-979a-8ae9fc69b238" />

### 3. Lấy tên của Scanner Stack và URL SQS của Scanner Stack.
* Truy cập vào **AWS CloudFormation**.
* Tìm và chọn **Scanner Stack** mà bạn đã triển khai.
* Nhấp vào tab **Outputs**.
* Sao chép tên của **Scanner Stack**.
* Tìm khóa (key) có tên **ScannerQueueURL**.
* Sao chép giá trị của **ScannerQueueURL**.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/1ad88048-ccb5-4fe3-93e3-33c801f2f17e" />

---

## Triển khai mẫu CloudFormation dưới đây

[Khởi tạo Stack (Launch Stack)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=c1fss-lifecycle-workshop&templateURL=https://aws-workshop-c1as-cft-templates.s3.amazonaws.com/fss-lifecycle.yml)

1. **Điền các tham số cần thiết vào mẫu với các giá trị đã sao chép trước đó:**
   * **C1API**: Dán API Key Cloud One của bạn.
   * **C1RegionEndpoint**: Dán Region của tài khoản Cloud One.
   * **SQSURL**: Dán giá trị URL SQS từ Scanner Stack.
   * **StackName**: Dán tên của Scanner Stack đã triển khai.
   * Nhấp **Next**.
   * (Tùy chọn) - Cấu hình thẻ (tags) nếu muốn.
   * Nhấp **Next**.
   * Tích vào ô xác nhận ở dưới cùng để chấp nhận việc tạo tài nguyên IAM (**acknowledge IAM resource creation**).
   * Nhấp **Create Stack**.

LaunchStack()
<img width="800" alt="image" src="https://github.com/user-attachments/assets/bcb59452-6bdc-42e9-a3e3-b97e2e4404cd" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/fe888208-87fa-4fb9-975d-6fed593a6a68" />

2. **Theo dõi quá trình triển khai stack** cho đến khi đạt trạng thái: **CREATE_COMPLETE**.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/3b537097-0eca-45bf-bad4-f0ae2919a2db" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/8d93a959-63cb-477e-b920-c9b107397ad6" />

---

## Kiểm tra tính năng tự động hóa

### Tạo một bucket S3 mới
> [NHẤP VÀO ĐÂY](https://aws.amazon.com/video/watch/5c76e13b7fe/) - Hướng dẫn từng bước để tạo một S3 bucket.

---
<img width="800" alt="image" src="https://github.com/user-attachments/assets/378851dc-a6dc-4450-8ac2-78dc65a4031c" />

### Xác minh và Dọn dẹp

1. **Theo dõi CloudFormation**: Sau khi bucket S3 được tạo, hãy kiểm tra CloudFormation để thấy Storage stack mới đang được triển khai tự động. Đợi cho đến khi stack đạt trạng thái **CREATE_COMPLETE**.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/91866103-4289-4d85-841d-3a716ad12e17" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/0f858c97-be8d-4eab-a822-26db7fddb59c" />

2. **Kiểm tra Cloud One**: Khi stack hoàn tất triển khai, hãy kiểm tra bảng điều khiển Cloud One File Storage để xác nhận bucket mới đã nằm trong danh sách được giám sát.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/6dfb554a-938e-43e7-8431-cc8e9c348d83" />

3. **Xóa bucket S3**:
   * Trong giao diện AWS, đi tới **S3**.
   * Tìm và chọn bucket bạn vừa tạo ở bước trên.
   * Nhấp **Delete**.
   * Xác nhận việc xóa bằng cách nhập/dán tên bucket và nhấp **Delete bucket**.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/15e78b50-005e-4618-882e-285148120ee0" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/6f2a2e85-fe2b-4272-b912-830f06fdaad7" />

4. **Theo dõi việc gỡ bỏ**: Kiểm tra **CloudFormation** để thấy stack tương ứng đang được tự động gỡ bỏ.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/deed64a2-786f-47e4-baa8-06734c262211" />

5. **Kiểm tra cuối cùng**: Sau khi stack bị xóa, hãy kiểm tra lại bảng điều khiển Cloud One File Storage để xác nhận bucket không còn nằm trong danh sách giám sát.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/fc91869b-ea2a-4eb9-942a-492760cb2d98" />
