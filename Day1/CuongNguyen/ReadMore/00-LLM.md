# Mô hình ngôn ngữ lớn (LLM) – Tài liệu hướng dẫn

13/10/2026

**TS. Nguyễn Cường**
Giám đốc khoa học, Công ty LOBI
NCVC, Viện CNTT, VAST

## Mục tiêu bài học

Sau phần này, người học trả lời được ba câu hỏi: LLM là gì, LLM được huấn luyện ra sao, và nên chọn LLM nào cho công việc của mình.

Cụ thể, người học sẽ:

1. Giải thích được LLM bằng lời của mình, dùng các khái niệm token, dự đoán token tiếp theo và kiến trúc Transformer.
2. Mô tả được các giai đoạn huấn luyện: tiền huấn luyện, tinh chỉnh có giám sát, căn chỉnh theo phản hồi và học tăng cường cho suy luận.
3. Kể tên được các họ LLM chính hiện nay, phân biệt mô hình đóng với mô hình trọng số mở, và biết các tiêu chí để chọn.

**Cách dùng tài liệu.** Mỗi phần có ba lớp: ý chính (đọc trước), giải thích kèm ví dụ, và hộp "Dừng lại suy nghĩ" để tự kiểm tra. Người mới nên đọc tuần tự; người đã biết có thể nhảy thẳng tới Phần 3.

## Phần 1. LLM là gì?

**Ý chính:** LLM (Large Language Model – mô hình ngôn ngữ lớn) là một mạng nơ-ron rất lớn, được huấn luyện để làm đúng một việc: đoán mẩu văn bản tiếp theo. Mọi khả năng khác – trả lời câu hỏi, viết code, tóm tắt bài báo – đều nảy sinh từ việc làm thật giỏi việc đoán đó.

### 1.1. Bắt đầu từ một trò chơi đoán chữ

Hãy hoàn thành câu: "Gen mã hoá protein được phiên mã thành \_\_\_". Hầu hết người học sinh học sẽ điền "mRNA". Bạn làm được vì đã đọc đủ nhiều tài liệu để biết từ nào thường đi sau ngữ cảnh đó.

LLM làm y hệt, nhưng ở quy mô hàng nghìn tỷ từ. Với mỗi ngữ cảnh, mô hình trả ra một **phân phối xác suất** trên toàn bộ từ vựng, ví dụ: mRNA 0,82; RNA 0,11; protein 0,02… Sau đó nó chọn một từ, gắn vào câu, rồi đoán tiếp. Cách sinh lần lượt từng mẩu này gọi là **tự hồi quy (autoregressive)**.

### 1.2. Token – đơn vị mà LLM thực sự "đọc"

LLM không đọc chữ cái hay từ, mà đọc **token**: các mảnh văn bản do một bộ tách (tokenizer) chia ra, thường bằng thuật toán BPE.

- Một token tiếng Anh trung bình khoảng 3/4 từ. Tiếng Việt thường tốn nhiều token hơn cho cùng một ý vì có dấu.
- Mỗi token được ánh xạ thành một **vector nhúng (embedding)** – một dãy vài nghìn con số biểu diễn "nghĩa" của nó.
- **Cửa sổ ngữ cảnh (context window)** là số token tối đa mô hình xem được một lúc, từ vài nghìn ở thế hệ đầu tới hàng trăm nghìn hoặc hơn một triệu token ở các mô hình hiện nay.

**Ví dụ minh hoạ.** Cách tách dưới đây mang tính minh hoạ; mỗi tokenizer cho kết quả hơi khác nhau.

| Câu đầu vào | Cách tách thành token | Số token (xấp xỉ) |
| --- | --- | --- |
| `Gene expression` | `Gene` · `  expression ` | 2 |
| `unbelievable` | `un` · `believ` · `able` | 3 |
| `Heo nái đẻ nhiều con` | `He` · `o` · `  n ` · `ái` · `  đ ` · `ẻ` · `  nhiều ` · `  con ` | 8 |
| `ATGCGTAC` (k-mer, k = 3) | `ATG` · `CGT` · `AC` | 3 |

Ví dụ thứ ba cho thấy tiếng Việt có dấu thường bị cắt vụn, nên tốn token hơn tiếng Anh. Hệ quả thực tế: cùng một tài liệu, bản tiếng Việt chiếm nhiều chỗ trong cửa sổ ngữ cảnh hơn và tốn phí API hơn. Sau khi tách, mỗi token được đổi thành một số hiệu (ID) trong từ vựng, ví dụ `Gene` → một số nguyên cố định (giá trị tuỳ tokenizer), rồi mới tra ra vector embedding.

