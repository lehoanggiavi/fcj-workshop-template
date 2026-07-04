---
title: "Tự đánh giá"
date: 2026-04-19
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

Trong thời gian thực tập tại **AWS** với vị trí **Cloud Engineering**, tôi đã tập trung thực hiện project cá nhân: **xây dựng hệ thống phát hiện gian lận thẻ tín dụng bằng Machine Learning trên AWS**.

Project không chỉ yêu cầu kiến thức về Machine Learning mà còn cần khả năng thiết kế kiến trúc cloud, tổ chức dữ liệu, triển khai dịch vụ AWS và viết tài liệu workshop để người khác có thể theo dõi lại các bước thực hiện.

Các nội dung chính tôi đã thực hiện gồm:

- Phân tích bài toán phát hiện gian lận giao dịch thẻ tín dụng.
- Thiết kế pipeline gồm **Training Zone** và **Real-time Zone**.
- Sử dụng Amazon S3 làm Data Lake để lưu dataset, model artifact và kết quả prediction.
- Trình bày quy trình huấn luyện mô hình Random Forest bằng Amazon SageMaker.
- Xây dựng luồng realtime với API Gateway, Lambda, Kinesis, SageMaker Endpoint, SNS, Firehose và CloudWatch.
- Viết báo cáo theo dạng Hugo Workshop Website, có worklog, proposal, workshop, blog, events, self-evaluation và feedback.
- Bổ sung hình ảnh minh chứng từ AWS Console cho các bước chính như S3, SageMaker, API Gateway, Lambda, Kinesis, SNS và cleanup.

Qua quá trình thực hiện, tôi tự đánh giá bản thân theo các tiêu chí sau:

| STT | Tiêu chí | Mức đánh giá | Nhận xét |
| --- | --- | --- | --- |
| 1 | **Kiến thức chuyên môn** | Tốt | Tôi đã vận dụng được kiến thức về Python, Machine Learning và AWS vào một bài toán thực tế. Báo cáo thể hiện được vai trò của dữ liệu, model, endpoint, realtime processing, alert và logging trong một hệ thống ML trên cloud. |
| 2 | **Khả năng học hỏi** | Tốt | Tôi chủ động tìm hiểu các dịch vụ AWS cần thiết cho project như S3, SageMaker, Lambda, Kinesis, SNS, Firehose và CloudWatch. Các khái niệm như IAM Role, SageMaker Endpoint và realtime inference được đưa vào báo cáo theo đúng ngữ cảnh sử dụng. |
| 3 | **Tính chủ động** | Tốt | Tôi chủ động xây dựng hướng project riêng thay vì chỉ dựa vào template mẫu. Khi nội dung template không còn phù hợp, tôi rà soát và điều chỉnh lại để bám đúng pipeline Fraud Detection. |
| 4 | **Tinh thần trách nhiệm** | Tốt | Tôi hoàn thành các phần chính của báo cáo theo đúng cấu trúc yêu cầu, bao gồm thông tin sinh viên, worklog, proposal, workshop, blog, events, self-evaluation và feedback. Nội dung được rà soát nhiều lần để thống nhất với project thực tế. |
| 5 | **Kỷ luật trong công việc** | Khá | Tôi duy trì tiến độ làm báo cáo theo từng phần và kiểm tra lại nội dung sau mỗi lần chỉnh sửa. Điểm cần cải thiện là quản lý thời gian tốt hơn để giảm áp lực ở giai đoạn hoàn thiện cuối. |
| 6 | **Khả năng giao tiếp và trình bày** | Tốt | Tôi trình bày nội dung theo hướng dễ theo dõi, chia rõ mục tiêu, kiến trúc, dịch vụ sử dụng, bước triển khai, hình ảnh minh chứng và kết quả cần đạt. |
| 7 | **Khả năng làm việc nhóm / trao đổi** | Khá | Trong quá trình làm project và báo cáo, tôi biết ghi nhận góp ý, điều chỉnh nội dung khi phát hiện lệch hướng và ưu tiên kiểm tra từng phần trước khi đi tiếp. Tôi có thể cải thiện thêm bằng cách trao đổi sớm hơn khi gặp vấn đề kỹ thuật phức tạp. |
| 8 | **Tư duy giải quyết vấn đề** | Tốt | Tôi biết chia bài toán lớn thành các phần nhỏ: dữ liệu, training, deployment, realtime pipeline, alert, lưu lịch sử và cleanup. Khi website chưa khớp project hoặc đường dẫn ảnh bị lỗi, tôi xác định nguyên nhân và chỉnh lại theo đúng cấu trúc Hugo. |
| 9 | **Khả năng sử dụng công cụ** | Tốt | Tôi đã làm quen với Hugo Workshop Template, Markdown, cấu trúc thư mục `content/` và `static/images/`, đồng thời hiểu cách nội dung Markdown được render thành website. Tôi cũng thực hành thao tác trực tiếp trên AWS Console để tạo tài nguyên và kiểm tra kết quả triển khai. |
| 10 | **Đóng góp vào project cá nhân** | Tốt | Tôi đã xây dựng được hướng project có tính cá nhân, bám bài toán Fraud Detection và sử dụng nhiều dịch vụ AWS thay vì sao chép nguyên template mẫu. Báo cáo thể hiện rõ pipeline, mục tiêu, rủi ro, chi phí và hướng phát triển. |
| 11 | **Khả năng tự đánh giá và cải thiện** | Tốt | Tôi rà soát lại nội dung nhiều lần, cập nhật hình ảnh minh chứng, chỉnh các phần chưa khớp với project và làm rõ các bước cleanup để báo cáo nhất quán hơn. |
| 12 | **Đánh giá tổng thể** | Tốt | Nhìn chung, tôi đã đạt được mục tiêu chính là xây dựng báo cáo workshop website cho project Fraud Detection trên AWS. Nội dung thể hiện được kiến trúc, quy trình triển khai, minh chứng thao tác và bài học rút ra trong quá trình thực tập. |

