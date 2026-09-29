# BÁO CÁO TỔNG KẾT TƯ DUY & ÁP DỤNG UML TRONG PHÁT TRIỂN PHẦN MỀM

# 1. Bản chất của UML
- Không phải code, mà là "Bản vẽ thiết kế": UML giống như bản vẽ kỹ thuật của một ngôi nhà. Nó mô tả cái khung (What - Hệ thống làm gì, cấu trúc ra sao) chứ không đi sâu vào việc xây gạch thế nào (How - Code chi tiết, tối ưu vòng lặp)
- Ngôn ngữ giao tiếp chung: Giúp chuẩn hóa cách hiểu giữa toàn bộ các thành viên trong team (từ Dev, Tester đến Leader), tránh tình trạng "mỗi người hiểu một kiểu" dẫn đến code sai lệc
- Nguyên tắc: "Vẽ đủ để hiểu, hình mang lại giá trị giải quyết logic tốt hơn mười hình vẽ chỉ để ngắm
- Giá trị cốt lõi - Giúp chuyển hóa các yêu cầu nghiệp vụ thành kiến trúc cụ thể, từ đó chốt được thiết kế và nhìn ra các rủi ro sai sót ngay từ sớm trước khi bắt tay vào code 
- Một hình vẽ UML có thể thay thế cho mô tả dài dòng, giúp việc hướng dẫn người mới hoặc tìm lỗi khi sửa code diễn ra cực kỳ nhanh chóng

# 2. Các biểu đồ cốt lõi (Tập trung vào 2 nhóm chính)
- UML có đến 14 loại 
Nhưng quan tâm 2 loại sau
# Nhóm Cấu trúc 
- Class Diagram (Biểu đồ lớp): Định hình khung xương của code
- Liệt kê các class, thuộc tính, phương thức và mối quan hệ (kế thừa, phụ thuộc) để chia trách nhiệm rõ ràng
- (Trong Godot, mỗi Scene/Node chứa script thường đóng vai trò như một Class)

# Nhóm Hành vi (Hệ thống Làm Gì?):
- Use Case Diagram: Nhìn từ góc độ Actor (Người dùng/Người test), mô tả họ có thể làm những hành động gì với hệ thống để chốt phạm vi tính năng
- Sequence Diagram (Biểu đồ tuần tự):
Mô tả thứ tự các đối tượng gọi hàm, gửi tín hiệu (signal) cho nhau theo dòng thời gian từ trên xuống
- Activity / State Machine Diagram:
Mô tả các luồng rẽ nhánh hoặc sơ đồ chuyển trạng thái (trong làm game để tránh bug kẹt trạng thái)

# 3. Tư duy áp dụng UML trong môi trường làm việc thực tế
- Doanh nghiệp lớn: 
Bắt buộc cần quy trình UML chặt chẽ để quản lý hệ thống phức tạp và hàng trăm nhân sự không bị rối loạn
- Team nhỏ/Startup: 
Tốc độ và sản phẩm thực tế quan trọng hơn. Đôi khi chỉ cần chốt Game Design/Logic cốt lõi là tiến hành code luôn để kịp playtest
- Tính ổn định của thiết kế: Một leader có kinh nghiệm sẽ thiết kế kiến trúc chuẩn từ đầu, giúp dev có thể triển khai code trơn tru mà không vướng phải các trường hợp ngoại lệ  làm vỡ kiến trúc, từ đó hạn chế tối đa việc phải "đập đi vẽ lại" UML
- Giá trị của việc "Dịch ngược code thành UML": 
Việc dùng source code đang có để vẽ ngược lại UML (như task hiện tại) là một bài tập giúp lập rèn luyện tư duy thiết kế hệ thống thay vì chỉ có góc nhìn hẹp vào từng dòng code lẻ tẻ

# 4. Kế hoạch hành động (Action Plan) cho dự án 
- Tách biệt rõ ràng 2 nhóm Use Case: Người chơi (Player) và Người thử nghiệm (Tester) để thiết kế hệ thống Cheat mà không ảnh hưởng logic game cốt lõi
- Sử dụng Use Case Diagram để chốt toàn bộ tính năng Cheat (Tăng tiền, Tự động thắng, Chọn level).
- Vẽ Class Diagram các Node chính VD: (CryptogramGame, LetterCell,...) để nắm kiến trúc hiện tại
- Vẽ Sequence Diagram cho luồng logic cốt lõi nhất (như việc nhập chữ cái -> check kết quả -> update UI)

 