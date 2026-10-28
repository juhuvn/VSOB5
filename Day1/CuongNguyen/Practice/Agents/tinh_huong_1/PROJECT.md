# Dự án
Tình huống 1: Phân tích dữ liệu bulk RNA-seq ruồi giấm Drosophila melanogaster.

# Mục tiêu
Phân tích bulk RNA-seq cho 12 mẫu ruồi giấm (2 quần thể Maine và Panama × 2 mức nhiệt độ 21°C (low) và 29°C (high) × 3 lặp sinh học), từ dữ liệu FASTQ đến danh sách gene biểu hiện khác biệt. Công việc được giao theo từng nội dung ND1–ND4.

# Thành viên
- BioinformaticianAgent (agents/BioinformaticianAgent.md): thực hiện phân tích.
- Người dùng: giao việc, duyệt kế hoạch và kết quả.

# Thiết kế thí nghiệm
Thiết kế **2×2**, mỗi nhóm 3 lặp sinh học, tổng 12 mẫu:
- Yếu tố 1 — quần thể: Maine (ôn đới) và Panama (nhiệt đới).
- Yếu tố 2 — nhiệt độ nuôi: 21°C (low) và 29°C (high).

Nhóm tham chiếu: Maine và low.

# Dữ liệu đầu vào
- 00_RawData/: 24 file FASTQ paired-end, mỗi mẫu 2 file _1 và _2.
- 00_Ref/: genome FASTA, annotation GTF, và index STAR có sẵn trong 00_Ref/star_index/.
- 00_metadata/metadata.tsv: thông tin mẫu.

# Lưu ý về dữ liệu
- Dữ liệu thực hành chỉ có 30.000 reads mỗi file (hậu tố `sub30k`) để chạy nhanh. Một số chỉ số QC sẽ khác so với dữ liệu đầy đủ, và phân tích biểu hiện khác biệt hầu như không ra kết quả. Đây là điều bình thường, không phải lỗi.
- Khi được giao phân tích với ma trận count đầy đủ, dữ liệu nằm trong 04_DEG_full/ và có thể chứa giá trị count không nguyên (count ước lượng). Cần kiểm tra và xử lý trước khi đưa vào DESeq2.

# Phương pháp dự kiến
- ND1–ND3: FastQC, fastp, MultiQC, STAR (dùng index có sẵn, **không tạo lại**), featureCounts.
- ND4: DESeq2 với mô hình có tương tác `~ quần thể + nhiệt độ + quần thể:nhiệt độ`. Hệ số tương tác trả lời câu hỏi: gene nào đáp ứng với nhiệt độ khác nhau giữa hai quần thể.

# Thư mục kết quả
- 01_QC/, 02_Alignment/, 03_Counts/, 04_DEG/: kết quả của ND1–ND4.
- Các thư mục khác (ví dụ 04_DEG_full/, 05_Report/) sẽ được nêu rõ khi giao việc.
- scripts/: script; logs/: nhật ký lỗi và cách sửa.
