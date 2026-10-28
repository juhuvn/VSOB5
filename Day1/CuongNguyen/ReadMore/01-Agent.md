Chatbot, AI Assistant, AI Agent và Bioinformatics Pipeline – Tài liệu hướng dẫn
====================

13/10/2026

**TS. Nguyễn Cường**
Giám đốc khoa học, Công ty LOBI
NCVC, Viện CNTT, VAST

# Mục tiêu bài học

Bốn khái niệm này khác nhau chủ yếu ở **mức tự chủ**: chatbot trả lời, assistant giúp làm việc, agent tự hoàn thành nhiệm vụ, còn pipeline chạy đúng các bước đã định sẵn. Sau phần này, người học sẽ:

1. Định nghĩa được chatbot, AI assistant, AI agent và bioinformatics pipeline bằng lời của mình.
2. Giải thích được mỗi loại hoạt động ra sao bên trong.
3. Chỉ ra điểm giống và khác giữa chúng theo các tiêu chí cụ thể.
4. Chọn đúng công cụ cho một bài toán tin sinh học, và biết cách kết hợp agent với pipeline.

**Tiền đề:** đã nắm phần LLM (token, huấn luyện, các mô hình hiện nay). Ba khái niệm đầu đều dùng LLM làm "bộ não"; pipeline thì có thể không có AI nào cả.

**Một hình ảnh để nhớ:** hãy tưởng tượng một phòng thí nghiệm.

- **Chatbot** như quầy hỏi đáp: bạn hỏi, người trực trả lời, xong là hết.
- **AI assistant** như trợ lý riêng: nhớ bạn là ai, mở được tài liệu, soạn giúp email, nhưng chờ bạn giao từng việc.
- **AI agent** như nghiên cứu viên: nhận một mục tiêu ("tìm gen khác biệt trong bộ dữ liệu này"), tự lên kế hoạch, tự chạy phân tích, tự sửa lỗi, rồi báo cáo.
- **Pipeline** như dây chuyền máy móc tự động: mẫu đi vào, qua các máy theo thứ tự cố định, kết quả đi ra, lần nào cũng giống nhau.

# Phần 1. Chatbot

**Ý chính:** Chatbot là chương trình trò chuyện với con người bằng ngôn ngữ tự nhiên, theo kiểu **hỏi – đáp từng lượt**. Nó phản hồi khi được hỏi và không tự hành động gì ngoài việc tạo câu trả lời.

## 1.1. Ba thế hệ chatbot

| Thế hệ | Cách hoạt động | Ví dụ | Hạn chế |
| --- | --- | --- | --- |
| Dựa trên luật (từ 1966) | So khớp từ khoá với kịch bản viết sẵn: thấy "giá" thì trả lời bảng giá | ELIZA (1966), chatbot chăm sóc khách hàng đời đầu, menu "bấm 1, bấm 2" | Chỉ hiểu đúng những gì đã lập trình; hỏi lệch một chút là "Xin lỗi, tôi không hiểu" |
| Dựa trên nhận dạng ý định (khoảng 2015–2022) | Mô hình học máy phân loại ý định (intent) và trích thông tin (entity), rồi gọi kịch bản tương ứng | Dialogflow, Rasa, Siri thế hệ đầu | Phải định nghĩa trước mọi ý định; không xử lý được câu hỏi mở |
| Dựa trên LLM (từ cuối 2022) | LLM sinh câu trả lời tự do từ toàn bộ ngữ cảnh hội thoại | ChatGPT bản đầu, chatbot hỏi đáp trên website | Có thể ảo giác; chỉ biết những gì đã học hoặc được đưa vào ngữ cảnh |

## 1.2. Chatbot LLM hoạt động thế nào?

Mỗi lượt hội thoại diễn ra theo bốn bước:

1. Người dùng gửi tin nhắn.
2. Hệ thống ghép **system prompt** (lời dặn của nhà phát triển, ví dụ "Bạn là trợ lý của khoa Sinh học, trả lời ngắn gọn bằng tiếng Việt") với **lịch sử hội thoại** và tin nhắn mới.
3. Toàn bộ chuỗi đó được gửi vào LLM; LLM sinh câu trả lời từng token.
4. Câu trả lời hiển thị cho người dùng và được thêm vào lịch sử cho lượt sau.

Điểm cần nhớ: **LLM không có trí nhớ giữa các lượt.** Cảm giác "nó nhớ" là do ứng dụng gửi lại toàn bộ lịch sử mỗi lần. Hội thoại quá dài sẽ vượt cửa sổ ngữ cảnh và phần đầu bị cắt bỏ hoặc tóm tắt.

## 1.3. Ví dụ trong tin sinh học

- Chatbot hỏi đáp về quy trình của một core facility giải trình tự: "Mẫu RNA cần RIN tối thiểu bao nhiêu?"
- Chatbot giải thích khái niệm cho sinh viên: "FPKM và TPM khác nhau thế nào?"
- Chatbot dùng **RAG** trên tài liệu hướng dẫn của một phần mềm (ví dụ tài liệu GATK) để trả lời câu hỏi kèm trích dẫn đúng trang.

