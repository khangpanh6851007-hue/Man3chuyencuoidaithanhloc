# Chuyến Đò Chiều ULTRA 4.0 — Đò Chiều Chuyến Cuối

Phiên bản triển khai GitHub 2026, cập nhật thêm đồng hồ đếm ngược 13 năm.

## Nội dung nổi bật

- Giao diện ULTRA 4.0 tương thích máy tính và điện thoại.
- Khu vực **Đò Chiều Chuyến Cuối** với thông điệp Đại Thanh Lọc Tâm Thức và Chuyển Giao Màn 3.
- Đồng hồ đếm ngược hiển thị năm, ngày, giờ, phút và giây; tự cập nhật mỗi giây.
- Mốc thời gian được cấu hình trong HTML: **23/11/2039 23:59:59 (UTC+7)**.
- Trò chơi, nhiệm vụ, điểm thưởng, kho báu, hồ sơ và các phần demo có sẵn trong giao diện.
- PWA: manifest và service worker (cần kiểm tra cài đặt/HTTPS sau khi triển khai).

## Cấu trúc dự án

```text
.
├── public/
│   ├── index.html
│   ├── manifest.webmanifest
│   ├── icon.svg
│   └── sw.js
├── server/
│   └── server.js
├── .github/workflows/deploy.yml
├── package.json
├── .env.example
└── README.md
```

## Triển khai giao diện lên GitHub Pages

1. Tạo repository GitHub mới hoặc mở repository dự án.
2. Tải toàn bộ nội dung thư mục này lên repository.
3. Vào **Settings → Pages** và chọn **GitHub Actions** làm Build and deployment source.
4. Đảm bảo workflow `.github/workflows/deploy.yml` được commit.
5. Push lên nhánh `main` (hoặc chạy workflow thủ công trong tab Actions).
6. Mở URL GitHub Pages hiển thị trong phần Pages/Actions.

Workflow triển khai thư mục `public/` lên GitHub Pages. Nó chỉ triển khai giao diện tĩnh; GitHub Pages **không chạy** máy chủ Express/SQLite.

## Chạy backend API riêng (tùy chọn)

Yêu cầu Node.js 20 trở lên.

```bash
npm install
cp .env.example .env
npm start
```

Cấu hình các biến môi trường bí mật trong `.env` hoặc trong hosting backend. Không commit `.env`, JWT secret hay thông tin nhạy cảm lên GitHub.

> Backend API trong thư mục `server/` là starter riêng. Giao diện hiện tại vẫn chạy chế độ demo trên trình duyệt và chưa tự động kết nối API; muốn dùng tài khoản thật, dữ liệu đồng bộ và bảng xếp hạng toàn cầu cần triển khai backend, cấu hình bảo mật và tích hợp API.

## Tùy chỉnh thời hạn đếm ngược

Trong `public/index.html`, tìm dòng:

```js
const countdownTarget = new Date("2039-11-23T23:59:59+07:00").getTime();
```

Thay ngày/giờ theo định dạng ISO 8601 có múi giờ. Đồng hồ hiển thị thời gian còn lại đến mốc đã cấu hình; đây là bộ đếm thời gian của ứng dụng, không phải dự báo hay thông báo về một sự kiện có thật.

## Bảo toàn phiên bản

Gói này là bản phát hành mới có hậu tố `countdown13`. Không ghi đè các file ULTRA 4.0, bản Chuyến Cuối hoặc các bản cũ đã tạo trước đó.
