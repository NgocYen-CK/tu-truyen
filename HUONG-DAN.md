# Tủ truyện — hướng dẫn cài đặt

Tủ truyện là một trang web chạy hoàn toàn trên máy bạn. Không có máy chủ của ai khác giữ truyện, nên không ai có thể khoá hay xoá kho truyện của bạn. Truyện được lưu ở 3 nơi, và cả 3 đều do bạn giữ:

1. Bộ nhớ trình duyệt trên từng máy (đọc được khi không có mạng).
2. Vùng ẩn trong Google Drive của chính bạn (để đồng bộ máy tính ↔ điện thoại).
3. Tệp sao lưu `.json` bạn tự xuất ra và cất đi (USB, ổ cứng, email…).

Mọi thứ đều được **mã hoá bằng mã PIN/mật khẩu** của bạn. Ai có đường link cũng chỉ thấy màn hình khoá trống.

Trên máy của bạn có thể chọn **"Không khoá"** (mặc định khi tạo thư viện): máy đó mở thẳng vào tủ truyện, không hỏi mã. Đổi lại trong Cài đặt → Bảo mật. Máy mới, bản trên Google Drive và tệp sao lưu vẫn luôn cần mã khoá.

> Quan trọng: **quên mã khoá là mất dữ liệu**, vì không ai giải mã được, kể cả Google. Hãy ghi mã khoá ra chỗ an toàn.

---

## Bước 1 — Đưa ứng dụng lên mạng (miễn phí, khoảng 10 phút)

Dùng GitHub Pages:

1. Tạo tài khoản tại https://github.com (nếu chưa có).
2. Bấm **New repository**. Đặt tên, ví dụ `tu-truyen`. Chọn **Public** (mã nguồn công khai, nhưng truyện thì không: truyện chỉ nằm trên máy bạn và trong Drive của bạn, đã mã hoá). Bấm **Create repository**.
3. Bấm **uploading an existing file**, kéo toàn bộ các tệp trong thư mục này vào (index.html, sw.js, config.js, manifest.webmanifest, icon-192.png, icon-512.png), rồi bấm **Commit changes**.
4. Vào **Settings → Pages**. Ở mục *Branch*, chọn `main` và thư mục `/ (root)`, rồi bấm **Save**.
5. Đợi 1–2 phút. Địa chỉ của bạn sẽ có dạng `https://ten-cua-ban.github.io/tu-truyen/`.

Mở địa chỉ đó trên máy tính, đặt mã PIN hoặc mật khẩu. Từ lúc này bạn đã dùng được ngay, chưa cần đồng bộ.

## Bước 2 — Bật đồng bộ Google (để điện thoại nhận truyện từ máy tính)

Bạn tạo một "Client ID" riêng trên Google. Chỉ cần làm một lần:

1. Vào https://console.cloud.google.com, đăng nhập bằng Gmail của bạn, rồi tạo **dự án mới** (ví dụ "Tu truyen").
2. **APIs & Services → Library**: tìm **Google Drive API** và bấm **Enable**.
3. **APIs & Services → OAuth consent screen** (hoặc *Google Auth Platform*):
   - User type: **External**. App name: Tủ truyện. Điền email của bạn ở các ô bắt buộc.
   - Mục **Test users / Audience**: thêm **đúng Gmail của bạn**. Ứng dụng để nguyên ở chế độ *Testing* thì **chỉ những email trong danh sách này đăng nhập được**, người khác bị Google chặn.
4. **Credentials → Create credentials → OAuth client ID**:
   - Application type: **Web application**.
   - **Authorized JavaScript origins**: thêm `https://ten-cua-ban.github.io` (chỉ phần tên miền, không có `/tu-truyen/` phía sau).
   - Bấm Create, rồi sao chép **Client ID** (dạng `xxxx.apps.googleusercontent.com`).
5. Trên GitHub, mở tệp `config.js` → bấm biểu tượng bút chì để sửa:
   ```js
   googleClientId: "dán-client-id-vào-đây",
   ownerEmail: "gmail-cua-ban@gmail.com"
   ```
   Bấm **Commit changes**. Đợi 1 phút.
6. Mở lại ứng dụng → **Cài đặt → Đồng bộ Google → Đăng nhập bằng Google**. Lần đầu Google sẽ báo "ứng dụng chưa được xác minh": đây là ứng dụng của chính bạn, bấm **Tiếp tục**.

## Bước 3 — Cài lên điện thoại

1. Mở cùng địa chỉ bằng **Safari** (iPhone) hoặc **Chrome** (Android).
2. iPhone: nút Chia sẻ → **Thêm vào MH chính**. Android: menu ⋮ → **Cài đặt ứng dụng / Thêm vào màn hình chính**.
3. Mở biểu tượng Tủ truyện, đặt **đúng mã khoá giống trên máy tính**.
4. Cài đặt → Đăng nhập bằng Google. Truyện từ máy tính sẽ tải về và lưu sẵn trên điện thoại.

