# Dự án
Tình huống 2: Đội ngũ AI Agent hỗ trợ nghiên cứu, phân tích lại bộ dữ liệu GSE167342.

# Mục tiêu chung
Phân tích lại bộ dữ liệu RNA-seq GSE167342 (lúa, dòng chuyển gen mang Saltol so với giống gốc mẫn cảm, đối chứng và xử lý mặn) để làm rõ cơ chế phân tử giúp dòng chuyển gen chịu mặn tốt hơn, và viết một bài báo ngắn bằng tiếng Việt cho kỷ yếu Hội nghị Công nghệ Sinh học toàn quốc năm 2027.

# Thành viên
- IdeaAgent (agents/IdeaAgent.md): cụ thể hóa định hướng thành câu hỏi nghiên cứu.
- DataAgent (agents/DataAgent.md): thẩm định và chuẩn hóa dữ liệu.
- BioinformaticianAgent (agents/BioinformaticianAgent.md): phân tích dữ liệu.
- WriterAgent (agents/WriterAgent.md): viết bản thảo bài báo.
- ReviewerAgent (agents/ReviewerAgent.md): phản biện độc lập bản thảo.
- Người dùng là Trưởng nhóm (Lead): giao việc, duyệt và ra quyết định cuối cùng.

# Bối cảnh chuyên môn
Sinh học phân tử thực vật, cơ chế chịu mặn ở lúa: điều hòa ion Na+/K+, tín hiệu ABA, stress oxy hóa, quang hợp dưới điều kiện stress. QTL Saltol từ giống FL478 là nguồn gen chịu mặn được dùng trong chọn giống.

# Thiết kế thí nghiệm
Thiết kế **2×2**, mỗi nhóm 3 lặp sinh học, tổng 12 mẫu:
- Yếu tố 1 — dòng lúa: giống gốc mẫn cảm mặn (`PL12`) và dòng chuyển gen mang Saltol (`IL22`).
- Yếu tố 2 — điều kiện: đối chứng và xử lý 80 mM NaCl trong 24 giờ.
- Mô: lá. Chỉ một thời điểm thu mẫu.

Nhóm tham chiếu: `PL12` và đối chứng.

# Dữ liệu đầu vào
- 00_RawData/: ma trận raw count (GSE167342_Raw_counts.xlsx) và metadata của GEO (GSE167342_series_matrix.txt.gz).
- 00_Ref/: chú giải gene lúa (rice_gene_annotation.tsv) và chú giải Gene Ontology (rice_GO_annotation.tsv). Lúa **không có sẵn gói chú giải trong R**, nên phân tích chức năng phải dùng hai file này.
- 00_Literature/: tóm tắt bài báo gốc (PMID 35126422).
- 00_Guidelines/the-le-viet-bai_chi-tiet.docx: thể lệ viết bài của Hội nghị; bản thảo phải tuân thủ thể lệ này.
- 00_Backup/: kết quả mẫu, chỉ dùng khi Lead yêu cầu.

# Lưu ý về dữ liệu
- Tên cột của ma trận count có dạng `S40`, `S41`… **không trùng** với mã GSM hay tên mẫu. Cầu nối nằm ở trường `description` của từng mẫu trong metadata GEO.
- Metadata GEO gọi giống gốc là `PL12`, trong khi bài báo gọi là `OLESA`.
- Khoảng 6.900 gene có count bằng 0 ở cả 12 mẫu.

# Phương pháp dự kiến
DESeq2 với mô hình có tương tác: `~ dòng lúa + điều kiện + dòng lúa:điều kiện`. Hệ số tương tác trả lời câu hỏi chính: gene nào đáp ứng với mặn khác nhau giữa hai dòng.

# Quy trình
1. IdeaAgent → điểm duyệt 1 (Lead chọn câu hỏi nghiên cứu)
2. DataAgent → điểm duyệt 2 (Lead duyệt sample sheet)
3. BioinformaticianAgent
4. WriterAgent → ReviewerAgent → WriterAgent sửa → điểm duyệt 3 (Lead duyệt bản thảo)

# Giao thức giao tiếp
- Mỗi khâu lưu kết quả vào thư mục riêng: 01_Idea/, 02_Data/, 03_Analysis/, 04_Manuscript/, 05_Review/.
- Agent đọc đầu vào từ thư mục của khâu trước; không sửa file của agent khác.
- Mỗi khâu có một file README.md gồm: (1) kết quả chính, (2) căn cứ (đường dẫn file, số liệu), (3) điểm chưa chắc chắn, (4) đề xuất cho khâu tiếp theo.
- Lead ghi các quyết định ở điểm duyệt vào logs/decisions.md; agent đọc file này để biết các quyết định đã đưa ra.

# Quy tắc riêng của dự án
(bổ sung cho các quy tắc chung trong AGENTS.md)
- Chỉ trích dẫn tài liệu có PMID hoặc DOI xác minh được; nếu không truy cập được Internet để kiểm tra, ghi rõ "chưa xác minh".
- Khi Lead và agent bất đồng, agent nêu lập luận kèm căn cứ; Lead quyết định.
- ReviewerAgent làm việc độc lập: chỉ đọc sản phẩm (bản thảo, kết quả), không đọc trao đổi với các agent khác.
