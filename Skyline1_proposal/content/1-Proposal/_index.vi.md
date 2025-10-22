---
title: "Bản đề xuất"
date: 2025-10-21T00:00:00Z
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# Cloud Racket Platform
## Giải pháp AWS Serverless hợp nhất cho giám sát thời tiết thời gian thực  

### 1. Tóm tắt điều hành  
Badminton Court Finder Platform được thiết kế nhằm hỗ trợ người chơi cầu lông tại TP. Hồ Chí Minh dễ dàng tìm kiếm, đặt sân, và quản lý lịch chơi theo thời gian thực. Ứng dụng được xây dựng hoàn toàn trên kiến trúc AWS Serverless, tích hợp các công nghệ như AI gợi ý cá nhân hóa, phân tích cảm xúc từ đánh giá người dùng, và bản đồ vị trí sân gần nhất thông qua Google API đồng thời hỗ trợ thống kê doanh số hàng tháng cho chủ sân.  

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Việc tìm và đặt sân cầu lông hiện nay chủ yếu dựa vào liên hệ thủ công (số điện thoại hoặc mạng xã hội) , lịch đặt sân không được cập nhật theo thời gian thực và thiếu độ phủ sóng của các sân làm gây trở ngại về ước tính quãng đường đến sân. Đồng thời, chủ sân gặp khó khăn trong việc quản lý, sắp xếp số lượng sân cũng như thống kê doanh thu không hiệu quả.

*Giải pháp*  
Trang web này mang lại quy trình tự động hóa cho việc tìm kiếm, đặt sân và quản lý hiệu quả cho chủ doanh nghiệp. Người dùng có thể tìm kiếm sân gần vị trí của mình thông qua Amazon Location Service , xem tình trạng sân theo thời gian thực trong Amazon DynamoDB  và được gợi ý sân phù hợp qua Amazon Personalize. Chủ sân có thể đăng ký và cập nhật thông tin sân, nhận email xác nhận đặt sân qua Amazon SES và thống kê doanh thu qua thông qua bảng điều khiển tùy chỉnh (Custom Dashboard) được xây dựng bằng AWS Amplify, Lambda, và biểu đồ Chart.js từ dữ liệu trong DynamoDB/S3.Giao diện web được triển khai bằng AWS Amplify và quản lý người dùng qua Amazon Cognito.

*Lợi ích và hoàn vốn đầu tư (ROI)*  
- Đối với người chơi: dễ dàng tìm và đặt sân phù hợp chỉ trong vài giây, nhận gợi ý cá nhân hóa dựa trên hành vi và vị trí, đồng thời nhận email xác nhận tự động. Thời gian tìm sân giảm 90% (từ 30 phút còn 3 phút), và thời gian xác nhận đặt sân rút ngắn từ 2–24 giờ xuống chỉ còn 5 phút.

- Đối với chủ sân: quản lý sân, lịch và người đặt tự động thông qua dashboard trung tâm, giảm 80% thời gian thao tác thủ công. Hệ thống cung cấp báo cáo doanh thu, lượt đặt và đánh giá trung bình trực quan, hỗ trợ ra quyết định dựa trên dữ liệu.

- Đối với nhóm phát triển: Hệ thống hoàn toàn không máy chủ (serverless), chi phí vận hành cực thấp (<1 USD/tháng ở giai đoạn đầu, ước tính $8–15/tháng sau Free Tier). Hệ thống vừa là giải pháp thực tế, vừa là môi trường học tập giàu giá trị cung cấp dữ liệu thật phục vụ nghiên cứu AI, NLP tiếng Việt và mô hình gợi ý.
### 3. Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc AWS Serverless giúp vận hành ổn định, dễ mở rộng và tiết kiệm chi phí. Dữ liệu về người dùng, sân và lịch đặt được lưu trữ trong Amazon DynamoDB. Giao tiếp giữa các thành phần thông qua Amazon API Gateway và các hàm AWS Lambda. Giao diện web và di động được triển khai bằng AWS Amplify, trong khi Amazon Cognito đảm bảo kiểm soát truy cập an toàn.
Amazon Personalize gợi ý sân dựa trên lịch sử người dùng và Amazon Comprehend cân nhắc sân dựa trên bình luận và sao đánh giá, Custom Dashboard sẽ trực quan hóa dữ liệu hoạt động cho chủ sân và người dùng. Tất cả hoạt động được giám sát qua 

Amazon CloudWatch và tự động hóa bằng Amazon EventBridge.

![Cloud Racket Platform Architecture](images/Proposal/Skyline1_CloudRacket.jpg)

