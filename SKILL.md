---
name: report-writer
description: >
  Chuyển đổi dữ liệu thô, tài liệu kỹ thuật, source code, hoặc báo cáo có sẵn thành báo cáo học thuật/chuyên nghiệp hoàn chỉnh theo định dạng Word (.docx).

  LUÔN kích hoạt kỹ năng này khi người dùng dùng bất kỳ cụm từ nào sau: "làm báo cáo", "viết báo cáo", "tạo báo cáo", "hoàn thiện báo cáo", "điền vào báo cáo", "chuyển thành báo cáo", "xuất báo cáo", "làm word", "tạo file word", "tạo docx".
  
  Cũng kích hoạt khi người dùng upload source code (.ino, .py, .c) hoặc file .docx mẫu kèm theo yêu cầu về báo cáo, dù không dùng từ "báo cáo" tường minh — ưu tiên suy luận ý định.

  Kỹ năng tạo ra báo cáo đầy đủ cấu trúc 12 phần, ngôn ngữ học thuật, chuẩn hội đồng chấm Việt Nam, sinh thẳng ra file .docx không hỏi lại giữa chừng.
---

# Report Writer Skill

## Mục Tiêu

Tổng hợp và chuyển đổi các nguồn dữ liệu thô thành báo cáo học thuật hoàn chỉnh (.docx), đúng chuẩn hội đồng chấm Việt Nam, sẵn sàng nộp giảng viên. Sinh file trực tiếp — không hỏi xác nhận outline giữa chừng.

---

## Bước 0 — Đọc Toàn Bộ Tài Liệu Nguồn Trước Khi Làm Bất Cứ Điều Gì

**Bắt buộc. Không bỏ qua.**

Trước khi viết một chữ nào, đọc kỹ TẤT CẢ tài liệu được cung cấp:

- **Source code** (.ino, .py, .c…): xác định kiến trúc task, pin mapping, thư viện, state machine, biến volatile dùng chung
- **File mẫu .docx**: ghi nhớ cấu trúc chương, văn phong, thuật ngữ đã dùng — ưu tiên giữ nguyên
- **README / tài liệu kỹ thuật**: trích xuất thông số phần cứng, hướng dẫn cài đặt
- **Ghi chú / outline thô**: mở rộng dựa trên ngữ cảnh kỹ thuật đã đọc

Nếu nhiều file source code → ưu tiên file tên `*Complete*`, `*Full*`, hoặc file nhiều dòng nhất.

---

## Bước 1 — Cấu Trúc Báo Cáo Mặc Định (12 Phần)

Nếu có file mẫu: giữ nguyên cấu trúc của mẫu.  
Nếu không có mẫu: áp dụng cấu trúc sau:

1. Trang bìa — Tên trường, Khoa, Tên đề tài, Nhóm thực hiện, GVHD, Năm
2. Nhận xét của giảng viên — để trống để thầy/cô điền
3. Mục lục — đánh số trang đầy đủ
4. Danh mục hình ảnh
5. Danh mục bảng biểu
6. Bảng chú thích thuật ngữ viết tắt
7. Lời mở đầu — lý do chọn đề tài, mục tiêu, phạm vi
8. Chương 1: Cơ sở lý thuyết
9. Chương 2: Phân tích & Thiết kế hệ thống
10. Chương 3: Thử nghiệm & Đánh giá
11. Kết luận & Hướng phát triển
12. Tài liệu tham khảo + Phụ lục

---

## Bước 2 — Quy Tắc Viết Nội Dung

### Phong Cách Bắt Buộc (áp dụng mọi báo cáo)

