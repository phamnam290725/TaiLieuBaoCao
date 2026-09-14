## BÁO CÁO PHÂN TÍCH GAME: CRYPTOGRAM - LOGIC PUZZLE GAME
---------------------------------------------------------

# 1. Tổng quan:
Tên game: Cryptogram: Logic Puzzle Game
Thể loại: Giải đố logic, tìm từ vựng 

# 2. Cách chơi:
- Cơ chế điều khiển cơ bản: Chạm (Tap) vào các ô chứa số, sau đó sử dụng bàn phím ảo ở nửa dưới màn hình để nhập chữ cái
- Vòng lặp gameplay chính / Cách qua màn: Người chơi quan sát các con số, kết hợp logic và vốn từ vựng tiếng Anh để đoán chữ. Khi nhập một chữ cái, hệ thống sẽ tự động quét và lấp đầy toàn bộ các ô có cùng con số đó trên màn hình (cơ chế check và update mảng dữ liệu rất nhanh)
- Màn chơi kết thúc thắng lợi khi toàn bộ đoạn văn bản ẩn được giải mã xong

# 3. Các tính năng chính:
- Giao diện người dùng (UI) / Hệ thống tương tác: Layout UI được phân mảng rất hợp lý cho thao tác mobile
- Nửa trên là Scroll Container chứa câu đố, nửa dưới neo cố định bàn phím
- Các ô lưới đang tương tác được highlight màu đẹp và rất trực quan
- Hệ thống tính điểm/nâng cấp: Không có thăng cấp nhân vật, game tập trung giữ chân người dùng chủ yếu qua hệ thống Nhiệm vụ và Chuỗi ngày chơi liên tục để mở khóa phần thưởng

# Các cơ chế đặc biệt khác:

- Hệ thống Gợi ý: Các nút Kính lúp/Bóng đèn hỗ trợ mở sẵn 1 ô chữ khi bí. Tính năng này gắn liền với (yêu cầu người chơi tiêu xu hoặc mua bằng tiền thật)
- Hệ thống Quảng cáo: Tùy chọn Bật/Tắt quảng cáo (Ads ON/OFF) và xem Video Ads để nhân đôi thưởng

# Các phần bổ xung thêm với góc nhìn cá nhân

- Game nhắm đến nhóm người chơi Casual thích các game rèn luyện tư duy nhẹ nhàng, giải trí giết thời gian và những người muốn trau dồi, kiểm tra vốn từ vựng/ngữ pháp tiếng Anh

+ Dưới góc độ người chơi:
- Người chơi dựa vào vốn từ vựng, ngữ pháp tiếng Anh (như dự đoán các từ ngắn quen thuộc: THE, YOU, ARE...) và dùng bàn phím ảo bên dưới để điền thử chữ cái vào ô số tương ứng

+ Dưới góc độ người làm game 
Vòng lặp cốt lõi (Core loop) rất gọn: Nhận Input -> So sánh dữ liệu (Check Logic) -> Cập nhật hiển thị (Update UI)

- Về mặt logic code, game lưu trữ dữ liệu các câu văn (có thể dùng file JSON), sau đó thuật toán sẽ bóc tách chuỗi string này ra, gán ngẫu nhiên mỗi ký tự với một số nguyên để tạo thành màn chơi
- Khi người chơi nhập Input từ bàn phím, hệ thống gọi hàm tìm kiếm và để lật mở toàn bộ các Key trùng khớp cùng lúc

+ Giữ chân người chơi
- Sun Streak: Đếm chuỗi ngày chơi liên tục để tạo thói quen mở app hằng ngày.
- Goals/Nhiệm vụ: Đặt ra mốc hoàn thành để tặng thưởng, kích thích người chơi cày cuốc
 
==> Tổng kết: Đây là một game có logic lập trình không quá phức tạp (rất phù hợp để làm bằng các engine 2D), nhưng làm rất tốt phần UI/UX và có hệ thống data từ vựng đồ sộ, kết hợp vòng lặp giữ chân người chơi cực kỳ hiệu quả và thú vị