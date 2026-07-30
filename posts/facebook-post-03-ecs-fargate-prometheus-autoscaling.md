# Facebook Post 03 — ECS Fargate Auto Scaling bằng Prometheus Metrics

**Ảnh đăng kèm:** `posts/images/blog-03-fargate-prometheus-autoscaling.png`

---

📊 **[GÓC CHIA SẺ AWS & CLOUD OBSERVABILITY]**

💡 **GIÁM SÁT VÀ AUTO SCALING AMAZON ECS FARGATE BẰNG PROMETHEUS METRICS**

Chào mọi người! 👋

Khi cấu hình auto scaling cho container, CPU và memory thường là hai metric đầu tiên được nghĩ đến. Nhưng sau khi đọc và dịch bài viết của AWS về Prometheus trên Amazon ECS Fargate, mình nhận ra rằng hai metric hạ tầng này không phải lúc nào cũng mô tả đúng áp lực mà ứng dụng đang chịu.

🧐 **Vì sao CPU và memory có thể chưa đủ?**

Một ứng dụng Java/Tomcat có thể bắt đầu chậm hoặc từ chối request do:

🔹 Số connection đang hoạt động tăng cao.

🔹 Thread pool gần cạn.

🔹 JVM heap hoặc garbage collection bất thường.

🔹 Số session và thời gian xử lý request tăng.

Trong các trường hợp này, CPU vẫn có thể nằm dưới ngưỡng cảnh báo. Nếu chỉ scale theo CPU, hệ thống sẽ phản ứng trễ hoặc thậm chí không phản ứng.

💡 **Giải pháp trong bài viết**

AWS sử dụng một ứng dụng Java/Tomcat trên Amazon ECS Fargate và expose metric qua Prometheus JMX Exporter. Sau đó CloudWatch Agent thu thập các metric này, chuyển chúng vào CloudWatch và dùng một application-level metric để điều khiển ECS Service Auto Scaling.

🔄 **Luồng dữ liệu có thể hình dung như sau:**

Ứng dụng Tomcat → Prometheus/JMX Exporter → CloudWatch Agent → CloudWatch Metric → CloudWatch Alarm → ECS Service Auto Scaling.

1️⃣ **Chuẩn bị container có hỗ trợ Prometheus**

Ứng dụng phục vụ traffic trên cổng riêng, còn JMX Exporter expose endpoint `/metrics` trên cổng Prometheus. Container image được build và lưu trong Amazon ECR.

Task definition còn sử dụng label để CloudWatch Agent tự động khám phá workload cần scrape. Nhờ đó, collector không phải lưu thủ công địa chỉ IP của từng Fargate task vốn có thể thay đổi sau mỗi lần triển khai.

2️⃣ **Thu thập metric bằng CloudWatch Agent**

CloudWatch Agent chạy như một ECS task riêng và sử dụng cấu hình Prometheus để scrape metric từ application task.

Một cấu hình thứ hai xác định metric nào cần chuyển thành CloudWatch metric thông qua Embedded Metric Format. Việc chọn lọc rất quan trọng: nếu gửi mọi time series và mọi dimension lên CloudWatch, chi phí và độ phức tạp có thể tăng nhanh.

Các metric đáng chú ý trong ví dụ gồm:

✅ JVM memory và garbage collection.

✅ Số thread hiện tại.

✅ Tomcat active session và rejected session.

✅ Request count, error count và processing time.

✅ Số connection trong Tomcat thread pool.

3️⃣ **Tạo alarm từ metric phản ánh tải ứng dụng**

Bài viết lựa chọn metric `tomcat_threadpool_connectioncount` để theo dõi số connection đang hoạt động. CloudWatch Alarm được kích hoạt khi giá trị vượt qua ngưỡng trong khoảng thời gian quy định.

Điểm quan trọng không phải tên metric cụ thể, mà là cách chọn metric: nó phải có quan hệ rõ ràng với saturation và chất lượng phục vụ của ứng dụng.

4️⃣ **Kết nối alarm với ECS Service Auto Scaling**

Khi alarm scale-out được kích hoạt, Application Auto Scaling tăng desired count của ECS service. Khi tải giảm ổn định, alarm scale-in đưa số lượng task về mức phù hợp.

Để tránh hệ thống liên tục tăng rồi giảm task, cần xác định:

🔹 Minimum và maximum task count.

🔹 Ngưỡng scale-out và scale-in khác nhau.

🔹 Số evaluation period.

🔹 Cooldown đủ dài để task mới khởi động và nhận traffic.

🔹 Health check để chỉ đưa task khỏe mạnh vào load balancer.

⚠️ **Những điều mình sẽ kiểm tra trước khi áp dụng**

Không phải cứ có metric Prometheus là có thể dùng ngay để scaling. Mình sẽ đặt các câu hỏi:

✅ Metric tăng có thực sự đồng nghĩa workload cần thêm capacity không?

✅ Metric được tính theo từng task hay toàn service?

✅ Khi thêm task, giá trị metric có giảm như kỳ vọng không?

✅ Khi collector hoặc metric bị thiếu, hệ thống nên giữ nguyên hay scale theo fallback?

✅ Scale-in có làm gián đoạn connection hoặc request đang xử lý không?

✅ Chi phí custom metric, log ingestion, Fargate task và load balancer có phù hợp không?

🎯 **Bài học mình rút ra**

🔹 Metric hạ tầng cho biết container dùng bao nhiêu tài nguyên; metric ứng dụng cho biết hệ thống đang phục vụ tốt đến đâu.

🔹 Service discovery giúp collector theo kịp các Fargate task có vòng đời động.

🔹 Chỉ nên thu thập metric và dimension phục vụ quyết định vận hành cụ thể.

🔹 Auto scaling cần được kiểm thử bằng load test, không chỉ kiểm tra alarm trên console.

🔹 Cooldown, health check và giới hạn task quan trọng không kém threshold.

🔹 Observability có giá trị nhất khi metric dẫn đến một hành động vận hành rõ ràng.

Nếu hệ thống của mọi người có thể chọn một application metric để auto scaling, đó sẽ là request rate, queue depth, latency hay active connection? 🙌

📚 **Bài viết gốc từ AWS:**
https://aws.amazon.com/blogs/mt/monitor-and-scale-your-amazon-ecs-on-aws-fargate-application-using-prometheus-metrics/

#AWS #AmazonECS #AWSFargate #Prometheus #AmazonCloudWatch #AutoScaling #Observability #Containers #DevOps #FCAJ