- **Ngôn ngữ học thuật** — câu đủ 3–5 câu/đoạn, không viết đoạn đơn dòng
- **Số liệu khách quan, thực tế** — ưu tiên thông số đo được, thông số kỹ thuật từ datasheet
- **Không chú thích dạng `[tiếng Anh (Tiếng Việt)]` quá nhiều** — chỉ giải thích lần đầu tiên, sau đó dùng viết tắt
- **Dùng dấu gạch ngang (—)** để nối mệnh đề thay vì dấu phẩy kép hoặc ngoặc đơn
- **Không cảm xúc, không khen ngợi chủ quan** — tránh "hệ thống rất hiệu quả", "kết quả tuyệt vời"
- **Không dùng "chúng tôi" quá nhiều** — ưu tiên câu bị động hoặc chủ thể là "hệ thống", "đề tài", "nhóm"
- **Thuật ngữ tiếng Anh**: lần đầu ghi đầy đủ + viết tắt trong ngoặc → sau đó dùng viết tắt
- Hình ảnh/sơ đồ: `Hình X.X – Tên hình` (căn giữa, in nghiêng, bên dưới hình)
- Bảng biểu: `Bảng X.X – Tên bảng` (căn giữa, in nghiêng, bên trên bảng)

### Từ Source Code Nhúng (Arduino / FreeRTOS)

- Mô tả kiến trúc task bằng văn xuôi: tên, chức năng, chu kỳ `vTaskDelay`, ưu tiên, tài nguyên dùng chung
- Giải thích state machine theo mô hình: Trạng thái → Sự kiện → Hành động → Trạng thái kế tiếp
- Trình bày bảng nối chân: Chân GPIO — Thiết bị — Chức năng
- Giải thích biến `volatile`: lý do cần dùng khi chia sẻ giữa các task trong FreeRTOS
- Nêu lý do chọn FreeRTOS: đảm bảo real-time, phân chia tác vụ độc lập, tránh blocking toàn bộ vòng lặp

### Hướng Dẫn Nội Dung Từng Chương

**Chương 1 — Cơ sở lý thuyết**

| Mục | Nội dung |
|-----|----------|
| 1.1 Tổng quan chủ đề chính | Định nghĩa, phân loại, thực trạng, ưu/nhược điểm |
| 1.2 Chủ đề liên quan | Hệ thống con, công nghệ bổ trợ |
| 1.3 Hệ điều hành / Framework | Kiến trúc, thành phần cốt lõi, cơ chế (Task, Scheduler, Queue, Semaphore) |
| 1.4 Phần cứng sử dụng | Tên đầy đủ, thông số kỹ thuật, nguyên lý, lý do chọn |

**Chương 2 — Phân tích & Thiết kế**

| Mục | Nội dung |
|-----|----------|
| 2.1 Yêu cầu hệ thống | Functional + Non-functional (real-time, độ tin cậy, nguồn điện) |
| 2.2 Sơ đồ khối | Hình khối tổng thể + giải thích luồng dữ liệu |
| 2.3 Thiết kế phần mềm | Bảng task (tên, chu kỳ, ưu tiên), cơ chế giao tiếp, lý do phân chia |
| 2.4 Thiết kế phần cứng | Bảng nối chân, lưu ý 3.3V vs 5V, sơ đồ mạch nếu có |
| 2.5 Lưu đồ thuật toán | Lưu đồ từng chức năng chính |

**Chương 3 — Thử nghiệm & Đánh giá**

| Mục | Nội dung |
|-----|----------|
| 3.1 Môi trường thử nghiệm | Phần cứng, Arduino IDE version, thư viện, điều kiện |
| 3.2 Kết quả từng chức năng | Bảng Test Case: Tên — Điều kiện — Kết quả mong đợi — Kết quả thực — Đánh giá |
| 3.3 Đánh giá tổng thể | Mức độ đáp ứng yêu cầu, ưu điểm, hạn chế |
| 3.4 Hướng phát triển | Cải tiến ngắn hạn + định hướng dài hạn |

---

## Bước 3 — Tạo File Word (.docx)

Dùng thư viện `docx` (npm). **Không dùng phương pháp khác.**

```bash
npm install -g docx
node generate_report.js
python3 /mnt/skills/public/docx/scripts/office/validate.py output.docx
```

### Thông Số Kỹ Thuật Bắt Buộc

