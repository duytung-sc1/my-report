---
title : "Tích hợp Slack"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 4.4.3. </b> "
---

## Tổng quan

Đây là một **bài thực hành tùy chọn** nếu bạn muốn tích hợp thông báo từ Cloud One - File Storage Security vào không gian làm việc Slack của mình dựa trên một kênh cụ thể mà bạn xác định.

Trong lần tích hợp này, chúng ta sẽ sử dụng một hàm Lambda để gửi tin nhắn đến Slack mỗi khi có một phát hiện mới (mã độc) trên Cloud One - File Storage Security.

---

## Yêu cầu chuẩn bị

### 1. Cấu hình ứng dụng Slack Webhook
Đầu tiên, bạn cần thiết lập một Incoming Webhook trong không gian làm việc Slack của mình:

1. Tạo một kênh Slack cụ thể để nhận thông báo (ví dụ: `#fss-alerts`).
2. Truy cập vào **App Directory** của Slack > Tìm kiếm **Incoming WebHooks**.
3. Nhấp vào **Incoming WebHooks**, sau đó nhấp **“Add to Slack”**.
4. Chọn kênh bạn đã tạo ở bước 1 để nhận thông báo.
5. Nhấp vào **Add Incoming WebHooks integration**.
6. **Sao chép Webhook URL**: Hãy lưu lại mã này để sử dụng khi triển khai sau này.
7. (Tùy chọn) Tùy chỉnh **Tên** (ví dụ: `FSS-Bot`) và **Biểu tượng (Icon)**.
8. Nhấp **“Save Settings”**.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/08fb51a9-8e5c-4fc0-a739-904918d02d84" />

> Để biết thêm chi tiết về cách tạo Incoming Webhooks trên Slack, bạn có thể tham khảo: [Thông tin bổ sung](https://slack.com/help/articles/115005265063-Incoming-webhooks-for-Slack).

### 2. Tìm ARN của ScanResultTopic
1. Trong bảng điều khiển AWS (AWS Console), đi tới **Services > CloudFormation**.
2. Chọn **Storage Stack** của bạn (thường nằm lồng bên trong stack All-in-One).
3. Nhấp vào tab **Resources**.
4. Cuộn xuống để tìm Logical ID có tên `ScanResultTopic`.
5. Sao chép mã **ARN** vào một nơi tạm thời.
   * *Ví dụ:* `arn:aws:sns:us-east-1:000000000000:FileStorageSecurity-StorageStack-ScanResultTopic-N8DD2JH1GRKF`

<img width="800" alt="image" src="https://github.com/user-attachments/assets/9e9af668-ca62-4cfd-896b-a8823d935ef4" />

---

## Triển khai Slack Plugin

Chúng ta sẽ sử dụng AWS Serverless Application Repository để triển khai quá trình tích hợp này.

1. Mở ứng dụng [CloudOne-FSS-Plugin-Slack](https://serverlessrepo.aws.amazon.com/applications/us-east-1/024368254241/CloudOne-FSS-Plugin-Slack) trong bảng điều khiển AWS Lambda.
2. Nhấp **Deploy**.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/8ec6d16b-0ba5-4273-918b-ed64d95b40b2" />
<img width="800" alt="image" src="https://github.com/user-attachments/assets/9095b27d-1582-4353-9f9b-7486f490210d" />

3. Điền các tham số trong phần **Application settings**:
   * **ScanResultTopicARN**: Dán mã ARN bạn đã sao chép ở phần trước.
   * **SlackChannel**: Nhập tên kênh Slack của bạn (ví dụ: `#fss-alerts`).
   * **SlackURL**: Dán Webhook URL bạn đã tạo trên Slack.
   * **SlackUsername**: Nhập tên người dùng (tên bot) bạn muốn hiển thị khi gửi thông báo.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7fb5d44c-ba55-42f7-af8a-93288d46d7cb" />
<img width="1635" height="431" alt="image" src="https://github.com/user-attachments/assets/3271d6b8-2942-41a9-a123-00aad4a7f3f5" />

4. Đảm bảo ứng dụng đạt trạng thái "create complete" (tạo hoàn tất).
<img width="800" alt="image" src="https://github.com/user-attachments/assets/0baef418-43e0-4ccc-8d25-4450898d9d21" />

5. Nhấp **Deploy**.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/cc331d2f-57ab-494f-a5d9-e55bbd9be4d9" />

Hãy đợi vài phút để trạng thái chuyển sang **Create complete**.

---

## Kiểm tra Tích hợp

Để xác minh rằng thông báo Slack đang hoạt động chính xác:

1. Tạo một sự kiện mã độc mới bằng cách tải tệp thử nghiệm `eicar` lên **Scanning Bucket** của bạn (như đã thực hiện trong các bài thực hành trước).
2. Đợi khoảng 15–30 giây để quá trình quét hoàn tất.
3. Kiểm tra kênh Slack của bạn. Bạn sẽ nhận được một thông báo chứa các chi tiết phát hiện, chẳng hạn như tên tệp, tên bucket và loại mã độc được tìm thấy.

> Để biết thêm về cấu hình nâng cao hoặc mã nguồn, hãy truy cập [GitHub Repository](https://github.com/trendmicro/cloudone-filestorage-plugins/tree/master/post-scan-actions/aws-python-slack-notification) của chúng tôi.