**Khi nào chatbot là đủ:** câu hỏi đơn lẻ, cần câu trả lời bằng chữ, không cần chạm vào dữ liệu hay hệ thống nào.

> **Dừng lại suy nghĩ.** Bạn hỏi chatbot "Chạy giúp tôi DESeq2 trên file counts.csv này". Một chatbot thuần tuý sẽ làm được gì, và không làm được gì?

# Phần 2. AI Assistant (trợ lý AI)

**Ý chính:** AI assistant là chatbot được "trang bị thêm": có **bộ nhớ**, đọc được **tài liệu và dữ liệu của bạn**, dùng được **công cụ** (tìm web, chạy code, tạo file), và tích hợp vào nơi bạn làm việc. Nó chủ động hơn chatbot nhưng vẫn **làm theo từng yêu cầu của người dùng**; người dùng là người cầm lái.

## 2.1. Assistant = chatbot + gì?

| Thành phần thêm vào | Ý nghĩa | Ví dụ |
| --- | --- | --- |
| Bộ nhớ dài hạn | Nhớ thông tin, sở thích của người dùng qua nhiều cuộc trò chuyện | Nhớ bạn làm về proteomics, thích câu trả lời ngắn |
| Truy cập tài liệu (RAG, file đính kèm) | Trả lời dựa trên tài liệu của bạn, không chỉ kiến thức đã học | Đọc file PDF bài báo, bảng Excel kết quả |
| Công cụ (tool use) | Gọi chức năng bên ngoài khi cần | Tìm PubMed, chạy Python vẽ biểu đồ, tạo file Word |
| Tích hợp ứng dụng | Làm việc ngay trong email, lịch, trình soạn thảo, IDE | Trợ lý trong Google Workspace, Microsoft 365, trình viết code |
| Cá nhân hoá | Điều chỉnh giọng văn, định dạng theo người dùng | Luôn trả lời bằng tiếng Việt, kèm trích dẫn |

## 2.2. Assistant hoạt động thế nào?

Với mỗi yêu cầu, assistant thường đi qua một chu trình ngắn:

1. **Hiểu yêu cầu** và lấy thêm ngữ cảnh: bộ nhớ, file đính kèm, tài liệu liên quan.
2. **Quyết định có cần công cụ không.** LLM được mô tả danh sách công cụ (tên, chức năng, tham số). Nếu cần, nó sinh ra một lời gọi có cấu trúc, ví dụ `search_pubmed(query="TP53 single-cell")`.
3. **Hệ thống thực thi công cụ** và trả kết quả về cho LLM.
4. **LLM tổng hợp** kết quả thành câu trả lời và chờ yêu cầu tiếp theo.

Phần lớn các assistant chỉ gọi một vài công cụ cho mỗi yêu cầu, rồi dừng lại chờ người dùng. Đó là ranh giới với agent.

**Giao thức MCP (Model Context Protocol):** chuẩn mở do Anthropic công bố cuối 2024, nay được nhiều hãng hỗ trợ, cho phép kết nối LLM với công cụ và nguồn dữ liệu theo một cách thống nhất. Đã có các máy chủ MCP cho PubMed, bioRxiv, UniProt…, nên assistant có thể tra cứu cơ sở dữ liệu sinh học trực tiếp.

## 2.3. Ví dụ

### 2.3.1 Assistant đa dụng Claude, ChatGPT, Gemini, Microsoft Copilot

- **Assistant lập trình:** GitHub Copilot gợi ý code R/Python ngay trong trình soạn thảo khi bạn viết script phân tích.
- **Trong tin sinh học:** bạn tải lên bảng kết quả DESeq2 và hỏi "10 gen tăng mạnh nhất thuộc con đường nào? Vẽ volcano plot giúp tôi". Assistant chạy code, vẽ hình, tra cứu chức năng gen và giải thích. Bạn xem kết quả rồi quyết định bước tiếp theo.

> **Dừng lại suy nghĩ.** Hãy liệt kê ba việc trong công việc hằng tuần của bạn mà một AI assistant có thể làm giúp, và một việc bạn chưa muốn giao cho nó. Vì sao?

# Phần 3. AI Agent (tác tử AI)

**Ý chính:** AI agent là hệ thống dùng LLM để **tự theo đuổi một mục tiêu qua nhiều bước**: tự lập kế hoạch, tự gọi công cụ, quan sát kết quả, tự sửa lỗi và quyết định khi nào xong. Người dùng giao **mục tiêu**, không giao từng bước.

Một định nghĩa ngắn hay được dùng: *agent = LLM + công cụ + vòng lặp*. Anthropic phân biệt thêm: trong **workflow**, các bước do lập trình viên định sẵn; trong **agent**, chính LLM quyết định bước tiếp theo.

## 3.1. Vòng lặp của agent

Agent không chạy thẳng một mạch: sau mỗi hành động, nó đọc kết quả rồi quyết định làm tiếp, đổi cách hay dừng lại.

Vòng lặp này còn được gọi là **ReAct** (Reasoning + Acting, Yao và cs., 2022): mô hình xen kẽ giữa *suy nghĩ* ("cần kiểm tra chất lượng dữ liệu trước"), *hành động* (gọi công cụ FastQC) và *quan sát* (đọc báo cáo trả về).

