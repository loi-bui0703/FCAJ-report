---
title: "Event 3"
date: 2026-07-22
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Báo cáo tổng kết: “AWS Tech Meetup và Chia sẻ kiến thức cộng đồng”

### Mục tiêu sự kiện

* Giải thích mối quan hệ giữa service-level commitment, monitoring và customer experience.
* Chia sẻ cách chuẩn bị có cấu trúc cho AWS Certified Cloud Practitioner CLF-C02.
* Giới thiệu AI-assisted application-security review và vai trò trong DevSecOps.
* Tạo cơ hội để người học trao đổi kinh nghiệm operations và security.

### Diễn giả

* **Nguyen Huynh Son:** Infrastructure Support Engineer tại Endava, nguyên Infrastructure Reliability Engineer tại SPS, thành viên AWS Student Builder Group HUFLIT.
* **Ngo Le Tan Huy:** Diễn giả chia sẻ lộ trình chứng chỉ AWS Cloud Practitioner.
* **Nguyen Tuan Thinh:** DevOps/DevSecOps/Cloud Engineer tại Styl Solutions, thành viên First Cloud AI Journey.

### Nội dung nổi bật

#### Monitoring trải nghiệm thật của người dùng

Session monitoring phản biện giả định rằng infrastructure khỏe mạnh đồng nghĩa application khỏe mạnh. CPU, memory, load-balancer target và health endpoint có thể bình thường trong khi người dùng không thể login hoặc hoàn thành transaction vì downstream dependency.

#### Actionable alerting

Monitoring hierarchy được đề xuất đi từ cloud infrastructure và application signal đến business action cùng customer outcome. Mỗi alarm cần xác định owner, notification path, investigation procedure và expected response.

#### Chuẩn bị AWS Certified Cloud Practitioner

Session chứng chỉ tổ chức nội dung CLF-C02 theo official domain và Shared Responsibility Model. Một kỹ thuật hữu ích là phân tích vì sao từng đáp án sai không phù hợp thay vì chỉ ghi nhớ đáp án đúng.

#### AI-assisted application security

Session security trình bày AI hỗ trợ architecture review, code review và application testing. Generated finding/fix vẫn cần reproducible evidence, authorization check, business-logic review và human approval.

### Bài học chính

#### Tư duy vận hành

* Theo dõi user journey và business outcome bên cạnh infrastructure health.
* Gắn mỗi alarm với owner và response procedure rõ ràng.
* Dùng Shared Responsibility Model để xác định AWS vận hành phần nào và workload team phải cấu hình phần nào.
* Lưu evidence để incident và security finding có thể được tái hiện.

#### Tư duy bảo mật

* Shift security review về design, source code, dependency, infrastructure và deployment pipeline.
* AI có thể tăng tốc review nhưng không thay thế expert judgment.
* Authentication, authorization và business logic vẫn cần human analysis cẩn thận.

### Ứng dụng vào công việc

* Bổ sung application-level success indicator vào monitoring plan của dự án.
* Giữ security check trong pull-request và CI/CD pipeline.
* Ghi rõ manual approval point bảo vệ production deployment.
* Ghi lại lý do automated finding được chấp nhận, từ chối hoặc cần review thêm.

### Trải nghiệm sự kiện

#### Học hỏi từ diễn giả

Sự kiện kết nối operations, certification knowledge và application security. Sự kết hợp này giúp tôi thấy AWS service knowledge phải được chuyển thành user outcome và operational responsibility.

#### Demo và ví dụ kỹ thuật

Ví dụ infrastructure metric màu xanh nhưng user login thất bại thể hiện rõ giới hạn của infrastructure-only monitoring. Các ví dụ security cũng cho thấy automated output luôn cần validation.

#### Networking và thảo luận

Community discussion giúp tôi nhận ra khoảng trống trong monitoring và security assumption của mình. Tôi nhận được nhiều cách học và troubleshooting có thể áp dụng sau sự kiện.

#### Bài học rút ra

Bài học quan trọng nhất là system health phải được đánh giá từ góc nhìn người dùng. Reliable cloud engineering cũng yêu cầu ownership, evidence và security control xuyên suốt development lifecycle.



> Nhìn chung, meetup giúp tôi củng cố hiểu biết về user-centered monitoring, shared cloud responsibility, certification reasoning và evidence-based application security.
