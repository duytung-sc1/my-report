---
title : "Giới thiệu"
date : 2026-03-27
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

#### Thành phần Serverless
+ **Dịch vụ Serverless** là các tài nguyên được AWS quản lý hoàn toàn, tự động mở rộng, có tính sẵn sàng cao và không yêu cầu quản lý hạ tầng. Chúng cho phép bạn tập trung vào logic ứng dụng mà không cần lo lắng về việc vận hành hay khởi tạo máy chủ.
+ Trong kiến trúc này, **Amazon S3** cung cấp khả năng lưu trữ an toàn, **Amazon CloudFront** đóng vai trò là điểm truy cập toàn cầu và lớp bảo mật, còn **AWS Lambda** thực hiện các tác vụ tính toán theo yêu cầu.

#### Tổng quan Workshop
Trong workshop này, bạn sẽ triển khai một môi trường serverless hoàn toàn (100% serverless).
+ **"Lớp Frontend"** bao gồm một **S3 bucket** chứa các tệp web tĩnh. Để đảm bảo an toàn, bucket này được giữ ở chế độ riêng tư (private) và chỉ cấp quyền truy cập thông qua CloudFront bằng tính năng **Origin Access Control (OAC)**.
+ **"Lớp Backend"** sử dụng **AWS Lambda** để thực thi logic đánh giá bảo mật. Hàm được kích hoạt thông qua **Lambda Function URL**, cho phép frontend giao tiếp an toàn với backend thông qua CloudFront. Cấu hình này mô phỏng một ứng dụng web thực tế nơi backend được bảo vệ khỏi các kết nối trực tiếp từ internet công cộng.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)
