---
title: "Event 1"
date: 2026-07-25
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Báo cáo sự kiện: “FCAJ X Agentic AI Build Week – Show Up. Build. Pitch. Win!”

### Mục tiêu sự kiện

* Tạo môi trường thực hành có tính cạnh tranh, nơi developer, data engineer và sinh viên xây dựng ứng dụng Agentic AI tự chủ để giải quyết bài toán kinh doanh thực tế.
* Chia sẻ kiến trúc cloud-native trên AWS cùng kinh nghiệm triển khai từ các đội đạt thành tích tại Agentic AI Build Week.
* Khuyến khích tư duy đổi mới, tinh thần học tập liên tục và kỹ năng teamwork hiệu quả trong kỷ nguyên AI Agent.

### Diễn giả và đại diện các đội

* **Joseph Marazota:** Head of Technology tại AWS.
* **Nguyen Gia Hung:** Head of Solution Architect tại AWS Vietnam và Nhà sáng lập First Cloud AI Journey (FCAJ).
* **One Team — Giải Nhất AWS Track:** Đại diện bởi Chung và các thành viên.
* **Signal Scout — Giải Nhì AWS Track:** Hoang Hieu, Quoc Hao, Minh Quan (Willer), Cong Minh, Duy Khiem và Tuan Luc.
* **Plan B Team:** Long, Vi, Phat, An và Nghia.
* **3K Team:** Nguyen Huy, Huynh An Khuong, Hoang Huynh Duc, Ngo Khoi và Dang Nguyen Phuoc Loc.
* **Six Pillars Team:** Viet, Nguyen Van Linh, Nguyen, Minh Nhat và Phuoc Huyen.

### Nội dung nổi bật

#### Opening keynote: Thay đổi mental model trong kỷ nguyên AI Agent

Joseph Marazota trình bày cách AI Agent đang thay đổi tốc độ phát hành phần mềm. Những quy trình từng cần cả quý hoặc nhiều tuần nay có thể hoàn thành trong vài phút. Sự thay đổi này yêu cầu engineer xem xét lại vòng đời phát triển sản phẩm truyền thống và chủ động đặt câu hỏi đối với các giả định cũ.

Engineer trẻ có lợi thế khi không bị giới hạn bởi tư duy mainframe hoặc on-premises. Tuy nhiên, tốc độ cao hơn không loại bỏ trách nhiệm của con người. Ngay cả hệ thống AI tiên tiến và hoạt động robot quy mô lớn của Amazon vẫn cần con người đánh giá đề xuất, phê duyệt hành động quan trọng, đồng thời bảo đảm an toàn và độ chính xác thông qua cơ chế **Human-in-the-Loop**.

#### Đặt món bằng hội thoại với AI: KFC Agent của One Team

One Team bắt đầu từ một thất bại thực tế: hệ thống AI đặt món drive-through không hiểu đúng ngữ cảnh hội thoại và tạo ra đơn hàng bất hợp lý. Đội xây dựng một Agent hoạt động trực tiếp trong ứng dụng nhắn tin quen thuộc như Zalo hoặc WhatsApp, nhờ đó người dùng không phải tải ứng dụng mới hoặc đăng ký thêm tài khoản.

Giải pháp sử dụng **Amazon Bedrock AgentCore** để duy trì session memory và sở thích khách hàng. **AWS WAF** bảo vệ hạ tầng public, trong khi TinyFish thu thập menu mới nhất từ website chính thức của KFC để lưu trong AWS database. Chi phí vận hành được ước tính khoảng **0,006 USD cho mỗi đơn hàng**, giảm 75% so với mô hình xử lý truyền thống.

#### Nền tảng competitor intelligence Multi-Agent: Signal Scout

Signal Scout giới thiệu nền tảng thu thập các market signal công khai đang phân tán, kết nối dữ liệu tài chính và doanh nghiệp, sau đó dự báo ROI nếu một doanh nghiệp cân nhắc áp dụng chiến lược của đối thủ.

Kiến trúc sử dụng mô hình **Agent-to-Agent (A2A)**. Supervisor Agent điều phối các Sub-agent chuyên biệt cho crawling, analysis và validation. Crawler tự động chọn Apify cho trang tĩnh hoặc TinyFish cho nguồn dữ liệu động. Validation loop chấm điểm chất lượng dữ liệu và thử thu thập lại tối đa hai lần trước khi chuyển trường hợp chưa giải quyết được cho con người review.

