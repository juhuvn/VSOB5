# ChatGPT từ nền tảng đến ứng dụng

*Lộ trình tự học có ví dụ, bài tập và câu hỏi tự kiểm tra*

15/10/2026

**TS. Nguyễn Cường**
Giám đốc khoa học, Công ty LOBI
NCVC, Viện CNTT, VAST

Tài liệu tự học qua các ví dụ bioinformatics, genomics và transcriptomics; dùng dữ liệu giả lập hoặc dữ liệu công khai để luyện cách đặt câu hỏi, phân tích và kiểm chứng.

Cập nhật nội dung: 15/10/2026. Tên tính năng, quyền truy cập và lộ trình sản phẩm có thể thay đổi theo tài khoản, khu vực và workspace.

> **Ý chính**
>
> ChatGPT là sản phẩm để trò chuyện và làm việc với AI. Trong sinh tin học, bạn có thể dùng nó để hiểu thuật ngữ, đọc tài liệu, rà mã hoặc diễn giải bảng kết quả; mô hình vẫn có thể sai, nên không xem đầu ra là kết luận khoa học hay chẩn đoán. Công cụ và không gian làm việc giúp tổ chức từng bước.

Lộ trình gợi ý: học 1–4 để nắm nền tảng; 5–8 để thực hành tính năng và cá nhân hóa; 9 dành cho nhà phát triển; 10–15 để tạo quy trình làm việc an toàn; 16–17 dùng để ôn tập và tra cứu.

Mỗi chương có ví dụ và phần “Thực hành và tự kiểm tra”. Dùng dữ liệu giả lập hoặc công khai được phép sử dụng; ghi lại đầu vào, kết quả và bước kiểm chứng. Các ví dụ không thay thế quy trình khoa học đã được nhóm nghiên cứu phê duyệt.

Cách học: đọc từng chương theo thứ tự; làm yêu cầu mẫu trong tài khoản ChatGPT nếu có thể; tự trả lời câu hỏi cuối chương trước khi xem chương tiếp theo. Không cần hoàn thành toàn bộ trong một lần.

# Mục lục