### Dịch vụ AWS sử dụng
- **AWS Amplify Hosting**: Lưu trữ và triển khai ứng dụng web/mobile. 	
- **Amazon API Gateway**: Giao tiếp giữa client và backend.
- **AWS Lambda**: Xử lý logic nghiệp vụ và kết nối các dịch vụ AWS.
- **Amazon DynamoDB**: Lưu trữ thông tin người dùng, sân và lịch đặt.
- **Amazon Cognito**: Xác thực và phân quyền người dùng..
- **Amazon SES**: Gửi email xác nhận và thông báo tự động.
- **Amazon S3**: Lưu trữ hình ảnh sân và dữ liệu phân tích.
- **Amazon Personalize**: Đưa ra gợi ý sân phù hợp cho người dùng.
- **Amazon Comprehend (Optional)**:  phân tích cảm xúc trong bình luận tiếng Việt để bổ sung điểm đánh giá tổng hợp.
- **Amazon Location Service + DynamoDB GeoLib** : Tìm kiếm sân gần vị trí người dùng.
- **Custom Dashboard**: Trực quan hóa dữ liệu và phân tích báo cáo thông qua bảng điều khiển tùy chỉnh (Custom Dashboard) được xây dựng bằng AWS Amplify, AWS Lambda, và biểu đồ Chart.js từ dữ liệu lưu trong Amazon DynamoDB hoặc Amazon S3.
- **Amplify Admin UI (Admin Portal)**: quản lý CRUD sân, duyệt bình luận, theo dõi logs. 
- **Amplify CI/CD**: Tự động triển khai và cập nhật hệ thống.
- **Amazon CloudWatch**: Theo dõi log, hiệu suất và cảnh báo.
- **Amazon EventBridge (Scheduler)**: Tự động hóa lịch gửi thông báo và dọn dẹp dữ liệu.
- **AWS IAM + KMS + WAF**:  Quản lý bảo mật, mã hóa dữ liệu và ngăn chặn tấn công web.
*Thiết kế thành phần*  
- **User Module**: Amazon Cognito quản lý đăng ký, đăng nhập và hồ sơ người dùng; dữ liệu người chơi, lịch sử đặt sân và sân yêu thích lưu trong DynamoDB.
- **Court Module**: Chủ sân thêm, chỉnh sửa thông tin và ảnh sân; dữ liệu sân lưu trong DynamoDB, hình ảnh trên S3; cập nhật trạng thái sân qua API Gateway + Lambda.
- **Booking Flow**: API Gateway → Lambda → DynamoDB → SES xử lý đặt sân, kiểm tra trùng lịch và gửi email xác nhận tự động.
- **Recommendation System** : Amazon Personalize phân tích hành vi và đánh giá người dùng để gợi ý sân; Lambda truy vấn kết quả gợi ý theo mô hình 70% hành vi + 30% rating.
- **Geo Search**: DynamoDB Geo Library hoặc Amazon Location Service tìm sân gần vị trí người chơi; tích hợp Google Maps hiển thị bản đồ và hướng đi.
- **Admin Dashboard**: Bảng điều khiển tùy chỉnh hiển thị doanh thu, lượt đặt và đánh giá, được xây dựng bằng AWS Amplify và Chart.js, với dữ liệu tổng hợp từ DynamoDB hoặc S3 thông qua AWS Lambda.
- **Automation Layer**: EventBridge kích hoạt Lambda định kỳ để gửi nhắc lịch, huấn luyện lại Personalize và dọn dữ liệu cũ.
### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
Dự án được chia thành 4 giai đoạn chính:
- Nghiên cứu và thiết kế kiến trúc: Lên sơ đồ hệ thống AWS Serverless, xác định quy trình đặt sân và luồng dữ liệu (Tuần 1).
- Phát triển và kiểm thử: Xây dựng API Gateway + Lambda, tích hợp DynamoDB và Cognito, kiểm thử chức năng (Tuần 2-3).
- Phân tích: Thêm gợi ý từ Personalize,  hiển thị dữ liệu bằng Dashboard (Tuần 4).
- Triển khai và tối ưu: Sử dụng Amplify CI/CD để triển khai tự động, thiết lập CloudWatch và EventBridge để giám sát (Tuần 5).

*Yêu cầu kỹ thuật*  
- Frontend: ReactJS / Next.js (AWS Amplify Hosting) 
- Backend: AWS Lambda (Node.js hoặc Python) + Amazon API Gateway
- Database: Amazon DynamoDB (lưu người dùng, sân, lịch đặt, rating; hỗ trợ truy vấn Geo qua DynamoDB Geo Library hoặc AWS Location Service)
- AI Integration: Amazon Personalize (phân tích hành vi và đánh giá để gợi ý sân phù hợp)
- Auth & Security: Amazon Cognito (đăng nhập/xác thực), AWS IAM (phân quyền), AWS KMS (mã hóa dữ liệu), AWS WAF (chống tấn công web)
- Email: Amazon SES (gửi xác nhận đặt sân, thông báo, nhắc lịch tự động)
- Analytics: Custom Dashboard (trực quan hóa doanh thu, lượt đặt và đánh giá từ dữ liệu DynamoDB hoặc S3, hiển thị qua AWS Amplify + Lambda + Chart.js).
- Automation: Amazon EventBridge (Scheduler) tự động hóa nhắc lịch, cập nhật dữ liệu gợi ý và dọn dẹp dữ liệu cũ
- Maps API: AWS Location Service hoặc Google Maps / Places / Distance Matrix (tìm sân gần, hiển thị bản đồ và chỉ đường)
### 5. Lộ trình & Mốc triển khai  
- *Thời lượng dự án*: 3 tháng (giai đoạn thực tập).  
Tháng 1 – Nghiên cứu & Chuẩn bị

