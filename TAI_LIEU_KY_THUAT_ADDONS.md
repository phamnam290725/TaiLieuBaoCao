S# TÀI LIỆU KỸ THUẬT DỰ ÁN NEXTGZ-GODOT-ADDONS


# PHẦN 1: HIỂU RÕ CẤU TRÚC DỰ ÁN
* Dự án được chia tách thành 2 khu vực rõ ràng: Nơi viết code Native để build thư viện và Nơi chứa thư viện hoàn chỉnh để các game kéo về dùng

-----------------------------------
- Thư mục custom_plugin/ (Nơi viết code Java Android gốc)
- Nhiệm vụ: Chứa toàn bộ mã nguồn Java thuần và cấu hình Gradle
- Đây là nơi làm việc với SDK của Google và hệ điều hành Android để xuất ra file thư viện .aar
- Các thư mục con bên trong:
-----------------------------------
---------------
- custom_plugin/android_util/: Chứa code Java xử lý thông báo hẹn giờ, rung máy và bắt sự kiện mở app
- custom_plugin/google_sign_in/: Chứa code Java kết nối Google Play Services Auth để đăng nhập tài khoản
- custom_plugin/google_billing/: Chứa code Java kết nối Google Play Billing v7 để thanh toán in-app
- build.gradle.kts và settings.gradle.kts: File cấu hình để quản lý phiên bản SDK và chạy lệnh build tự động cho các module con
---------------
-----------------------------------
- Thư mục addons/ (Nơi chứa sản phẩm hoàn thiện để dùng cho Game)
- Nhiệm vụ: Chứa các gói thư viện đã build xong. Khi làm game mới, dev chỉ việc copy các thư mục này vào dự án game là chạy được ngay mà không cần quan tâm đến mã nguồn Java
- Các thư mục con bên trong:
- addons/android_util/: Chứa file GodotAndroidUtil-release.aar và file điều khiển AndroidUtil.gd
- addons/google_sign_in/: Chứa file GodotGoogleSignIn-release.aar và file điều khiển GoogleSignIn.gd
- addons/google_billing/: Chứa file GodotGoogleBilling-release.aar và file điều khiển GoogleBilling.gd
- addons/godot_firebase/: Chứa bộ thư viện kết nối cơ sở dữ liệu Firebase
- addons/admob/: Chứa bộ thư viện hiển thị quảng cáo Google AdMob
-----------------------------------
---------------
- File CLAUDE.md (Quy chuẩn kỹ thuật của dự án)
- Nhiệm vụ: Đặt ra các rào chắn kỹ thuật bắt buộc cho dev và AI khi làm việc: 
- Cấm đưa text hay logic riêng của game vào addon; cấm dùng quyền Android vi phạm chính sách; bắt buộc dùng hàng đợi để chống lỗi
- Thư mục docs/ (Tài liệu chi tiết)
- Nhiệm vụ: Lưu trữ các bản giải thích chi tiết về tham số và tính năng của từng plugin để dev tra cứu sâu khi cần
---------------


## PHẦN 2: HƯỚNG DẪN SỬ DỤNG CÁC ADDON

* Tất cả addon đều được cấu hình dùng chung toàn game (Autoload/Singleton) và có sẵn cơ chế chạy giả lập (Safe-Mock) để test giao diện không bao giờ bị văng game
- Addon AndroidUtil (Thông báo nội bộ & Rung máy)
- Nhiệm vụ: 
Bắn thông báo nhắc người chơi quay lại game theo các mốc ngày (retention) và rung máy khi bấm nút
- Cách vận hành: 
Addon không chứa nội dung chữ của game
- Phía game tự gửi danh sách gồm mốc thời gian và nội dung cần nhắc vào một hàm duy nhất để addon lên lịch; có sẵn hàng đợi giữ dữ liệu an toàn để người chơi bấm thông báo mở app không bị crash


