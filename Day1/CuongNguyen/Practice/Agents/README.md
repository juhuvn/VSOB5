# Bộ file định nghĩa AI Agent — VSOB5

Thư mục này chứa sẵn toàn bộ file `AGENTS.md`, định nghĩa agent và `PROJECT.md`
dùng trong hai tình huống thực hành của khóa VSOB5. Học viên **chép về là dùng
được ngay**, không phải gõ lại bằng tay.

Nội dung các file giống hệt phần in trong tài liệu
[Hands-on.md](../Hands-on.md), mục 2.3.3 và 3.2.

---

## 1. Ba loại file, ba nhiệm vụ khác nhau

Điều quan trọng nhất cần hiểu trước khi dùng: không gian làm việc được tách
thành ba lớp, mỗi lớp trả lời một câu hỏi riêng.

| File | Trả lời câu hỏi | Khi nào sửa |
| -- | -- | -- |
| `AGENTS.md` | Không gian làm việc tổ chức thế nào? Quy tắc chung mọi agent phải tuân theo là gì? | Viết một lần, dùng cho cả khóa học |
| `agents/<TênAgent>.md` | Agent này là ai, giỏi gì, làm việc theo cách nào? | Viết một lần, dùng lại cho nhiều dự án |
| `<dự án>/PROJECT.md` | Dự án này làm gì, dữ liệu ở đâu, ai tham gia, kết quả lưu đâu? | Mỗi dự án một file |

Nhờ tách như vậy, `BioinformaticianAgent` viết ở Tình huống 1 được **dùng lại
nguyên vẹn** ở Tình huống 2 — chỉ cần viết thêm một file `PROJECT.md` mới.

---

## 2. Cấu trúc thư mục

```text
Agents/
├── AGENTS.md                       # hướng dẫn chung cho mọi agent
├── agents/
│   ├── BioinformaticianAgent.md    # dùng ở cả Tình huống 1 và 2
│   ├── IdeaAgent.md                # Tình huống 2
│   ├── DataAgent.md                # Tình huống 2
│   ├── WriterAgent.md              # Tình huống 2
│   └── ReviewerAgent.md            # Tình huống 2
├── tinh_huong_1/
│   └── PROJECT.md                  # mô tả dự án Tình huống 1
└── tinh_huong_2/
    └── PROJECT.md                  # quy chế làm việc nhóm Tình huống 2
```

Sau khi chép về máy chủ, thư mục home của học viên sẽ trông như sau:

```text
~/                                  # VSCode mở thư mục này
├── AGENTS.md                       # Codex tự đọc mỗi khi bắt đầu làm việc
├── agents/                         # định nghĩa từng agent
├── tinh_huong_1/                   # dự án 1: dữ liệu và kết quả
│   ├── PROJECT.md
│   ├── 00_RawData/  00_Ref/  00_metadata/
│   └── 01_QC/  02_Alignment/  03_Counts/  04_DEG/
└── tinh_huong_2/                   # dự án 2: dữ liệu và kết quả
    ├── PROJECT.md
    ├── 00_RawData/  00_Ref/  00_Literature/  00_Guidelines/  00_Backup/
    └── 01_Idea/  02_Data/  03_Analysis/  04_Manuscript/  05_Review/
```

---

## 3. Cách chép về (chạy trong Terminal, tại thư mục home)

Tùy chọn `-n` của lệnh `cp` giúp **không ghi đè** file học viên đã tự tạo. Muốn
thay bằng bản chuẩn thì xóa file cũ trước rồi chạy lại.

### Tình huống 1

```bash
mkdir -p agents tinh_huong_1/{scripts,logs}
cp -n ../shared_data/Agents/AGENTS.md ./
cp -n ../shared_data/Agents/agents/BioinformaticianAgent.md ./agents/
cp -n ../shared_data/Agents/tinh_huong_1/PROJECT.md ./tinh_huong_1/
```

### Tình huống 2

```bash
mkdir -p agents tinh_huong_2
cp -n ../shared_data/Agents/agents/{IdeaAgent,DataAgent,WriterAgent,ReviewerAgent}.md ./agents/
cp -n ../shared_data/Agents/tinh_huong_2/PROJECT.md ./tinh_huong_2/
```

