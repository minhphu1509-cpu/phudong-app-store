# PhuDong Store

Thư viện ứng dụng và công cụ số dạng website tĩnh. Giao diện nằm trong `index.html`; không cần cài thư viện hay chạy bước build.

## Chạy cục bộ

Mở `index.html` trong trình duyệt để xem giao diện. Đăng nhập quản trị yêu cầu các Vercel Functions trong `api/`; hãy chạy qua Vercel hoặc triển khai lên Vercel thay vì mở trang bằng `file://`.

## Đưa lên Git

1. Tạo repository Git mới hoặc kết nối thư mục này với repository hiện có.
2. Đưa các tệp trong thư mục dự án lên Git. Không đưa thư mục `.vercel`, tệp `.env` hoặc dữ liệu cá nhân vào repository.
3. Kết nối repository với Vercel để tự động triển khai mỗi lần cập nhật nhánh production.

## Cấu hình Vercel

- Framework preset: **Other**
- Root directory: thư mục gốc của repository
- Build command: để trống
- Output directory: `.`
- Install command: để trống

`vercel.json` thêm các HTTP security headers cơ bản. Vercel phục vụ trực tiếp `index.html` và tự triển khai hai hàm trong `api/` để xác thực phiên quản trị.

## Cấu hình đăng nhập quản trị bằng Google

1. Tạo OAuth 2.0 Client ID loại **Web application** trong Google Cloud Console. Thêm domain production vào **Authorized JavaScript origins**.
2. Trong Vercel Project → Settings → Environment Variables, đặt:
   - `GOOGLE_CLIENT_ID`: Client ID của ứng dụng OAuth.
   - `ADMIN_SESSION_SECRET`: chuỗi ngẫu nhiên riêng tư dài ít nhất 32 byte.
3. Áp dụng biến cho Production (và Preview nếu cần), sau đó redeploy. Không commit giá trị bí mật vào Git.

API phía máy chủ xác minh chữ ký ID token cùng audience, issuer, thời hạn, trạng thái email đã xác minh và địa chỉ được phép `phudongai@gmail.com`. Phiên quản trị được lưu trong cookie `HttpOnly`, `Secure`, `SameSite=Strict` có thời hạn một giờ.

## Quản trị nội dung

Mở **Quản trị** trên website để quản lý ứng dụng, danh mục, nội dung trang chủ và liên kết Telegram, Zalo, TikTok, YouTube, Facebook, GitHub. Dùng **Sao lưu** trước khi chuyển dữ liệu hoặc đổi trình duyệt; **Khôi phục** để nạp tệp JSON đã xuất.

Nội dung quản trị hiện được lưu cục bộ bằng IndexedDB trên trình duyệt. Dữ liệu không tự đồng bộ lên Vercel hoặc sang trình duyệt của khách truy cập. Muốn thay đổi xuất hiện đồng nhất với mọi người, hãy quản lý dữ liệu nguồn rồi triển khai lại hoặc bổ sung backend/CMS và xác thực quản trị. Không dùng giao diện quản trị phía trình duyệt làm cơ chế bảo vệ dữ liệu nhạy cảm.

## Lưu trữ và riêng tư

Website lưu danh sách ứng dụng, danh mục, liên kết mạng xã hội, nội dung trang và danh sách yêu thích trong IndexedDB của trình duyệt. Giới hạn ứng dụng đặt ở 500 MB; dung lượng thực tế do trình duyệt và thiết bị quyết định. Giao diện tải font chữ từ Google Fonts; các liên kết ứng dụng và mạng xã hội được mở đến các website bên ngoài.
