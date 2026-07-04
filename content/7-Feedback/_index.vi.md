---
title: "Chia sẻ, đóng góp ý kiến"
date: 2026-04-19
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

Trong quá trình tham gia thực tập và thực hiện báo cáo theo hình thức **Workshop Website**, tôi có cơ hội tiếp cận gần hơn với cách một project cloud được trình bày, triển khai và đánh giá. Thay vì chỉ viết báo cáo dạng văn bản thông thường, việc xây dựng website giúp tôi phải suy nghĩ rõ hơn về cấu trúc nội dung, luồng triển khai và cách người khác có thể đọc lại hoặc làm theo project.

Project tôi thực hiện là **phát hiện gian lận thẻ tín dụng bằng Machine Learning trên AWS**. Đây là một chủ đề giúp tôi kết nối nhiều mảng kiến thức: dữ liệu, Machine Learning, kiến trúc cloud, realtime processing, alert, logging và tối ưu chi phí.

## 1. Đánh giá chung về chương trình

Tôi đánh giá chương trình thực tập là một trải nghiệm hữu ích vì không chỉ yêu cầu tìm hiểu lý thuyết về AWS mà còn hướng đến việc xây dựng một project cá nhân có cấu trúc rõ ràng.

Thông qua project, tôi hiểu hơn rằng một giải pháp cloud thực tế không chỉ gồm một dịch vụ riêng lẻ. Với bài toán Fraud Detection, hệ thống cần nhiều thành phần phối hợp với nhau:

- Amazon S3 để lưu dataset, model artifact và prediction history.
- Amazon SageMaker để huấn luyện và triển khai model.
- API Gateway và Lambda để nhận và xử lý request realtime.
- Kinesis để tiếp nhận luồng giao dịch.
- SNS để gửi cảnh báo khi phát hiện Fraud.
- Firehose để lưu lịch sử dự đoán xuống S3.
- CloudWatch để hỗ trợ logging và debug.

Điểm tôi thấy giá trị nhất là chương trình giúp tôi nhìn project theo hướng end-to-end, từ ý tưởng đến kiến trúc, từ dữ liệu đến triển khai và từ triển khai đến báo cáo.

## 2. Môi trường học tập và làm việc

Môi trường thực tập giúp tôi có cơ hội rèn luyện tính chủ động. Khi làm project Fraud Detection, có nhiều khái niệm ban đầu tôi chưa nắm chắc như IAM Role, SageMaker Endpoint, realtime inference hoặc cách Hugo render Markdown thành website.

Việc phải tự tìm hiểu, ghi nhận phần chưa rõ và bổ sung dần vào báo cáo giúp tôi học theo hướng thực tế hơn. Tôi không chỉ đọc khái niệm mà còn phải đặt câu hỏi:

- Dịch vụ này nằm ở đâu trong pipeline?
- Input và output của mỗi bước là gì?
- Nếu người khác làm theo workshop, họ cần chuẩn bị gì?
- Hình ảnh nào cần chụp để chứng minh bước triển khai?
- Tài nguyên nào có thể phát sinh chi phí và cần clean-up?

Những câu hỏi này giúp tôi hiểu rõ hơn bản chất của project thay vì chỉ liệt kê dịch vụ AWS.

## 3. Sự phù hợp với chuyên ngành và định hướng cá nhân

Project phù hợp với định hướng học tập của tôi vì kết hợp giữa **Machine Learning** và **Cloud Engineering**. Trước đây, khi học Machine Learning, tôi thường tập trung vào phần model, dữ liệu train/test và kết quả đánh giá. Qua project này, tôi nhận ra rằng trong thực tế, model chỉ là một phần của hệ thống.

Để model có thể được sử dụng trong một hệ thống thực tế, cần thêm nhiều thành phần khác:

- Nơi lưu trữ dữ liệu đầu vào.
- Cách đóng gói model.
- Endpoint để phục vụ inference.
- API để nhận request từ bên ngoài.
- Cơ chế xử lý realtime.
- Cảnh báo khi phát hiện bất thường.
- Lưu lịch sử kết quả để phân tích sau.
- Theo dõi log và kiểm soát chi phí.

Điều này giúp tôi có cái nhìn đầy đủ hơn về vòng đời của một hệ thống ML trên cloud.

## 4. Điều hài lòng nhất

Điều tôi hài lòng nhất là đã xây dựng được một hướng project riêng thay vì chỉ chỉnh sửa nội dung từ template mẫu. Ban đầu, template có nhiều phần chưa khớp với project cá nhân, đặc biệt là các nội dung cũ về VPC Endpoint và PrivateLink. Khi rà soát lại, tôi đã điều chỉnh dần để nội dung website bám đúng hơn vào pipeline Fraud Detection.

Tôi cũng hài lòng vì báo cáo được tổ chức theo từng phần rõ ràng:

- Student Information.
- Worklog 12 tuần.
- Proposal.
- Blog Posts đã có Blog 1, Blog 2 và Blog 3 với nội dung hoàn chỉnh ở bản tiếng Việt.
- Events Participated đã cập nhật hai sự kiện FCAJ Community Day cùng nội dung chính, bài học rút ra và hình ảnh minh chứng.
- Workshop kỹ thuật.
- Self-evaluation.
- Feedback.

Cách làm từng phần giúp tôi dễ kiểm tra tiến độ và tránh viết lệch hướng.

## 5. Khó khăn gặp phải

Một số khó khăn chính trong quá trình thực hiện gồm:

### 5.1. Hiểu và map đúng pipeline kỹ thuật

