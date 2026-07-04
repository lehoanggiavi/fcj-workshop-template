---
title: "Worklog Tuần 11"
date: 2026-06-28
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

**Thời gian:** 28/06/2026 - 04/07/2026

## Mục tiêu tuần 11

- Bổ sung giám sát, log và cảnh báo vận hành cho hệ thống.
- Rà soát bảo mật cơ bản theo nguyên tắc least privilege.
- Xem xét các điểm có thể tối ưu chi phí trong quá trình demo và vận hành.

## Công việc đã thực hiện

- Kiểm tra CloudWatch Logs của các Lambda function.
- Theo dõi log khi request đi qua các thành phần:
  - API Gateway
  - Lambda ingest
  - Kinesis
  - Lambda feature processing
  - SageMaker Endpoint
  - SNS
  - Firehose
- Xác định một số metric cần quan sát:
  - Số lượng request API.
  - Lỗi Lambda.
  - Thời gian xử lý Lambda.
  - Lỗi khi gọi SageMaker Endpoint.
  - Số lượng record đi qua Kinesis/Firehose.
- Rà soát IAM Role cho từng thành phần:
  - Lambda chỉ có quyền ghi vào Kinesis nếu cần.
  - Lambda realtime chỉ có quyền gọi SageMaker Endpoint, publish SNS và ghi Firehose theo phạm vi cần thiết.
  - Không hard-code access key hoặc secret key trong source code.
- Ghi nhận các hướng tối ưu chi phí:
  - Chỉ bật SageMaker Endpoint khi cần demo.
  - Dọn dẹp endpoint sau khi thực hành.
  - Sử dụng dữ liệu demo vừa đủ.
  - Theo dõi tài nguyên phát sinh chi phí.

## Kết quả đạt được

- Có kế hoạch giám sát hệ thống bằng CloudWatch Logs và metric.
- Nắm được các điểm cần kiểm tra khi hệ thống realtime gặp lỗi.
- Rà soát được các quyền IAM cơ bản để tránh cấp quyền quá rộng.
- Xác định được các hành động tối ưu chi phí và giảm rủi ro phát sinh chi phí AWS.