## Cách dùng hằng ngày

- **Trên máy tính**: thêm truyện (dán chữ hoặc chọn tệp Word .docx, chọn được nhiều tệp cùng lúc), sửa chương, thêm chương, xoá truyện.
- **Trên điện thoại**: mở ứng dụng, nhập mã khoá. Ứng dụng tự kéo bản mới về rồi lưu lại để đọc offline. Vị trí đang đọc chỉ lưu riêng trên từng máy, không gửi lên Google.
- Nút ở góc trên (ví dụ "Đã đồng bộ 14:32") cho biết trạng thái. Nếu thấy "Chạm để đồng bộ" thì bấm vào, vì phiên Google chỉ kéo dài khoảng 1 giờ.
- **Thùng rác**: truyện bị xoá nằm trong Cài đặt → Thùng rác cho tới khi bạn bấm "Xoá vĩnh viễn".
- **Thiết bị**: Cài đặt → Thiết bị đã đăng nhập, xem máy nào đang đồng bộ và đăng xuất máy bị mất.

## Lưu thẳng vào thư mục trên máy tính (Chrome hoặc Edge)

Cài đặt → **Thư mục trên máy tính** → **Chọn thư mục…** → chọn `D:\Claude Cowork\Tủ truyện` → cho phép.
Ứng dụng **không tự lưu**. Chỉ khi bạn bấm:

- **Xuất bản sao lưu**: mỗi lần bấm tạo một tệp riêng, tên có ngày giờ, trong thư mục con `Sao lưu` (đã mã hoá, mở bằng mã khoá).
- **Xuất ra Word / Tải về Word**: mỗi truyện một tệp .docx trong thư mục con `Word`, bản đã sửa ghi đè bản cũ cùng tên.

Lần đầu bấm sau khi mở lại trình duyệt, Chrome có thể hỏi quyền ghi vào thư mục: bấm **Cho phép**.

## Sao lưu — nên làm mỗi 1–2 tuần

Cài đặt → **Xuất bản sao lưu**. Bạn được một tệp `tu-truyen-sao-luu-NGAY-GIO.json`, đã mã hoá bằng mã khoá hiện tại (nếu đã chọn thư mục thì tệp nằm trong thư mục con `Sao lưu`). Cất tệp này ở nhiều nơi.
Khôi phục: Cài đặt → **Khôi phục từ tệp…**, nhập mã khoá lúc xuất, rồi chọn *Gộp* hoặc *Thay thế toàn bộ*.

Tệp sao lưu dùng được độc lập: kể cả khi GitHub hay Google không còn, bạn chỉ cần đưa bộ tệp này lên một trang web khác (Netlify, Cloudflare Pages…), mở ra và khôi phục.

## Xuất ra Word

- Một truyện: mở truyện → **Tải về Word**.
- Nhiều truyện: Cài đặt → Xuất ra Word → **Xuất truyện mới và đã sửa**. Nút này chỉ xuất truyện chưa xuất lần nào hoặc đã sửa sau lần xuất trước, gom trong một tệp .zip. Giải nén vào cùng thư mục cũ và chọn *Replace / Ghi đè*, bản đã sửa sẽ thay bản cũ vì tên tệp giữ nguyên theo tên truyện.
- **Xuất lại tất cả**: xuất toàn bộ kho.
- Tệp Word **không mã hoá**. Nhập ngược lại vào Tủ truyện thì ứng dụng tự điền tên truyện, tác giả, tag và tách đúng chương.

## Xoá tạm và xoá vĩnh viễn

- **Xoá tạm**: mở truyện → Sửa thông tin → **Chuyển vào Thùng rác**. Truyện còn nguyên chương và tiến độ.
- **Khôi phục hoặc xoá vĩnh viễn**: vào **Thùng rác** (đường dẫn ở cuối Tủ truyện, hoặc Cài đặt → Thùng rác). Xoá vĩnh viễn sẽ xoá trên mọi thiết bị đồng bộ và trên Google Drive.
- **Xoá một chương**: Sửa chương → Xoá chương. Việc này xoá luôn, không qua Thùng rác.

## Câu hỏi thường gặp

- **Người khác mở link của tôi thì sao?** Họ chỉ thấy màn hình tạo mã khoá với một tủ truyện trống trên máy của họ. Truyện của bạn không nằm trên trang web.
- **Đổi mã khoá?** Cài đặt → Bảo mật → Đổi mã khoá. Sau đó đổi giống hệt trên các máy còn lại để tiếp tục đồng bộ.
- **Dung lượng?** Mỗi bộ truyện chữ thường chỉ vài MB. Google Drive miễn phí có 15 GB.
- **Tệp .doc cũ?** Mở bằng Word rồi *Lưu thành* `.docx`.