Việc thay thế một số thành phần bên thứ ba bằng browser và web tool native trên AWS giúp giảm chi phí vận hành ước tính từ **94 USD xuống 35 USD mỗi tháng**, đồng thời hỗ trợ yêu cầu data residency.

#### Tự động tạo sơ đồ kiến trúc và hạ tầng: Plan B

Plan B giải quyết một bottleneck phổ biến của Solutions Architect: phải tạo architecture diagram, cost estimate và deployment plan trong thời gian rất ngắn. Workflow AI-native của đội chuyển đổi requirement dạng ngôn ngữ tự nhiên hoặc tài liệu thành:

**Nhập requirement → phân tích policy và constraint → tạo sơ đồ Draw.io → tính cost estimation → sinh Terraform hoặc CloudFormation → triển khai lên AWS**

Workflow sử dụng bộ icon kiến trúc AWS chính thức và validation script để từ chối những service nằm trong blacklist nội bộ của doanh nghiệp. Điều này cho thấy hạ tầng do AI sinh ra vẫn phải tuân thủ policy tổ chức và được kiểm tra kỹ thuật.

#### Giám sát luồng người theo thời gian thực: Sheper của 3K Team

3K Team thiết kế Sheper nhằm giảm tình trạng ùn tắc tại sân bay, siêu thị và sự kiện lớn. Video được truyền qua **Amazon Kinesis Video Streams** và xử lý trên **AWS Fargate**. YOLOv8 hoặc YOLOv11 phát hiện người, còn ByteTrack gán tracking ID và hỗ trợ tính confidence score.

Operator có thể xác định vùng giám sát tùy chỉnh và đánh giá mật độ di chuyển theo thời gian thực. Bedrock Agent tổng hợp kết quả quan sát và tạo đề xuất điều phối nhân sự, giúp đơn vị vận hành phản ứng trước khi ùn tắc trở nên nghiêm trọng.

#### Phát hiện rửa tiền: Adaptive Workflow Engine của Six Pillars

Six Pillars tập trung vào tỷ lệ false positive rất cao của cảnh báo giao dịch đáng ngờ trong ngân hàng và fintech. Giải pháp sử dụng kiến trúc ba lớp:

1. **Fast Detection:** Kinesis Data Streams tiếp nhận giao dịch, Lambda thực hiện feature engineering và XGBoost lọc hoạt động có mức rủi ro thấp.
2. **Deep Investigation:** AWS Step Functions điều phối các Sub-agent chuyên biệt cho KYC, money flow và sanctions. OpenSearch vector database hỗ trợ RAG để truy xuất tiền lệ pháp lý và xây dựng evidence có cấu trúc.
3. **Decision và Human Review:** Hai LLM cross-validation kết quả, trong khi Bedrock Guardrails giảm nguy cơ hallucination. Chỉ những trường hợp có mức rủi ro cao thực sự mới được chuyển đến dashboard để con người quyết định.

### Phân tích so sánh

| Tiêu chí | Cách làm truyền thống hoặc thủ công | Kiến trúc Agentic AI trên AWS |
|---|---|---|
| Đặt món F&B | Nhân viên xử lý thủ công hoặc AI cơ bản có thể hiểu sai context và hallucination. | Messaging Agent kết hợp Bedrock session memory; khoảng 0,006 USD mỗi đơn và giảm 75% chi phí xử lý. |
| Competitor intelligence | Nghiên cứu thủ công chậm, chi phí vận hành từ 94 USD mỗi tháng. | Supervisor, crawler, analysis và validation Agent; giảm còn khoảng 35 USD mỗi tháng với AWS-native tool. |
| Thiết kế kiến trúc và ước tính | Solutions Architect vẽ sơ đồ và tính chi phí thủ công bằng spreadsheet. | Ngôn ngữ tự nhiên tạo Draw.io, cost estimate, IaC và deployment workflow. |
| Giám sát đám đông | CCTV được xem lại sau khi ùn tắc đã xảy ra. | Kinesis Video, YOLO, ByteTrack và Bedrock phân tích thời gian thực, đưa ra khuyến nghị chủ động. |
| Phát hiện AML | 90–95% false positive, khoảng ba giờ mỗi case và 20–25 USD cho một lượt review thủ công. | XGBoost filtering, Step Functions và RAG investigation, dual-LLM validation, Guardrails và human escalation có chọn lọc. |

### Bài học chính

#### Design thinking

