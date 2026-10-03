### ỨNG DỤNG AI & ĐÓNG GÓI SKILL TRONG CÔNG VIỆC

# 1. PHƯƠNG PHÁP LÀM VIỆC VỚI AI (THAY ĐỔI ĐỂ KHÔNG LÀM THỦ CÔNG)
- Trước đây: Mỗi lần làm một plugin mới lại phải ngồi prompt từ đầu, nhắc lại từng bước (cấu hình Gradle, viết Java, build file AAR, viết script Godot) 
- Hiện tại: Chuyển sang phương pháp đóng gói Skill vào file cấu hình (CLAUDE.md)
- Mọi kinh nghiệm, rào chắn kỹ thuật và quy trình chuẩn được cố định sẵn trong dự án. Tôi chỉ cần đưa ra yêu cầu cốt lõi, AI tự kích hoạt Skill để thực hiện đồng bộ

# 2. TRONG 2 TUẦN QUA, AI ĐÃ ĐƯỢC DÙNG TRONG CÁC VIỆC GÌ?
- AI được sử dụng xuyên suốt qua 5 nhóm việc thực tế:
- Viết mã nguồn Java Native: Tạo module Android kết nối với các SDK Google Play Services Auth (Sign-In) và Google Play Billing v7
- Tự động hóa Build: Viết cấu hình Gradle, tự động chạy lệnh xuất file .aar release đặt đúng thư mục plugin của Godot
- Xử lý lỗi nền tảng phức tạp:(treo app lúc mở), fix lỗi 10:DEVELOPER_ERROR của Firebase qua trích xuất SHA-1 keystore
 
# 3. SKILL ĐÃ TẠO RA ĐỂ HỖ TRỢ (TRỌNG TÂM)
* Skill 1: Quy trình 4 bước tự động tạo Plugin Android Native
- Nội dung đóng gói: Chuẩn hóa toàn bộ quy trình từ tạo module Java trong custom_plugin, cấu hình Gradle, xuất file .aar release đến viết wrapper GDScript
- Ứng dụng: 
Bất kỳ khi nào cần làm plugin mới (Google Sign-In, Billing, Facebook, TikTok, AppsFlyer), chỉ cần ra lệnh 1 câu, AI sẽ tự động chạy tuần tự đúng bước đó
 
* Skill 2: Bộ quy chuẩn Clean Code & Tách biệt UI (RULE.md)
- Nội dung đóng gói:
- Cấm code UI bằng script: 100% giao diện, popup phải dựng bằng file cảnh .tscn. Script chỉ làm nhiệm vụ hứng sự kiện nút bấm và gán dữ liệu
- Biến và Comment: Cấm magic number (phải gán const rõ nghĩa), comment đúng 1 dấu # bằng tiếng Việt giải thích lý do "Tại sao làm"
- Ứng dụng: Đảm bảo toàn bộ code do AI sinh ra luôn sạch sẽ, đồng nhất, khi đọc vào hiểu được ngay

* Skill 4: Kiến trúc dịch vụ tập trung 
- Nội dung đóng gói:
Mọi cuộc gọi bên thứ ba (Firebase, AdMob, Google Auth, IAP) bắt buộc phải quy về một file Singleton trung tâm (như GameServices.gd), cấm các màn chơi riêng lẻ tự gọi plugin native
Ứng dụng: Giữ cho kiến trúc game luôn liền mạch, dễ bảo trì, sau này muốn thay đổi SDK chỉ cần sửa đúng 1 nơi


---------------------------------
- Không phó mặc toàn bộ cho AI:
- Không ném cả bài toán lớn hay prompt mơ hồ để AI tự biên tự diễn
- Người làm đóng vai trò kiến trúc sư: phân tích luồng dữ liệu trước, chia nhỏ tính năng thành từng bước cụ thể 
(1-2 dòng prompt cho mỗi tác vụ: tạo module Java, cấu hình Gradle, bọc GDScript, dựng UI node)
- Thiết lập kỷ luật qua Rule và Context (RULE.md / CLAUDE.md):
- Ép AI tuân thủ nghiêm ngặt chuẩn code: hàm ngắn 5-15 dòng, không magic string/number, cấm tự tạo nút bằng code (bắt buộc dựng UI 100% trong file .tscn) -(Nếu có)
- Đưa sẵn các cảnh báo kỹ thuật vào file hướng dẫn để AI không mắc lỗi lặp lại:
+ cơ chế hàng đợi xử lý cold-start Android, cấm quyền exact alarm gây reject Google Play
---------------------------------

---------------------------------
# Phân chia đúng vai trò công cụ:
- Dùng AI  để đọc hiểu kiến trúc toàn dự án, bắt lỗi logcat và xử lý môi trường hệ thống
- Dùng AI để sửa nhanh mã nguồn trực tiếp theo từng module nhỏ khi đã hiểu 
- Kiểm soát code chặt chẽ 
- Mọi file code AI sinh ra đều được review từng dòng qua phần theo dõi trước khi nhận
- Tuyệt đối không đoán mò: Mọi tính năng đều được nạp file APK và test thực tế trên thiết bị thật qua cổng ADB để đối soát kết quả
---------------------------------



## 4. HIỆU QUẢ THỰC TẾ TRONG CÔNG VIỆC
- Rút ngắn thời gian viết prompt: Thay vì mỗi lần giao việc phải viết cả trang mô tả, nay chỉ cần 1 câu lệnh ngắn vì toàn bộ luật đã nằm sẵn trong file
- Chuẩn hóa chất lượng code: Code AI viết ra có chất lượng đồng nhất, không còn code rác, không còn tình trạng mỗi dự án viết một kiểu
- Tự động hóa kế thừa: Khi một người mới tham gia dự án, chỉ cần mở file CLAUDE.md lên là cả người và AI đều biết rõ luật chơi và cách thức làm việc của dự án
-- Tốc độ triển khai vượt trội (Rút ngắn 70-80% thời gian)
