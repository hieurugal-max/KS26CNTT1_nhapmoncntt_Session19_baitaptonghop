# (Bài tập tổng hợp) Rà Soát An Toàn Thông Tin Trước Khi Bàn Giao Dự Án SmartCampus

## Phần 1 – Nhận diện rủi ro và xử lý sự cố

1. Tình huống 1:
   
+Loại tấn công: Typosquatting kết hợp Phishing

+Dấu hiệu giả mạo: Đường link https://githuh-security.com/verify sử dụng tên miền githuh-security.com, cố tình viết sai tên GitHub thành githuh

## 2. Tình huống 2
Đây là cạm bẫy Mã độc Crack (Malware).

Yêu cầu tắt Windows Defender rất nguy hiểm vì phần mềm bảo vệ sẽ không
còn khả năng phát hiện và ngăn chặn mã độc. File crack có thể chứa virus
hoặc Trojan để đánh cắp dữ liệu và mật khẩu.

Cách xử lý: Không tải, không giải nén và không chạy phần mềm crack.
## 3. Áp dụng Quy tắc 5 KHÔNG
- Tình huống 1: Không nhấn vào đường link lạ, không cung cấp mật khẩu
  cho email không rõ nguồn gốc.
- Tình huống 2: Không tải phần mềm crack, không tắt Windows Defender
  theo hướng dẫn của trang web lạ.
## 4. Quy trình Cấp cứu 4 Bước
Nếu đã lỡ chạy file crack, cần thực hiện:
- Bước 1: Ngắt kết nối Internet ngay để hạn chế mã độc gửi dữ liệu
  ra ngoài.
- Bước 2: Cô lập máy tính, không đăng nhập tài khoản quan trọng
  hoặc cắm USB vào máy.
- Bước 3: Quét toàn bộ máy bằng Windows Defender hoặc công cụ bảo
  mật đáng tin cậy để phát hiện và xử lý mã độc.
- Bước 4: Dùng thiết bị sạch để đổi mật khẩu các tài khoản quan
  trọng, đăng xuất phiên lạ và bật 2FA.
# PHẦN 2 -- CHUYỂN SANG PASSWORD MANAGER
## 1. Rủi ro khi dùng chung mật khẩu
Nếu email nhóm bị lộ mật khẩu, hacker có thể dùng mật khẩu đó để đăng
nhập vào GitHub và Vercel.

Đây là kiểu tấn công Credential Stuffing. Khi một mật khẩu được dùng
cho nhiều tài khoản, chỉ cần một tài khoản bị lộ thì các tài khoản còn
lại cũng có nguy cơ bị chiếm quyền.

Giải pháp là sử dụng mật khẩu riêng cho từng tài khoản và lưu bằng
Password Manager.
## 2. Zero-Knowledge Architecture
Zero-Knowledge Architecture giúp bảo vệ dữ liệu bằng cách mã hóa ngay
trên thiết bị người dùng trước khi gửi lên máy chủ Bitwarden. Máy chủ
chỉ lưu dữ liệu đã mã hóa nên không thể đọc được mật khẩu thật.

Vì vậy, nếu máy chủ bị hacker xâm nhập, dữ liệu vẫn được bảo vệ nếu
hacker không có khóa giải mã.
## 3. Cấu hình Generator
Sử dụng Bitwarden Password Generator với cấu hình:

  Thông số            Giá trị
  Độ dài              20 ký tự
Chữ hoa (A--Z)      Có
Chữ thường (a--z)   Có
Chữ số (0--9)       Có
Ký tự đặc biệt      Có

Tạo 3 mật khẩu khác nhau cho:
- GitHub.
- Vercel.
- Email nhóm.
Không sử dụng lại mật khẩu cũ hoặc dùng chung mật khẩu giữa các tài
khoản.
# PHẦN 3 -- KÍCH HOẠT 2FA CHO TÀI KHOẢN GITHUB
## 1. Vì sao nên dùng Authenticator App thay SMS OTP?
Nên dùng Google Authenticator vì ứng dụng tạo mã xác thực trực tiếp trên
điện thoại, không phụ thuộc vào tin nhắn SMS.

Hai nhược điểm của SMS OTP:
- SIM Swapping: Hacker có thể chiếm quyền sử dụng SIM để nhận mã
  OTP.
- Đánh chặn SMS: Tin nhắn chứa mã OTP có thể bị đánh cắp trong quá
  trình truyền nhận.
2. Các bước bật 2FA bằng Google Authenticator
1. Đăng nhập tài khoản GitHub.
2. Nhấn ảnh đại diện, chọn Settings.
3. Chọn Password and authentication.
4. Tìm mục Two-factor authentication.
5. Chọn bật xác thực hai yếu tố bằng ứng dụng Authenticator.
6. Mở Google Authenticator trên điện thoại.
7. Nhấn dấu cộng (+), chọn quét mã QR trên GitHub.
8. Google Authenticator sẽ tạo mã xác thực 6 số.
9. Nhập mã 6 số vào GitHub để hoàn tất kích hoạt.
3. Nơi lưu 10 mã khôi phục
- Nên lưu trong Bitwarden hoặc in ra giấy và cất ở nơi an toàn.
- Không lưu công khai trên GitHub, không gửi qua Zalo, Messenger hoặc
  email nhóm.
- Không lưu chung trong file mã nguồn của dự án.
# PHẦN 4 -- BẢO VỆ SECRETS TRƯỚC KHI PUSH CODE
## 1. Hai giá trị Secrets bị hardcode
Trong file config.js có 2 thông tin nhạy cảm:
- sk-proj-abc123456789: API Key.
- SmartCampus@2026: Database Password.
Nếu đẩy lên GitHub công khai, người khác có thể lấy những thông tin này
để truy cập trái phép.
## 2. Code sau khi sửa
File config.js:
const API_KEY = process.env.OPENAI_API_KEY;
const DB_PASSWORD = process.env.DB_PASSWORD;

function connectDatabase() {
  return connect(DB_PASSWORD);
}
## 3. Nội dung 3 file cần tạo
File .env -- Chứa Secret thật, chỉ lưu trên máy cá nhân.
OPENAI_API_KEY=NHAP_API_KEY_THAT
DB_PASSWORD=NHAP_MAT_KHAU_THAT
File .gitignore -- Ngăn Git đưa file chứa Secret lên GitHub.
.env
.env.*
!.env.example
node_modules/
*.log
File .env.example -- Chỉ chứa tên biến để các thành viên biết cần khai
báo thông tin gì.
OPENAI_API_KEY=
DB_PASSWORD=
## 4. Quy tắc 4 Bước Kiểm tra trước khi Push
- Bước 1: Kiểm tra code: Tìm API Key, mật khẩu và token bị viết
  trực tiếp trong mã nguồn. Đảm bảo đã chuyển sang process.env.
- Bước 2: Kiểm tra .gitignore: Đảm bảo file .env đã được thêm
  vào danh sách bỏ qua.
- Bước 3: Kiểm tra file chuẩn bị đẩy lên Git: Dùng git status để
  chắc chắn không có file .env hoặc dữ liệu bí mật trong danh sách
  commit.
- Bước 4: Kiểm tra lần cuối: Quét Secret trong mã nguồn và lịch sử
  Git. Nếu Secret đã từng bị đẩy lên GitHub thì phải thu hồi và tạo
  Secret mới trước khi push.
Sau khi kiểm tra xong, thực hiện:
git add .
git commit -m "security: remove hardcoded secrets"
git push origin main