| Thông số | Giá trị |
|----------|---------|
| Trang | A4 — `width: 11906, height: 16838` (DXA) |
| Lề trái | 30mm — `1701 DXA` |
| Lề phải | 20mm — `1134 DXA` |
| Lề trên/dưới | 25mm — `1417 DXA` |
| Font body | Times New Roman, 13pt (`size: 26`) |
| Tiêu đề Chương | 16pt, bold, allCaps (`size: 32`) |
| Tiêu đề Mục 1.1 | 14pt, bold (`size: 28`) |
| Tiêu đề Tiểu mục 1.1.1 | 13pt, bold (`size: 26`) |
| Giãn dòng | 1.5 (`line: 360`) |
| Số trang | Footer, căn giữa |
| Header | Tên báo cáo rút gọn, căn phải, 10pt |

### Quy Tắc Kỹ Thuật docx-js (KHÔNG vi phạm)

- Heading dùng `HeadingLevel.HEADING_1/2/3` + `outlineLevel` — bắt buộc để TOC hoạt động
- Danh sách dùng `LevelFormat.BULLET` với `numbering config` — **KHÔNG dùng ký tự unicode thủ công**
- Bảng: đặt `columnWidths` trên `Table` VÀ `width` trên từng `TableCell` — phải khớp nhau
- Shading: dùng `ShadingType.CLEAR` — **KHÔNG dùng SOLID** (gây nền đen)
- Không dùng `\n` trong `TextRun` — dùng `Paragraph` riêng biệt
- `PageBreak` phải nằm trong `Paragraph`
- Luôn dùng `WidthType.DXA` cho bảng — **KHÔNG dùng PERCENTAGE**

---

## Bước 4 — Kiểm Tra Chất Lượng

Trước khi giao file, kiểm tra toàn bộ checklist:

| # | Hạng mục | Tiêu chí |
|---|----------|----------|
| 1 | Cấu trúc | Đủ 12 phần, không bỏ mục nào |
| 2 | Nội dung | Mỗi mục có dẫn nhập + thân bài + kết mục |
| 3 | Chuyển đổi code | Task/module mô tả bằng văn xuôi, không copy code nguyên xi |
| 4 | Phong cách | Học thuật, số liệu khách quan, dùng dấu gạch ngang, không cảm xúc |
| 5 | Định dạng | Font, lề, cỡ chữ, giãn dòng đúng thông số |
| 6 | Chú thích | Hình X.X / Bảng X.X đầy đủ |
| 7 | Tài liệu tham khảo | Đủ nguồn, đúng định dạng IEEE hoặc APA |
| 8 | Phụ lục | Bảng nối chân, thông số kỹ thuật, link mã nguồn |
| 9 | File output | Tại `/mnt/user-data/outputs/`, tên không dấu, đã validate |

---

## Bước 5 — Giao File

1. Validate: `python3 /mnt/skills/public/docx/scripts/office/validate.py output.docx`
2. Copy sang `/mnt/user-data/outputs/[ten]_baocao.docx`
3. Gọi `present_files` tool
4. Kèm tóm tắt ≤ 3 câu — **không liệt kê lại toàn bộ cấu trúc**

**Đặt tên file:** `[chu_de]_baocao.docx` — không dấu, không khoảng trắng, chữ thường.  
Ví dụ: `smarthome_freertos_baocao.docx`

---

## Xử Lý Tình Huống Đặc Biệt

| Tình huống | Cách xử lý |
|------------|------------|
| Thiếu dữ liệu cho một mục | Ghi `[Cần bổ sung: ...]` và tiếp tục — không dừng để hỏi |
| Nhiều file source code | Ưu tiên `*Complete*`, `*Full*`, hoặc file nhiều dòng nhất |
| File mẫu .docx có phần trống | Điền nội dung phù hợp, giữ nguyên cấu trúc gốc |
| Outline chỉ 1–2 dòng/mục | Mở rộng từ kiến thức kỹ thuật đã đọc trong source code |
| Source code dùng FreeRTOS nhưng thiếu lý thuyết | Tự động thêm mục FreeRTOS vào Chương 1 và mục thiết kế task vào Chương 2 |
| Yêu cầu thêm/bớt chương | Điều chỉnh và cập nhật mục lục tương ứng |