*Tự thử:* dán một câu bất kỳ vào [OpenAI Tokenizer](https://platform.openai.com/tokenizer) hoặc [Tiktokenizer](https://tiktokenizer.vercel.app) để xem token được tô màu.

*Liên hệ tin sinh học:* chuỗi DNA cũng có thể tách thành token (k-mer hoặc BPE trên nucleotide). Đây chính là ý tưởng của các mô hình ngôn ngữ cho gen như DNABERT hay Nucleotide Transformer.

### 1.3. Kiến trúc Transformer và cơ chế chú ý

Gần như mọi LLM hiện nay dựa trên **Transformer** (bài báo "Attention Is All You Need", Google, 2017). Thành phần cốt lõi là **self-attention (tự chú ý)**: khi xử lý một token, mô hình "nhìn" sang mọi token khác trong ngữ cảnh và quyết định nên chú ý bao nhiêu vào mỗi cái.

Ví dụ: trong câu "Con heo nái này đẻ 14 con vì **nó** có kiểu gen ESR thuận lợi", attention giúp mô hình hiểu "nó" chỉ con heo nái, không phải 14 con.

Một LLM xếp chồng hàng chục tới hàng trăm lớp Transformer. Mỗi lớp gồm attention và một mạng truyền thẳng (feed-forward). Các **tham số** (trọng số) của những lớp này là thứ được học trong huấn luyện; số tham số dao động từ vài tỷ tới hàng nghìn tỷ.

Hai biến thể kiến trúc đáng biết:

- **Dense (đặc):** mọi tham số tham gia tính mỗi token.
- **Mixture of Experts – MoE (hỗn hợp chuyên gia):** mô hình có nhiều "chuyên gia" con, mỗi token chỉ kích hoạt vài chuyên gia. Nhờ vậy tổng tham số rất lớn nhưng chi phí tính toán mỗi token thấp. Nhiều mô hình mở hiện nay (DeepSeek, Qwen, Mixtral…) dùng MoE.

### 1.4. Vì sao gọi là "lớn", và điều gì xảy ra khi lớn lên

"Lớn" ở ba chiều: số tham số, lượng dữ liệu huấn luyện và lượng tính toán. Khi cả ba tăng đồng thời, sai số dự đoán giảm đều đặn theo các **quy luật mở rộng (scaling laws)**. Đồng thời xuất hiện những khả năng không được dạy trực tiếp: dịch thuật, giải toán, viết code, học từ vài ví dụ trong prompt (**in-context learning**).

### 1.5. Những điều LLM không phải là

- **Không phải cơ sở dữ liệu.** Kiến thức nằm phân tán trong trọng số, không tra cứu được chính xác. Vì thế LLM có thể **ảo giác (hallucination)**: tạo ra thông tin nghe hợp lý nhưng sai, ví dụ trích dẫn một bài báo không tồn tại.
- **Kiến thức có hạn chót.** Mô hình chỉ biết dữ liệu tới **ngày cắt dữ liệu (knowledge cutoff)**, trừ khi được nối với công cụ tìm kiếm.
- **Không tự hành động.** LLM chỉ sinh văn bản. Khi được trao công cụ (chạy code, gọi API, đọc file) và vòng lặp lập kế hoạch, nó trở thành **tác tử (agent)** – chủ đề của các phần sau trong khoá học.

> **Dừng lại suy nghĩ.** (1) Vì sao một mô hình chỉ học "đoán token tiếp theo" lại giải được bài toán di truyền? (2) Nếu tách chuỗi DNA thành k-mer với k = 6, có bao nhiêu token khác nhau trong từ vựng?

## Phần 2. LLM được huấn luyện như thế nào?

**Ý chính:** Một LLM hiện đại đi qua bốn giai đoạn nối tiếp:&#32;

1. Tiền huấn luyện (pretraining)
2. Tinh chỉnh có giám sát (SFT)
3. Căn chỉnh theo sở thích (alignment)
4. Học tăng cường cho suy luận (RL for reasoning).&#32;

Giai đoạn đầu dạy mô hình ngôn ngữ và kiến thức; các giai đoạn sau dạy nó cách cư xử, làm theo chỉ dẫn và suy luận. Có thể hình dung như đào tạo một nghiên cứu sinh: đọc thật nhiều, học mẫu từ thầy, được góp ý, rồi tự giải bài để rèn tư duy.

### 2.1. Giai đoạn 1 – Tiền huấn luyện (pretraining)

- **Dữ liệu:** hàng chục nghìn tỷ token từ web, sách, bài báo khoa học, mã nguồn, dữ liệu đa ngôn ngữ. Dữ liệu được lọc trùng lặp, lọc chất lượng và loại nội dung độc hại.
- **Mục tiêu:** dự đoán token tiếp theo. Không cần ai gán nhãn, vì chính văn bản là đáp án – gọi là **tự giám sát (self-supervised)**.
- **Thuật toán:** tính sai số (cross-entropy loss) giữa dự đoán và token thật, rồi dùng lan truyền ngược (backpropagation) và gradient descent để điều chỉnh tỷ tham số một chút sau mỗi bước.
- **Chi phí:** hàng nghìn tới hàng chục nghìn GPU chạy nhiều tuần tới nhiều tháng; mô hình tiên phong tốn từ hàng chục tới hàng trăm triệu USD.
- **Kết quả:** **mô hình nền (base model)**. Nó viết tiếp văn bản rất giỏi nhưng chưa biết "trả lời". Hỏi "Thủ đô của Việt Nam là gì?", nó có thể viết tiếp thêm năm câu hỏi trắc nghiệm khác thay vì trả lời.

Một công thức hữu ích từ quy luật mở rộng Chinchilla (DeepMind, 2022): số token huấn luyện tối ưu xấp xỉ 20 lần số tham số. Các mô hình hiện nay thường huấn luyện vượt xa tỷ lệ này để mô hình nhỏ hơn mà vẫn mạnh, tiết kiệm chi phí khi sử dụng.

### 2.2. Giai đoạn 2 – Tinh chỉnh có giám sát (SFT)

Người ta soạn hàng chục nghìn tới hàng triệu cặp *(chỉ dẫn → câu trả lời mẫu)* chất lượng cao, do chuyên gia viết hoặc do mô hình mạnh hơn tạo rồi được kiểm duyệt. Mô hình nền được huấn luyện thêm trên dữ liệu này để học **định dạng hội thoại** và **cách làm theo yêu cầu**. Kết quả là **mô hình chỉ dẫn (instruct/chat model)**.

### 2.3. Giai đoạn 3 – Căn chỉnh theo sở thích (alignment)

SFT dạy mô hình bắt chước, nhưng không dạy được câu trả lời nào *tốt hơn*. Giai đoạn này dạy điều đó:

1. **RLHF (Reinforcement Learning from Human Feedback):** người đánh giá so sánh từng cặp câu trả lời và chọn câu tốt hơn. Từ đó huấn luyện một **mô hình phần thưởng (reward model)**, rồi dùng học tăng cường (thường là thuật toán PPO) để tối ưu LLM theo điểm thưởng. Đây là kỹ thuật làm nên ChatGPT (InstructGPT, OpenAI, 2022).
2. **DPO (Direct Preference Optimization):** học trực tiếp từ các cặp ưu tiên, bỏ qua bước huấn luyện mô hình phần thưởng; đơn giản và rẻ hơn, phổ biến trong cộng đồng mô hình mở.
3. **RLAIF và Constitutional AI:** thay một phần người đánh giá bằng AI chấm điểm theo một bộ nguyên tắc viết sẵn ("hiến pháp"). Anthropic dùng cách này cho Claude.

Mục tiêu của căn chỉnh thường được tóm tắt là **hữu ích, trung thực, vô hại**.

### 2.4. Giai đoạn 4 – Học tăng cường cho suy luận (RL for reasoning)

Từ cuối 2024, bước tiến lớn nhất đến từ việc cho mô hình **tự giải bài và được chấm đúng/sai tự động**: bài toán có đáp số, code có bộ test, bài tập có lời giải kiểm chứng được. Phương pháp này gọi là **RLVR (RL with verifiable rewards)**.

Mô hình học cách "nghĩ" thành một chuỗi suy luận dài (**chain-of-thought**) trước khi trả lời: thử, kiểm tra, sửa sai. Đây là nền tảng của các **mô hình suy luận (reasoning models)** như dòng o của OpenAI, DeepSeek-R1, và chế độ suy nghĩ mở rộng (extended thinking) của Claude hay Gemini. DeepSeek-R1 (1/2025) đã công bố công khai rằng thuật toán GRPO kết hợp phần thưởng đúng/sai đơn giản đủ để hình thành hành vi suy luận dài.

Hiện nay, học tăng cường còn được dùng để huấn luyện **hành vi tác tử**: dùng công cụ, chạy nhiều bước, sửa lỗi trong môi trường mô phỏng.

### 2.5. Sau huấn luyện: tinh chỉnh cho bài toán riêng

Người dùng cuối hiếm khi huấn luyện lại từ đầu. Ba lựa chọn thực tế, từ rẻ tới đắt:

| Cách làm | Khi nào dùng | Chi phí |
| --- | --- | --- |
| Prompt engineering + RAG (truy xuất tài liệu đưa vào ngữ cảnh) | Cần kiến thức riêng, cập nhật thường xuyên | Thấp, không cần GPU |
| Fine-tuning hiệu quả tham số (LoRA, QLoRA) | Cần đổi phong cách, định dạng, thuật ngữ chuyên ngành | Trung bình, 1–vài GPU |
| Tiếp tục tiền huấn luyện trên dữ liệu chuyên ngành | Lĩnh vực có ngôn ngữ riêng (y sinh, gen) | Cao |

> **Dừng lại suy nghĩ.** (1) Mô hình nền khác mô hình chat ở điểm nào? (2) Vì sao toán và lập trình là "mảnh đất màu mỡ" cho RLVR, còn viết văn thì khó hơn? (3) Bạn muốn LLM trả lời câu hỏi về quy trình xét nghiệm nội bộ của công ty – nên chọn RAG hay fine-tuning?

## Phần 3. Hiện nay có những LLM nào? Đặc điểm của chúng?

**Ý chính:** Thị trường chia thành hai nhóm. **Mô hình đóng** (OpenAI, Anthropic, Google, xAI) dẫn đầu về năng lực, chỉ dùng qua API hoặc ứng dụng. **Mô hình trọng số mở (open-weight)**, phần lớn từ các phòng lab Trung Quốc và Meta, tải về tự chạy được và kém nhóm đầu khoảng một thế hệ. Danh sách dưới đây cập nhật tới đầu tháng 10/2026 – lĩnh vực này thay đổi hằng tháng, nên hãy xem đây là ảnh chụp tại một thời điểm.

### 3.1. Sáu tiêu chí để "đọc" một LLM

Trước khi xem danh sách, người học nên biết cách so sánh:

1. **Đóng hay mở:** mô hình đóng chỉ gọi qua API; mô hình mở tải được trọng số, chạy trên máy riêng, dữ liệu không rời khỏi hệ thống. "Open-weight" khác "open-source": thường chỉ công bố trọng số, không công bố dữ liệu và mã huấn luyện. Giấy phép cũng khác nhau (MIT, Apache 2.0, hay giấy phép riêng có điều kiện).
2. **Kích thước và kiến trúc:** tổng tham số, số tham số hoạt động (với MoE), dense hay MoE.
3. **Cửa sổ ngữ cảnh:** phổ biến 128 nghìn tới 1 triệu token; Llama 4 Scout công bố 10 triệu. Giới hạn nhận vào không đồng nghĩa với việc hiểu tốt ở độ dài đó.
4. **Khả năng suy luận:** có chế độ "suy nghĩ" (reasoning/thinking) và mức nỗ lực (effort) điều chỉnh được hay không.
5. **Đa phương thức:** đọc ảnh, âm thanh, video; có dùng công cụ, điều khiển máy tính được không.
6. **Chi phí:** tính theo triệu token đầu vào/đầu ra. Ngày nay các nhóm kỹ thuật đo **chi phí cho mỗi tác vụ hoàn thành** vì cùng một mô hình ở mức effort khác nhau có thể chênh giá tới 7 lần.

### 3.2. Các mô hình đóng tiên phong

| Hãng | Mô hình tiêu biểu (10/2026) | Đặc điểm nổi bật |
| --- | --- | --- |
| Anthropic | Claude Opus 5.5, Sonnet 5.5, Haiku 5.5; Claude Fable 5.1 (hạng Mythos) | Opus 5.5 dẫn đầu chỉ số tổng hợp Artificial Analysis (57,6 điểm); mạnh về lập trình, tác tử và độ chính xác thông tin. Sonnet 5.5 (28/9/2026) gần ngang Opus với giá bằng một phần năm. Mythos Preview chỉ cấp cho tổ chức được thẩm định. |
| OpenAI | GPT-6 Astra, GPT-6.1 Sol, GPT-6 Luna; GPT-5.6 trong ChatGPT | Chia tầng rõ: Astra mạnh nhất, Sol cân bằng chi phí, Luna rất rẻ. Mạnh về suy luận toán và lý luận tổng quát. Có mô hình khoa học sự sống gpt-rosalind-research cho tổ chức nghiên cứu được duyệt. |
| Google | Gemini 3.8 Flash; Gemini 4 Argon (mới công bố 30/9/2026) | Đa phương thức tự nhiên (văn bản, ảnh, âm thanh, video), ngữ cảnh 1 triệu token, tích hợp sâu với hệ sinh thái Google. Argon có tỷ lệ ảo giác thấp nhất từng đo nhưng mới chỉ cấp cho nhóm chuyên gia an ninh mạng. |
| xAI | Grok 4.7 | Gắn với nền tảng X, giá token thấp nhưng sinh nhiều token nên chi phí mỗi tác vụ không rẻ. |

Một xu hướng mới đáng nói với người học: các mô hình mạnh nhất ngày càng được **phát hành có kiểm soát** (chỉ cho tổ chức được thẩm định) vì năng lực an ninh mạng của chúng. Một bản phát hành của OpenAI đã bị huỷ sau kiểm thử an toàn nội bộ.

### 3.3. Các mô hình trọng số mở

| Họ mô hình | Tổ chức | Quy mô | Ngữ cảnh | Giấy phép | Đặc điểm |
| --- | --- | --- | --- | --- | --- |
| DeepSeek V4 (Pro, Flash) | DeepSeek (TQ) | 1,7 nghìn tỷ / 304 tỷ tham số, MoE | 1 triệu | MIT | Hiệu quả chi phí, mạnh lập trình và suy luận; DeepSeek-R1 từng mở đường cho mô hình suy luận mở |
| Qwen3.8 | Alibaba (TQ) | Từ bản 27B dense tới 2,4 nghìn tỷ (95B hoạt động) | 262 nghìn, mở rộng tới 1 triệu | Apache 2.0 (bản 27B) | Nhiều kích cỡ nhất, đa ngôn ngữ tốt kể cả tiếng Việt, được tải nhiều nhất trên Hugging Face |
| Kimi K3 | Moonshot (TQ) | 2,8 nghìn tỷ (104B hoạt động) | 1 triệu | Giấy phép riêng | Đầu vào văn bản, ảnh, video; hướng tới tác tử dài hơi |
| GLM-5.3 | Z.ai (TQ) | 753 tỷ | 1 triệu | Giấy phép riêng, khá thoáng | Tối ưu cho lập trình và tác vụ dài |
| MiMo-V2.6-Pro | Xiaomi (TQ) | – | – | MIT | Điểm cao nhất nhóm mở trên chỉ số Artificial Analysis, chi phí mỗi tác vụ rất thấp |
| Llama 4 (Scout, Maverick); Muse Glimmer-30B | Meta (Mỹ) | 109B và 400B (17B hoạt động); \~30B dense | 10 triệu / 1 triệu; 131 nghìn | Llama 4 Community; Apache 2.0 | Hệ sinh thái phương Tây lớn nhất; Muse Glimmer chạy được trên máy trạm |
| Gemma 4 | Google | Từ vài tỷ tới 12B | – | Gemma | Nhỏ gọn, chạy trên laptop 16 GB RAM |
| Mistral Large 4 | Mistral AI (Pháp) | 1 nghìn tỷ (49B hoạt động) | – | Sắp công bố | Mới xem trước 6/10/2026, hứa công bố trọng số cuối tháng 10 |
| gpt-oss-120b / 20b | OpenAI | 120B / 20B | – | Apache 2.0 | Bản mở đầu tiên của OpenAI kể từ GPT-2 |

### 3.4. Nên chọn mô hình nào?

- **Dùng hằng ngày, viết, tóm tắt, phân tích tài liệu:** một mô hình đóng tầm trung (Claude Sonnet, Gemini Flash, GPT Sol) là đủ và rẻ.
- **Lập trình, tác tử nhiều bước, phân tích phức tạp:** mô hình đóng hàng đầu (Claude Opus, GPT Astra).
- **Dữ liệu nhạy cảm không được rời máy chủ** (dữ liệu gen, hồ sơ khách hàng): mô hình mở tự triển khai, ví dụ Qwen3.8-27B hoặc Muse Glimmer-30B trên một máy trạm GPU.
- **Tinh chỉnh cho chuyên ngành:** mô hình mở cỡ nhỏ (7–30B) với LoRA.

Nguyên tắc vàng: **không có mô hình tốt nhất cho mọi việc.** Hãy thử hai mô hình trên chính 5–10 tác vụ thật của bạn, đo chất lượng và chi phí, rồi mới quyết định.

> **Dừng lại suy nghĩ.** (1) Một phòng xét nghiệm cần LLM hỗ trợ phân tích dữ liệu giải trình tự gen của bệnh nhân, không được gửi dữ liệu ra ngoài. Bạn chọn nhóm mô hình nào, vì sao? (2) Vì sao số tham số "hoạt động" quan trọng hơn tổng tham số khi tính chi phí chạy MoE?

*Nguồn số liệu: [Local AI Zone – October 2026 AI Model Updates](https://local-ai-zone.github.io/blog/October_2026_AI_Model_Updates.html) (đối chiếu chỉ số Artificial Analysis), [Wavect – Open-Weight LLMs 2026](https://wavect.io/blog/open-weight-llm-comparison-2026/) (thông số mô hình mở, rà soát 5/10/2026).*

## Phần 4. LLM trong tin sinh học

**Ý chính:** Ý tưởng "đoán token tiếp theo" không chỉ áp dụng cho tiếng người. DNA, protein và biểu hiện gen cũng là "ngôn ngữ" có ngữ pháp riêng, nên cùng kiến trúc Transformer đã sinh ra cả một họ **mô hình nền sinh học**. Song song, LLM đa dụng đang trở thành "trợ lý nghiên cứu" điều phối các công cụ tin sinh học.

### 4.1. Bốn hướng LLM đi vào tin sinh học

| Hướng | Ý tưởng | Ví dụ mô hình | Ứng dụng |
| --- | --- | --- | --- |
| Mô hình ngôn ngữ cho chuỗi DNA | Token là nucleotide hoặc k-mer; học "ngữ pháp" bộ gen | DNABERT-2, Nucleotide Transformer, HyenaDNA, Evo 2 | Dự đoán vùng điều hoà, ảnh hưởng của biến dị, sinh chuỗi |
| Mô hình ngôn ngữ protein | Token là axit amin | ESM-2, ESM3 | Dự đoán cấu trúc, chức năng, thiết kế protein |
| Mô hình đơn bào | Token là gen, xếp theo mức biểu hiện | Geneformer, scGPT | Chú giải loại tế bào, dự đoán hiệu ứng khi tắt gen |
| LLM đa dụng làm tác tử | LLM đọc yêu cầu, viết code, gọi công cụ (BLAST, PLINK, R) | Claude, GPT, Gemini, Qwen kèm công cụ | Tự động hoá pipeline, đọc tài liệu, giải thích kết quả |

### 4.2. Ví dụ theo từng lĩnh vực omics

Mỗi dòng dưới đây là một tình huống học viên có thể gặp ngay trong luận văn hay dự án: người nghiên cứu nêu câu hỏi bằng ngôn ngữ tự nhiên, LLM (thường ở vai trò tác tử) chọn công cụ, viết và chạy code, rồi giải thích kết quả.

| Lĩnh vực | Câu hỏi của người nghiên cứu | LLM / tác tử làm gì | Công cụ, mô hình liên quan |
| --- | --- | --- | --- |
| Genomics | "Từ dữ liệu giải trình tự toàn bộ gen, biến dị nào có thể gây bệnh?" | Dựng pipeline căn chỉnh → gọi biến dị → chú giải; lọc biến dị hiếm, gây mất chức năng; giải thích từng biến dị kèm nguồn tham chiếu | BWA-MEM2, GATK, VEP, ClinVar; Evo 2 chấm điểm ảnh hưởng biến dị |
| Transcriptomics (bulk RNA-seq) | "Gen nào biểu hiện khác biệt giữa mẫu bệnh và đối chứng, thuộc con đường tín hiệu nào?" | Viết code phân tích biểu hiện khác biệt, vẽ volcano plot, phân tích làm giàu GO/KEGG, tóm tắt ý nghĩa sinh học | DESeq2, edgeR, clusterProfiler |
| Single-cell transcriptomics | "Dữ liệu scRNA-seq mô phổi gồm những loại tế bào nào?" | Tiền xử lý, phân cụm, gợi ý tên loại tế bào từ gen chỉ thị; dùng mô hình nền đơn bào để chú giải tự động | Scanpy, Seurat; Geneformer, scGPT |
| Proteomics | "Protein nào thay đổi có ý nghĩa sau xử lý thuốc trong dữ liệu khối phổ?" | Đọc bảng đầu ra, xử lý giá trị thiếu, chuẩn hoá, kiểm định thống kê, vẽ heatmap | MaxQuant, Perseus, limma |
| Cấu trúc và chức năng protein | "Protein chưa rõ chức năng này có thể làm gì?" | Dự đoán cấu trúc, tìm protein tương đồng, suy luận chức năng từ domain bảo tồn và embedding | ESM-2, ESMFold, AlphaFold, InterProScan, BLAST |
| Interactomics | "Trong mạng tương tác của các protein khác biệt, đâu là protein trung tâm?" | Truy vấn cơ sở dữ liệu tương tác, dựng mạng, tính độ trung tâm, tìm module và giải thích chức năng từng module | STRING, BioGRID, NetworkX, Cytoscape |
| Metagenomics | "Hệ vi sinh vật đường ruột khác nhau thế nào giữa hai nhóm?" | Dựng pipeline 16S hoặc shotgun, tính đa dạng alpha/beta, tìm taxon khác biệt | QIIME 2, Kraken2, MetaPhlAn |
| Multi-omics và tổng quan tài liệu | "Tích hợp dữ liệu gen, biểu hiện và protein; tóm tắt các bài báo mới về gen này" | Ghép dữ liệu nhiều tầng, tìm tín hiệu nhất quán; tra PubMed, tổng hợp bằng chứng có trích dẫn | MOFA+, PubMed, bioRxiv |

Điểm chung của các ví dụ: LLM không thay thế phần mềm chuyên ngành mà đóng vai **người điều phối** – hiểu câu hỏi, chọn đúng công cụ, kiểm tra đầu ra và diễn giải kết quả. Còn các mô hình nền sinh học (Evo 2, ESM, Geneformer) là những "công cụ" chuyên biệt mà người điều phối đó có thể gọi tới.

**Lưu ý khi dùng:**

- **Kiểm chứng mọi thứ:** LLM có thể bịa tên gen, ID protein, tham số lệnh hoặc trích dẫn bài báo không tồn tại. Đối chiếu với NCBI, Ensembl, UniProt, PubMed.
- **Để ý phiên bản tham chiếu:** nhầm hệ toạ độ hg19 với hg38, hay phiên bản cơ sở dữ liệu, là lỗi phổ biến và khó phát hiện.
- **Giữ khả năng tái lập:** lưu lại code, phiên bản công cụ và tham số mà LLM đã dùng, không chỉ lưu câu trả lời.
- **Bảo mật dữ liệu:** dữ liệu gen người và dữ liệu bệnh nhân không nên gửi lên API công cộng; cân nhắc mô hình mở chạy nội bộ.

> **Dừng lại suy nghĩ.** (1) Geneformer xem mỗi tế bào là một "câu" và mỗi gen là một "từ", xếp theo mức biểu hiện. Mô hình có thể học được gì từ hàng chục triệu "câu" như vậy? (2) Trong pipeline RNA-seq, bước nào bạn sẽ giao cho LLM, và bước nào bạn nhất định tự kiểm tra?

## Tổng kết và tự kiểm tra

### Tóm tắt trong năm câu

1. LLM là mạng Transformer rất lớn, học cách dự đoán token tiếp theo trên hàng chục nghìn tỷ token văn bản.
2. Tiền huấn luyện tạo ra mô hình nền có kiến thức; SFT dạy làm theo chỉ dẫn; RLHF/DPO/Constitutional AI dạy cư xử tốt; RL với phần thưởng kiểm chứng được dạy suy luận.
3. LLM có thể ảo giác, có ngày cắt dữ liệu và chỉ hành động được khi nối với công cụ.
4. Mô hình đóng (Claude, GPT, Gemini, Grok) dẫn đầu năng lực; mô hình mở (DeepSeek, Qwen, Kimi, GLM, Llama, Gemma) cho phép tự triển khai và tinh chỉnh.
5. Chọn mô hình bằng cách thử trên tác vụ thật và đo chi phí cho mỗi tác vụ hoàn thành.

### Bảng thuật ngữ

| Thuật ngữ | Nghĩa ngắn gọn |
| --- | --- |
| Token | Mảnh văn bản nhỏ nhất mà mô hình xử lý |
| Embedding | Vector số biểu diễn nghĩa của một token |
| Context window | Số token tối đa mô hình xem được cùng lúc |
| Self-attention | Cơ chế cho mỗi token "nhìn" mọi token khác để hiểu ngữ cảnh |
| Tham số (parameter) | Các trọng số được học trong huấn luyện |
| MoE | Kiến trúc chỉ kích hoạt một phần "chuyên gia" cho mỗi token |
| Pretraining | Huấn luyện tự giám sát trên lượng văn bản khổng lồ |
| SFT | Tinh chỉnh trên cặp chỉ dẫn – câu trả lời mẫu |
| RLHF / DPO | Căn chỉnh theo sở thích con người |
| RLVR | Học tăng cường với phần thưởng kiểm chứng được tự động |
| Hallucination | Mô hình tạo thông tin nghe hợp lý nhưng sai |
| RAG | Truy xuất tài liệu liên quan rồi đưa vào ngữ cảnh |
| LoRA | Tinh chỉnh chỉ một phần nhỏ tham số bổ sung |
| Open-weight | Công bố trọng số để tải về, chưa chắc công bố dữ liệu và mã |
| Agent (tác tử) | LLM có công cụ và vòng lặp lập kế hoạch để tự thực hiện nhiệm vụ |

### Gợi ý đáp án các hộp "Dừng lại suy nghĩ"

**Phần 1.** (1) Để đoán đúng token tiếp theo trong hàng triệu trang sách di truyền học, mô hình buộc phải nắm các quy luật như phiên mã, dịch mã, phân ly; kiến thức xuất hiện như sản phẩm phụ của việc dự đoán. Tuy vậy, đó là quy luật thống kê, nên mô hình vẫn có thể sai ở bài toán lạ. (2) Mỗi vị trí có 4 nucleotide, nên số 6-mer khác nhau là 4⁶ = 4.096 token. So với bảng ví dụ ở mục 1.2: k càng lớn, từ vựng càng lớn nhưng chuỗi càng ít token.

**Phần 2.** (1) Mô hình nền chỉ viết tiếp văn bản; mô hình chat đã qua SFT và căn chỉnh nên hiểu đầu vào là một câu hỏi và trả lời đúng định dạng hội thoại. (2) Toán và code có đáp án kiểm tra tự động được (so đáp số, chạy bộ test), nên có thể tạo phần thưởng hàng triệu lần mà không cần người chấm; văn chương khó chấm khách quan. (3) RAG: quy trình nội bộ thay đổi thường xuyên và cần trích nguồn chính xác; fine-tuning hợp với việc đổi phong cách, định dạng hơn là nạp kiến thức mới.

**Phần 3.** (1) Mô hình trọng số mở tự triển khai trên máy chủ nội bộ (ví dụ Qwen3.8-27B hoặc Muse Glimmer-30B trên máy trạm GPU), kết hợp công cụ tin sinh học và RAG trên tài liệu quy trình. Lý do: dữ liệu gen người là dữ liệu nhạy cảm, không được rời hệ thống; cần kiểm tra giấy phép của mô hình trước khi dùng. (2) Chi phí tính toán mỗi token tỷ lệ với số tham số thực sự tham gia tính toán, tức số tham số hoạt động; tuy vậy bộ nhớ GPU vẫn phải chứa toàn bộ tham số.

**Phần 4.** (1) Gen nào thường cùng biểu hiện (đồng điều hoà), gen nào đặc trưng cho từng loại tế bào, và mạng điều hoà ngầm giữa các gen; nhờ đó có thể mô phỏng tắt một gen và dự đoán thay đổi. (2) Gợi ý: giao cho LLM viết code, vẽ hình, tra cứu chức năng gen; tự kiểm tra thiết kế thí nghiệm, kiểm soát chất lượng mẫu, ngưỡng thống kê và kết luận sinh học cuối cùng.

### Tài liệu đọc thêm

- Vaswani và cs. (2017). [Attention Is All You Need](https://arxiv.org/abs/1706.03762) – bài báo gốc về Transformer.
- Ouyang và cs. (2022). [Training language models to follow instructions with human feedback](https://arxiv.org/abs/2203.02155) – InstructGPT và RLHF.
- Bai và cs. (2022). [Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073).
- DeepSeek-AI (2025). [DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948).
- Andrej Karpathy, video [Intro to Large Language Models](https://www.youtube.com/watch?v=zjkBMFhNj_g) – giới thiệu dễ hiểu cho người mới.