Nếu bắt đầu thẳng từ Tình huống 2 (bỏ qua Tình huống 1), chạy thêm:

```bash
cp -n ../shared_data/Agents/AGENTS.md ./
cp -n ../shared_data/Agents/agents/BioinformaticianAgent.md ./agents/
```

### Kiểm tra

```bash
ls AGENTS.md agents/ tinh_huong_1/PROJECT.md tinh_huong_2/PROJECT.md
```

Kết quả mong đợi sau khi chép đủ cho cả hai tình huống:

```text
AGENTS.md
tinh_huong_1/PROJECT.md
tinh_huong_2/PROJECT.md

agents/:
BioinformaticianAgent.md  DataAgent.md  IdeaAgent.md  ReviewerAgent.md  WriterAgent.md
```

---

## 4. Cách giao việc cho agent

Mở cửa sổ Codex trong VSCode, rồi dán prompt bắt đầu bằng **một câu duy nhất**
cho biết đóng vai agent nào và làm việc cho dự án nào:

```text
Đóng vai BioinformaticianAgent, làm việc cho dự án tinh_huong_1.

Hãy thực hiện ND1. QC và tiền xử lý dữ liệu.
[… phần nhiệm vụ cụ thể …]

Trước khi chạy, hãy trình bày kế hoạch để tôi duyệt.
```

Theo hướng dẫn trong `AGENTS.md`, Codex sẽ **tự đọc** hai file:
`agents/BioinformaticianAgent.md` và `tinh_huong_1/PROJECT.md`. Học viên không
phải dán lại định nghĩa agent ở mỗi lần giao việc.

> **Mỗi agent một cửa sổ chat riêng.** Ở Tình huống 2 điều này là bắt buộc, để
> `ReviewerAgent` phản biện độc lập — nó chỉ được thấy sản phẩm, không thấy trao
> đổi giữa các agent khác.

Nội dung prompt đầy đủ của từng nội dung thực hành (ND1–ND4, báo cáo tổng kết,
và bốn khâu của Tình huống 2) nằm trong [Hands-on.md](../Hands-on.md).

---

## 5. Giới thiệu từng agent

| Agent | Chuyên môn | Dùng ở |
| -- | -- | -- |
| **BioinformaticianAgent** | Phân tích bulk RNA-seq từ dữ liệu thô đến diễn giải: tiền xử lý, DESeq2/edgeR/limma (**chọn theo dạng dữ liệu**), khám phá dữ liệu, phân tích chức năng | Mọi dự án |
| **IdeaAgent** | Xây dựng câu hỏi nghiên cứu từ dữ liệu sẵn có; nắm phương pháp phân tích dữ liệu thứ cấp; tìm kiếm tài liệu | Khâu 1 |
| **DataAgent** | Các kho dữ liệu công khai (GEO, SRA, ArrayExpress, **recount3**, Expression Atlas); **nhận biết dạng dữ liệu** và đánh giá tính phù hợp với phương pháp | Khâu 2 |
| **WriterAgent** | Viết bài báo khoa học tiếng Việt trong lĩnh vực Công nghệ Sinh học | Khâu 4 |
| **ReviewerAgent** | Phản biện bài báo dựa trên dữ liệu biểu hiện gene; thống kê, hiệu chỉnh đa kiểm định, lực thống kê, yếu tố gây nhiễu | Khâu 4 |

Học viên đóng vai **Trưởng nhóm (Lead)**: giao việc, chuyển kết quả giữa các
agent, và ra quyết định ở các điểm duyệt.

> **Cả 5 agent đều không gắn với một đề tài, một loài hay một kho dữ liệu cụ thể.**
> Bối cảnh chuyên môn, thiết kế thí nghiệm, tên file dữ liệu và phương pháp dự kiến
> đều nằm trong `PROJECT.md` của từng dự án. Nhờ vậy cùng một bộ agent dùng được
> cho lúa, chuột hay người; cho dữ liệu lấy từ GEO hay recount3.

---

## 6. Tự chỉnh sửa định nghĩa agent

