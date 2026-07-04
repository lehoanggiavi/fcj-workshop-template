---
title: "Blog 1 - Phát hiện gian lận thẻ tín dụng bằng Machine Learning trên AWS"
date: 2026-04-19
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Xây dựng hệ thống phát hiện gian lận thẻ tín dụng thời gian thực trên nền tảng AWS

## 1. Đặt vấn đề

Trong kỷ nguyên số, gian lận thẻ tín dụng gây ra thiệt hại rất lớn cho ngành tài chính. Thách thức của bài toán này không chỉ nằm ở việc phát hiện giao dịch gian lận, mà còn nằm ở tốc độ phản ứng: hệ thống cần phát hiện dấu hiệu bất thường gần như ngay lập tức, trước khi giao dịch được hoàn tất hoặc gây ra thiệt hại lớn hơn.

Trong bài viết này, nhóm chia sẻ quá trình thiết kế một pipeline trên AWS nhằm tự động tiếp nhận giao dịch, xử lý dữ liệu theo thời gian thực, gọi mô hình Machine Learning để dự đoán rủi ro gian lận và gửi cảnh báo cho quản trị viên khi phát hiện giao dịch nghi ngờ.

## 2. Phân tích kiến trúc hệ thống

Hệ thống được chia thành hai khu vực chính: **Training Zone** và **Real-time Zone**. Hai khu vực này hoạt động độc lập ở từng giai đoạn, nhưng liên kết với nhau thông qua mô hình đã được huấn luyện và triển khai trên Amazon SageMaker.

### A. Training Zone

**Amazon S3 Data Lake** đóng vai trò là nơi lưu trữ dữ liệu giao dịch lịch sử. Dữ liệu này có thể bao gồm dữ liệu gốc, dữ liệu đã xử lý, tập train/test và các artifact sinh ra trong quá trình huấn luyện.

**Amazon SageMaker** là thành phần trung tâm của khu vực huấn luyện. Dữ liệu từ S3 được đưa vào SageMaker để thực hiện tiền xử lý, feature engineering, huấn luyện và đánh giá mô hình. Sau khi mô hình đạt kết quả kỳ vọng, các artifact như `model.joblib`, `scaler.joblib` và `inference.py` được đóng gói thành `model.tar.gz`, sau đó triển khai thành một SageMaker Real-time Endpoint để sẵn sàng phục vụ dự đoán.

### B. Real-time Zone

**Amazon API Gateway** và **AWS Lambda** là điểm vào của hệ thống realtime. Khi người dùng hoặc hệ thống giao dịch gửi request, API Gateway tiếp nhận request và kích hoạt Lambda để parse JSON, validate dữ liệu và chuẩn hóa định dạng đầu vào.

**Amazon Kinesis Data Streams** đóng vai trò như một lớp đệm tốc độ cao cho luồng giao dịch. Thay vì để Lambda đầu vào gọi trực tiếp mô hình, transaction được đưa vào Kinesis để giúp hệ thống tách biệt bước tiếp nhận dữ liệu và bước xử lý dự đoán. Cách thiết kế này giúp pipeline chịu tải tốt hơn khi lưu lượng tăng đột biến.

Ở bước inference, một Lambda khác đọc dữ liệu từ Kinesis, thực hiện mapping feature và gọi đến SageMaker Endpoint để nhận kết quả dự đoán. Nếu giao dịch được phân loại là `Fraud`, hệ thống sẽ gửi cảnh báo qua **Amazon SNS** đến email của quản trị viên.

Song song với quá trình cảnh báo, dữ liệu giao dịch và kết quả prediction được ghi về **Amazon S3** thông qua **Kinesis Data Firehose**. Phần dữ liệu này có thể dùng cho audit, phân tích sau triển khai hoặc tái huấn luyện mô hình trong tương lai.

## 3. Những bài học và chia sẻ từ nhóm

Trong quá trình thiết kế kiến trúc, nhóm rút ra một số kinh nghiệm thực tiễn về cách lựa chọn và kết hợp các dịch vụ AWS cho bài toán phát hiện gian lận.

### Sử dụng dịch vụ phù hợp với từng vai trò cụ thể

Ban đầu, nhóm cân nhắc sử dụng một Lambda duy nhất để vừa nhận request, vừa xử lý dữ liệu, vừa gọi mô hình. Cách này đơn giản hơn, nhưng dễ làm hệ thống bị phụ thuộc chặt giữa bước tiếp nhận giao dịch và bước dự đoán.