* Bắt đầu từ business problem và pain point cụ thể thay vì xây một ứng dụng chung chung chỉ để thể hiện độ phức tạp kỹ thuật.
* Trong thời hạn 24–48 giờ, cần xác định rõ in-scope và out-of-scope, đồng thời ưu tiên một MVP ổn định.
* Đo lường chi phí vận hành Cloud và cân nhắc data residency hoặc compliance khi lựa chọn managed service và công cụ bên thứ ba.

#### Kiến trúc kỹ thuật

* Mô hình Supervisor và Sub-agent chuyên biệt có thể chia nhỏ workflow phức tạp mà không tạo ra một Agent quá lớn.
* Cần kiểm soát hallucination bằng validation loop, dual-model cross-check, Bedrock Guardrails, evidence và human approval.
* Dịch vụ Kinesis có thể kết nối video hoặc transaction data thời gian thực với computer vision và machine-learning model.
* Kiến trúc và IaC do AI sinh ra vẫn cần policy check, security control và technical validation trước khi triển khai.

#### Phát triển bản thân

* Xây dựng sản phẩm dưới áp lực thời gian giúp rèn resilience, khả năng ưu tiên và xử lý incident mà việc học lý thuyết khó mang lại.
* Low-ego collaboration, active listening và phân chia trách nhiệm rõ giữa frontend, backend, AI, business và pitching là điều kiện quan trọng để hoàn thành dự án tham vọng.

### Ứng dụng vào công việc

* Áp dụng workflow Supervisor–Sub-agent cho dự án cá nhân khi task có thể chia thành retrieval, analysis, validation và action.
* Củng cố CI/CD bằng Git history rõ ràng, quản lý `.env` nghiêm túc, secret scanning và approval rõ trước production deployment.
* Quản lý hạ tầng bằng Terraform hoặc CloudFormation để các environment có thể review, version control và tái tạo nhất quán.
* Xây dựng MVP ổn định, có thể demo trực quan và chuẩn bị phương án dự phòng cho network disruption, service limit hoặc hết AI-token budget.
* Bổ sung business outcome đo lường được, cost estimate và validation evidence vào technical proposal thay vì chỉ trình bày architecture.

### Trải nghiệm sự kiện

#### Chia sẻ kiến thức cởi mở và thực tế

Các diễn giả và đội thi chia sẻ cả thành tích lẫn những tình huống khó khăn, chẳng hạn vô tình đẩy `.env` lên GitHub, network latency, cạn AI-token budget và phát sinh chi phí SageMaker ngoài dự kiến. Những ví dụ này làm bài học kỹ thuật trở nên chân thực và cho thấy cách các đội phục hồi dưới áp lực.

#### Cơ hội networking đa dạng

Sự kiện kết nối sinh viên và engineer từ nhiều trường đại học và chuyên ngành khác nhau, gồm AI, security, software engineering và business. Các cuộc trao đổi cho thấy kỹ năng bổ trợ giữa nhiều vai trò có thể tạo nên sản phẩm và phần pitching tốt hơn.

#### Động lực vượt qua giới hạn cá nhân

Việc chứng kiến các prototype có chất lượng gần production được xây dựng trong 24–48 giờ giúp giảm rào cản tâm lý khi tham gia Hackathon. Sự kiện khuyến khích tôi học thông qua trải nghiệm thực tế thay vì chờ đến khi cảm thấy bản thân đã chuẩn bị hoàn hảo.

#### Bài học rút ra

Công nghệ là phương tiện, còn giá trị thực tế mới là mục tiêu. Một kiến trúc phức tạp chỉ hữu ích khi giải quyết đúng bài toán của người dùng hoặc doanh nghiệp. Thất bại trong testing là cơ hội rèn khả năng thích nghi, còn kết quả tốt trong kỷ nguyên AI phụ thuộc vào vai trò rõ ràng, tinh thần học tập liên tục và khả năng cùng nhau phát triển.

#### Một số hình ảnh sự kiện

![Bùi Hữu Lợi tham dự FCAJ X Agentic AI Build Week ngày 25/07/2026](/images/events/fcaj-agentic-ai-build-week-2026-07-25.png)

<!-- ẢNH BỔ SUNG EVENT 1: Chèn thêm ảnh trình bày của đội thi hoặc ảnh networking đã được cho phép bên dưới comment này.
Tên file đề xuất: static/images/events/fcaj-agentic-ai-build-week-additional.jpg
-->

> Nhìn chung, FCAJ X Agentic AI Build Week giúp tôi hiểu cách business-first thinking, kiến trúc Agentic AI, cost awareness, validation control và low-ego teamwork có thể biến một ý tưởng tham vọng thành prototype thực tế dưới áp lực thời gian cao.
