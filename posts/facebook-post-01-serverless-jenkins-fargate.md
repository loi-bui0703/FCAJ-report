# Facebook Post 01 — Serverless Jenkins trên AWS Fargate

**Ảnh đăng kèm:** `posts/images/blog-01-serverless-jenkins-fargate.jpg`

---

🚀 **[GÓC CHIA SẺ KIẾN THỨC AWS & DEVOPS]**

💡 **XÂY DỰNG MÔI TRƯỜNG JENKINS SERVERLESS TRÊN AWS FARGATE**

Chào mọi người! 👋

Gần đây mình đã đọc và dịch bài viết kỹ thuật của AWS về chủ đề **“Building a serverless Jenkins environment on AWS Fargate”**. Điều mình thấy thú vị nhất là cách kiến trúc này giữ lại hệ sinh thái quen thuộc của Jenkins nhưng loại bỏ phần lớn công việc quản trị máy chủ và worker node.

🧐 **Jenkins truyền thống thường gặp những vấn đề gì?**

Khi triển khai Jenkins Controller và Agent trên Amazon EC2 hoặc một cụm container tự quản lý, đội ngũ vận hành thường phải:

🔹 Cập nhật hệ điều hành, vá lỗi và theo dõi sức khỏe máy chủ.

🔹 Duy trì worker node kể cả khi không có build job nào chạy.

🔹 Bảo vệ dữ liệu cấu hình, plugin và lịch sử job của Jenkins Controller.

🔹 Mở rộng tài nguyên khi số lượng job tăng, sau đó thu hẹp khi tải giảm.

🔹 Phân tách quyền AWS giữa các loại pipeline khác nhau.

💡 **Kiến trúc serverless trong bài viết giải quyết vấn đề như thế nào?**

1️⃣ **Chạy Jenkins Controller trên Amazon ECS Fargate**

Jenkins Controller được đóng gói thành container và chạy dưới dạng một ECS service sử dụng Fargate. Nhờ đó, đội ngũ không phải trực tiếp quản lý EC2 instance bên dưới.

Controller được đặt trong private subnet. Application Load Balancer cung cấp điểm truy cập cho giao diện Jenkins, còn AWS Certificate Manager có thể được sử dụng để bảo vệ kết nối bằng HTTPS.

2️⃣ **Lưu dữ liệu bền vững bằng Amazon EFS**

Container có thể được thay thế hoặc khởi động lại, nhưng cấu hình Jenkins không được phép mất theo container. Amazon EFS được gắn vào task của Controller để lưu plugin, cấu hình và dữ liệu cần duy trì.

Điểm mình rút ra là: **serverless compute không đồng nghĩa với stateless application**. Phần compute và phần dữ liệu cần được thiết kế riêng.

3️⃣ **Tạo Jenkins Agent theo từng build job**

Thông qua Amazon ECS plugin, Jenkins có thể yêu cầu ECS tạo một Agent container riêng khi có job mới. Agent tự đăng ký với Controller, thực thi build và dừng sau khi hoàn tất.

Mô hình Agent ngắn hạn này mang lại ba lợi ích:

✅ Không phải duy trì worker chạy nhàn rỗi.

✅ Mỗi job có môi trường sạch và tài nguyên CPU/memory riêng.

✅ Giảm nguy cơ dữ liệu hoặc dependency của job trước ảnh hưởng đến job sau.

AWS Cloud Map được sử dụng để Agent tìm thấy Controller thông qua service discovery.

4️⃣ **Phân loại workload bằng Fargate và Fargate Spot**

Các job quan trọng hoặc không thể chấp nhận gián đoạn, chẳng hạn bước triển khai production, có thể chạy trên capacity provider `FARGATE`.

Các job build hoặc test có khả năng chạy lại có thể sử dụng `FARGATE_SPOT` để tận dụng dung lượng dự phòng với mức giá thấp hơn. Tuy nhiên, Spot có thể bị thu hồi với cảnh báo ngắn, vì vậy pipeline phải được thiết kế để retry an toàn.

5️⃣ **Tự động hóa và bảo mật bằng Infrastructure as Code**

Toàn bộ môi trường được mô tả bằng Terraform. Mật khẩu quản trị Jenkins được lưu dưới dạng `SecureString` trong AWS Systems Manager Parameter Store thay vì hard-code.

Các Agent template có thể sử dụng IAM role với phạm vi quyền khác nhau. AWS Backup bảo vệ dữ liệu trên EFS, còn Amazon SNS có thể gửi thông báo khi môi trường hoặc build job gặp lỗi.

⚠️ **Một giới hạn quan trọng**

Amazon EFS là network-attached storage, vì vậy hiệu năng mặc định có thể chưa phù hợp với mọi Jenkins workload. Trước khi dùng trong production, cần kiểm thử throughput, latency và cân nhắc performance mode phù hợp thay vì mặc định rằng kiến trúc serverless luôn nhanh hơn.

🎯 **Bài học mình rút ra**

🔹 Tách compute khỏi persistent data giúp Controller có thể được thay thế an toàn.

🔹 Ephemeral Agent giảm tài nguyên nhàn rỗi và tạo môi trường build sạch hơn.

🔹 Fargate Spot chỉ phù hợp với job có khả năng chịu gián đoạn và chạy lại.

🔹 IAM role nên được phân tách theo loại Agent và mức độ nhạy cảm của job.

🔹 Terraform giúp kiến trúc có thể kiểm tra, nhân bản và triển khai nhất quán.

Theo mọi người, với một Jenkins workload mới trên AWS, lựa chọn hợp lý hơn sẽ là ECS Fargate, Amazon EKS hay một dịch vụ CI/CD được quản lý hoàn toàn? 🙌

📚 **Bài viết gốc từ AWS:**
https://aws.amazon.com/blogs/devops/building-a-serverless-jenkins-environment-on-aws-fargate/

#AWS #Jenkins #AWSFargate #AmazonECS #AmazonEFS #Terraform #DevOps #Serverless #FCAJ
