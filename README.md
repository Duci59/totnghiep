# 🎓 Thiệp Mời Tốt Nghiệp Online Tương Tác (Interactive Graduation Invitation)

Trang web thiệp mời tốt nghiệp trực tuyến tương tác cao, thiết kế theo phong cách **Dreamy Pastel (Hồng phấn - Xanh Matcha - Be kem - Điểm xuyết hoa Ly & Vàng Gold)**, tối ưu hiển thị chuẩn tỉ lệ mobile (430px căn giữa).

---

## ✨ Điểm Nổi Bật & Tính Năng

1. **Màn hình Hero & Phong Bì 3D Tương Tác**:
   - Phong bì matcha pastel với hiệu ứng lật nắp 3D (`rotateX(180deg)`).
   - Con dấu sáp hoàng gia (Gold Wax Seal) khắc biểu tượng cử nhân & hoa ly cùng hiệu ứng phát sáng dập dìu.
   - Khi chạm vào con dấu:
     - Nắp phong bì mở ra, thiệp chính trượt lên kiêu sa.
     - Bung pháo hoa kim tuyến nghệ thuật (`canvas-confetti`).
     - Tự động phát nhạc nền piano êm dịu (kèm nút Bật/Tắt nhạc và visualizer sóng âm ở góc màn hình).
     - Tự động dẫn hướng cuộn xuống các phần tiếp theo.

2. **Phần 1: Thông Tin Thiệp Mời (Vintage Stamp Invitation Letter)**:
   - Khung viền tem cổ điển dát vàng mộng mơ với hoa văn hoa ly tinh tế ở 4 góc.
   - Thư mời trang trọng gửi quý Thầy Cô, Gia đình và Bạn bè.
   - Nổi bật tên tân cử nhân **Hồ Tiểu Điệp** (UFM).
   - Vòng tròn hoa nguyệt quế xoay nhẹ bao quanh mốc thời gian: **Thứ Sáu, 13 Tháng 11, 2026 (13h30 - 15h30)**.
   - Bộ đếm ngược thời gian thực (Live Countdown) theo Ngày, Giờ, Phút, Giây.
   - Nút bấm **"Thêm vào Lịch nhắc nhở"** (Google Calendar / iCal).

3. **Phần 2: Địa Điểm & Bản Đồ Chỉ Đường (Location Guide)**:
   - Thông tin chi tiết: **Trường Đại học Tài Chính - Marketing (UFM)**, Hội trường Lớn A, số **306 Võ Văn Hát, Phường Long Trường, TP. Thủ Đức, TP.HCM**.
   - Nút sao chép địa chỉ nhanh kèm Toast thông báo.
   - Bản đồ Google Maps nhúng trực quan.
   - Nút mở Google Maps dẫn đường trực tiếp.
   - Hướng dẫn hữu ích cho khách: Chỗ gửi xe miễn phí, khung giờ chụp ảnh đẹp nhất, gợi ý trang phục (Dress code).

4. **Phần 3: Liên Hệ & Sổ Lưu Bút Lời Chúc (Contact & RSVP)**:
   - Thẻ Profile cá nhân với ảnh đại diện, số điện thoại, link Zalo, Facebook, Instagram.
   - Phím tắt gọi điện hoặc nhắn tin Zalo ngay tức thì.
   - Biểu mẫu RSVP tương tác: Khách nhập tên, mối quan hệ, chọn tình trạng tham dự và gửi lời chúc tốt nghiệp.
   - Lời chúc được lưu vào `localStorage` và hiển thị trực tiếp lên bảng sổ lưu bút!

5. **Phần 4: Nhật Ký Kỷ Yếu (Photo Diary & Lightbox Gallery)**:
   - Bố cục lưới ảnh kỷ yếu Polaroid nghệ thuật.
   - Chạm vào bất kỳ ảnh nào để xem phóng to (Lightbox Modal) sắc nét, có nút chuyển ảnh và đóng tiện lợi.
   - Lời cảm ơn chân thành ("With Love & Gratitude - Thank You") kết thúc trang web.

6. **Hiệu ứng & Âm thanh**:
   - Hiệu ứng Sparkle / Bụi sao vàng và cánh hoa ly rơi bay bổng ở background bằng HTML5 Canvas.
   - Hệ thống âm thanh thông minh: Hỗ trợ nhạc nền MP3 chất lượng cao, đồng thời tích hợp **Web Audio API Synthesizer** dự phòng để đảm bảo nhạc luôn phát nhẹ nhàng ngay cả khi ngoại tuyến hoặc mạng yếu.

---

## 🚀 Hướng Dẫn Sử Dụng & Mở Trang Web

- **Cách 1 (Mở trực tiếp)**: Bạn chỉ cần nhấp đúp chuột vào file `index.html` để mở ngay trên trình duyệt (Chrome, Safari, Edge, Cốc Cốc, v.v.).
- **Cách 2 (Mở qua Local Server)**: Chạy lệnh `npx serve .` hoặc Live Server trong IDE.
- **Cách 3 (Đăng online miễn phí)**: Kéo thả file `index.html` lên [Vercel](https://vercel.com), [Netlify Drop](https://app.netlify.com/drop) hoặc GitHub Pages để gửi link mời bạn bè qua Zalo, Messenger, SMS!

---

## 🛠️ Hướng Dẫn Chỉnh Sửa Thông Tin

Tất cả mã nguồn được tối ưu trong một file duy nhất [`index.html`](file:///c:/Users/Ducii/OneDrive/Documents/totnghiep/index.html):
- **Đổi tên chủ nhân buổi lễ**: Tìm `Hồ Tiểu Điệp` và thay bằng tên của bạn.
- **Đổi thời gian & ngày tổ chức**: Tìm chuỗi thời gian `2026-11-13T13:30:00+07:00` ở phần script để đổi ngày đếm ngược, và sửa các dòng chữ hiển thị ngày trong HTML.
- **Đổi địa điểm**: Tìm kiếm `306 Võ Văn Hát` hoặc `UFM` để cập nhật địa chỉ trường/hội trường của bạn.
- **Đổi số điện thoại & mạng xã hội**: Tìm `0987654321` và các đường link `facebook.com`, `zalo.me` để gắn link cá nhân.
- **Thay ảnh kỷ yếu**: Thay các đường link ảnh `https://images.unsplash.com/...` trong thẻ `<img>` và mảng `galleryData` bằng đường dẫn ảnh chụp kỷ yếu thật của bạn.
