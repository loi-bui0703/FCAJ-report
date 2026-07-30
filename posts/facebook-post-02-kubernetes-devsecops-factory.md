# Facebook Post 02 — Kubernetes-based DevSecOps Software Factory

**Ảnh đăng kèm:** `posts/images/blog-02-kubernetes-devsecops-factory.png`

---

🛡️ **[GÓC CHIA SẺ AWS & DEVSECOPS]**

💡 **XÂY DỰNG NHÀ MÁY PHẦN MỀM DEVSECOPS END-TO-END TRÊN AMAZON EKS**

Chào mọi người! 👋

Mình vừa đọc và dịch bài viết của AWS về cách xây dựng một **Kubernetes-based DevSecOps Software Factory**. Thay vì xem security là một bước quét duy nhất ở cuối pipeline, kiến trúc này đưa nhiều kiểm soát bảo mật vào xuyên suốt vòng đời phần mềm.

🧐 **DevSecOps Software Factory cần bảo vệ điều gì?**

Bài viết phân tách security thành hai góc nhìn rất rõ:

1️⃣ **Security of the software factory:** bảo vệ chính pipeline, repository, IAM role, artifact, log và hạ tầng vận hành.

2️⃣ **Security in the software factory:** kiểm tra secret, dependency, source code, container image, ứng dụng đang chạy và hành vi runtime.

Nếu pipeline có nhiều security scanner nhưng IAM role quá rộng hoặc artifact có thể bị thay thế ngoài quy trình, toàn bộ kết quả quét vẫn chưa đủ đáng tin cậy.

🏗️ **Luồng hoạt động chính của kiến trúc**

🔹 Developer commit code vào AWS CodeCommit.

🔹 Amazon CloudWatch Events kích hoạt AWS CodePipeline để điều phối quy trình.

🔹 AWS CodeBuild đóng gói source code và lưu artifact vào Amazon S3.

🔹 Pipeline kiểm tra secret, xây container image, thực hiện các security scan và đẩy image đạt yêu cầu lên Amazon ECR.

🔹 Ứng dụng được triển khai lên Amazon EKS.

🔹 Kết quả từ nhiều công cụ được Lambda chuẩn hóa và tập hợp trong AWS Security Hub.

Điểm mình đánh giá cao là kiến trúc không khóa người dùng vào một scanner duy nhất. CodeBuild hỗ trợ cách tiếp cận “bring your own tool”, vì vậy từng tổ chức có thể thay đổi công cụ nhưng vẫn giữ nguyên các loại kiểm soát cần thiết.

🔐 **Sáu lớp kiểm tra nổi bật trong pipeline**

1️⃣ **Secret Analysis — git-secrets**

Pipeline tìm AWS access key, secret key hoặc chuỗi nhạy cảm trước khi chúng đi sâu hơn vào quá trình build. Khi phát hiện secret, build bị dừng ngay.

2️⃣ **Software Composition Analysis — Snyk hoặc Anchore**

SCA kiểm tra package và thư viện bên thứ ba trong application/container image. Đây là lớp quan trọng vì phần lớn ứng dụng hiện đại phụ thuộc vào nhiều component mã nguồn mở.

3️⃣ **Static Application Security Testing**

Source code hoặc image được phân tích để tìm pattern có khả năng dẫn đến lỗ hổng trước khi ứng dụng được triển khai.

4️⃣ **Amazon ECR Image Scanning**

Container image trong registry tiếp tục được quét để phát hiện package vulnerability. Pipeline chỉ nên promote đúng image digest đã vượt qua policy.

5️⃣ **Dynamic Application Security Testing — OWASP ZAP**

Sau khi ứng dụng đã chạy, OWASP ZAP kiểm tra bề mặt web từ góc nhìn bên ngoài. DAST có thể phát hiện những vấn đề chỉ xuất hiện khi routing, authentication và application behavior kết hợp với nhau.

6️⃣ **Runtime Protection — Sysdig Falco**

Falco theo dõi sự kiện runtime trên EKS và gửi cảnh báo đến CloudWatch. Đây là lớp giúp phát hiện hành vi bất thường mà các bước quét trước deployment không thể quan sát.

📊 **Tại sao cần AWS Security Hub?**

Mỗi công cụ có định dạng finding và giao diện riêng. Nếu engineer phải mở từng dashboard để điều tra, security data rất dễ bị phân mảnh.

Trong kiến trúc này, AWS Lambda xử lý kết quả scan và đưa finding về AWS Security Hub như một “single pane of glass”. Điều này hỗ trợ:

✅ Theo dõi finding tập trung.

✅ Liên kết finding với pipeline stage và artifact.

✅ Tạo quy trình triage nhất quán.

✅ Giữ bằng chứng phục vụ audit và compliance.

Tuy nhiên, tập trung finding không tự động loại bỏ false positive. Team vẫn cần severity threshold, owner, thời hạn xử lý và cơ chế risk acceptance rõ ràng.

🎯 **Bài học mình rút ra**

🔹 Shift-Left không có nghĩa chỉ quét sớm; security cần xuất hiện trước, trong và sau deployment.

🔹 Pipeline cũng là một hệ thống production và phải được bảo vệ như application.

🔹 Mỗi security gate nên có tiêu chí pass/fail, owner và evidence cụ thể.

🔹 Container image cần được định danh bằng digest để bảo đảm artifact được quét cũng chính là artifact được deploy.

🔹 Security Hub giúp hợp nhất finding, nhưng quyết định ưu tiên vẫn cần context của workload.

🔹 Bài viết tập trung vào application vulnerability scanning; security của EKS cluster và network vẫn cần được đánh giá bằng các lớp kiểm soát riêng.

Nếu được thiết kế pipeline DevSecOps cho một dự án mới, mọi người sẽ đặt security gate bắt buộc nào trước bước deploy production? 🤔

📚 **Bài viết gốc từ AWS:**
https://aws.amazon.com/blogs/devops/building-an-end-to-end-kubernetes-based-devsecops-software-factory-on-aws/

#AWS #AmazonEKS #DevSecOps #Kubernetes #AWSCodePipeline #AWSCodeBuild #AWSSecurityHub #ContainerSecurity #ShiftLeft #FCAJ
