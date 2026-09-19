# Những hiểu biết về firebase, các tính năng Ứng dụng vào game

# BUILD 
- Xác thực (Authentication): Đăng nhập Google Play / Apple / Chơi ẩn danh để lưu tiến trình (Cloud Save)
- Xác minh số điện thoại: Gửi OTP SMS chống tạo nick ảo cày cuốc
- App check: Chặn bản game lậu, mod APK gọi phá hoại server
- Quy tắc bảo mật (Security Rules): Chặn người chơi tự sửa điểm, tự hack vàng/gem
- SQL Connect: Kết nối database quan hệ cho game RPG/MMO có dữ liệu phức tạp
- Firestore: Lưu dữ liệu nhân vật, hòm đồ (inventory), thông tin tài khoản
==>  RealTime Database (Làm Addon): Đồng bộ dữ liệu cực nhanh cho chat ingame, phòng chờ (Lobby), trạng thái online
- Storage: Lưu trữ avatar, tải map mới, tải gói DLC/asset phụ từ xa
- App Hosting / Hosting: Dựng web Landing Page giới thiệu game, web nhập Giftcode
- Cloud Functions: Viết logic server chống hack: xác thực hóa đơn nạp IAP với Google/Apple, trao thưởng sự kiện
- Công cụ mô phỏng (Emulator): Chạy giả lập Firebase để test offline trên máy cá nhân mà không tốn phí

# RUN (Vận hành & Kiếm tiền)
- Test Lab: Chạy test tự động trên hàng trăm máy thật của Google để kiểm tra lỗi màn hình, văng game
- App Distribution: Gửi file APK nội bộ cho Tester/QA tải về test nhanh
- Crashlytics (Làm Addon): Báo cáo lỗi văng game, chỉ đích danh dòng code bị crash
- Performance Monitoring: Đo thời gian load scene, độ tụt FPS, tốc độ mạng trong game
- Remote Config: Đổi thông số game từ xa không cần cập nhật bản mới (chỉnh máu quái, bật sự kiện, đổi giá shop)
- A/B Testing: Thử nghiệm xem 2 phương án (ví dụ nút Shop đỏ hay xanh) cái nào người chơi nạp nhiều hơn
==>  Cloud Messaging - FCM (Làm Addon): Bắn thông báo đẩy ra màn hình khoá để kéo người chơi quay lại game 
- In-app Messaging: Hiện popup ưu đãi giảm giá ngay khi người chơi đang ở trong game
==>  Analytics (Làm Addon): Đo hành vi người chơi (vượt màn, bỏ game ở màn nào, mua đồ gì)
==>  Admob (Làm Addon): Kiếm tiền từ quảng cáo (Banner, Interstitial, Video xem nhận quà hồi sinh)
Ads (Google Ads): Chạy quảng cáo kéo người chơi mới tải game

# AI 
- Gemini trong Firebase: Sinh lời thoại NPC thông minh không trùng lặp, tự tạo nhiệm vụ hàng ngày
- Công cụ, kỹ năng MCP: Cho AI kết nối với data game để phân tích cân bằng chỉ số hoặc làm bot
- Logic AI của Firebase: Tự động phát hiện và chặn từ ngữ thô tục trong khung chat game

---------------------------------------------------------
# Các tính năng cần chú ý 
**Firestore khác Realtime Database**
- Realtime DB: Tốc độ nhanh --> Dùng cho chat ingame, xem ai đang online, phòng chờ
- Firestore: Chuyên lưu trữ có tổ chức --> Dùng cho hòm đồ, thông tin người chơi, bảng xếp hạng

**FCM vs In-App Messaging**
- FCM: Bắn thông báo ra ngoài khi người chơi đã tắt game để kéo họ vào lại
- In-App Messaging: Bật banner/popup giảm giá khi người chơi đang mở game

**Remote Config vs Storage**
- Remote Config: Đổi vài con số/chữ từ xa (chỉnh máu quái, giá shop)
- Storage: Tải file nặng (ảnh avatar, âm thanh, map tải thêm)
------------------------------------------------------------
# VD: Các tính năng này phối hợp trong 1 vòng đời game
- Vừa cài game: Auth tự cấp nick khách -> Remote Config tải thông số màn chơi -> Analytics đếm lượt tân thủ vào game
- Đang chơi: Database lưu vàng và hòm đồ -> Crashlytics canh xem game có bị văng không -> AdMob bật video thưởng khi người chơi cần hồi sinh
- Tắt game: Sau vài tiếng, FCM hú thông báo ngoài màn hình khóa: "Đầy năng lượng rồi, vào chơi tiếp đi
- Nạp tiền: Cloud Functions đứng ở giữa check hóa đơn với Google Play để chặn hack nạp lậu rồi mới cộng vật phẩm 

