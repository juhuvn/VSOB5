# VSOB5 — Trường hè Sinh học Việt Nam lần thứ 5

**Mastering Agentic AI in Bioinformatics: From Insight to Impact**

*Làm chủ AI Agent trong Tin sinh học: Từ hiểu biết đến ứng dụng*

📍 ICISE, 07 Science Avenue, phường Quy Nhơn Nam, Gia Lai
📅 29–31 tháng 10 năm 2026

---

## Khóa học này là gì?

VSOB5 là khóa đào tạo ba ngày về cách ứng dụng **AI Agent** vào công việc Tin
sinh học hằng ngày. Khác với việc dùng chatbot để hỏi đáp, AI Agent có thể **tự
lập kế hoạch, gọi công cụ, chạy phân tích, đọc lỗi và tự sửa** — còn nhà nghiên
cứu giữ vai trò định hướng, thẩm định và chịu trách nhiệm khoa học.

Khóa học đi theo đúng mạch *from insight to impact*:

| | Nội dung |
| -- | -- |
| **Ngày 1** | Nền tảng về LLM và AI Agent; hai phiên thực hành dài với dữ liệu thật |
| **Ngày 2** | Case study challenge — chia nhóm, mỗi nhóm giải một bài toán Tin sinh học riêng, có TA và tutor kèm. Kèm chia sẻ kinh nghiệm từ học viên và gala dinner |
| **Ngày 3** | Các nhóm báo cáo, hội đồng chuyên gia đánh giá, trao giải VSOB5 Championship |

Sau khóa học, học viên có thể tự xây dựng và vận hành một **đội ngũ AI Agent**
cho đề tài của chính mình, đồng thời biết cách kiểm chứng kết quả mà agent tạo ra.

---

## 📋 Chương trình chi tiết

👉 **[VSOB5-Tentative-programme.md](VSOB5-Tentative-programme.md)** — lịch đầy đủ
ba ngày, kèm tên các báo cáo viên và phiên làm việc. Xem được ngay trên GitHub.

Bản Word chính thức, đầy đủ định dạng:
[VSOB5-Tentative programme.docx](VSOB5-Tentative%20programme.docx) *(bấm để tải về)*

### Các báo cáo chính

| Ngày | Báo cáo viên | Chủ đề |
| -- | -- | -- |
| 1 | **TS. Trần Thương Văn Du**<br>Swiss Institute of Bioinformatics; Giáo sư thỉnh giảng, Trường ĐH Khoa học Tự nhiên, ĐHQG-HCM | Toward sustainable life sciences: privacy preserving AI and multimodal data integration |
| 1 | **TS. Bùi Văn Thạch**<br>Khoa CNTT, Trường ĐH Khoa học Tự nhiên, ĐHQG-HCM | From biostatistics to Agentic AI in bioinformatics |
| 2 | **PGS.TS. Nguyễn Hoàng Hải**<br>Đại học Quốc gia Hà Nội | Triết học khoa học trong thời đại AI và công nghệ sinh học |
| 3 | **PGS.TS. Chu Đình Tới**<br>Trưởng khoa Khoa học Ứng dụng, Trường Quốc tế, ĐHQGHN | "Quang di truyền" — giải thưởng Nobel Y học 2026: Sinh học là phần cứng, AI là phần mềm và ánh sáng là chìa khóa? |

### Báo cáo mời khác

| Ngày | Báo cáo viên | Chủ đề |
| -- | -- | -- |
| 2 | **Thao My Nguyen**<br>Founding Member, Head of Product Design & Business Development, Drylab, Inc. | How to work with AI to run your dry lab |

---

## 📚 Tài liệu theo ngày

### Ngày 1 — Agentic Bioinformatics in Practice

*Giảng viên: **TS. Nguyễn Cường**, Công ty LOBI, Viện Công nghệ Thông tin, VAST*

#### Bài giảng

| Tài liệu | Mô tả |
| -- | -- |
| 🖨️ [Agentic Bioinformatics in Practice.pdf](Day1/CuongNguyen/Agentic%20Bioinformatics%20in%20Practice.pdf) | **Slide bài giảng**, 60 trang. Bản PDF xem được trực tiếp trên GitHub, không cần tải về |
| 🎞️ [VSOB5-intro.pptx](Day1/CuongNguyen/VSOB5-intro.pptx) | Slide khai mạc: giới thiệu chuỗi VSOB qua các năm, ban tổ chức, báo cáo viên mời, và máy chủ CBAS dùng cho phiên thực hành *(bấm để tải về)* |

#### Thực hành

| Tài liệu | Mô tả |
| -- | -- |
| 📖 [Hands-on.md](Day1/CuongNguyen/Practice/Hands-on.md) | **Tài liệu thực hành chính.** Công thức tạo AI Agent, hai tình huống thực hành đầy đủ, và phần bàn luận về các hệ thống AI Agent đã được công bố |
| 🖨️ [Hands-on.pdf](Day1/CuongNguyen/Practice/Hands-on.pdf) | Bản PDF để in, có trang bìa và mục lục |
| 🤖 [Agents/](Day1/CuongNguyen/Practice/Agents/) | Bộ file định nghĩa AI Agent, chép về là dùng được ngay — [xem hướng dẫn](Day1/CuongNguyen/Practice/Agents/README.md) |

Nội dung tài liệu thực hành:

1. **AI Agent** — agent là gì, công thức tạo một agent, công thức tạo một nhóm agent và quy chế làm việc nhóm.
2. **Tình huống 1: Giao việc cho một agent** — phân tích bulk RNA-seq ruồi giấm *Drosophila melanogaster*, từ FASTQ đến danh sách gene biểu hiện khác biệt (FastQC, fastp, STAR, featureCounts, DESeq2).
3. **Tình huống 2: Xây dựng đội ngũ agent** — phân tích lại dữ liệu công khai GEO về lúa chịu mặn, từ lên ý tưởng đến viết bài báo cho kỷ yếu hội thảo.
4. **Bàn luận thêm** — Virtual Lab, The AI Scientist, Co-Scientist, và phương pháp luận phân tích dữ liệu thứ cấp.

#### Đọc thêm

| Tài liệu | Nội dung |
| -- | -- |
| [00-LLM.md](Day1/CuongNguyen/ReadMore/00-LLM.md) | Mô hình ngôn ngữ lớn (LLM) — tài liệu hướng dẫn |
| [01-Agent.md](Day1/CuongNguyen/ReadMore/01-Agent.md) | Phân biệt Chatbot, AI Assistant, AI Agent và Bioinformatics Pipeline |
| [05-DocThem-ChatGPT.md](Day1/CuongNguyen/ReadMore/05-DocThem-ChatGPT.md) | ChatGPT từ nền tảng đến ứng dụng — lộ trình tự học |
| [05-DocThem-Claude.md](Day1/CuongNguyen/ReadMore/05-DocThem-Claude.md) | Claude toàn tập cho nhà nghiên cứu và kỹ thuật |
| [05-DocThem-Gemini.md](Day1/CuongNguyen/ReadMore/05-DocThem-Gemini.md) | Cẩm nang toàn diện hệ sinh thái Gemini |

### Ngày 2 — Case study challenge

| Tài liệu | Mô tả |
| -- | -- |
| 📖 [01-Case-study-challenge.md](Day2/01-Case-study-challenge.md) | **Đề bài cho các nhóm.** Bảy bối cảnh nghiên cứu khác nhau, khai thác dữ liệu công khai (GEO, recount3) bằng đội ngũ AI Agent: thẩm định dữ liệu, lên ý tưởng, phân tích, viết bài. Kèm thang điểm và quy định |
| 🖨️ [01-Case-study-challenge.pdf](Day2/01-Case-study-challenge.pdf) | Bản PDF để in, có trang bìa và mục lục |

### Ngày 3 — Báo cáo và trao giải

📁 [Day3/](Day3/) — *tài liệu sẽ được cập nhật*

---

## 🔧 Chuẩn bị trước khi đến lớp

Phiên thực hành Ngày 1 chạy trên máy chủ của khóa học, học viên kết nối qua
VSCode. Cần chuẩn bị sẵn:

- **VSCode** với các extension:
  - **Codex – OpenAI's coding agent**, phiên bản `26.1007.21434` *(dùng đúng phiên bản này)*
  - **HTML Preview** `v0.2.5`
  - **PDF Preview**
  - **CSV/TSV Viewer**
- **Kết nối tới máy chủ VSOB5** qua VSCode

Hướng dẫn cài đặt chi tiết nằm trong phần 2.3.1 của
[tài liệu thực hành](Day1/CuongNguyen/Practice/Hands-on.md).

---

## 🧬 Dữ liệu dùng trong khóa học

Toàn bộ dữ liệu thực hành là **dữ liệu công khai**, đã được Ban tổ chức chuẩn bị
sẵn trên máy chủ:

| Tình huống | Dữ liệu | Nguồn |
| -- | -- | -- |
| Tình huống 1 | RNA-seq ruồi giấm, 12 mẫu (2 quần thể × 2 mức nhiệt độ × 3 lặp) | NCBI SRA, SRR1576457–SRR1576516 |
| Tình huống 1 (ND4) | Ma trận count đầy đủ | [Harvard FAS Informatics](https://informatics.fas.harvard.edu/resources/tutorials/differential-expression-analysis/) |
| Tình huống 2 | RNA-seq lá lúa, dòng chuyển gen mang QTL *Saltol* | [GEO GSE167342](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE167342) |

Danh sách tài liệu tham khảo đầy đủ nằm ở cuối
[tài liệu thực hành](Day1/CuongNguyen/Practice/Hands-on.md).

---

## ⚠️ Lưu ý quan trọng khi dùng AI Agent

Đây là thông điệp xuyên suốt khóa học, không phải một ghi chú phụ:

> **Mọi kết quả do AI Agent tạo ra đều phải được người nghiên cứu kiểm chứng.**
> Người nghiên cứu chịu trách nhiệm khoa học cuối cùng đối với kết quả công bố.

Cụ thể:

- **Kiểm chứng mọi con số và trích dẫn.** AI có thể bịa số liệu, bịa trích dẫn, và bịa cả bảng kết quả.
- **Phân biệt rõ kết quả và giả thuyết.** Agent rất giỏi việc đưa ra những diễn giải nghe hợp lý nhưng dữ liệu chưa chứng minh.
- **Khai báo minh bạch.** Bài báo hoặc bản phản biện có phần đáng kể do AI tạo ra cần được ghi rõ.
- **Bảo mật dữ liệu.** Không đưa dữ liệu chưa công bố hoặc dữ liệu bệnh nhân vào các dịch vụ AI mà bạn không kiểm soát được nơi lưu trữ.

---

## 📄 Giấy phép

Tài liệu được phát hành theo giấy phép Creative Commons — xem [LICENSE](LICENSE).

## 📬 Liên hệ

**TS. Nguyễn Cường** — Giám đốc khoa học, Công ty LOBI; Nghiên cứu viên chính,
Viện Công nghệ Thông tin, VAST.