Việc đưa Amazon Kinesis vào giữa giúp tách biệt hai phần này. Lambda đầu vào chỉ cần tập trung vào việc nhận và kiểm tra dữ liệu, còn Lambda xử lý phía sau có thể đọc stream và gọi SageMaker Endpoint. Thiết kế này giúp hệ thống dễ mở rộng hơn và giảm rủi ro mất giao dịch khi lưu lượng tăng đột biến.

### Tự động hóa luồng cảnh báo

Thay vì tự xây dựng email server hoặc tích hợp API gửi email bên thứ ba, nhóm sử dụng **Amazon SNS** để gửi cảnh báo. Khi model dự đoán một giao dịch là gian lận, SNS có thể gửi email đến quản trị viên gần như ngay lập tức. Với phạm vi workshop, SNS là lựa chọn phù hợp vì cấu hình đơn giản, dễ kiểm thử và tích hợp tốt với các dịch vụ AWS khác.

### Tận dụng SageMaker Real-time Endpoint

Một điểm thuận lợi khi dùng SageMaker là quá trình đưa mô hình từ giai đoạn huấn luyện sang giai đoạn phục vụ inference được đơn giản hóa. Sau khi model được đóng gói đúng cấu trúc, SageMaker có thể triển khai model thành endpoint để các thành phần khác gọi qua API. Điều này giúp nhóm tập trung nhiều hơn vào luồng dữ liệu và logic phát hiện gian lận, thay vì phải tự quản lý server phục vụ model.

### Giảm code vận hành nhờ Kinesis Data Firehose

Nếu tự viết code gom dữ liệu stream và lưu xuống S3, hệ thống sẽ cần thêm logic xử lý batch, retry và lỗi ghi dữ liệu. Với **Kinesis Data Firehose**, dữ liệu prediction có thể được tự động đưa về S3 mà không cần quản lý server riêng. Đây là điểm phù hợp với mục tiêu xây dựng một pipeline serverless, dễ vận hành và dễ mở rộng.

## 4. Chiến lược tối ưu chi phí

Chi phí cloud là một yếu tố cần được cân nhắc ngay từ giai đoạn thiết kế. Với bài toán này, nhóm định hướng tối ưu chi phí theo ba hướng chính.

### Ưu tiên kiến trúc serverless

Các thành phần như API Gateway, Lambda, SNS và Kinesis giúp giảm nhu cầu duy trì máy chủ EC2 chạy liên tục. Hệ thống chỉ phát sinh chi phí tương ứng với mức sử dụng thực tế, phù hợp với môi trường demo, workshop hoặc giai đoạn thử nghiệm ban đầu.

### Tối ưu chi phí huấn luyện với SageMaker

Quá trình huấn luyện mô hình có thể tiêu tốn nhiều tài nguyên CPU/GPU. Với SageMaker, nhóm có thể cân nhắc sử dụng **Managed Spot Training** để tận dụng các instance rảnh rỗi của AWS, từ đó giảm chi phí huấn luyện so với việc luôn dùng On-Demand Instance.

### Quản lý vòng đời dữ liệu trên S3

Dữ liệu giao dịch và lịch sử prediction có thể tăng dần theo thời gian. Vì vậy, nhóm đề xuất sử dụng **S3 Lifecycle Policies** để tự động chuyển dữ liệu cũ sang các lớp lưu trữ chi phí thấp hơn như S3 Standard-IA hoặc S3 Glacier sau một khoảng thời gian nhất định. Cách này giúp giữ lại dữ liệu phục vụ phân tích dài hạn nhưng vẫn kiểm soát được chi phí lưu trữ.

## 5. Hướng phát triển trong tương lai

Trong phạm vi workshop, hệ thống tập trung vào việc mô phỏng pipeline end-to-end và sử dụng mô hình Machine Learning truyền thống như Random Forest để phân loại giao dịch `Fraud` hoặc `Normal`.

Ở các bước phát triển tiếp theo, nhóm có thể cải tiến phần lõi AI trong SageMaker. Vì dữ liệu gian lận tài chính thường mất cân bằng nghiêm trọng, các kỹ thuật cân bằng dữ liệu như SMOTE-ENN có thể được thử nghiệm để cải thiện khả năng nhận diện lớp gian lận. Ngoài ra, các mô hình học sâu xử lý chuỗi thời gian như Bi-LSTM cũng có thể được nghiên cứu nếu hệ thống cần khai thác hành vi giao dịch theo chuỗi thời gian.

Nhìn chung, kiến trúc này cho thấy cách kết hợp các dịch vụ AWS như S3, SageMaker, API Gateway, Lambda, Kinesis, Firehose và SNS để xây dựng một pipeline phát hiện gian lận theo thời gian thực. Đây là nền tảng tốt để tiếp tục mở rộng thành một hệ thống giám sát giao dịch hoàn chỉnh hơn trong tương lai.