Pipeline Fraud Detection gồm nhiều dịch vụ AWS liên kết với nhau. Nếu chỉ nhìn từng dịch vụ riêng lẻ, rất dễ viết báo cáo theo kiểu liệt kê mà không thể hiện được luồng dữ liệu. Vì vậy, tôi cần tách hệ thống thành hai phần:

- **Training Zone:** dữ liệu, preprocessing, training, model artifact và SageMaker Endpoint.
- **Real-time Zone:** API Gateway, Lambda, Kinesis, Lambda Read Features, SageMaker Endpoint, SNS, Firehose và S3.

Cách chia này giúp báo cáo rõ hơn và dễ theo dõi hơn.

### 5.2. Chuyển nội dung Markdown thành website

Ban đầu tôi chưa hiểu rõ việc các file Markdown trong thư mục `content/` sẽ được Hugo render thành website. Sau khi kiểm tra bằng Hugo server, tôi hiểu hơn cách cấu trúc thư mục, file `_index.vi.md`, hình ảnh trong `static/images/` và đường dẫn `/images/...` hoạt động.

Một lỗi thực tế gặp phải là dùng đường dẫn ảnh kiểu Windows như:

```text
E:\aws\fcj-workshop-template\static\images\avatar.jpg
```

Cách đúng trong Markdown phải là:

```text
/images/avatar.jpg
```

Lỗi này giúp tôi hiểu rõ hơn cách Hugo xử lý static files.

### 5.3. Tổ chức hình ảnh minh chứng thực tế

Một khó khăn ban đầu là xác định ảnh nào thật sự cần thiết cho từng bước trong workshop. Nếu dán quá nhiều ảnh, nội dung sẽ dài và khó theo dõi; nếu thiếu ảnh ở các bước quan trọng, người đọc khó hình dung kết quả triển khai.

Vì vậy, tôi chọn bổ sung ảnh cho các bước có giá trị minh chứng rõ ràng, chẳng hạn như S3 bucket, cấu trúc Data Lake, SageMaker Endpoint, API Gateway endpoint, Lambda, Kinesis Data Stream, SNS email alert và bước cleanup SageMaker. Với các bước chỉ kiểm tra code hoặc mô tả cấu hình ngắn, tôi giữ nội dung dạng text để tránh làm báo cáo rườm rà.

## 6. Góp ý và đề xuất cải thiện

Từ trải nghiệm cá nhân, tôi có một số đề xuất sau:

- Nên có checklist rõ hơn cho từng giai đoạn của báo cáo: Proposal, Worklog, Workshop, Self-evaluation và Feedback.
- Nên có ví dụ minh họa về cách tổ chức ảnh trong Hugo, đặc biệt là khác biệt giữa thư mục `static/images/` và đường dẫn `/images/...` trong Markdown.
- Nên có một buổi hướng dẫn ngắn về cách chạy Hugo local để sinh viên kiểm tra trực quan website trước khi nộp.
- Nên khuyến khích sinh viên ghi rõ phạm vi đã thực hiện, phạm vi giữ ở mức mô tả và phạm vi cần kiểm chứng thêm, để báo cáo minh bạch và dễ đánh giá hơn.
- Với các project dùng AWS service có chi phí như SageMaker Endpoint hoặc Kinesis, nên nhấn mạnh clean-up ngay từ đầu.

## 7. Có giới thiệu chương trình cho bạn bè không?

Tôi sẽ giới thiệu chương trình cho các bạn quan tâm đến AWS, cloud engineering hoặc muốn có một project cá nhân để đưa vào báo cáo/thực hành.

Lý do là chương trình giúp người học không chỉ đọc tài liệu mà còn phải tự xây dựng một sản phẩm có cấu trúc. Khi làm báo cáo theo dạng workshop website, người học phải suy nghĩ kỹ hơn về mục tiêu, kiến trúc, bước triển khai, hình ảnh minh chứng, kiểm thử và clean-up.

Tuy nhiên, tôi cũng nghĩ người tham gia cần chuẩn bị tinh thần tự học khá nhiều, vì khi đi vào project cá nhân sẽ có nhiều phần không thể làm theo template 100%. Đây cũng là điểm khó nhưng là phần giúp học được nhiều nhất.

## 8. Mong muốn sau chương trình

Sau chương trình, tôi mong muốn tiếp tục phát triển project Fraud Detection theo hướng thực tế hơn:

1. Mở rộng kiểm thử end-to-end với nhiều kịch bản giao dịch Fraud/Normal.
2. Bổ sung dashboard hoặc metric tổng hợp để theo dõi kết quả prediction.
3. Tối ưu thêm IAM Role và chính sách quyền theo nguyên tắc least privilege.
4. Cải thiện cơ chế quan sát hệ thống bằng CloudWatch Logs/metric.
5. Phát triển bản tiếng Anh dựa trên bản tiếng Việt đã được rà soát.

## 9. Kết luận

Nhìn chung, quá trình thực tập và làm báo cáo giúp tôi hiểu rõ hơn cách biến một ý tưởng Machine Learning thành một hệ thống cloud có cấu trúc. Project Fraud Detection trên AWS giúp tôi rèn luyện cả tư duy kỹ thuật lẫn cách trình bày một workshop để người khác có thể đọc, hiểu và triển khai lại.

Điểm quan trọng nhất tôi rút ra là: một project cloud tốt không chỉ nằm ở việc dùng nhiều dịch vụ AWS, mà nằm ở việc các dịch vụ đó được kết nối hợp lý để giải quyết đúng bài toán. Với project này, bài toán là phát hiện giao dịch nghi ngờ gian lận, gửi cảnh báo kịp thời và lưu lại lịch sử dự đoán để phục vụ phân tích sau.
