# 📊 Hướng Dẫn Kết Nối Thiệp Mời Với Google Sheets (Google Trang Tính)

Hướng dẫn từng bước chi tiết giúp bạn tự động lưu toàn bộ thông tin xác nhận tham dự (RSVP) và lời chúc của khách mời trực tiếp vào một file Google Sheet trên Google Drive của bạn hoàn toàn **miễn phí, nhanh chóng và không giới hạn**.

---

## 🛠️ BƯỚC 1: Tạo Google Sheet mới
1. Mở trình duyệt và truy cập: [https://sheets.new](https://sheets.new) (hoặc vào Google Drive tạo một Google Trang tính mới).
2. Đặt tên file là: **Lời Chúc Tốt Nghiệp - Hồ Tiểu Điệp** (hoặc tên của bạn).
3. Tại dòng đầu tiên (Hàng 1), tạo các cột tiêu đề như sau:
   - **Cột A**: `Thời gian gửi`
   - **Cột B**: `Tên khách mời`
   - **Cột C**: `Mối quan hệ`
   - **Cột D**: `Xác nhận tham dự`
   - **Cột E**: `Lời chúc tốt nghiệp`

*(Mẹo: Bạn có thể tô đậm hàng tiêu đề và đổ màu nền xanh matcha nhẹ để trang tính đẹp mắt).*

---

## 💻 BƯỚC 2: Thêm Google Apps Script
1. Trên thanh menu của Google Sheet, bấm vào: **Tiện ích mở rộng (Extensions)** ➔ **Apps Script**.
2. Một tab mới mở ra, xóa toàn bộ mã có sẵn trong file `Mã.gs` (hoặc `Code.gs`) và dán toàn bộ đoạn code sau vào:

```javascript
/**
 * Script nhận dữ liệu RSVP & Lời chúc tốt nghiệp từ Landing Page
 * và tự động ghi vào Google Sheets
 */
function doPost(e) {
  var lock = LockService.getScriptLock();
  lock.tryLock(10000); // Tránh xung đột khi nhiều người gửi cùng lúc

  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = {};

    // Hỗ trợ cả dữ liệu gửi dạng JSON và Form Data
    if (e.postData && e.postData.contents) {
      try {
        data = JSON.parse(e.postData.contents);
      } catch (err) {
        data = e.parameter;
      }
    } else {
      data = e.parameter || {};
    }

    var timestamp = data.timestamp || new Date().toLocaleString("vi-VN", { timeZone: "Asia/Ho_Chi_Minh" });
    var name = data.name || "Khách mời";
    var relation = data.relation || "Bạn bè";
    var attendance = data.attendance || "Chắc chắn tham gia 💐";
    var message = data.message || "";

    // Thêm một dòng mới vào Google Sheet
    sheet.appendRow([
      timestamp,
      name,
      relation,
      attendance,
      message
    ]);

    return ContentService.createTextOutput(JSON.stringify({
      result: "success",
      message: "Đã lưu lời chúc thành công!"
    })).setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({
      result: "error",
      error: error.toString()
    })).setMimeType(ContentService.MimeType.JSON);

  } finally {
    lock.releaseLock();
  }
}

// Hàm đọc toàn bộ danh sách lời chúc từ Google Sheet để hiển thị lên Landing Page
function doGet(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var rows = sheet.getDataRange().getValues();
    var wishes = [];

    // Bỏ qua hàng 0 (tiêu đề cột), đọc từ hàng 1
    for (var i = 1; i < rows.length; i++) {
      var row = rows[i];
      // Nếu cột Tên (cột 1) có nội dung
      if (row[1] && row[1].toString().trim() !== "") {
        wishes.push({
          timestamp: row[0] ? row[0].toString() : "",
          name: row[1] ? row[1].toString() : "Khách mời",
          relation: row[2] ? row[2].toString() : "Bạn bè",
          attendance: row[3] ? row[3].toString() : "Chắc chắn tham gia 💐",
          message: row[4] ? row[4].toString() : ""
        });
      }
    }

    // Đảo ngược để lời chúc mới nhất hiển thị trên cùng
    wishes.reverse();

    return ContentService.createTextOutput(JSON.stringify({
      result: "success",
      data: wishes
    })).setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({
      result: "error",
      error: error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

3. Bấm biểu tượng **Lưu (Save / Biểu tượng đĩa mềm 💾)** hoặc ấn phím `Ctrl + S`.

---

## 🚀 BƯỚC 3: Triển khai thành Web App (Deploy)

> 🔔 **LƯU Ý QUAN TRỌNG KHI CẬP NHẬT CODE:**
> Nếu bạn đã từng Triển khai trước đó, hãy làm theo cách sau để link Web App nhận code mới:
> - Bấm **Triển khai (Deploy)** ➔ **Quản lý bản triển khai (Manage deployments)**.
> - Bấm vào biểu tượng **Chỉnh sửa ✏️ (Edit)** ở góc trên bên phải.
> - Ở mục **Phiên bản (Version)**, chọn **Phiên bản mới (New version)**.
> - Bấm **Triển khai (Deploy)**. Như vậy link Web App giữ nguyên và tự động cập nhật!

**Nếu là lần đầu tiên Triển khai:**
1. Ở góc trên bên phải màn hình Apps Script, bấm vào nút màu xanh **Triển khai (Deploy)** ➔ Chọn **Tùy chọn triển khai mới (New deployment)**.
2. Bấm vào biểu tượng **bánh răng ⚙️** bên cạnh "Chọn loại" ➔ Chọn **Ứng dụng web (Web app)**.
3. Cấu hình các mục như sau:
   - **Mô tả (Description)**: `Nhan va doc loi chuc tot nghiep`
   - **Thực thi dưới dạng (Execute as)**: **Tôi (Me - your email)** *(để script có quyền đọc/ghi vào sheet của bạn)*.
   - **Ai có quyền truy cập (Who has access)**: **Bất kỳ ai (Anyone)** *(RẤT QUAN TRỌNG: Phải chọn mục này để khách vào web có thể xem và gửi lời chúc mà không cần đăng nhập Google)*.
4. Bấm **Triển khai (Deploy)**.
5. Nếu Google hiển thị cửa sổ **Ủy quyền truy cập (Authorize Access)**:
   - Bấm **Ủy quyền truy cập (Authorize Access)** và chọn tài khoản Google của bạn.
   - Bấm **Nâng cao (Advanced)** ở góc dưới bên trái ➔ Bấm **Đi tới [Tên dự án] (không an toàn) / Go to ... (unsafe)**.
   - Bấm **Cho phép (Allow)**.
6. Sau khi triển khai xong, bạn sẽ nhận được một đường link **URL ứng dụng web (Web App URL)**, có dạng:
   ```text
   https://script.google.com/macros/s/AKfycby..._chuoi_ky_tu_dai.../exec
   ```
7. Hãy **Sao chép (Copy)** đường link này!

---

## 🔗 BƯỚC 4: Dán link vào file `index.html`
1. Mở file `index.html` bằng trình soạn thảo (VS Code, Notepad, v.v.).
2. Tìm đến dòng có biến `GOOGLE_SHEET_URL` (khoảng dòng 1750 trong file):
   ```javascript
   // ============================================================
   // CẤU HÌNH GOOGLE SHEETS (Dán link Web App của bạn vào đây)
   // ============================================================
   const GOOGLE_SHEET_URL = "DÁN_LINK_WEB_APP_CỦA_BẠN_VÀO_ĐÂY";
   ```
3. Dán link vừa copy ở Bước 3 vào giữa hai dấu ngoặc kép `""`.
4. Lưu file lại (`Ctrl + S`).
5. **Hoàn tất!** Giờ đây mỗi khi bất kỳ ai gửi lời chúc hoặc xác nhận tham dự trên web, dữ liệu sẽ ngay lập tức xuất hiện trong Google Sheet của bạn trong vòng 1-2 giây! 🎉

---

## 💌 BƯỚC 5: Hướng Dẫn Tạo Link Thiệp Mời Cá Nhân Hóa Từng Khách Mời

Bạn không cần backend vẫn có thể gửi link riêng cho từng người bạn. Chỉ cần thêm tham số `?to=Tên_Bạn` vào sau đường link trang web!

### Cách tạo link:
- Link chung (không kèm tên, hiển thị mặc định *"Bạn thân mến"*):  
  `https://totnghiep-mu.vercel.app/`
- Link gửi cho bạn Hoàng Yến:  
  `https://totnghiep-mu.vercel.app/?to=Hoàng+Yến`
- Link gửi cho bạn Thảo Vy:  
  `https://totnghiep-mu.vercel.app/?to=Thảo+Vy`
- Link gửi cho Anh Nam:  
  `https://totnghiep-mu.vercel.app/?to=Anh+Nam`

*(Mẹo: Khoảng trắng giữa các chữ bạn có thể gõ dấu `+` hoặc `%20` hoặc gõ tiếng Việt có dấu bình thường trên Zalo/Messenger/Facebook, trình duyệt sẽ tự động nhận diện).*

### Dữ liệu ghi nhận lên Google Sheet:
- Khi bạn bè nhận được link cá nhân hóa và bấm gửi lời chúc, dù ở ô "Tên của bạn" họ có điền biệt danh (ví dụ *"Yến Cún"*, *"Vy Vy"*, hay bất kỳ tên gì), hệ thống sẽ **tự động đính kèm tên từ link** gửi lên Google Sheet:
  - **Cột B (Tên khách mời)**: `Yến Cún [Link: Hoàng Yến]`
  - **Cột C (Mối quan hệ)**: `Link mời: Hoàng Yến`
- Nhờ vậy bạn luôn biết chính xác 100% lời chúc này đến từ người bạn nào mà bạn đã gửi link!