Chép file về là bước đầu, **không phải bước cuối**. Học viên nên mở từng file ra
đọc và chỉnh cho phù hợp với lĩnh vực của mình. Đây chính là phần thực hành quan
trọng nhất của mục 1.2 trong tài liệu.

Mỗi file định nghĩa agent theo công thức 8 thành phần:

```text
# Danh xưng          ← Agent này là ai?
# Chuyên môn         ← Giỏi về lĩnh vực, phương pháp nào?
# Mục tiêu           ← Kết quả cuối cùng cần đạt là gì?
# Nhiệm vụ           ← Làm những việc gì, theo thứ tự nào?
# Công cụ được dùng  ← Được dùng công cụ, nguồn dữ liệu nào?
# Ràng buộc          ← Điều gì không được làm?
# Đầu ra             ← Kết quả trình bày dưới dạng nào?
# Tiêu chí hoàn thành ← Khi nào coi là xong, khi nào cần hỏi lại?
```

**Khi đổi sang đề tài khác, thường không phải sửa file agent nào cả** — chỉ cần
viết một `PROJECT.md` mới. Đây là nguyên tắc tách bạch được ghi trong `AGENTS.md`:

| Thuộc về | Ví dụ | Ở đâu |
| -- | -- | -- |
| **Năng lực nghề nghiệp** | "biết các kho dữ liệu công khai", "phân biệt được raw count với RPKM" | `agents/*.md` |
| **Đặc thù dự án** | "cơ chế chịu mặn ở lúa", "thiết kế 2×2, 12 mẫu", "tên cột dạng `S40`" | `PROJECT.md` |

Nếu phải sửa file agent mỗi lần đổi đề tài, nghĩa là thông tin dự án đã bị viết
nhầm vào đó.

> **Lưu ý:** nghiên cứu về Virtual Lab (mục 4.1 của tài liệu) cho thấy agent có
> chuyên môn mô tả rõ ràng cho kết quả **tốt hơn hẳn** agent chung chung. Phần
> **Chuyên môn** không phải để trang trí.

---

## 7. Những lỗi hay gặp

| Hiện tượng | Nguyên nhân và cách xử lý |
| -- | -- |
| Agent không biết dữ liệu nằm ở đâu | Thiếu `PROJECT.md` trong thư mục dự án, hoặc câu đầu prompt chưa nêu tên dự án |
| Agent làm sai vai trò | Thiếu file `agents/<TênAgent>.md`, hoặc viết sai tên agent trong prompt |
| Agent sửa vào dữ liệu gốc | Kiểm tra `AGENTS.md` có còn dòng cấm ghi vào thư mục `00_*` không |
| Agent chạy luôn, không chờ duyệt | Thêm câu "Trước khi chạy, hãy trình bày kế hoạch để tôi duyệt" vào cuối prompt |
| Agent bịa số liệu hoặc trích dẫn | Yêu cầu agent ghi rõ nguồn cho từng con số. Với tính mới, buộc phải tra cứu bằng công cụ thật thay vì tự phán đoán |
| Đường dẫn trong agent không đúng | Mọi đường dẫn trong `agents/*.md` và `PROJECT.md` đều tính **từ thư mục dự án**, không phải từ thư mục home |

---

## 8. Khi nào cần sửa `AGENTS.md`

`AGENTS.md` chứa các quy tắc chung cho cả khóa học, nên **hiếm khi phải sửa**.
Những trường hợp cần sửa:

- Máy chủ cho phép dùng nhiều hơn 2 luồng → sửa dòng về giới hạn `threads`.
- Chuyển sang máy cá nhân, không dùng chung → có thể bỏ ràng buộc về tài nguyên.
- Muốn agent báo cáo bằng tiếng Anh → sửa dòng cuối.

Các quy tắc **không nên bỏ**, vì đây là phần giữ cho kết quả đáng tin:

- Trình bày kế hoạch và chờ duyệt trước khi chạy.
- Không ghi vào thư mục dữ liệu gốc `00_*`.
- Không bịa thông tin; không chắc thì ghi "chưa xác minh".
- Phân biệt rõ kết quả và giả thuyết.