- [1. Bản đồ các khái niệm](#1-bản-đồ-các-khái-niệm)
- [2. LLM và lựa chọn mô hình](#2-llm-và-lựa-chọn-mô-hình)
- [3. Chatbot, assistant và agent](#3-chatbot-assistant-và-agent)
- [4. Cách giao việc cho ChatGPT](#4-cách-giao-việc-cho-chatgpt)
- [5. Công cụ và khả năng đa phương thức](#5-công-cụ-và-khả-năng-đa-phương-thức)
- [6. Projects, memory và ngữ cảnh](#6-projects-memory-và-ngữ-cảnh)
- [7. Skills trong ChatGPT](#7-skills-trong-chatgpt)
- [8. GPT tùy chỉnh và lộ trình Plugins](#8-gpt-tùy-chỉnh-và-lộ-trình-plugins)
- [9. API và agent dành cho nhà phát triển](#9-api-và-agent-dành-cho-nhà-phát-triển)
- [10. Canvas, artifacts và đầu ra có thể dùng tiếp](#10-canvas-artifacts-và-đầu-ra-có-thể-dùng-tiếp)
- [11. Tác vụ theo lịch và kích hoạt theo sự kiện](#11-tác-vụ-theo-lịch-và-kích-hoạt-theo-sự-kiện)
- [12. Apps và kết nối dịch vụ](#12-apps-và-kết-nối-dịch-vụ)
- [13. Tùy chỉnh trải nghiệm](#13-tùy-chỉnh-trải-nghiệm)
- [14. Riêng tư, an toàn và kiểm chứng](#14-riêng-tư-an-toàn-và-kiểm-chứng)
- [15. Quy trình mẫu từ đầu đến cuối](#15-quy-trình-mẫu-từ-đầu-đến-cuối)
- [16. Từ điển nhanh](#16-từ-điển-nhanh)
- [17. Nguồn tham khảo chính thức](#17-nguồn-tham-khảo-chính-thức)

# 1. Bản đồ các khái niệm

**Sau chương này, bạn có thể:** Nhận ra các lớp chính của ChatGPT và biết khái niệm nào liên quan đến nhu cầu của mình.

Khi dùng ChatGPT, bạn có thể gặp nhiều tên gọi nghe gần giống nhau. Hãy hình dung chúng như các lớp trong một bộ công cụ: mô hình tạo và lập luận trên nội dung; ứng dụng ChatGPT cung cấp giao diện; công cụ giúp tìm kiếm hoặc thao tác; còn project, GPT tùy chỉnh và automation giúp tổ chức cách làm việc.

| **Khái niệm** | **Hiểu ngắn gọn** | **Ví dụ** |
|----|----|----|
| LLM / mô hình | Động cơ AI xử lý đầu vào và tạo phản hồi. | Chọn chế độ phù hợp để giải thích bảng QC hoặc đọc paper. |
| ChatGPT | Ứng dụng trợ lý AI để trò chuyện và dùng tính năng đi kèm. | Nhờ giải thích count matrix, đọc protocol hoặc rà mã R. |
| Chatbot | Tên chung cho hệ thống trao đổi bằng hội thoại. | Bot hỏi đáp SOP và quy ước đặt tên mẫu của phòng lab. |
| Assistant | Trợ lý được hướng dẫn để hỗ trợ người dùng hoặc một nhiệm vụ. | Trợ lý giúp đọc bảng biến thể theo checklist của nhóm. |
| Agent | Hệ thống có thể lập kế hoạch nhiều bước và dùng công cụ trong phạm vi được cấp. | Tra annotation, lấy nguồn và tạo bản nháp báo cáo. |
| Project | Không gian gom chat, tệp và chỉ dẫn quanh một mục tiêu. | Project phân tích RNA-seq đáp ứng stress. |
| GPT tùy chỉnh | Phiên bản ChatGPT được cấu hình cho mục đích cụ thể. | Trợ lý giải thích thuật ngữ genomics theo tài liệu nhóm. |
| API | Cách nhà phát triển tích hợp mô hình vào ứng dụng riêng. | Cổng nghiên cứu tra gene annotation qua dịch vụ được phê duyệt. |

> **Ví dụ phân lớp**
>
> **Yêu cầu mẫu:** “Tóm tắt kết quả kiểm tra chất lượng của bộ RNA-seq giả lập này và cho biết bước nào cần kiểm tra tiếp.”
>
> **Cách làm / đầu ra mong đợi:** ChatGPT là giao diện giao việc; mô hình diễn giải đầu vào; tệp FASTQ hoặc bảng QC cung cấp dữ liệu; project lưu thiết kế thí nghiệm và quy ước đặt tên; công cụ phân tích tạo số liệu. Xác minh số liệu bằng pipeline gốc, không suy ra cơ chế sinh học chỉ từ bản tóm tắt.

### Thực hành và tự kiểm tra

**Thực hành:** Chọn một tác vụ như đọc FASTQ, tra gene annotation hoặc tổng hợp paper. Vẽ sơ đồ ứng dụng, mô hình, dữ liệu, công cụ và điểm cần nhà nghiên cứu xác nhận.

**Tự hỏi:** Bạn có thể giải thích sự khác nhau giữa ChatGPT, mô hình, project và API bằng ví dụ riêng không?

# 2. LLM và lựa chọn mô hình

**Sau chương này, bạn có thể:** Hiểu mô hình làm gì, giới hạn ở đâu và chọn mô hình theo việc cần làm.

LLM là viết tắt của mô hình ngôn ngữ lớn. Mô hình nhận văn bản, hình ảnh, âm thanh hoặc dữ liệu khác tùy khả năng, rồi dự đoán và tạo nội dung tiếp theo. Mô hình có thể giải thích, viết, phân loại, tóm tắt, dịch hoặc hỗ trợ suy luận; nhưng câu trả lời vẫn có thể sai.

Không cần chọn mô hình mạnh nhất cho mọi việc. Hãy cân nhắc độ khó, độ mới của thông tin, định dạng đầu vào và mức độ chính xác cần thiết. Danh sách mô hình, giới hạn và quyền truy cập có thể đổi theo gói, khu vực và thời điểm.

| **Nhu cầu** | **Cách chọn thực tế** |
|----|----|
| Giải thích thuật ngữ | Yêu cầu giải thích TPM và raw counts cho người mới; nhờ kiểm tra bằng tài liệu nguồn. |
| Rà metadata RNA-seq | Dùng lựa chọn có khả năng xử lý tệp/bảng; cung cấp quy ước cột và yêu cầu báo lỗi. |
| Cần dữ kiện hiện tại | Tìm phiên bản mới của reference genome hoặc công cụ; ưu tiên tài liệu chính thức và ghi ngày. |
| Làm việc với ảnh, âm thanh, tệp | Kiểm tra khả năng đa phương thức trên mô hình và giao diện đang dùng. |
| Diễn giải kết quả omics | Chia bước; kiểm tra design, replicate, phương pháp và xác minh với output gốc. |

> **So sánh mô hình**
>
> **Yêu cầu mẫu:** “Dùng bộ câu hỏi nhỏ để giải thích FASTQ, BAM và VCF; với mỗi câu, trích phần hỗ trợ từ tài liệu tôi đưa.”
>
> **Cách làm / đầu ra mong đợi:** Thử cùng yêu cầu trên các lựa chọn khả dụng. So sánh độ chính xác thuật ngữ, khả năng bám nguồn và mức độ thừa nhận điều chưa biết. Đây là đánh giá tiện ích cho tác vụ học tập, không phải benchmark khoa học tổng quát.

### Thực hành và tự kiểm tra

**Thực hành:** Thử nhờ giải thích thuật ngữ RNA-seq và nhờ rà một bảng metadata có lỗi giả lập. Ghi lại độ chính xác và điều cần đối chiếu với nguồn gốc.

**Tự hỏi:** Với một câu hỏi cần tin tức mới, bạn sẽ làm gì để kiểm chứng câu trả lời?

# 3. Chatbot, assistant và agent

**Sau chương này, bạn có thể:** Phân biệt hội thoại, trợ lý được cấu hình và hệ thống tự thực hiện nhiều bước.

Chatbot nhấn mạnh giao diện hội thoại; assistant nhấn mạnh vai trò hỗ trợ; agent nhấn mạnh khả năng tự điều phối một chuỗi bước và dùng công cụ. Một hệ thống có thể mang cả ba đặc điểm. Ranh giới quan trọng nằm ở quyền hạn và mức tự chủ, không chỉ ở tên gọi.

| **Mức công việc** | **Phù hợp khi** | **Ví dụ** |
|----|----|----|
| Hội thoại | Cần giải đáp hoặc tạo một đầu ra ngay. | Giải thích khác nhau giữa reads, counts và TPM. |
| Assistant có cấu hình | Nhiệm vụ lặp lại, có quy tắc và tài liệu tham khảo. | Rà VCF theo checklist, báo thiếu genome build. |
| Agent có công cụ | Cần nhiều bước, truy cập công cụ và theo dõi trạng thái. | Tìm paper, trích phương pháp, lập bảng tổng hợp có nguồn. |

> **Từ câu hỏi đến agent**
>
> **Yêu cầu mẫu:** “Mỗi tuần rà các bài báo mới về single-cell RNA-seq trong một chủ đề cụ thể, tóm tắt phương pháp và gắn liên kết nguồn.”
>
> **Cách làm / đầu ra mong đợi:** Bước đầu: tự chạy tìm kiếm và kiểm tra từng bài. Bước cao hơn: thiết kế agent với nguồn dữ liệu, truy vấn, tiêu chí lọc, mẫu tóm tắt và bước duyệt của người nghiên cứu. Không coi thứ hạng hay tóm tắt tự động là đánh giá chất lượng nghiên cứu.

### Thực hành và tự kiểm tra

**Thực hành:** Chia workflow RNA-seq từ FASTQ đến báo cáo thành các bước; đánh dấu nơi phần mềm chuyên dụng chạy, nơi ChatGPT chỉ hỗ trợ và nơi chuyên gia cần duyệt.

**Tự hỏi:** Điều gì khiến một tác vụ cần agent thay vì một prompt thông thường?

# 4. Cách giao việc cho ChatGPT

**Sau chương này, bạn có thể:** Viết yêu cầu có mục tiêu, bối cảnh, đầu vào, giới hạn và định dạng đầu ra.

Một yêu cầu tốt cho biết bạn muốn đạt kết quả gì, ai sẽ dùng kết quả, đầu vào nào cần xét, ràng buộc gì và muốn nhận đầu ra ở dạng nào. Nếu chưa biết đầy đủ, yêu cầu ChatGPT hỏi những câu làm rõ có ảnh hưởng đáng kể.

| **Thành phần** | **Câu hỏi gợi ý** | **Ví dụ** |
|----|----|----|
| Mục tiêu | Bạn muốn hoàn thành việc gì? | Rà cấu trúc metadata RNA-seq. |
| Bối cảnh | Ai đọc, tình huống ra sao? | Người học bioinformatics mới làm quen bulk RNA-seq. |
| Đầu vào | Dựa trên dữ liệu nào? | Count matrix, metadata và design đã cung cấp. |
| Ràng buộc | Điều gì phải hoặc không được làm? | Không suy luận nhân quả; báo thiếu replicate/design. |
| Định dạng | Muốn nhận kết quả thế nào? | Bảng QC, lỗi, bằng chứng và câu hỏi cần xác nhận. |

> **Prompt trước và sau**
>
> **Yêu cầu mẫu:** “Phân tích RNA-seq.”
>
> **Cách làm / đầu ra mong đợi:** Tôi mới học transcriptomics. Hãy giải thích bảng count matrix và metadata tôi tải lên: xác định hàng/cột, kiểm tra mẫu có khớp mã không, nêu các giả định và lỗi định dạng có thể thấy. Chỉ mô tả QC; không kết luận gene khác biệt biểu hiện nếu chưa biết thiết kế, số lần lặp và phương pháp thống kê.

Làm theo vòng lặp: yêu cầu bản nháp → đọc và chỉ ra điểm cần sửa → cung cấp thêm dữ kiện → yêu cầu sửa theo tiêu chí → kiểm tra kết quả cuối. Với việc lớn, chia thành các bước như lập dàn ý, xác nhận dữ kiện, viết bản nháp và rà soát.

> **Tạo tài liệu học**
>
> **Yêu cầu mẫu:** “Giải thích sự khác nhau giữa genome, transcriptome và proteome cho sinh viên năm nhất bằng một ví dụ tế bào; sau đó tạo 5 câu hỏi tự kiểm tra.”
>
> **Cách làm / đầu ra mong đợi:** Yêu cầu xác định người học, phạm vi và định dạng. Người học tự trả lời trước, rồi đối chiếu giải thích với giáo trình hoặc nguồn được dẫn.

### Thực hành và tự kiểm tra

**Thực hành:** Viết lại yêu cầu “phân tích gene” thành prompt nêu organism, đầu vào, mục tiêu, design/contrast, định dạng và giới hạn diễn giải. Thử bằng dữ liệu giả lập.

**Tự hỏi:** Bạn đã nêu rõ nguồn dữ liệu và tiêu chí hoàn thành chưa?

# 5. Công cụ và khả năng đa phương thức

**Sau chương này, bạn có thể:** Chọn đúng khả năng cho web, nghiên cứu, tệp, hình ảnh, voice hoặc Canvas.

Công cụ mở rộng những gì ChatGPT có thể làm ngoài việc trả lời dựa trên nội dung cuộc trò chuyện. Tên công cụ, quyền truy cập và cách mở có thể khác theo gói, khu vực, model và workspace. Hãy chọn theo đầu việc, rồi kiểm tra nguồn hoặc đầu ra.

| **Khả năng** | **Dùng khi** | **Ví dụ yêu cầu** |
|----|----|----|
| Tìm kiếm web | Cần thông tin mới hoặc nguồn cụ thể. | Tìm tài liệu phiên bản mới nhất của công cụ bioinformatics; dẫn tài liệu chính thức. |
| Deep Research | Câu hỏi nhiều bước cần tổng hợp nhiều nguồn. | Tổng hợp các phương pháp single-cell RNA-seq từ review và paper gốc, dẫn nguồn. |
| Tệp và Data Analysis | Cần đọc tài liệu, tính toán hoặc trực quan hóa dữ liệu. | Tính library size từ count matrix giả lập và vẽ QC plot. |
| Ảnh và tạo ảnh | Cần hiểu hình ảnh hoặc tạo/chỉnh sửa hình minh họa. | Đọc sơ đồ workflow trong ảnh; tạo hình minh họa cấu trúc DNA cho bài giảng. |
| Voice | Muốn trao đổi bằng giọng nói hoặc luyện hội thoại. | Luyện giải thích RNA-seq bằng lời cho nhóm liên ngành. |
| Canvas | Cần cùng viết, sửa hoặc gỡ lỗi nội dung dài. | Mở bản nháp trong Canvas, rút gọn đoạn 2 và giữ nguyên luận điểm. |

Tìm kiếm web phù hợp với câu hỏi cập nhật đơn giản; Deep Research dành cho việc cần lập kế hoạch nghiên cứu, đọc nhiều nguồn và tổng hợp thành báo cáo có dẫn nguồn. Khi dùng tệp hoặc kết quả phân tích, hãy nêu rõ cột, định nghĩa và đơn vị cần dùng. Với kết quả quan trọng, mở nguồn và kiểm tra lại con số.

> **Chọn công cụ**
>
> **Yêu cầu mẫu:** “Tìm hướng dẫn chính thức mới nhất của công cụ aligner X và so sánh với protocol PDF tôi tải lên. Ghi phiên bản, ngày, tham số khác nhau và trích đoạn hỗ trợ; nếu không xác định được phiên bản, nêu rõ.”
>
> **Cách làm / đầu ra mong đợi:** Tìm web cho tài liệu hiện hành, dùng PDF làm nguồn đối chiếu. Nếu cần tổng hợp nhiều paper hoặc protocol, cân nhắc Deep Research. Mở từng nguồn và kiểm tra đúng phiên bản trước khi áp dụng vào pipeline.

> **Phân tích dữ liệu**
>
> **Yêu cầu mẫu:** “Từ count matrix và metadata giả lập, kiểm tra tên mẫu, số gene bằng 0, tổng counts mỗi mẫu và các giá trị thiếu. Tạo bảng QC và biểu đồ thư viện; chưa chạy kiểm định differential expression.”
>
> **Cách làm / đầu ra mong đợi:** Yêu cầu nêu rõ các phép kiểm tra và giới hạn suy luận. Đối chiếu tổng counts bằng R/Python hoặc pipeline gốc; QC không tự chứng minh chất lượng sinh học hay quan hệ nhân quả.

### Thực hành và tự kiểm tra

**Thực hành:** Dùng tài liệu protocol chính thức hoặc count matrix giả lập. Chọn web, tệp hay Data Analysis; kiểm tra một tham số hoặc con số trong nguồn gốc.

**Tự hỏi:** Khi nào cần Deep Research thay vì tìm kiếm web thông thường?

# 6. Projects, memory và ngữ cảnh

**Sau chương này, bạn có thể:** Tổ chức công việc dài hạn và hiểu vai trò của project, memory, tài liệu nguồn.

Project giúp tập hợp hội thoại, tệp và hướng dẫn quanh một mục tiêu kéo dài. Thay vì nhắc lại bối cảnh mỗi lần, bạn có thể đặt chỉ dẫn cho project và lưu các nguồn hữu ích. Memory phục vụ cá nhân hóa theo cài đặt; nó không phải kho lưu trữ đầy đủ hay thay thế việc quản lý tài liệu.

- Dùng project khi công việc có nhiều phiên, nhiều nguồn hoặc quy tắc ổn định.

- Đặt hướng dẫn ngắn và có thể hành động: vai trò, đối tượng, giọng văn, định dạng.

- Dùng tên tệp và nguồn rõ ràng; yêu cầu ChatGPT nêu tài liệu nào hỗ trợ kết luận.

- Kiểm tra thiết lập memory và quyền riêng tư trong tài khoản/workspace.

> **Project phân tích RNA-seq**
>
> **Yêu cầu mẫu:** “Tạo project “Đáp ứng lạnh ở Arabidopsis” bằng dữ liệu công khai hoặc giả lập. Thêm design, metadata, protocol và từ điển cột. Trong chỉ dẫn: “Chỉ mô tả kết quả từ tệp; gắn tên nguồn; không khẳng định quan hệ nhân quả; báo thiếu lặp hoặc lệch thiết kế.””
>
> **Cách làm / đầu ra mong đợi:** Tách chat theo việc như kiểm tra metadata, đọc QC và diễn giải bảng kết quả. Ghi rõ reference genome, phiên bản annotation và nguồn dữ liệu để giảm nhầm lẫn.

### Thực hành và tự kiểm tra

**Thực hành:** Tạo project cho bài tập transcriptomics; thêm metadata mẫu, design và glossary. Hỏi về tên mẫu để xem ChatGPT có bám đúng tệp không.

**Tự hỏi:** Thông tin nào nên để trong hướng dẫn project, thông tin nào nên cung cấp theo từng lần?

# 7. Skills trong ChatGPT

**Sau chương này, bạn có thể:** Nhận biết khi nào quy trình lặp lại đủ ổn định để đóng gói thành skill.

Skill là một quy trình có thể tái sử dụng, gồm hướng dẫn và có thể kèm ví dụ, tài liệu hoặc mã. Khi skill được cài đặt, ChatGPT có thể tự chọn dùng khi phù hợp hoặc người dùng có thể gọi theo cách giao diện hỗ trợ. Skills trong ChatGPT hiện dành cho một số workspace đủ điều kiện; cách tạo, cài đặt và chia sẻ tùy quyền quản trị.

| **Thành phần** | **Ví dụ skill kiểm tra tài liệu** |
|----|----|
| Chỉ dẫn | Đọc tài liệu theo checklist tuân thủ đã cho. |
| Tài nguyên | Checklist, mẫu báo cáo và định nghĩa thuật ngữ. |
| Quy trình | Trích vấn đề; gắn vị trí; phân loại mức độ; nêu câu hỏi cần làm rõ. |
| Kiểm tra | Thử với tài liệu đạt chuẩn, có lỗi và thiếu thông tin. |

> **Khi nào nên tạo skill**
>
> **Yêu cầu mẫu:** “Mỗi lần nhận count matrix, kiểm tra cấu trúc cột, khớp sample ID với metadata, đếm giá trị thiếu/âm, tính library size và xuất danh sách vấn đề; không tự sửa dữ liệu gốc.”
>
> **Cách làm / đầu ra mong đợi:** Nếu nhóm lặp quy trình QC và có checklist ổn định, skill có thể đóng gói các bước và định nghĩa cột. Thử trên ma trận đúng, lỗi tên mẫu và trường hợp thiếu metadata trước khi dùng thường xuyên.

Phân biệt nhanh: prompt là yêu cầu cho một lần làm việc; custom instructions đặt sở thích chung; skill đóng gói quy trình tái sử dụng; app kết nối dịch vụ ngoài; plugin có thể kết hợp hướng dẫn tái sử dụng với app. Quyền và tên gọi có thể khác theo sản phẩm.

### Thực hành và tự kiểm tra

**Thực hành:** Viết checklist QC count matrix gồm khớp sample ID, missing values, counts âm, library size và báo lỗi. Thử với ma trận chuẩn và ma trận lỗi.

**Tự hỏi:** Skill của bạn có nêu đầu vào, đầu ra, bước kiểm tra và trường hợp ngoại lệ không?

# 8. GPT tùy chỉnh và lộ trình Plugins

**Sau chương này, bạn có thể:** Hiểu cách cấu hình trợ lý chuyên biệt và chuẩn bị kiểm thử hoặc chuyển đổi khi cần.

GPT tùy chỉnh là trợ lý được cấu hình bằng hướng dẫn, tài liệu kiến thức và một số khả năng. Quyền tạo mới hiện phụ thuộc loại tài khoản, gói và workspace; tài liệu OpenAI hiện nêu việc tạo GPT mới không khả dụng trên tài khoản cá nhân Free, Go, Plus và Pro, trong khi một số workspace Business, Enterprise và Edu có thể tạo theo quyền quản trị. OpenAI đang công bố lộ trình chuyển GPT tùy chỉnh sang Plugins; mốc di chuyển và ngày áp dụng có thể khác theo tài khoản hoặc workspace. Hãy kiểm tra thông báo trong sản phẩm trước khi xây quy trình mới hoặc di chuyển GPT đang dùng.

Khi đang dùng GPT tùy chỉnh, lưu lại mục tiêu, chỉ dẫn, tệp tham khảo, app/action đã kết nối, các câu hỏi kiểm tra và những người cần quyền truy cập. Sau khi di chuyển, so sánh kết quả của plugin thay thế với các prompt quen thuộc; quyền chia sẻ và tích hợp có thể không tự chuyển nguyên vẹn.

| **Phần cấu hình** | **Ví dụ trợ lý biên tập** |
|----|----|
| Mục tiêu | Giải thích kết quả bioinformatics cho nhóm nghiên cứu. |
| Quy tắc | Tách quan sát khỏi diễn giải; không thêm số liệu hoặc paper không có nguồn. |
| Kiến thức | Glossary, protocol và quy ước đặt tên mẫu đã được nhóm duyệt. |
| Công cụ/kết nối | Chỉ bật nguồn cần thiết; xác nhận quyền. |
| Kiểm thử | Thử với dữ kiện đầy đủ, thiếu và mâu thuẫn. |

> **Mô tả quy trình trợ lý**
>
> **Yêu cầu mẫu:** “Hỗ trợ đọc bảng kết quả RNA-seq cho sinh viên. Chỉ dùng tệp và nguồn được cung cấp; giải nghĩa cột; nêu phép kiểm tra; đánh dấu [CẦN XÁC NHẬN] nếu thiếu design hoặc đơn vị; không tự đặt ngưỡng significance hay khẳng định cơ chế.”
>
> **Cách làm / đầu ra mong đợi:** Nêu nhiệm vụ, nguồn, giới hạn và định dạng. Kiểm thử với bảng đủ metadata, bảng thiếu nhóm đối chứng và bảng có tên mẫu không khớp.

### Thực hành và tự kiểm tra

**Thực hành:** Soạn chỉ dẫn cho trợ lý giải thích VCF chỉ từ tài liệu được cung cấp; tạo một ví dụ đủ build/reference và một ví dụ thiếu genome build để trợ lý hỏi lại.

**Tự hỏi:** Bạn đã ghi rõ nguồn kiến thức, giới hạn và cách xử lý dữ kiện thiếu chưa?

# 9. API và agent dành cho nhà phát triển

**Sau chương này, bạn có thể:** Phân biệt dùng ChatGPT trực tiếp với tích hợp AI vào phần mềm.

Nếu muốn đưa AI vào website hoặc phần mềm của riêng mình, nhà phát triển gọi API. Đây là hướng khác với việc cấu hình trợ lý để dùng trực tiếp trong ChatGPT. “Assistant” trong ngôn ngữ thường có thể chỉ một trợ lý; còn Assistants API là tên một API cụ thể đã ngừng hoạt động ngày 26/08/2026. Với dự án mới, tài liệu OpenAI hiện khuyến nghị Responses API; Conversations API có thể giữ trạng thái hội thoại. Agents SDK hoặc Agents API phù hợp khi cần điều phối agent nhiều bước, tùy nơi muốn chạy và cách quản lý trạng thái.

| **Nhu cầu nhà phát triển** | **Điểm bắt đầu** |
|----|----|
| Gọi mô hình và tự quản lý luồng | Responses API. |
| Lưu trạng thái hội thoại qua nhiều lượt | Responses API kết hợp Conversations API hoặc cơ chế state phù hợp. |
| Tự xây agent trong ứng dụng | Agents SDK với công cụ và luồng do ứng dụng kiểm soát. |
| Dùng runtime agent được OpenAI quản lý | Agents API; kiểm tra kỹ môi trường và yêu cầu dữ liệu. |
| Nhúng trải nghiệm chat vào sản phẩm | ChatKit hoặc giao diện tự xây cùng API. |

> **Ví dụ chọn API**
>
> **Yêu cầu mẫu:** “Thiết kế trợ lý trong cổng nghiên cứu để tìm gene trong annotation đã duyệt, truy vấn tài liệu nội bộ và trả lời kèm gene ID, phiên bản genome, nguồn và mức không chắc chắn. Chỉ tạo bản nháp; không tự ghi annotation vào cơ sở dữ liệu.”
>
> **Cách làm / đầu ra mong đợi:** Responses API có thể phù hợp cho tích hợp trực tiếp; Agents SDK cho luồng nhiều bước do ứng dụng kiểm soát. Phân quyền dữ liệu, log truy vấn và bước xác nhận của nhà nghiên cứu là phần của thiết kế.

# 10. Canvas, artifacts và đầu ra có thể dùng tiếp

Canvas là không gian làm việc tương tác để cùng viết, chỉnh sửa hoặc gỡ lỗi với ChatGPT. “Artifact” có thể được dùng ở một số giao diện để chỉ đầu ra riêng có thể xem hoặc tiếp tục chỉnh sửa, nhưng đừng mặc định đây là tên tính năng có sẵn ở mọi tài khoản. Hãy gọi rõ loại đầu ra và nơi bạn muốn dùng nó.

| **Muốn làm gì** | **Cách yêu cầu** |
|----|----|
| Sửa một phần bản thảo | Mở/tiếp tục trên Canvas; sửa đoạn 2, giữ luận điểm và nêu thay đổi. |
| Tạo tệp | Nêu định dạng: DOCX, PDF, CSV, HTML hoặc định dạng phù hợp. |
| Tạo mã hoặc trang tương tác | Nêu người dùng, thao tác, dữ liệu đầu vào và cách kiểm tra. |
| Phân tích hoặc trực quan hóa | Nêu câu hỏi, phép tính, đơn vị và dạng biểu đồ mong muốn. |

> **Tạo đầu ra có thể chỉnh sửa**
>
> **Yêu cầu mẫu:** “Tạo template báo cáo RNA-seq gồm: mô tả cohort/mẫu, QC, phương pháp, bảng kết quả, giới hạn diễn giải và nguồn. Dùng dữ liệu giả lập, ghi rõ chỗ cần điền, xuất thành DOCX có thể chỉnh sửa.”
>
> **Cách làm / đầu ra mong đợi:** Yêu cầu định dạng và mục đích sử dụng rõ ràng. Rà lại thuật ngữ, phiên bản phần mềm và mọi số liệu giả lập trước khi dùng làm báo cáo thật.

### Thực hành và tự kiểm tra

**Thực hành:** Vẽ luồng cho dịch vụ tra cứu gene annotation: nhà nghiên cứu → ứng dụng → API/database được duyệt → câu trả lời kèm accession/version → bước xác nhận. Đánh dấu dữ liệu được lưu.

**Tự hỏi:** Bạn cần tự kiểm soát luồng hay cần runtime agent? Căn cứ chọn là gì?

# 11. Tác vụ theo lịch và kích hoạt theo sự kiện

**Sau chương này, bạn có thể:** Phân biệt chạy theo thời gian với chạy khi có sự kiện; xác định bước kiểm soát cần thiết.

Tác vụ theo lịch chạy tại thời điểm hoặc nhịp định trước, phù hợp với nhắc việc, bản tin định kỳ hoặc kiểm tra lặp lại. Tác vụ kích hoạt theo sự kiện bắt đầu khi có hoạt động được hỗ trợ trong app, chẳng hạn email hoặc thay đổi trên hệ thống liên kết. Không phải mọi app hay tài khoản đều hỗ trợ mọi loại kích hoạt. Codex Automations là tính năng riêng của Codex, không đồng nghĩa Scheduled tasks trong ChatGPT.

> **1.** Viết rõ việc cần làm, nguồn dữ liệu, đầu ra và tiêu chí báo.
>
> **2.** Chọn lịch chạy hoặc sự kiện phù hợp trong phần Scheduled/tác vụ nếu có.
>
> **3.** Kiểm tra tài khoản app đã kết nối, quyền đọc/ghi và múi giờ.
>
> **4.** Thử chạy một lần; xem kết quả, nguồn và hành động đã thực hiện.
>
> **5.** Xem lại định kỳ; tạm dừng hoặc xóa khi không còn cần.

> **Theo lịch**
>
> **Yêu cầu mẫu:** “Mỗi thứ Sáu lúc 16 giờ, nhắc tôi kiểm tra checklist phân tích tuần này: metadata, QC, phiên bản genome/annotation và backup kết quả. Chỉ nhắc; không chạy hoặc thay đổi pipeline.”
>
> **Cách làm / đầu ra mong đợi:** Tác vụ theo lịch phù hợp để nhắc việc. Dữ liệu thực nghiệm, pipeline và nơi lưu kết quả vẫn cần được kiểm tra thủ công theo quy trình lab.

> **Theo sự kiện**
>
> **Yêu cầu mẫu:** “Khi có file metadata mới trong thư mục dự án, tạo bản tóm tắt các sample ID mới, trường bị thiếu và tên file; chỉ báo cáo, không sửa dữ liệu hay khởi chạy phân tích.”
>
> **Cách làm / đầu ra mong đợi:** Đây là tác vụ theo sự kiện nếu dịch vụ lưu trữ và tính năng hỗ trợ. Xem lại quyền truy cập và tránh đưa dữ liệu nhạy cảm vào kết nối chưa được phê duyệt.

### Thực hành và tự kiểm tra

**Thực hành:** Thiết kế nhắc rà soát metadata hoặc trigger báo file mới. Ghi điều kiện chạy, quyền đọc, đầu ra, hành động bị cấm và cách tắt.

**Tự hỏi:** Tác vụ có gửi hoặc thay đổi dữ liệu bên ngoài không? Nếu có, ai duyệt?

# 12. Apps và kết nối dịch vụ

**Sau chương này, bạn có thể:** Kết nối dịch vụ đúng phạm vi và kiểm tra dữ liệu, trích dẫn, hành động được phép.

Apps trong ChatGPT có thể kết nối tới dịch vụ bạn dùng để tìm thông tin, tóm tắt nội dung hoặc thực hiện một số hành động được hỗ trợ. “Connector” thường được dùng như tên chung cho kết nối nguồn dữ liệu; cách gọi và menu thay đổi theo bề mặt sản phẩm. Plugin hiện cũng được OpenAI dùng cho quy trình có thể gộp hướng dẫn tái sử dụng và app, trong đó có lộ trình di chuyển custom GPT được công bố.

> **1.** Mở Settings/Plugins hoặc mục Apps theo giao diện tài khoản.
>
> **2.** Chọn dịch vụ, đọc quyền được yêu cầu và kết nối đúng tài khoản.
>
> **3.** Trong chat hoặc task, chọn app phù hợp; nêu rõ nguồn cần tìm và kết quả cần trả.
>
> **4.** Kiểm tra trích dẫn, dữ liệu được truy cập và mọi hành động ngoài ChatGPT.
>
> **5.** Ngắt kết nối hoặc thu hồi quyền khi không còn nhu cầu.

> **Tìm protocol trong Drive**
>
> **Yêu cầu mẫu:** “Tìm protocol RNA extraction mới nhất trong Drive, nêu tên file, ngày/phiên bản và bước cần chuẩn bị. Nếu có nhiều bản, liệt kê chúng và không tự chọn bản hiện hành.”
>
> **Cách làm / đầu ra mong đợi:** Kết nối Drive nếu app có sẵn và được phép. Kiểm tra quyền, xác nhận với người quản lý lab đâu là SOP đang hiệu lực trước khi làm thí nghiệm.

### Thực hành và tự kiểm tra

**Thực hành:** Nếu workspace cho phép, kết nối kho tài liệu lab chỉ đọc. Tìm SOP RNA extraction, xác minh phiên bản và kiểm tra cách thu hồi quyền.

**Tự hỏi:** Quyền app đang cấp có tương xứng với nhiệm vụ không?

# 13. Tùy chỉnh trải nghiệm

**Sau chương này, bạn có thể:** Chọn đúng phạm vi cho chỉ dẫn chung, project, skill hoặc trợ lý tùy chỉnh.

Tùy chỉnh đặt hướng dẫn ở phạm vi phù hợp: custom instructions cho sở thích chung; project instructions cho một mục tiêu; skill cho quy trình lặp lại; plugin hoặc cấu hình trợ lý cho một trải nghiệm chuyên biệt. Memory có thể cá nhân hóa dựa trên thông tin hữu ích đã lưu, theo cài đặt của tài khoản. Những phần này không thay thế việc cung cấp dữ liệu cụ thể cho từng nhiệm vụ.

> **Chỉ dẫn chung**
>
> **Yêu cầu mẫu:** “Trả lời bằng tiếng Việt, giữ nguyên gene symbol và tên công cụ. Phân biệt dữ kiện trong tệp, diễn giải và giả thuyết. Với thông tin về tool/version, dẫn tài liệu chính thức. Nếu thiếu design, genome build hoặc đơn vị, hỏi lại trước khi kết luận.”
>
> **Cách làm / đầu ra mong đợi:** Thử chỉ dẫn trên một câu hỏi thuật ngữ và một bảng kết quả để xem hướng dẫn có nhất quán mà không áp đặt một kiểu trả lời.

### Thực hành và tự kiểm tra

**Thực hành:** Viết một custom instruction ngắn. Thử trên hai yêu cầu khác nhau để xem nó hữu ích mà không làm câu trả lời thiếu linh hoạt.

**Tự hỏi:** Chỉ dẫn nào áp dụng chung, chỉ dẫn nào chỉ đúng cho một project?

# 14. Riêng tư, an toàn và kiểm chứng

**Sau chương này, bạn có thể:** Đánh giá dữ liệu, quyền truy cập và độ tin cậy trước khi dùng đầu ra.

- Kiểm tra cài đặt dữ liệu, memory, quyền app và chính sách của workspace trước khi đưa dữ liệu vào.

- Chỉ kết nối dịch vụ và cấp quyền cần thiết cho công việc.

- Xác minh dữ kiện quan trọng bằng nguồn gốc; tách dữ kiện, suy luận và điều chưa rõ.

- Trước khi gửi email, đăng nội dung, xóa hoặc sửa dữ liệu bên ngoài, kiểm tra hành động và người nhận.

- Không dựa riêng vào đầu ra AI trong lĩnh vực có hậu quả lớn; dùng quy trình chuyên gia hoặc kiểm tra độc lập.

- Khi chia sẻ task, plugin hoặc đầu ra, rà soát nội dung hướng dẫn và quyền truy cập được cấp cho người khác.

> **Rà soát kết quả**
>
> **Yêu cầu mẫu:** “Đọc phần diễn giải gene khác biệt biểu hiện. Lập bảng: khẳng định, số liệu/cột hỗ trợ, phương pháp và ngưỡng đã dùng, mức chắc chắn, điều cần xác nhận. Không bổ sung cơ chế hoặc paper ngoài nguồn.”
>
> **Cách làm / đầu ra mong đợi:** Bảng này giúp người nghiên cứu phát hiện kết luận vượt quá dữ liệu; đối chiếu bảng gốc, thiết kế mẫu và pipeline trước khi đưa vào manuscript.

### Thực hành và tự kiểm tra

**Thực hành:** Dùng bảng “khẳng định – cột/output hỗ trợ – phương pháp – mức chắc chắn – người xác nhận” để rà diễn giải RNA-seq. Chỉ dùng dữ liệu công khai/giả lập nếu chưa được duyệt.

**Tự hỏi:** Bạn có thể chỉ ra điều gì là dữ kiện, suy luận và điều còn chưa biết không?

# 15. Quy trình mẫu từ đầu đến cuối

**Sau chương này, bạn có thể:** Kết hợp project, tệp, prompt, kiểm chứng và bước duyệt thành một quy trình hoàn chỉnh.

Tình huống xuyên suốt: một nhóm nghiên cứu đang học cách phân tích RNA-seq bulk để khảo sát đáp ứng stress ở thực vật bằng dữ liệu công khai hoặc dữ liệu giả lập. Mục tiêu là tạo báo cáo QC và diễn giải có kiểm soát, không suy ra quan hệ nhân quả từ biểu hiện gene đơn thuần.

> **1.** Tạo project “RNA-seq đáp ứng stress”; ghi câu hỏi nghiên cứu, organism, reference genome/build, annotation version và nguồn dữ liệu.
>
> **2.** Tải metadata và bảng counts giả lập hoặc công khai; kiểm tra sample ID, nhóm, batch, replicate và định dạng.
>
> **3.** Yêu cầu ChatGPT lập checklist QC: library size, giá trị thiếu/âm, mẫu lệch và biểu đồ cần xem; yêu cầu nêu phép tính, không tự chạy pipeline nếu chưa được giao.
>
> **4.** Nếu có bảng differential expression, kiểm tra design, contrast, phương pháp, adjusted p-value và gene ID; hỏi rõ điều chưa có trước khi diễn giải.
>
> **5.** Yêu cầu bản nháp kết quả tách “quan sát”, “diễn giải có hỗ trợ” và “giả thuyết cần kiểm chứng”.
>
> **6.** Đối chiếu từng số liệu với output gốc và tài liệu phương pháp; kiểm tra phiên bản tool, genome và annotation.
>
> **7.** Người phụ trách duyệt trước khi đưa vào báo cáo hoặc manuscript; không dùng đầu ra như tư vấn lâm sàng.

> **Prompt phân tích**
>
> **Yêu cầu mẫu:** “Dựa trên metadata, bảng QC và kết quả differential expression giả lập tôi tải lên, tạo báo cáo gồm: dữ liệu/phiên bản, kiểm tra mẫu, quan sát chính, giới hạn và câu hỏi cần xác nhận. Với mỗi nhận xét, ghi tên file/cột hỗ trợ. Không suy luận nhân quả, không gọi gene là biomarker, không tạo trích dẫn. Nếu thiếu design hoặc replicate, dừng diễn giải và liệt kê dữ liệu cần bổ sung.”
>
> **Cách làm / đầu ra mong đợi:** Prompt chỉ rõ nguồn, cấu trúc và giới hạn khoa học. Người học cần kiểm tra bảng gốc, thiết kế thí nghiệm và phương pháp trước khi dùng kết quả.

# 16. Từ điển nhanh

| **Từ** | **Nghĩa thực dụng** |
|----|----|
| Prompt | Yêu cầu hoặc chỉ dẫn cho một lần làm việc. |
| Context / ngữ cảnh | Thông tin liên quan có thể dùng trong lượt làm việc. |
| Hallucination | Thông tin nghe hợp lý nhưng sai hoặc thiếu bằng chứng. |
| Tool / công cụ | Khả năng như tìm web, phân tích dữ liệu hoặc gọi dịch vụ. |
| App / connector | Kết nối ChatGPT với dịch vụ hoặc nguồn dữ liệu. |
| Skill | Quy trình tái sử dụng, có thể gồm chỉ dẫn, ví dụ và tài nguyên. |
| Plugin | Gói trong ChatGPT có thể kết hợp hướng dẫn tái sử dụng và app. |
| Memory | Thông tin có thể được lưu để cá nhân hóa, tùy cài đặt. |
| Scheduled task | Tác vụ chạy theo lịch hoặc một lần trong ChatGPT. |
| Agent | Hệ thống điều phối nhiều bước và công cụ trong phạm vi được cấp. |
| API | Giao diện để phần mềm gọi mô hình hoặc tích hợp chức năng AI. |
| Responses API | API hiện được OpenAI khuyến nghị cho tích hợp mới. |

# 17. Nguồn tham khảo chính thức

Các nguồn dưới đây là trang trợ giúp và tài liệu OpenAI đã đối chiếu khi biên soạn. Những mốc chuyển đổi là kế hoạch tại ngày cập nhật; hãy ưu tiên thông báo mới nhất trong tài khoản hoặc workspace của bạn. Bài tập: mở một liên kết, ghi ngày kiểm tra và đánh dấu nội dung nào phụ thuộc gói hoặc workspace. Khi giao diện tài khoản khác tài liệu, hãy xác minh lại bằng nguồn chính thức mới nhất.

- [Tổng quan khả năng ChatGPT](https://help.openai.com/en/articles/9260256-chatgpt-capabilities-overview)
- [Projects trong ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)
- [GPTs và tạo GPT trong ChatGPT](https://help.openai.com/en/articles/8554397-creating-and-editing-gpts)
- [Lộ trình chuyển custom GPT sang Plugins](https://help.openai.com/en/articles/20001519-custom-gpt-retirement-and-migration-faq)
- [Skills trong ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt)
- [Connected apps trong ChatGPT](https://help.openai.com/en/articles/11487775-connected-apps)
- [Tác vụ theo lịch trong ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt)
- [Responses API](https://developers.openai.com/api/docs/guides/migrate-to-responses)
- [Di chuyển khỏi Assistants API](https://developers.openai.com/api/docs/assistants/migration)

Ghi chú: tài liệu này giải thích các khái niệm ở mức nhập môn. Tên tính năng, quyền truy cập và đường dẫn giao diện có thể khác giữa tài khoản cá nhân, workspace và phiên bản sản phẩm.

### Thực hành và tự kiểm tra

**Thực hành:** Làm thử chuỗi RNA-seq trên bảng giả lập: kiểm tra metadata, yêu cầu báo cáo QC, rà diễn giải output và ghi lại ít nhất một lỗi ChatGPT mắc phải.

**Tự hỏi:** Bạn biết kết luận nào đến từ nguồn nào và ai chịu trách nhiệm duyệt bản cuối không?

# Nhật ký tự học

Sau mỗi buổi học, ghi ngắn gọn điều đã thử và kết quả. Dùng nhật ký để xác định phần cần luyện thêm thay vì chỉ đánh dấu đã đọc.

**Ngày và chương đã học:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Việc tôi đã thử:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Điều ChatGPT làm tốt:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Điều tôi đã kiểm chứng hoặc cần kiểm chứng:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Câu hỏi tôi còn muốn tìm hiểu:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
