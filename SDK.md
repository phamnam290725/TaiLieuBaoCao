# Báo Cáo Đúc Kết: Bức Tranh Toàn Cảnh Về SDK Android
**Qua phần thực hành và lỗi thực tế chiều nay, em đã hiểu ý anh: nhớ từng bước code là không cần thiết vì các SDK cập nhật liên tục. Quan trọng nhất là nắm được "bản đồ" các công cụ để biết khi nào cần lôi cái nào ra dùng, và kỹ năng cốt lõi là đọc Document trên trang chủ của chúng**

# Bản chất của SDK
- Android SDK là bộ công cụ nền tảng của Google bắt buộc phải có để build được app
- SDK bên thứ ba là các gói mã nguồn (thư viện) do các hãng khác làm sẵn, mình nhúng vào app để dùng dịch vụ của họ (như quảng cáo, phân tích) mà không phải tự code từ số 0

# Các nhóm SDK thiết yếu và Mục đích sử dụng
**Nhóm Đăng nhập**: Mục đích để nhận diện người chơi, lưu tiến trình game tránh mất dữ liệu
- Các lựa chọn tốt nhất hiện nay là Google Sign-In hoặc Firebase Authentication (nếu muốn gộp cả Facebook, Email)
 
**Nhóm Quảng cáo**: Mục đích để kiếm tiền qua việc hiển thị banner hoặc video nhận thưởng
- Lựa chọn phổ biến và dễ nhất cho dự án mới là Google AdMob. Nếu game lớn muốn tối ưu doanh thu có thể dùng AppLovin MAX hoặc Unity LevelPlay

**Nhóm Phân tích (Analytics)**: Mục đích để biết người chơi làm gì trong game (chơi đến màn nào thì bỏ). Firebase Analytics hoặc GameAnalytics là những lựa chọn hàng đầu và miễn phí

**Nhóm Báo lỗi** : Dùng để thu thập log lỗi khi app bị văng trên máy của người dùng thật 

===> Tóm lại: Một game chuẩn phát hành thường cài bộ combo: Firebase (Analytics + Crashlytics) + AdMob + Google Sign-In

# Tư duy khi lựa chọn SDK
- Khi có nhiều bên cung cấp cùng một dịch vụ, tiêu chí để chọn không chỉ là tính năng mà còn là:

**Document (Tài liệu)** của họ có rõ ràng không, cộng đồng dùng có đông không để dễ tìm lỗi trên mạng
- Có cùng chung một hệ sinh thái không (ví dụ dùng toàn bộ họ nhà Google/Firebase sẽ rất nhẹ và ít xung đột)
- Có vi phạm chính sách của Google Play không (ví dụ SDK thanh toán bắt buộc phải dùng Google Play Billing)

# Quy trình làm việc "Bản chất" khi cần nhúng SDK mới
- Khi được giao tích hợp một công cụ mới (ví dụ AdMob), em sẽ không lên mạng xin code mẫu bậy bạ mà sẽ làm theo luồng sau:

- Bước 1: Lên thẳng trang chủ của SDK đó, tìm phần Document cho Android để đọc hướng dẫn mới nhất
- Bước 2: Khai báo tải thư viện vào Gradle và xin các quyền cần thiết (như Internet) trong Manifest đúng theo Docs hướng dẫn
- Bước 3: Tuân thủ kỷ luật làm việc: Chỉ thêm một SDK vào code, sau đó Sync và Run ngay lập tức. Nếu app bị crash, mở Logcat tìm ngay dòng "Caused by" để tra lỗi chứ không thêm dồn dập 3-4 cái cùng lúc