## 3.2. Bốn thành phần của một agent

| Thành phần | Vai trò | Ví dụ trong tin sinh học |
| --- | --- | --- |
| Bộ não (LLM) | Hiểu mục tiêu, suy luận, chọn hành động | Claude, GPT, Gemini, Qwen |
| Công cụ | Cách agent tác động lên thế giới | Shell, Python/R, BLAST, API của NCBI/Ensembl, trình chạy Nextflow |
| Bộ nhớ | Ngắn hạn: những gì đã làm trong phiên; dài hạn: ghi chú, kết quả cũ | File nhật ký phân tích, ghi chú về bộ dữ liệu |
| Lập kế hoạch và tự kiểm tra | Chia nhỏ mục tiêu, theo dõi tiến độ, phát hiện và sửa lỗi | Danh sách việc cần làm; đọc thông báo lỗi rồi sửa lệnh |

## 3.3. Ví dụ: agent phân tích RNA-seq

Mục tiêu người dùng giao: *"Tìm gen biểu hiện khác biệt giữa nhóm bệnh và đối chứng trong thư mục data/, viết báo cáo ngắn."* Một agent có thể tự làm như sau:

1. Liệt kê file, đọc bảng thông tin mẫu, nhận ra có 6 mẫu bệnh và 6 mẫu đối chứng.
2. Chạy FastQC; thấy một mẫu chất lượng kém, ghi chú lại.
3. Viết script R chạy DESeq2; lần đầu báo lỗi vì tên mẫu không khớp, agent đọc lỗi, sửa tên cột, chạy lại.
4. Vẽ volcano plot, chạy phân tích làm giàu GO.
5. Viết báo cáo, nêu rõ mẫu chất lượng kém và đề nghị người dùng quyết định có loại mẫu đó không.

Điểm khác assistant nằm ở bước 2–4: agent tự quyết định và tự sửa lỗi mà không hỏi lại sau mỗi bước.

## 3.4. Hệ nhiều agent (multi-agent)

Nhiệm vụ lớn có thể chia cho nhiều agent chuyên trách: một agent **điều phối** giao việc cho agent tìm tài liệu, agent viết code, agent kiểm tra kết quả. Ưu điểm là chia việc song song và kiểm tra chéo; nhược điểm là tốn nhiều token và khó gỡ lỗi hơn.

## 3.5. Skills: đóng gói kinh nghiệm cho agent

**Ý chính:** Skill (kỹ năng) là một **thư mục chứa hướng dẫn quy trình, có thể kèm script và tài liệu tham khảo**, mà agent tự tìm và nạp khi việc cần đến. Công cụ cho agent *khả năng làm* (chạy R, gọi API NCBI); skill dạy agent *làm thế nào cho đúng chuẩn* của bạn hoặc của lab.

**Vấn đề skill giải quyết.** LLM biết nhiều kiến thức chung nhưng không biết quy trình riêng của lab bạn: ngưỡng lọc nào, design nào, báo cáo theo mẫu nào, những lỗi nào nhóm đã từng mắc. Nếu không có skill, bạn phải dặn lại những điều đó mỗi lần, và dễ quên dặn đúng lúc quan trọng nhất.

### Cấu trúc một skill

