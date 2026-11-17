# DealNest - Trang voucher Shopee & TikTok Shop

Trang web tĩnh (HTML/CSS/JS thuần), không cần cài đặt, không cần build, không cần Supabase. Tải lên GitHub, bật Pages là chạy.

Mỗi nút **Get Voucher** mở đúng link bạn nhập, không đổi, không xoay vòng.

## Đưa web lên mạng (làm 1 lần, khoảng 3 phút)

1. Vào github.com, bấm **+ -> New repository**. Đặt tên (ví dụ `voucher`), chọn **Public**, bấm **Create repository**.
2. Giải nén file zip. Mở thư mục cho đến khi thấy `index.html`. Chọn tất cả file và thư mục bên trong (Ctrl+A), kéo thả vào trang GitHub (mục "uploading an existing file"), rồi bấm **Commit changes**.
3. Vào **Settings -> Pages**. Ở mục **Build and deployment**:
   - **Source**: chọn **Deploy from a branch**
   - **Branch**: chọn **main** và thư mục **/ (root)**, bấm **Save**
4. Chờ 1 đến 2 phút. Tải lại trang Pages, GitHub sẽ hiện link web của bạn:
   `https://TÊN-GITHUB.github.io/TÊN-KHO/`

## Thêm / sửa / xóa voucher

1. Trên GitHub mở file `vouchers.js`, bấm biểu tượng **cây bút (Edit)**.
2. Sửa nội dung giữa các cặp `{ }`. Mỗi voucher là một khối, kết thúc bằng dấu phẩy:

```js
{
  platform: "shopee",          // "shopee" hoặc "tiktok"
  title: "Tên voucher",
  discount: "Giảm 50K",
  minimum: "300K",             // đơn tối thiểu (tùy chọn)
  maximum: "100K",             // mức giảm tối đa (tùy chọn)
  expires: "auto",             // "auto" = luôn là ngày mai (tự cập nhật), hoặc "2026-12-31" (tùy chọn)
  used: 40,                    // % đã dùng THẬT, nếu bạn biết (tùy chọn)
  tag: "ShopeeVIP",            // nhãn nhỏ (tùy chọn)
  link: "https://link-cua-ban",
  featured: true,              // hiện ở mục "Voucher nổi bật" (tùy chọn)
},
```

3. Bấm **Commit changes**. Khoảng 1 phút sau web tự cập nhật (nhấn Ctrl+F5 để xem bản mới).

Nếu web trống hoặc báo lỗi đọc `vouchers.js`: thường do thiếu dấu phẩy, dấu ngoặc hoặc dấu nháy. Hãy kiểm tra lại khối vừa sửa.

## Voucher mẫu: nhãn "Mẫu" và thanh "Đã dùng" minh họa

Các voucher có sẵn đều có dòng `sample: true`. Chúng hiện nhãn **Mẫu** và thanh **Đã dùng (minh họa)**. Thanh này tự tăng dần theo thời gian trong khoảng 50% đến 99%, rồi quay về khoảng 50% khi chạm mốc cao nhất. Đây chỉ là hiệu ứng giao diện, không phải số liệu thật.

Khi bạn thay bằng voucher thật, hãy **xóa dòng `sample: true`**. Lúc đó thanh minh họa biến mất. Nếu bạn biết số lượng đã dùng thật, thêm dòng `used: 40` (nghĩa là 40%) thì thanh sẽ hiện đúng con số đó.

## Hạn dùng

- `expires: "auto"`: luôn hiện **ngày mai**, tự cập nhật theo ngày thật (các voucher nổi bật dùng cách này).
- `expires: "2026-12-31"`: ngày cố định. Qua ngày đó voucher hiện "Hết hạn".
- Không ghi dòng `expires`: không hiện hạn dùng (các voucher thường).

## Đổi hình Shopee / TikTok Shop

Mọi voucher của mỗi sàn dùng chung một hình trong thư mục `images/`. Hai hình hiện có là hình đơn giản tạo sẵn, không phải logo chính thức.

Muốn dùng hình của bạn: mở thư mục `images` trên GitHub, **Add file -> Upload files**, tải ảnh lên (khoảng 5:2, ví dụ 1000x400). Sau đó mở `vouchers.js`, đổi tên file ở phần `PLATFORM_IMAGES`.

Muốn một voucher có hình riêng: thêm dòng `image: "images/ten-anh.png",` vào khối voucher đó.

## Đổi tên web

Sửa dòng `SITE_NAME` ở đầu `vouchers.js`. Tiêu đề thẻ trình duyệt đổi theo.

## An toàn

Chỉ nhận link bắt đầu bằng `http://` hoặc `https://`. Link trống hoặc sai thì nút hiện "Chưa có link". Voucher đã quá ngày `expires` hiện "Hết hạn".
