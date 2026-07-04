---
title: "Blog 3 - Chạy Apache Spark Serverless với Amazon Athena"
date: 2026-04-19
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# [AWS Knowledge Sharing] Chạy Apache Spark Serverless với Amazon Athena – Không cần quản lý Cluster

Chào mọi người trong cộng đồng AWS Study Group VN.

Mình vừa đọc một bài viết khá hay từ AWS Big Data Blog về **Apache Spark engine trong Amazon Athena**. Điểm nổi bật là giờ đây chúng ta có thể chạy Spark hoàn toàn serverless, không cần dựng hay quản lý EMR hoặc các Spark Cluster như trước.

## Bài toán

Khi sử dụng Spark theo cách truyền thống, các đội Data thường phải:

- Quản lý EC2, networking và cấu hình Spark Cluster.
- Chờ cluster khởi động trước khi chạy job.
- Trả chi phí ngay cả khi cluster không hoạt động.
- Khó đáp ứng đồng thời nhiều nhu cầu như Notebook, ETL Pipeline và phân tích dữ liệu.

Điều này làm tăng chi phí vận hành và khiến thời gian phân tích dữ liệu chậm hơn.

## Giải pháp

AWS giới thiệu **Apache Spark Engine trong Amazon Athena**, cung cấp môi trường Spark hoàn toàn serverless.

Thay vì quản lý cluster, người dùng chỉ cần:

- Tạo một Spark Session.
- Kết nối thông qua Spark Connect.
- Chạy code Spark bằng công cụ quen thuộc như Jupyter Notebook, VS Code hoặc Apache Airflow + dbt.

Athena sẽ tự động khởi tạo tài nguyên, mở rộng khi cần và tự giải phóng sau khi hoàn thành.

## Kiến trúc

Kiến trúc sử dụng khá đơn giản:

- **Amazon Athena for Apache Spark** đóng vai trò là Spark Engine.
- **AWS Glue Data Catalog** quản lý metadata.
- Dữ liệu được lưu trên **Amazon S3**.
- Người dùng có thể kết nối từ Jupyter Notebook, VS Code hoặc Apache Airflow thông qua Spark Connect.
- Nếu cần triển khai trong môi trường riêng tư, có thể sử dụng **Amazon MWAA (Managed Airflow)** kết hợp với VPC Endpoint để kết nối an toàn.

## Điểm mới đáng chú ý

Phiên bản mới của Athena for Spark bổ sung nhiều tính năng hữu ích:

- **Spark Connect** giúp kết nối từ các công cụ bên ngoài một cách bảo mật.
- Khởi tạo Spark Session nhanh hơn, giảm đáng kể thời gian chờ.
- **Live Spark UI** hỗ trợ theo dõi và debug job.
- **Session-level Cost Attribution** giúp theo dõi chi phí theo từng phiên làm việc.
- Tích hợp **AWS Lake Formation** để quản lý quyền truy cập dữ liệu.

## Các mô hình sử dụng

AWS giới thiệu ba cách triển khai phổ biến:

- **Jupyter Notebook:** phù hợp cho Data Scientist thực hiện khám phá dữ liệu và Feature Engineering.
- **VS Code:** hỗ trợ lập trình và kiểm thử ứng dụng Spark ngay trên IDE quen thuộc.
- **Apache Airflow + dbt:** xây dựng các pipeline ETL tự động và quản lý workflow theo lịch.

## Điều mình thấy thú vị

Điểm mình ấn tượng nhất là giờ đây Spark không còn gắn liền với việc quản lý cluster.

Chúng ta chỉ cần tập trung viết code Spark, còn Athena sẽ tự động:

- Khởi tạo Spark Session trong vài giây.
- Auto Scaling theo khối lượng công việc.
- Tính phí theo thời gian sử dụng thay vì phải duy trì cluster 24/7.

Đây là một lựa chọn rất đáng cân nhắc cho các workload phân tích dữ liệu, ETL hoặc Machine Learning có lưu lượng không ổn định.

Theo mình, **Athena for Apache Spark** là một bước tiến giúp các đội Data giảm đáng kể chi phí vận hành và thời gian quản lý hạ tầng, đồng thời vẫn tận dụng được toàn bộ hệ sinh thái AWS như S3, Glue Data Catalog, Lake Formation và Airflow. Nếu mọi người đang xây dựng Data Lake hoặc Data Platform trên AWS, đây là một dịch vụ rất đáng để trải nghiệm.