Anthropic giới thiệu Agent Skills vào tháng 10/2025 và công bố thành **chuẩn mở** ([agentskills.io](https://agentskills.io)) vào tháng 12/2025. Đến nay nhiều công cụ agent đã hỗ trợ cùng định dạng: Claude, Claude Code, ChatGPT/Codex, Gemini CLI, GitHub Copilot, Cursor… Một skill viết một lần có thể dùng ở nhiều nơi.

```text
deseq2-analysis/
├── SKILL.md          # Bắt buộc: tên, mô tả "dùng khi nào", và hướng dẫn quy trình
├── scripts/          # Tuỳ chọn: code chạy được, ví dụ run_deseq2.R
├── references/       # Tuỳ chọn: tài liệu tham khảo, ví dụ quy chuẩn báo cáo của lab
└── assets/           # Tuỳ chọn: mẫu báo cáo, bảng ánh xạ mã gen
```

Ví dụ file `SKILL.md`:

```markdown
---
name: deseq2-analysis
description: Phân tích biểu hiện gen khác biệt bằng DESeq2 từ ma trận đếm RNA-seq.
  Dùng khi người dùng có bảng raw counts và bảng thông tin mẫu, cần tìm gen khác biệt.
---

# Quy trình DESeq2 của lab

1. Kiểm tra thứ tự mẫu trong ma trận đếm khớp bảng thông tin mẫu; không khớp thì dừng.
2. Hỏi người dùng nhóm tham chiếu nếu chưa rõ; luôn đặt bằng relevel().
3. Nếu có yếu tố ghép cặp hoặc batch (người hiến, lô thí nghiệm), đưa vào design
   trước yếu tố cần so sánh, ví dụ ~ donor + treatment.
4. Lọc gen có tổng số đếm < 10. Dùng padj < 0.05, không dùng p-value thô.
5. Chạy scripts/run_deseq2.R thay vì tự viết lại code.
6. Chuyển mã gen bằng assets/gene_map.csv; mã nào không có thì ghi "không tìm thấy", không đoán.
7. Báo cáo theo mẫu assets/report_template.md, ghi phiên bản R và các gói.
```

### Skill được nạp thế nào: tiết lộ dần (progressive disclosure)

Skill không được nhét toàn bộ vào ngữ cảnh ngay từ đầu, mà được nạp theo ba mức:

| Mức | Khi nào | Nạp gì | Tốn bao nhiêu ngữ cảnh |
| --- | --- | --- | --- |
| 1. Khám phá | Khi agent khởi động | Chỉ `name` và `description` của mọi skill | Vài chục token mỗi skill |
| 2. Kích hoạt | Khi việc đang làm khớp với `description` | Toàn bộ nội dung `SKILL.md` | Vài trăm đến vài nghìn token |
| 3. Thực thi | Khi hướng dẫn cần đến | Script, tài liệu, mẫu trong thư mục; script được **chạy**, không cần đọc hết | Chỉ phần cần dùng |

Nhờ vậy, một agent có thể "mang theo" hàng chục skill mà không chật cửa sổ ngữ cảnh. Hệ quả quan trọng: **`description` quyết định skill có được dùng hay không**. Mô tả phải nói rõ "làm gì" và "dùng khi nào".

### Skill khác gì các khái niệm khác?

| | Câu hỏi nó trả lời | Bản chất | Khi nào được dùng |
| --- | --- | --- | --- |
| **System prompt / file quy tắc** (CLAUDE.md, AGENTS.md) | Luôn phải tuân theo điều gì? | Lời dặn chung, ngắn | Luôn nạp, mọi lúc |
| **Công cụ / MCP** | Truy cập được gì, làm được gì? | Chức năng gọi được, kết nối dữ liệu | Khi agent quyết định gọi |
| **Skill** | Làm việc X thế nào cho đúng chuẩn? | Quy trình + script + tài liệu | Chỉ khi việc khớp mô tả |
| **Pipeline** | Chạy chuỗi bước cố định nào? | Mã workflow xác định | Khi được khởi chạy |

Một cách nhớ: file quy tắc là **nội quy phòng lab**, công cụ là **máy móc trong phòng**, skill là **sổ tay quy trình chuẩn (SOP)** cho từng loại thí nghiệm, còn pipeline là **dây chuyền tự động**.

### Skill trong tin sinh học

- **SOP phân tích:** QC dữ liệu giải trình tự theo ngưỡng của core facility; DESeq2 với các bẫy đã biết như ví dụ trên; gán tên cụm scRNA-seq theo bộ gen chỉ thị của lab.
- **Tra cứu có kiểm soát:** cách truy vấn NCBI, Ensembl, UniProt đúng phiên bản, kèm script tải dữ liệu.
- **Viết và báo cáo:** viết phần Phương pháp theo yêu cầu tạp chí; báo cáo kết quả theo mẫu chung của nhóm.
- **Điều phối pipeline:** hướng dẫn chọn tham số nf-core/rnaseq cho từng loại dữ liệu, cách đọc MultiQC và xử lý các lỗi thường gặp.

**Skill nằm giữa prompt và pipeline.** Skill vẫn để LLM linh hoạt xử lý tình huống, nhưng ép nó đi theo quy trình đã thống nhất và dùng script đã kiểm chứng. Khi một skill được dùng đủ nhiều và các bước đã ổn định, phần lõi của nó nên được cố định thành pipeline.

**Viết skill tốt:**

- Viết từ kinh nghiệm thật: sau khi làm xong một việc cùng agent, đóng gói những gì đã phải sửa và dặn thêm thành skill.
- Ngắn gọn, có thứ tự bước rõ ràng; chi tiết dài đưa vào `references/`.
- Phần tính toán đưa vào `scripts/` để chạy, không để LLM tự viết lại mỗi lần.
- Kiểm tra: mở phiên mới, mô tả việc **mà không nhắc tên skill**, xem agent có tự dùng skill và làm đúng không.

## 3.6. Rủi ro cần biết

- **Sai lầm lan truyền:** một bước sai ở đầu có thể kéo theo cả chuỗi kết luận sai.
- **Hành động không đảo ngược được:** xoá file, ghi đè dữ liệu gốc. Cần cấp quyền tối thiểu và làm việc trên bản sao.
- **Chi phí khó đoán:** vòng lặp dài tiêu tốn nhiều token; nên đặt giới hạn số bước và ngân sách.
- **Prompt injection:** nội dung độc hại trong file hoặc trang web có thể "ra lệnh" cho agent. Không cho agent tự làm theo chỉ dẫn tìm thấy trong dữ liệu.
- **Skill không rõ nguồn gốc:** skill có thể chứa script mà agent sẽ chạy trên máy bạn. Chỉ cài skill từ nguồn tin cậy, và đọc `SKILL.md` cùng các script trước khi dùng.
- **Cần con người duyệt** (human-in-the-loop) ở các điểm quyết định quan trọng.

> **Dừng lại suy nghĩ.** Trong ví dụ RNA-seq ở trên, nếu agent tự quyết định loại bỏ mẫu chất lượng kém mà không báo, điều gì có thể xảy ra với kết luận khoa học?

# Phần 4. Bioinformatics Pipeline (quy trình phân tích tin sinh học)

**Ý chính:** Pipeline là **chuỗi các bước phân tích được định nghĩa sẵn**, nối đầu ra của bước trước làm đầu vào của bước sau, chạy tự động từ dữ liệu thô tới kết quả. Pipeline là **xác định (deterministic)**: cùng dữ liệu, cùng phiên bản, cùng tham số thì cho cùng kết quả. Pipeline không cần AI; nó là xương sống của tin sinh học từ trước khi có LLM.

## 4.1. Ví dụ: pipeline RNA-seq chuẩn

| Bước | Việc làm | Công cụ thường dùng | Đầu ra |
| --- | --- | --- | --- |
| 1. Kiểm tra chất lượng | Đánh giá chất lượng read | FastQC, MultiQC | Báo cáo chất lượng |
| 2. Cắt adapter, lọc | Bỏ adapter và base chất lượng thấp | fastp, Trim Galore | FASTQ đã làm sạch |
| 3. Căn chỉnh hoặc định lượng | Gắn read vào bộ gen hoặc transcriptome | STAR, HISAT2; Salmon | File BAM hoặc bảng định lượng |
| 4. Đếm | Đếm số read trên mỗi gen | featureCounts | Ma trận đếm gen × mẫu |
| 5. Phân tích khác biệt | So sánh nhóm, kiểm định thống kê | DESeq2, edgeR | Danh sách gen khác biệt |
| 6. Diễn giải | Phân tích làm giàu chức năng | clusterProfiler, GSEA | Con đường sinh học có ý nghĩa |

Các pipeline tương tự tồn tại cho gọi biến dị (WGS/WES), ChIP-seq, ATAC-seq, scRNA-seq, metagenomics, proteomics khối phổ.

## 4.2. Pipeline được xây dựng thế nào?

Từ đơn giản đến chuyên nghiệp:

1. **Script shell** nối các lệnh: nhanh để thử, nhưng khó chạy lại khi lỗi giữa chừng và khó mở rộng.
2. **Trình quản lý workflow (workflow manager):**
   - **Snakemake** (cú pháp giống Python): khai báo luật "file A tạo ra file B bằng lệnh nào"; tự tính thứ tự chạy.
   - **Nextflow**: mạnh về chạy song song trên cluster và đám mây.
   - **WDL/Cromwell, CWL**: phổ biến trong các dự án lớn và Broad Institute.
3. **Pipeline cộng đồng đã chuẩn hoá:** **nf-core** cung cấp hàng trăm pipeline Nextflow được kiểm thử, như nf-core/rnaseq, nf-core/sarek (gọi biến dị), nf-core/scrnaseq.

## 4.3. Vì sao pipeline quan trọng?

- **Tái lập (reproducibility):** cố định phiên bản phần mềm bằng Conda, Docker hoặc Singularity, nên người khác chạy lại ra đúng kết quả.
- **Mở rộng:** chạy cùng một quy trình cho 10 hay 10.000 mẫu, trên máy tính cá nhân, cluster HPC hay đám mây.
- **Chạy tiếp khi lỗi:** workflow manager chỉ chạy lại bước bị lỗi, không chạy lại từ đầu.
- **Kiểm toán:** ghi lại đầy đủ lệnh, tham số, phiên bản – điều kiện bắt buộc trong xét nghiệm lâm sàng và công bố khoa học.

**Điểm yếu:** pipeline cứng nhắc. Gặp dữ liệu khác thường (định dạng lạ, mẫu hỏng, câu hỏi mới) thì nó không tự thích nghi; con người phải sửa.

## 4.4. LLM, chatbot, assistant và agent tham gia vào pipeline ở đâu?

AI không thay pipeline mà bám vào nó ở **bốn vị trí**: trước khi chạy (thiết kế, cấu hình), trong khi chạy (một bước xử lý), khi có sự cố (gỡ lỗi), và sau khi chạy (diễn giải, báo cáo). Mỗi loại hệ thống hợp với một vai trò khác nhau.

| Hệ thống | Vai trò với pipeline | Ví dụ cụ thể với pipeline RNA-seq ở mục 4.1 |
| --- | --- | --- |
| LLM (như một bước bên trong pipeline) | Một công cụ xử lý cố định trong chuỗi, nhận đầu vào xác định và trả đầu ra theo định dạng định sẵn | Bước 7 thêm vào: LLM đọc danh sách con đường làm giàu và viết đoạn tóm tắt kết quả cho từng mẫu; hoặc LLM chuẩn hoá bảng thông tin mẫu (metadata) ghi lộn xộn trước bước 1 |
| Chatbot | Hỏi đáp kiến thức và tài liệu xung quanh pipeline, không chạm vào dữ liệu | "Tham số `--aligner star_salmon` của nf-core/rnaseq nghĩa là gì?"; chatbot RAG trên tài liệu nội bộ của core facility về cách nộp mẫu và đọc báo cáo MultiQC |
| AI assistant | Giúp người dùng viết, sửa, cấu hình và diễn giải, người dùng duyệt từng bước | Viết Snakefile hoặc file cấu hình Nextflow từ mô tả bằng lời; tạo samplesheet.csv từ tên file FASTQ; đọc nhật ký lỗi và chỉ ra nguyên nhân; đọc kết quả DESeq2 và vẽ thêm biểu đồ |
| AI agent | Điều phối cả pipeline: chọn, cấu hình, chạy, theo dõi, xử lý lỗi và báo cáo | Nhận mục tiêu "phân tích RNA-seq chuột trong thư mục này", tự chọn nf-core/rnaseq, tải bộ gen tham chiếu đúng phiên bản, khởi chạy; khi bước STAR thiếu bộ nhớ thì tự tăng tài nguyên và chạy lại; cuối cùng đọc MultiQC, cảnh báo mẫu kém và viết báo cáo |

**Theo vòng đời của một pipeline:**

1. **Thiết kế:** assistant hoặc agent giúp chọn công cụ, viết mã workflow, viết test – phần mà trước đây tốn nhiều ngày nhất.
2. **Chuẩn bị dữ liệu:** LLM chuẩn hoá metadata, kiểm tra tên mẫu, phát hiện thiếu file.
3. **Thực thi:** pipeline chạy như bình thường, có thể chứa vài bước dùng LLM với đầu ra được kiểm tra định dạng.
4. **Giám sát và gỡ lỗi:** agent đọc nhật ký, phân loại lỗi (thiếu bộ nhớ, sai đường dẫn, sai định dạng), sửa và chạy lại phần lỗi.
5. **Diễn giải và báo cáo:** assistant hoặc agent đọc kết quả, tra cứu chức năng gen, viết báo cáo; chatbot trả lời câu hỏi của người đọc báo cáo.

**Nguyên tắc khi đưa AI vào pipeline:**

- **Giữ phần tính toán cốt lõi xác định:** căn chỉnh, đếm, thống kê do công cụ đã kiểm chứng làm, không để LLM "tính" thay.
- **Ghi lại mọi thứ AI thay đổi:** tham số agent đã chỉnh, phiên bản mô hình, prompt đã dùng – để vẫn tái lập được.
- **Kiểm tra đầu ra của LLM:** ép định dạng (ví dụ JSON theo schema), so khớp với dữ liệu gốc, không chấp nhận tên gen hay số liệu không có trong kết quả.
- **Đặt điểm duyệt của con người** trước khi loại mẫu, đổi tham số thống kê hoặc đưa ra kết luận.

> **Dừng lại suy nghĩ.** Vì sao một phòng xét nghiệm lâm sàng gần như bắt buộc dùng pipeline cố định đã thẩm định, thay vì để một AI agent tự quyết định các bước phân tích cho từng bệnh nhân?

# Phần 5. Giống và khác nhau

**Ý chính:** Chatbot, assistant và agent là ba nấc trên cùng một thang: cùng dùng LLM, khác nhau ở **mức tự chủ và khả năng hành động**. Pipeline đứng ở trục khác: **tự động nhưng không tự chủ** – nó chạy hoàn toàn tự động, nhưng mọi quyết định đã được con người viết sẵn.

## 5.1. Bảng đối chiếu

| Tiêu chí | Chatbot | AI Assistant | AI Agent | Bioinformatics Pipeline |
| --- | --- | --- | --- | --- |
| Người dùng giao gì | Một câu hỏi | Một việc cụ thể | Một mục tiêu | Dữ liệu đầu vào và tham số |
| Ai quyết định các bước | Không có bước nào | Người dùng, từng bước | LLM tự quyết định | Lập trình viên, viết sẵn từ trước |
| Bộ não | LLM (hoặc luật) | LLM | LLM | Không cần AI; các phần mềm chuyên dụng |
| Dùng công cụ | Không | Có, vài công cụ mỗi lượt | Có, nhiều công cụ qua nhiều vòng | Mỗi bước là một công cụ cố định |
| Bộ nhớ | Trong một cuộc trò chuyện | Có thể nhớ qua nhiều cuộc | Nhớ tiến trình nhiệm vụ, ghi chú | Lưu file trung gian, nhật ký chạy |
| Xử lý tình huống lạ | Trả lời chung chung hoặc bịa | Hỏi lại người dùng | Tự thử cách khác, tự sửa lỗi | Dừng và báo lỗi |
| Tính tái lập | Thấp (câu trả lời thay đổi mỗi lần) | Thấp đến trung bình | Thấp: đường đi có thể khác mỗi lần | Cao: cùng đầu vào cho cùng kết quả |
| Quy mô | Một người một lượt | Một người một việc | Một nhiệm vụ nhiều bước | Hàng nghìn mẫu, chạy song song |
| Rủi ro chính | Ảo giác | Ảo giác, lộ dữ liệu cá nhân | Hành động sai không đảo ngược, chi phí, prompt injection | Lỗi cấu hình lặp lại hàng loạt |
| Ví dụ | Hỏi đáp về quy trình nộp mẫu | Claude/ChatGPT đọc bảng kết quả, vẽ biểu đồ | Agent tự phân tích RNA-seq từ đầu tới báo cáo | nf-core/rnaseq |

## 5.2. Điểm giống nhau

- Ba khái niệm đầu **cùng nền tảng LLM**; nâng cấp từ chatbot lên agent là thêm dần công cụ, bộ nhớ và vòng lặp, không phải đổi mô hình.
- Agent và pipeline **cùng tự động hoá chuỗi nhiều bước**; khác ở chỗ ai quyết định thứ tự các bước.
- Cả bốn đều **cần con người kiểm tra đầu ra** trước khi đưa ra kết luận khoa học.

## 5.3. Ranh giới không tuyệt đối

Trong thực tế, các khái niệm chồng lấn. Một sản phẩm như Claude hay ChatGPT có thể vừa là chatbot (hỏi nhanh), vừa là assistant (đọc file, vẽ biểu đồ), vừa chạy như agent (giao nhiệm vụ dài, tự làm nhiều bước). Ngược lại, một pipeline có thể chứa bước dùng LLM, ví dụ tự viết đoạn tóm tắt kết quả cuối cùng. Vì vậy, hãy hỏi **"ai quyết định bước tiếp theo?"** để xác định hệ thống đang hoạt động ở chế độ nào.

> **Dừng lại suy nghĩ.** Một hệ thống nhận file FASTQ, luôn chạy đúng 6 bước như mục 4.1, nhưng cuối cùng gọi LLM để viết đoạn diễn giải kết quả. Đó là pipeline hay agent? Vì sao?

# Phần 6. Khi nào dùng cái gì?

**Ý chính:** Chọn hệ thống **đơn giản nhất làm được việc**. Càng tự chủ thì càng linh hoạt nhưng càng khó kiểm soát, tốn kém và khó tái lập. Quy trình đã rõ và cần chạy lặp lại thì dùng pipeline; câu hỏi mở và khám phá thì dùng agent.

## 6.1. Bốn câu hỏi để chọn

1. **Chỉ cần câu trả lời bằng chữ?** → Chatbot.
2. **Cần làm việc với tài liệu, dữ liệu của tôi, nhưng tôi muốn tự quyết từng bước?** → AI assistant.
3. **Nhiệm vụ nhiều bước, chưa biết trước chính xác phải làm gì, chấp nhận để AI tự xoay xở?** → AI agent, kèm điểm duyệt của con người.
4. **Quy trình đã chuẩn hoá, chạy cho nhiều mẫu, cần tái lập và kiểm toán?** → Pipeline.

## 6.2. Tình huống mẫu

| Tình huống | Lựa chọn phù hợp | Lý do |
| --- | --- | --- |
| Sinh viên hỏi "Phred score 30 nghĩa là gì?" | Chatbot | Câu hỏi kiến thức đơn lẻ |
| Đọc 5 bài báo mới về một gen và tóm tắt cho buổi họp nhóm | AI assistant | Làm việc trên tài liệu cụ thể, người dùng kiểm soát |
| Viết và sửa script vẽ heatmap cho bảng biểu hiện gen | AI assistant (lập trình) | Người dùng xem từng phiên bản code |
| Khám phá bộ dữ liệu scRNA-seq công khai mới, thử nhiều cách phân cụm | AI agent | Nhiệm vụ mở, nhiều bước, cần thử và sai |
| Gọi biến dị cho 2.000 mẫu exome của một dự án | Pipeline (ví dụ nf-core/sarek) | Quy mô lớn, cần nhất quán và tái lập |
| Xét nghiệm gen lâm sàng trả kết quả cho bệnh nhân | Pipeline đã thẩm định | Yêu cầu pháp lý về tính nhất quán và truy vết |
| Dựng pipeline mới cho một loại dữ liệu chưa có quy trình chuẩn | Agent hoặc assistant giúp viết pipeline, rồi cố định thành pipeline | Kết hợp sự linh hoạt khi thiết kế và tính ổn định khi chạy |

## 6.3. Kết hợp agent với pipeline: xu hướng hiện nay

Cách làm hiệu quả nhất thường không phải chọn một, mà **để agent điều phối pipeline**:

- **Agent chọn và cấu hình pipeline:** người dùng nói "phân tích RNA-seq chuột trong thư mục này", agent đọc dữ liệu, chọn nf-core/rnaseq, điền đúng bộ gen tham chiếu và bảng mẫu, rồi khởi chạy.
- **Pipeline làm phần nặng, có thể tái lập:** căn chỉnh, đếm, thống kê chạy bằng công cụ đã kiểm chứng.
- **Agent xử lý phần ngoại lệ và diễn giải:** đọc lỗi khi pipeline dừng, đề xuất cách sửa; đọc kết quả, tra cứu tài liệu, viết báo cáo.
- **Con người duyệt** ở các điểm quyết định: tham số quan trọng, loại mẫu, kết luận cuối cùng.
- **Skill ghi lại kinh nghiệm:** cách chọn tham số, cách đọc báo cáo, các lỗi thường gặp được đóng gói thành skill (mục 3.5), để lần sau agent làm đúng ngay từ đầu.

Nói ngắn gọn: **pipeline bảo đảm độ tin cậy, agent mang lại sự linh hoạt, con người chịu trách nhiệm khoa học.** Đây cũng là chủ đề trọng tâm của các phần tiếp theo trong khoá học về Agentic AI.

> **Dừng lại suy nghĩ.** Hãy chọn một quy trình phân tích bạn đang làm thủ công. Phần nào nên cố định thành pipeline, phần nào giao cho agent, và bạn sẽ đặt điểm duyệt của con người ở đâu?

# Tổng kết và tự kiểm tra

## Tóm tắt trong bốn câu

1. **Chatbot** trả lời câu hỏi theo từng lượt, không hành động.
2. **AI assistant** thêm bộ nhớ, tài liệu và công cụ, giúp làm từng việc theo yêu cầu của người dùng.
3. **AI agent** nhận mục tiêu, tự lập kế hoạch và lặp vòng suy nghĩ – hành động – quan sát cho tới khi xong.
4. **Bioinformatics pipeline** là chuỗi bước cố định, tự động và tái lập được; kết hợp tốt nhất khi agent điều phối và pipeline thực thi.

## Bảng thuật ngữ

| Thuật ngữ | Nghĩa ngắn gọn |
| --- | --- |
| System prompt | Lời dặn của nhà phát triển, định hình cách LLM cư xử |
| Tool use / function calling | LLM sinh lời gọi có cấu trúc để hệ thống chạy một công cụ |
| MCP | Giao thức mở để kết nối LLM với công cụ và nguồn dữ liệu |
| Skill | Thư mục chứa hướng dẫn quy trình (SKILL.md), script và tài liệu, agent tự nạp khi việc cần đến |
| Progressive disclosure | Nạp dần: chỉ mô tả skill lúc đầu, nạp nội dung đầy đủ khi cần |
| RAG | Truy xuất tài liệu liên quan rồi đưa vào ngữ cảnh |
| ReAct | Vòng lặp xen kẽ suy luận và hành động của agent |
| Human-in-the-loop | Con người duyệt tại các điểm quyết định quan trọng |
| Multi-agent | Nhiều agent chuyên trách phối hợp dưới một agent điều phối |
| Prompt injection | Nội dung độc hại trong dữ liệu cố "ra lệnh" cho LLM |
| Workflow manager | Phần mềm định nghĩa và chạy pipeline (Snakemake, Nextflow) |
| nf-core | Cộng đồng phát triển pipeline Nextflow chuẩn hoá |
| Container | Gói phần mềm kèm môi trường cố định (Docker, Singularity) |
| Reproducibility | Khả năng chạy lại ra đúng kết quả |

## Gợi ý đáp án các hộp "Dừng lại suy nghĩ"

**Phần 1.** Chatbot thuần tuý chỉ giải thích DESeq2 là gì và có thể viết mẫu đoạn code R. Nó không đọc được file, không chạy được code và không thấy kết quả thật; nếu nó "báo kết quả" thì đó là bịa.

**Phần 2.** Câu trả lời tuỳ người học. Việc dễ giao: tóm tắt bài báo, viết nháp email, sửa lỗi script, vẽ biểu đồ. Việc nên giữ lại: quyết định tham số thống kê, đánh giá bản thảo, kết luận khoa học – vì cần chuyên môn và trách nhiệm cá nhân.

**Phần 3.** Kết luận có thể sai lệch có hệ thống nếu mẫu bị loại thuộc riêng một nhóm, làm giảm cỡ mẫu hoặc che giấu một hiện tượng sinh học thật. Quyết định loại mẫu phải minh bạch và do con người duyệt.

**Phần 4.** Xét nghiệm lâm sàng yêu cầu mọi bệnh nhân được phân tích như nhau, quy trình được thẩm định trước và truy vết được. Agent có thể đi những con đường khác nhau mỗi lần chạy, nên không đáp ứng yêu cầu này.

**Phần 5.** Đó vẫn là pipeline: thứ tự các bước do người viết sẵn, không có LLM nào quyết định bước tiếp theo. LLM chỉ là một công cụ ở bước cuối.

**Phần 6.** Câu trả lời mở. Gợi ý: phần chuẩn và lặp lại (kiểm tra chất lượng, căn chỉnh, đếm) nên thành pipeline; phần khám phá và diễn giải giao cho agent; đặt điểm duyệt ở bước chọn tham số, loại mẫu và trước khi kết luận.

## Tài liệu đọc thêm

- Anthropic (2024). [Building effective agents](https://www.anthropic.com/research/building-effective-agents) – phân biệt workflow và agent, các mẫu thiết kế.
- Yao và cs. (2022). [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629).
- [Model Context Protocol](https://modelcontextprotocol.io) – tài liệu chính thức.
- Anthropic (2025). [Equipping agents for the real world with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) – giới thiệu skill và cơ chế nạp dần.
- [Agent Skills](https://agentskills.io) – đặc tả chuẩn mở và danh sách công cụ hỗ trợ.
- [nf-core](https://nf-co.re) – danh mục pipeline tin sinh học chuẩn hoá.
- Mölder và cs. (2021). [Sustainable data analysis with Snakemake](https://doi.org/10.12688/f1000research.29032.2).