## Điểm mạnh đạt được

- Hiểu rõ hơn cách một hệ thống Machine Learning trên AWS có thể được chia thành nhiều thành phần: dữ liệu, training, inference, realtime stream, alert và lưu trữ kết quả.
- Biết cách thiết kế kiến trúc ở mức tổng quan trước khi đi vào từng bước triển khai.
- Biết tổ chức báo cáo theo cấu trúc workshop để người đọc có thể theo dõi lại quá trình thực hiện.
- Có ý thức tránh sao chép template mẫu, thay vào đó điều chỉnh nội dung theo project cá nhân.
- Biết tổ chức hình ảnh minh chứng trong Hugo bằng thư mục `static/images/` và đường dẫn `/images/...`.
- Biết kiểm tra website bằng Hugo build để đảm bảo nội dung hiển thị đúng.

## Điểm cần cải thiện

- Cần tiếp tục thực hành sâu hơn với AWS Console để thao tác triển khai tự tin hơn.
- Cần kiểm thử end-to-end ở mức chi tiết hơn: gửi transaction mẫu, nhận prediction, kiểm tra SNS alert và kiểm tra kết quả ghi xuống S3.
- Cần quản lý chi phí AWS chặt chẽ hơn, nhất là với SageMaker Real-time Endpoint và các dịch vụ realtime.
- Cần tiếp tục cải thiện cách diễn đạt tiếng Anh khi map nội dung từ bản tiếng Việt sang bản tiếng Anh.

## Kế hoạch cải thiện tiếp theo

Trong giai đoạn tiếp theo, tôi sẽ tập trung vào các việc sau:

1. Rà soát bản tiếng Anh để đảm bảo bám sát bản tiếng Việt.
2. Kiểm thử lại luồng request mẫu và response prediction để tăng độ tin cậy của phần demo.
3. Rà soát IAM Role, chi phí và bước clean-up để báo cáo chặt chẽ hơn.
4. Kiểm tra website Hugo sau mỗi lần chỉnh sửa để đảm bảo nội dung hiển thị đúng.

## Kết luận tự đánh giá

Qua kỳ thực tập, tôi nhận thấy bản thân đã có tiến bộ rõ rệt trong việc kết nối kiến thức Machine Learning với môi trường cloud AWS. Project Fraud Detection giúp tôi hiểu rằng một hệ thống ML thực tế không chỉ dừng ở việc train model, mà còn cần quan tâm đến dữ liệu đầu vào, triển khai endpoint, realtime processing, cảnh báo, lưu lịch sử, logging, bảo mật IAM và chi phí vận hành.

Tôi tự đánh giá kết quả tổng thể ở mức **Tốt**. Báo cáo đã thể hiện được nền tảng nội dung, kiến trúc chính, hình ảnh minh chứng và các bài học quan trọng trong quá trình thực hiện project Fraud Detection trên AWS.
