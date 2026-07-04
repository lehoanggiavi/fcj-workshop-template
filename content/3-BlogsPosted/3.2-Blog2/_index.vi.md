---
title: "Blog 2 - Amazon tự động hóa bài toán lập kế hoạch nhân sự với Serverless như thế nào?"
date: 2026-04-19
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon tự động hóa bài toán lập kế hoạch nhân sự với Serverless như thế nào?

Chào mọi người trong cộng đồng AWS Study Group VN.

Mình vừa đọc một bài viết khá thú vị từ AWS Architecture Blog về hệ thống **ALAP (Automated Labor Assumptions Platform)** mà Amazon xây dựng để tự động hóa việc lập kế hoạch nhân sự cho hơn 100 trung tâm phân loại hàng hóa tại Bắc Mỹ.

## Bài toán

Trước đây, mỗi tuần các **Labor Planning Analyst (LPA)** phải tổng hợp dữ liệu từ nhiều nguồn, chỉnh sửa hàng loạt file Excel, họp với các bộ phận và tạo dữ liệu đầu vào cho hệ thống lập kế hoạch nhân sự.

Quy trình này mất khoảng **10+ giờ mỗi tuần cho mỗi planner**, dễ xảy ra sai sót, khó mở rộng và gần như không có audit trail.

## Kiến trúc giải pháp

Amazon xây dựng một nền tảng Serverless hoàn toàn trên AWS với các thành phần:

- **Amazon S3** lưu trữ dữ liệu và tài liệu hướng dẫn.
- **AWS Glue** xử lý ETL và tổng hợp dữ liệu từ nhiều hệ thống.
- **Amazon Aurora PostgreSQL** đóng vai trò Data Mart phục vụ các truy vấn phân tích.
- **Amazon EventBridge** lên lịch chạy workflow hàng tuần.
- **Amazon SQS** phân phối hơn 3.000 tác vụ song song cho từng site và từng metric.
- **AWS Lambda** xử lý tính toán, API backend và orchestration.
- **Amazon DynamoDB** lưu metadata, trạng thái job và lịch sử override.
- **Amazon Cognito + CloudFront + S3** xây dựng giao diện web cho người dùng.

## Quy trình hoạt động

Mỗi tuần, **EventBridge** tự động kích hoạt pipeline.

**Lambda** tạo hàng nghìn tác vụ song song để đọc dữ liệu lịch sử, áp dụng các quy tắc nghiệp vụ và kết quả từ mô hình Machine Learning, sau đó sinh ra bộ dữ liệu lập kế hoạch cho **13 tuần tiếp theo**.

Người quản lý có thể truy cập giao diện web để xem dữ liệu, chỉnh sửa (**override**), gửi phê duyệt và cuối cùng xuất dữ liệu sang hệ thống tối ưu hóa nhân sự.

## Kết quả đạt được

Sau khi triển khai ALAP, Amazon ghi nhận:

- Giảm khoảng **70% thời gian lập kế hoạch**, từ hơn 10 giờ xuống còn khoảng 3–4 giờ mỗi tuần cho mỗi planner.
- Chuẩn hóa quy trình cho hơn 100 trung tâm phân loại.
- Loại bỏ gần như hoàn toàn lỗi nhập liệu thủ công.
- Có đầy đủ lịch sử thay đổi và phê duyệt (**Audit Trail**).
- Hoàn thành hơn **3.000 tác vụ xử lý** chỉ trong khoảng 3 giờ.

## Điều mình học được

Điểm mình thấy ấn tượng nhất là cách Amazon kết hợp nhiều dịch vụ Serverless để xây dựng một hệ thống vừa dễ mở rộng vừa tối ưu chi phí:

- **Lambda** xử lý tính toán theo nhu cầu.
- **SQS** giúp fan-out hàng nghìn tác vụ song song.
- **Aurora PostgreSQL** phục vụ các truy vấn phân tích phức tạp.
- **DynamoDB** lưu metadata và trạng thái workflow.
- **EventBridge** tự động hóa toàn bộ quy trình theo lịch.

Đây là một ví dụ rất điển hình về cách áp dụng kiến trúc **Event-Driven** và **Serverless** để thay thế các quy trình thủ công, giúp tăng hiệu quả vận hành mà vẫn giảm chi phí quản lý hạ tầng.

Nếu mọi người đang xây dựng các hệ thống xử lý dữ liệu theo lô (**batch processing**), workflow tự động hoặc nền tảng nội bộ cho doanh nghiệp, kiến trúc của ALAP là một case study rất đáng để tham khảo.
