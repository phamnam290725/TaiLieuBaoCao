# BÁO CÁO: BẢN CHẤT ANDROID & QUY TRÌNH BUILD GAME TRÊN GODOT
 
### . Bản chất các thành phần & Cách dùng 
-------------------------------------------------------------
#### 1. Android Version 

* **Là gì:** Là tên hệ điều hành mà người dùng hay gọi (Android 14, 15, 16...)
* **Hiện tại mới nhất:** Là **Android 17** 
-------------------------------------------------------------
#### 2. API Level (Con số trong máy)

* **Là gì:** Máy móc không đọc chữ "Android 17", mà gán cho mỗi đời Android một con số nguyên:
  * Android 17 = **API 37**  
  * Android 16 = **API 36**
  * Android 15 = **API 35**
-------------------------------------------------------------
* **Dùng thế nào trong Godot:**
  * **`minSdkVersion` (Đời máy cũ nhất có thể chơi được) -> Điền `24`:**
    * *Hiểu đơn giản:* Giống như quy định chiều cao vào cổng khu vui chơi. Đặt 24 (tức Android 7.0) nghĩa là chỉ điện thoại nào từ Android 7 trở lên mới cài được game. Máy quá cũ (Android 5, 6 từ ngày xưa) sẽ không cài được. Đặt số 24 là chuẩn nhất vì hầu như ai bây giờ cũng dùng máy đời mới rồi

  * **`targetSdkVersion` (Luật bắt buộc của Google Play) -> Điền `36` (hoặc `37`):**
    * *Hiểu đơn giản:* Giống như đi thi phải làm đúng theo đề thi năm nay. Google Play ra quy định: game nộp lên chợ bắt buộc phải theo chuẩn Android 16 (API 36). Nếu bạn điền số nhỏ hơn (như 34 hay 35 cũ), Google sẽ **từ chối ngay và không cho đăng game**
-------------------------------------------------------------
#### 3. Android SDK & JDK 17 (đóng gói)

* **Cần cái này là vì** Game Godot viết xong chỉ là các file code và hình ảnh. Muốn biến nó thành một ứng dụng chạy được trên điện thoại, Godot phải mượn "bộ đồ nghề" của Google để đóng gói lại

* **Cần có trong máy:**
  * **JDK 17:** Là phần mềm Java 17 (dùng bản Adoptium). Không có nó thì máy tính không chạy được trình đóng gói
  * **Android SDK:** Thư mục chứa đồ nghề của Google, gồm:
    * `platform-tools`: Có công cụ `adb` để cắm dây cáp đẩy game vào điện thoại và xem báo lỗi
    * `build-tools`: Công cụ nén ảnh, nén code thành file cài đặt
    * `platforms/android-36`: Bản mẫu để kiểm tra xem code có bị sai luật của Android không
-------------------------------------------------------------
#### 4. Quy trình build Godot: Dùng cái gì trong trường hợp nào?

* **Nên xuất file APK hay AAB**
  * File **`.apk`**: Dùng để cài thử vào máy mình, gửi qua Zalo/Drive cho bạn bè, đồng nghiệp chơi thử
  * File **`.aab`**: Bắt buộc phải dùng khi nộp game lên cửa hàng Google Play

* **Keystore (Chữ ký xác nhận chủ sở hữu):**
  * **Debug Keystore:** Khóa tạm có sẵn trong máy tính, dùng khi thử nghiệm hàng ngày
  * **Release Keystore:** Khóa thật do mình tự tạo (bằng 1 dòng lệnh), **phải cất giữ cẩn thận**. Mất khóa này là sau này không bao giờ cập nhật được game trên Google Play nữa

======> Nếu game có gắn **quảng cáo AdMob hoặc đăng nhập Google**, hãy dùng Release Keystore ngay từ đầu để không bị lỗi đăng nhập và quảng cáo khi phát hành

* **Chế độ build trong Godot:**
  * **Xuất mặc định (Standard Export):** Dùng khi chỉ muốn test game nhanh (bấm cái là vài giây có file cài ngay)
  * **Bật "Use Gradle Build":** Bắt buộc bật khi muốn xuất file `.aab` nộp Store hoặc khi game có gắn thêm tính năng ngoài (quảng cáo, nạp tiền)

-------------------------------------------------------------
### 3. Bảng chọn nhanh: Cần làm gì thì chọn cái đó

1. **Cài thử máy mình / gửi bạn bè test** | File `.apk` + Debug Keystore | Export Project -> Chọn `.apk` -> Tick ô *Export With 
Debug*

2. **Nộp game lên Google Play** | File `.aab` + Release Keystore | Bật *Use Gradle Build* -> Chọn `.aab` -> Bỏ tick ô *Export With Debug*

3.  **Chọn đời máy chơi được** | Điền số `24` | Ô Min SDK trong mục Gradle Build

4.  **Để Google Play chịu duyệt game** | Điền số `36` (hoặc 37) | Ô Target SDK trong mục Gradle Build. 

5.  **Hỗ trợ hầu hết điện thoại hiện nay** | Tick chọn `arm64-v8a` | Mục Architectures (hầu hết máy bây giờ đều là 64-bit)

6.  **Game có gắn quảng cáo / đăng nhập** | Dùng Release Keystore | Điền file khóa vào mục Release của cửa sổ Export 

-------------------------------------------------------------

 

 