* Addon Google Sign-In (Đăng nhập Google)
- Nhiệm vụ: 
Mở bảng chọn tài khoản Google trên điện thoại, lấy Google ID, Email và Token xác thực
- Cách vận hành: 
Gọi lệnh đăng nhập và lắng nghe sự kiện thành công để nhận dữ liệu tài khoản; khi chạy trên PC Editor tự động trả về tài khoản mẫu giả lập để dev test nhanh các tính năng sau đăng nhập


* Addon Google Billing (Mua gói xu / IAP)
- Nhiệm vụ: 
Kết nối Google Play Store để bán các gói nạp xu và vật phẩm trong game
- Cách vận hành: 
Khởi động kết nối, mở bảng thanh toán gốc của Google,
Và tự động tiêu thụ gói hàng để người chơi mua tiếp được lần sau; tích hợp sẵn hàm tự động quét nhặt lại các đơn hàng bị kẹt khi rớt mạng để cộng bù xu cho người chơi khi mở lại game


* Addon Godot Firebase (Đồng bộ đám mây)
- Nhiệm vụ: 
Lưu trữ số xu, cấp độ màn chơi và tiến trình game lên cơ sở dữ liệu thời gian thực (Realtime Database)
- Cách vận hành: 
Dùng mã Google ID làm chìa khóa định danh; mọi thay đổi điểm số trong game được đồng bộ lên mạng, giúp người chơi không bị mất dữ liệu khi đổi điện thoại


* Addon AdMob (Quảng cáo)
- Nhiệm vụ: 
Hiển thị quảng cáo biểu ngữ (Banner), quảng cáo toàn màn hình khi qua màn (Interstitial) và video tặng thưởng (Rewarded Video)
- Cách vận hành: 
Gọi hiển thị và lắng nghe sự kiện người chơi xem hết video quảng cáo để tự động phát quà hoặc cộng lượt chơi




# PHẦN 3: HƯỚNG DẪN 4 BƯỚC TÍCH HỢP THÊM ADDON MỚI
- Khi cần làm thêm bất kỳ plugin Android Native nào mới (như Facebook, TikTok, AppsFlyer), thực hiện tuần tự 4 bước sau:

-----------------------------
* Bước 1: Viết mã nguồn Java Native trong custom_plugin
- Tạo thư mục mới cho plugin trong custom_plugin/ và khai báo vào file settings.gradle.kts.
- Viết class Java kế thừa GodotPlugin, dùng annotation @UsedByGodot cho các hàm muốn game gọi được.
- Bắt buộc gom các sự kiện trả về qua một hàng đợi an toàn ở tầng Java để chống lỗi xung đột luồng và lỗi văng app lúc khởi động
-----------------------------

-----------------------------
* Bước 2: Build file thư viện AAR bằng Gradle
- Chạy một dòng lệnh Gradle để biên dịch toàn bộ code Java vừa viết thành 1 file thư viện .aar duy nhất ở chế độ Release.
- Chuyển file .aar thành phẩm sang thư mục bin của addon tương ứng bên thư mục addons/
-----------------------------

-----------------------------
* Bước 3: Viết script cầu nối GDScript với cơ chế Safe-Mock
- Viết một file GDScript làm đại diện giao tiếp giữa game và file AAR.
- Cài đặt kiểm tra môi trường: Nếu chạy trên PC thì tự sinh dữ liệu mẫu giả lập để dev test giao diện trên máy tính mà không bị lỗi crash; nếu chạy trên Android thì mới gọi thư viện Native thật
- Chuyển đổi các sự kiện từ Java thành tín hiệu Signal chuẩn của Godot để các màn chơi dễ kết nối
-----------------------------

-----------------------------
* Bước 4: Đóng gói cấu hình và kích hoạt trong Game
- Tạo file plugin.cfg để Godot nhận diện plugin và file export_plugin.gd để engine tự động kẹp file AAR vào bộ cài APK khi xuất
- Sang dự án Game: Bật plugin trong Cài đặt dự án và thêm file script cầu nối vào mục nạp tự động (Autoload) là có thể gọi dùng ở bất kỳ đâu trong toàn bộ game
-----------------------------