---
title : "Triển khai Cloud One File Storage Security"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 4.3. </b> "
---

# Triển khai 

## Tạo S3 Bucket

[BẤM VÀO ĐÂY](https://aws.amazon.com/video/watch/5c76e13b7fe/) - Nếu bạn chưa có S3 Bucket và cần tạo một cái cho bài thực hành này!

---

## Triển khai Cloud One - File Storage Security

Cách tốt nhất để học là thực hành, vì vậy hãy cùng triển khai Cloud One - File Storage Security lên Tài khoản AWS của chúng ta. Trước tiên, hãy đảm bảo rằng tất cả các yêu cầu đã được đáp ứng, sau đó:

1. Đăng nhập vào [Nền tảng Cloud One](https://cloudone.trendmicro.com/), hệ thống sẽ yêu cầu thông tin đăng nhập Cloud One của bạn. Trong trường hợp bạn chưa có, hãy kiểm tra lại trang yêu cầu chứa tất cả các chi tiết cần thiết để tạo tài khoản.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/6cfeb834-fd01-445a-b103-64adf757cb2c" />

2. Chọn ô **File Storage Security**.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/94319145-f628-4239-8424-0cb9337cc07e" />

3. Nhấp vào **Stack management** (Quản lý ngăn xếp) ở phía bên trái giao diện của bạn.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/7e9bfbb4-7ca2-4d33-aa98-a31bc1c28d05" />

4. Nhấp vào **Deploy** (Triển khai).
<img width="800" alt="image" src="https://github.com/user-attachments/assets/796f660d-1b35-43da-90cf-b61123fcef59" />

5. Chọn **Scanner Stack and Storage Stack**, để triển khai toàn bộ giải pháp lên tài khoản AWS của bạn.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/3d4c17e9-be1a-472d-b860-9a0be0a239c7" />

6. Chọn khu vực (region) AWS phù hợp nhất với bạn (trong số các khu vực AWS được hỗ trợ) và nhấp vào **Launch Stack** (Khởi chạy ngăn xếp). Thao tác này sẽ chuyển hướng bạn đến tài khoản AWS của mình tại khu vực bạn đã chọn để triển khai. Hãy đảm bảo rằng bạn đã đăng nhập và có các quyền chính xác, bạn có thể kiểm tra chi tiết các quyền cần thiết trong phần Yêu cầu.
   
   > **Lưu ý:** Cố gắng đảm bảo tab bảng điều khiển Cloud One nằm trên cùng một cửa sổ trình duyệt, bằng cách này, quá trình Launch Stack sẽ tự động sử dụng phiên bản (session) AWS mà bạn đang mở sẵn.
   
   *Bạn có thể xác thực Cloud Formation Template bằng cách nhấp vào **Review Stack**. Để dễ dàng hơn, bạn cũng có thể xác minh cấu trúc mẫu này bằng cách nhấp vào các nút bên dưới:* [All In One Template](https://github1s.com/trendmicro/cloudone-filestorage-cloudformation-templates/blob/master/aws/FSS-All-In-One.template)||
   [Scanner Stack](https://github1s.com/trendmicro/cloudone-filestorage-cloudformation-templates/blob/master/aws/FSS-Scanner-Stack.template)||
   [Storage ](https://github1s.com/trendmicro/cloudone-filestorage-cloudformation-templates/blob/master/aws/FSS-Scanner-Stack.template)
<img width="800" alt="image" src="https://github.com/user-attachments/assets/c5704cdf-c717-4300-b45e-3bc24644f646" />

7. Trong trang CloudFormation, tham số bắt buộc duy nhất ở đây là tên của bucket mà bạn chọn để quét, chỉ cần thêm nó vào phần cấu hình (S3BucketToScan). Trong trường hợp của chúng ta, vui lòng sử dụng tên của S3 bucket mà bạn đã tạo trước đó trong bài thực hành này, hoặc sử dụng một S3 bucket có sẵn mà bạn muốn.

Nó cũng hỗ trợ các tham số khác nhau để tùy chỉnh cài đặt của bạn, chẳng hạn như Tiền tố tài nguyên (Resource prefixes) và tùy chọn tích hợp KMS. Để biết thêm chi tiết về các cấu hình này, hãy kiểm tra [Tài liệu hướng dẫn](https://cloudone.trendmicro.com/docs/file-storage-security/gs-deploy-all-in-one-stack/) của chúng tôi.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/818717f0-6e6e-47e0-ad11-88206d2beb2d" />

Sau khi thêm tên bucket, bạn sẽ cần đánh dấu xác nhận và nhấp vào "Create Stack" (Tạo ngăn xếp).

8. Trong trang CloudFormation, tham số bắt buộc duy nhất ở đây là tên của bucket mà bạn chọn để quét, chỉ cần thêm nó vào phần cấu hình (`S3BucketToScan`). Trong trường hợp của chúng ta, vui lòng sử dụng tên của S3 bucket mà bạn đã tạo trước đó trong bài thực hành này, hoặc sử dụng một S3 bucket có sẵn mà bạn muốn.
   
   > **Lưu ý:** Nó cũng hỗ trợ các tham số khác nhau để tùy chỉnh cài đặt của bạn, chẳng hạn như Tiền tố tài nguyên và tùy chọn tích hợp KMS. Để biết thêm chi tiết về các cấu hình này, hãy kiểm tra Tài liệu hướng dẫn của chúng tôi.
   
   Sau khi thêm tên bucket, bạn sẽ cần đánh dấu xác nhận và nhấp vào **Create Stack**.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/7bc8c8b7-da52-4954-bcb5-f7bfeff05963" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/4777cb73-df80-4f7e-be4f-f6c671362f8c" />

9. Sau khi triển khai ngăn xếp tất-cả-trong-một (all-in-one) trên tài khoản AWS của bạn, bạn phải cấu hình thông tin Amazon Resource Names (ARNs) của scanner stack và storage stack trong bảng điều khiển Cloud One. Các ARN này sẽ ánh xạ (map) một scanner stack với một storage stack, cho phép chúng nhận diện được nhau.
   
   Đi tới **CloudFormation > Stacks > [tên ngăn xếp all-in-one của bạn] > tab Outputs** và sao chép phần Giá trị (Value) tương ứng với các Khóa (Key) `ScannerStackManagementRoleARN` và `StorageStackManagementRoleARN`, sau đó dán thông tin này vào bảng điều khiển Cloud One - File Storage Security.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/5705c705-b5a0-4704-b106-26024e2c6c3f" />

Sau đó nhấp vào **Submit** (Gửi). Bạn sẽ thấy một vài thông báo thành công ở phía dưới cùng và ngăn xếp này cũng sẽ hiển thị trong mục Stack Management.

Bạn hiện đã hoàn tất việc triển khai ngăn xếp All-in-One, hãy cùng kiểm tra quá trình triển khai của chúng ta.

Tất cả các đối tượng (object) mới được tải lên bucket mà bạn đã thiết lập để quét, giờ đây sẽ tự động được quét để tìm phần mềm độc hại và được gắn thẻ là "malicious" (độc hại) hoặc "no issues found" (không tìm thấy vấn đề).

Dưới đây là video hướng dẫn từng bước về cách triển khai ngăn xếp All-in-One cho File Storage Security: [Deploying the File Storage Security All In One Stack
](https://youtu.be/_w1_k5W3tEQ?si=r5wNHPB9GyuWfVpE)