- Nghiên cứu các dịch vụ AWS (Amplify, Lambda, DynamoDB, Personalize, SES, Location Service).
- Thiết lập môi trường phát triển và cấu hình phần cứng.
Tháng 2 – Thiết kế hệ thống & Kiến trúc
- Thiết kế kiến trúc tổng thể và xác định các mô-đun chính.
- Phát triển schema API, vai trò người dùng (Cognito), và pipeline CI/CD.
- Chuẩn bị bộ dữ liệu mẫu cho Personalize và DynamoDB.
Tháng 3 – Triển khai & Triển khai thực tế
- Tuần 1: Hoàn thiện kiến trúc, định nghĩa schema DynamoDB, triển khai API Gateway + Lambda.
- Tuần 2: Phát triển backend và frontend (ReactJS/Next.js + Amplify Hosting).
- Tuần 3: Tích hợp Amazon Personalize, SES, và Location Service.
- Tuần 4: Kiểm thử, tối ưu hiệu năng và triển khai hoàn chỉnh trên AWS Amplify.
### 6. Ước tính ngân sách  
Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)  
Hoặc tải [tệp ước tính ngân sách](../attachments/budget_estimation.pdf).  

*Chi phí hạ tầng*  
+ Dịch vụ AWS:
- AWS Amplify Hosting: Free Tier: 500 phút build, 5 GB phục vụ. Sau Free Tier: ~$0.01/phút × 500 = $5.00/tháng
- AWS Lambda: $0.00/tháng (20,000 requests/ngày, 128 MB, trung bình 200 ms)
- Amazon API Gateway: $0.00/tháng (600,000 requests/tháng, trong Free Tier)
- Amazon DynamoDB: $0.00/tháng (5 GB dữ liệu, 100K đọc/ghi mỗi ngày)
- Amazon S3 (Lưu ảnh): $0.12/tháng (10 GB lưu trữ, 5,000 GET/PUT requests)
- Amazon SES (Email): $0.00/tháng (2,000 email/tháng trong Free Tier)
- Amazon Personalize: Miễn phí 2 tháng đầu (20 GB dữ liệu, 5M interactions). Sau đó: ~$8.00/tháng với batch inference (dữ liệu nhỏ + huấn luyện hàng tuần).
- Dashboard tùy chỉnh (Amplify + Chart.js): $0.00/tháng (sử dụng Amplify hiện có, dữ liệu từ S3/DynamoDB)
- Amazon Location Service: $0.00/tháng (10,000 map requests, 1,000 location requests)
- Amazon EventBridge (Scheduler): $0.00/tháng (10 quy tắc kích hoạt mỗi ngày/giờ)
- AWS IAM + KMS + WAF: $0.00/tháng (xác thực, mã hóa và bảo mật cơ bản)

+ Tổng cộng: $0.7/tháng, $8.40/12 tháng
- Tháng 1: $0.12/tháng (tất cả trong Free Tier)
- Tháng 2: $5.12/tháng (Personalize vẫn trong Free Tier, Amplify bắt đầu tính phí)
- Sau khi hết Free Tier: $13.12/tháng, ≈ $157.44/năm

### 7. Đánh giá rủi ro  
*Ma trận rủi ro*  
- Mất kết nối Internet: Tác động trung bình, xác suất trung bình  
- Truy cập trái phép: Tác động cao, xác suất thấp  
- Vượt ngân sách: Tác động thấp, xác suất thấp  
- Lỗi gợi ý AI: Tác động trung bình, xác suất thấp  

*Chiến lược giảm thiểu*  
- Mạng: Tự động thử lại khi mất kết nối
- Bảo mật: Áp dụng MFA qua Cognito, WAF ngăn chặn tấn công
- Chi phí: Cảnh báo qua AWS Budgets, tối ưu tần suất truy vấn
- AI: Theo dõi và cập nhật mô hình Personalize định kỳ

*Kế hoạch dự phòng*  
- Cho phép đặt sân tạm thời offline và đồng bộ khi có mạng  
- Rollback CodePipeline nếu có lỗi triển khai hoặc vượt chi phí  

### 8. Kết quả kỳ vọng  
*Cải tiến kỹ thuật*: Ứng dụng cung cấp khả năng tìm kiếm và đặt sân theo thời gian thực, gợi ý cá nhân hóa và báo cáo trực quan giúp tối ưu hóa hoạt động cho cả người chơi và chủ sân.
*Giá trị dài hạn*: Nền tảng có thể mở rộng sang các môn thể thao khác (tennis, bóng rổ, phòng gym), đóng vai trò như một mẫu khung cho các giải pháp thể thao thông minh dựa trên AWS Serverless và AI. Ngoài ra, đây là dự án thực hành lý tưởng cho sinh viên hoặc nhóm nghiên cứu muốn ứng dụng AWS trong việc phát triển hệ thống thông minh.