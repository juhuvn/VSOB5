Case Study Challenge: Khai thác dữ liệu RNAseq bằng đội ngũ AI Agent
===========================================================================

**TS. Nguyễn Cường**

Giám đốc khoa học, Công ty LOBI
NCVC, Viện CNTT, VAST

---

# 0. Yêu cầu chung cho các nhóm

## 0.1 Ban tổ chức cung cấp gì, nhóm phải tự làm gì?

Ngày 1 đã dạy **công thức** tạo một AI Agent (mục 1.2), **quy chế** làm việc nhóm agent (mục 1.3), và một **ví dụ hoàn chỉnh** đi hết quy trình (mục 3). Ngày 2 là lúc tự làm lại từ đầu, trên một đề tài khác.

| Ban tổ chức cung cấp                                         | Nhóm phải tự xây dựng                                                                                  |
| --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Bối cảnh:** một bài báo đã công bố             | **Đội ngũ agent:** có bao nhiêu agent, mỗi agent là ai, giỏi gì, ràng buộc gì             |
| **Dữ liệu:** mã truy cập trên GEO và/hoặc recount3 | **Mô tả dự án** (`PROJECT.md`): mục tiêu, dữ liệu, thành viên, thư mục kết quả        |
| Máy chủ, VSCode, Codex + DeepSeek                             | **Luồng làm việc:** thứ tự các khâu, điểm nào con người duyệt, có vòng lặp hay không |
|                                                                 | **Câu hỏi nghiên cứu** và toàn bộ chiến lược phân tích                                    |

Ban tổ chức **không** cung cấp: định nghĩa agent mẫu, prompt mẫu, danh sách bước phân tích, hay gợi ý về những vấn đề có trong dữ liệu. Việc phát hiện những vấn đề đó là một phần của bài tập.

Nhóm được phép tham khảo lại tài liệu Ngày 1 và bộ file trong [`Agents/`](../Day1/CuongNguyen/Practice/Agents/), nhưng **chép nguyên si sẽ không phù hợp**: bộ đó viết cho dữ liệu lúa và một luồng làm việc cụ thể.

## 0.2 Sản phẩm nộp

Sản phẩm cuối cùng là **một bài báo ngắn**. Nhưng hội đồng chấm cả **hệ thống agent** mà nhóm đã xây để tạo ra bài báo đó.

| Sản phẩm                 | Nội dung                                                                                                |
| -------------------------- | -------------------------------------------------------------------------------------------------------- |
| `AGENTS.md`              | Quy chế chung cho mọi agent của nhóm                                                                 |
| `agents/*.md`            | Định nghĩa từng agent, theo công thức ở mục 1.2 của Ngày 1                                     |
| `<dự án>/PROJECT.md`   | Mô tả dự án: mục tiêu, dữ liệu, thành viên, quy trình, thư mục kết quả                    |
| Sơ đồ luồng làm việc | Thứ tự các khâu và các điểm con người duyệt. Vẽ tay hay viết bằng chữ đều được       |
| Kết quả phân tích      | Bảng, hình, và script chạy lại được                                                              |
| Bản thảo bài báo       | Theo thể lệ có ở file <br />`/home/shared_data/tinh_huong_2/the-le-viet-bai_chi-tiet`.docx         |
| `logs/decisions.md`      | **Nhật ký giám sát:** những lúc nhóm bác bỏ hoặc sửa đề xuất của agent, kèm lý do |

> **Nhật ký giám sát là sản phẩm bắt buộc.** Đây là bằng chứng duy nhất cho thấy con người còn ở trong vòng lặp. Nộp thiếu file này, hoặc nộp một file trống, sẽ mất trọn phần điểm tương ứng.

## 0.3 Thang điểm

Thang điểm chấm **cách làm**, không chấm kết quả tìm được. Các nhóm nhận những bộ dữ liệu khác nhau nên kết quả vốn không so sánh trực tiếp được. Quan trọng hơn: nếu chấm "nhóm nào tìm được kết quả đẹp hơn", học viên sẽ học cách làm đẹp kết quả.

| Tiêu chí                                                                                                                                              | Điểm | Chấm dựa trên                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------------------------- |
| **Thiết kế đội ngũ agent** — phân vai hợp lý, không chồng chéo; mỗi agent có đủ 8 thành phần; ràng buộc đặt đúng chỗ     | 20     | `AGENTS.md`, `agents/*.md`, `PROJECT.md` |
| **Luồng làm việc** — có điểm duyệt của con người ở đúng chỗ; có cơ chế phản biện; lý giải được vì sao chọn luồng đó | 15     | Sơ đồ luồng, phần trình bày             |
| **Thẩm định dữ liệu** — phát hiện được bao nhiêu vấn đề trong dữ liệu và metadata                                               | 20     | Báo cáo thẩm định                         |
| **Thiết kế phân tích** — dạng dữ liệu có phù hợp phương pháp không; mô hình, nhóm tham chiếu, ngưỡng có hợp lý không     | 15     | Script, báo cáo phân tích                  |
| **Kiểm chứng và trung thực** — bắt được chỗ agent bịa; phân biệt rõ kết quả với giả thuyết; nêu đủ hạn chế                | 20     | `logs/decisions.md`, bản thảo              |
| **Tái lập** — người khác chạy lại script có ra cùng kết quả không                                                                    | 5      | `scripts/`                                   |
| **Trình bày**                                                                                                                                   | 5      | Slide và hỏi đáp                           |

### 0.4 Hội đồng sẽ hỏi gì

Nhóm nên chuẩn bị trước:

1. **Vì sao nhóm chia đội ngũ thành các agent như vậy?** Đã cân nhắc phương án nào khác?
2. **Nhóm đặt điểm duyệt của con người ở đâu, và vì sao ở đó?**
3. Dữ liệu của nhóm **không trả lời được** câu hỏi nào?
4. Nhóm đã **bác bỏ đề xuất nào** của agent? Vì sao?
5. Agent đã **bịa** thứ gì mà nhóm phát hiện được?
6. Phát hiện chính của nhóm là **kết quả** hay **giả thuyết**? Cần làm gì tiếp để chuyển nó thành kết luận?
7. Nếu làm lại từ đầu, nhóm sẽ **thay đổi gì** trong hệ thống agent của mình?

## 0.5 Quy định bắt buộc

- **Cấm tải FASTQ từ SRA và dóng hàng lại.** Bài tập làm việc từ ma trận biểu hiện. Các nhóm cùng chạy công cụ dóng hàng sẽ làm sập máy chủ.
- Mỗi lệnh dùng **tối đa 2 luồng**; không chạy song song nhiều lệnh nặng.
- Mọi trích dẫn phải có **PMID hoặc DOI xác minh được**; không xác minh được thì ghi "chưa xác minh".

# 1. Case study 1: Imbalanced Host Response to SARS-CoV-2 Drives Development of COVID-19

Trong case study 1 này, chúng ta sẽ tái lập lại kết quả nghiên cứu có trong bài báo:

> Blanco-Melo D., Nilsson-Payant B. E., Liu W.-C., Uhl S., Hoagland D., Møller R., Jordan T. X., Oishi K., Panis M., Sachs D., Wang T. T., Schwartz R. E., Lim J. K., Albrecht R. A., tenOever B. R. (2020). **Imbalanced Host Response to SARS-CoV-2 Drives Development of COVID-19**. *Cell* 181(5): 1036–1045.e9. PMID 32416070. https://doi.org/10.1016/j.cell.2020.04.026
>
> Toàn văn: https://pmc.ncbi.nlm.nih.gov/articles/PMC7227586/

Đây là một trong những công bố sớm và có ảnh hưởng nhất về cơ chế bệnh sinh của COVID-19, đặt nền cho hướng điều trị dựa trên điều hòa đáp ứng miễn dịch thay vì chỉ kháng virus.

### Câu hỏi nghiên cứu của bài báo

**Đáp ứng phiên mã của tế bào chủ với SARS-CoV-2 khác gì so với các virus hô hấp khác, và điểm khác biệt đó giải thích được bệnh cảnh COVID-19 như thế nào?**

Bài báo đặt câu hỏi này vì thời điểm đầu năm 2020, giới khoa học chưa rõ vì sao COVID-19 lại có diễn biến khác hẳn cúm mùa dù cùng là bệnh đường hô hấp. Nhóm tác giả không so sánh SARS-CoV-2 với nhóm đối chứng khỏe mạnh đơn thuần, mà **đặt nó cạnh nhiều virus hô hấp khác** trong cùng một hệ thống thí nghiệm.

Kết luận chính của bài báo: SARS-CoV-2 gây ra một đáp ứng **mất cân đối** (*imbalanced*) — interferon type I và III ở mức thấp, nhưng chemokine và IL-6 lại tăng cao. Nói cách khác, tế bào vừa **thiếu hàng rào kháng virus bẩm sinh**, vừa **thừa phản ứng viêm**. Đây chính là tổ hợp được cho là động lực thúc đẩy bệnh cảnh COVID-19.

### Dữ liệu

| Thông tin              | Nội dung                                                                                                                                                   |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mã GEO                 | [GSE147507](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE147507)                                                                                    |
| Loại dữ liệu         | Bulk RNA-seq, ma trận raw count có sẵn trên GEO                                                                                                         |
| Quy mô                 | 78 mẫu người, 21.797 gene (`GSE147507_RawReadCounts_Human.tsv.gz`)                                                                                     |
| Hệ thống thí nghiệm | Tế bào biểu mô phế quản nguyên phát (NHBE), dòng tế bào phổi A549, A549 biểu hiện ACE2, Calu-3, và mô phổi tử thiết bệnh nhân COVID-19 |
| Virus so sánh          | SARS-CoV-2, cúm A (IAV), IAV thiếu protein NS1 (IAVdNS1), RSV, HPIV3; cùng với xử lý interferon-beta                                                  |

Dữ liệu được tổ chức theo **"Series"**, mỗi Series là một thí nghiệm độc lập có nhóm đối chứng (Mock) riêng:

| Series      | Hệ thống        | Các nhóm mẫu có trong Series          |
| ----------- | ----------------- | ----------------------------------------- |
| Series1     | NHBE              | Mock, SARS-CoV-2                          |
| Series2, 5  | A549              | Mock, SARS-CoV-2                          |
| Series3     | A549              | Mock, RSV                                 |
| Series4     | A549              | Mock, IAV                                 |
| Series6, 16 | A549-ACE2         | Mock, SARS-CoV-2                          |
| Series7     | Calu-3            | Mock, SARS-CoV-2                          |
| Series8     | A549              | Mock, RSV, HPIV3                          |
| Series9     | NHBE              | Mock, IAV, IAVdNS1, IFN-beta              |
| Series15    | Mô phổi người | Mô khỏe mạnh, mô bệnh nhân COVID-19 |

# 2. Case study 2: Early life stress confers lifelong stress susceptibility in mice via ventral tegmental area OTX2

Case study này sử dụng bài báo:

> Peña C. J., Kronman H. G., Walker D. M., Cates H. M., Bagot R. C., Purushothaman I., Issler O., Loh Y.-H. E., Leong T., Kiraly D. D., Goodman E., Neve R. L., Shen L., Nestler E. J. (2017). Early life stress confers lifelong stress susceptibility in mice via ventral tegmental area OTX2. *Science* 356(6343): 1185–1188. PMID 28619944. https://doi.org/10.1126/science.aan4491
>
> Toàn văn: https://pmc.ncbi.nlm.nih.gov/articles/PMC5539403/
>
> Dữ liệu: **recount3**, mã nghiên cứu [`SRP093288`](https://rna.recount.bio/) (chuột)

### Câu hỏi nghiên cứu của bài báo

**Vì sao stress thời thơ ấu lại làm tăng tính dễ tổn thương với stress suốt đời, và cơ chế phân tử nào ghi nhớ điều đó?**

Bài báo đặt giả thuyết rằng stress trong một **giai đoạn nhạy cảm** sau sinh làm thay đổi điều hòa phiên mã ở **vùng mái bụng (ventral tegmental area — VTA)**, một vùng não thuộc hệ tưởng thưởng, và chính thay đổi đó khiến con vật dễ bị tổn thương bởi stress khi trưởng thành.

Thiết kế nghiên cứu gồm hai cú sốc cách nhau cả đời:

| Giai đoạn               | Tác động                                                                                          |
| ------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Thơ ấu**        | Tách mẹ (maternal separation), thử hai cửa sổ thời gian: sớm (PND2–12) và muộn (PND10–20) |
| **Trưởng thành** | Stress thất bại xã hội mạn tính (chronic social defeat stress — CSDS)                         |

Kết luận chính của bài báo:

1. **Chỉ cửa sổ muộn** mới làm tăng tính dễ tổn thương ở tuổi trưởng thành — tức là có một giai đoạn nhạy cảm thật sự.
2. Stress thơ ấu làm thay đổi 225 gene ở VTA, stress trưởng thành làm thay đổi 428 gene, và **69 gene chung** thay đổi **cùng chiều** ở cả hai.
3. **OTX2**, một yếu tố phiên mã phát triển, là yếu tố điều hòa thượng nguồn đứng đầu của dấu hiệu phiên mã này.
4. Can thiệp Otx2 ở **tuổi thiếu niên** làm thay đổi tính dễ tổn thương suốt đời, nhưng can thiệp ở **tuổi trưởng thành thì không** — củng cố ý tưởng về giai đoạn nhạy cảm.

### Dữ liệu

| Thông tin                 | Nội dung                                                                                                                            |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Thông tin                 | Nội dung                                                                                                                            |
| ---                        | ---                                                                                                                                  |
| Mã nghiên cứu           | **`SRP093288`** (recount3, chuột)                                                                                           |
| Quy mô cả nghiên cứu   | 187 mẫu RNA-seq, gồm cả chuột đực lẫn chuột cái, hai vùng não (VTA và NAc), phục vụ **hai công bố khác nhau** |
| Phần dùng cho bài tập  | **20 mẫu VTA chuột đực** (`RNAseq_ELSCtl*`, `RNAseq_ELSDefeat*`, `RNAseq_StdCtl*`, `RNAseq_StdDefeat*`)            |
| Thiết kế                 | **2×2**: ELS (có/không stress thơ ấu) × Defeat (có/không stress trưởng thành)                                       |
| Độ sâu giải trình tự | 35–46 triệu reads mỗi mẫu, độ dài read ~99 bp                                                                                 |

Hai mươi mẫu chia thành bốn nhóm, đúng thiết kế 2×2:

| Nhóm         | Thơ ấu        | Trưởng thành | Số mẫu |
| ------------- | --------------- | --------------- | -------- |
| `StdCtl`    | Nuôi chuẩn    | Đối chứng    | 4        |
| `StdDefeat` | Nuôi chuẩn    | Stress xã hội | 6        |
| `ELSCtl`    | Stress thơ ấu | Đối chứng    | 4        |
| `ELSDefeat` | Stress thơ ấu | Stress xã hội | 6        |

Thiết kế này **song song hoàn toàn** với Tình huống 2 ở Ngày 1 (2 dòng lúa × 2 điều kiện mặn), nên cách đặt mô hình có tương tác chuyển sang được nguyên vẹn. Chỉ có **phương pháp thống kê** là phải đổi.

# 3. Case study 3: Human Gut Microbiota from Autism Spectrum Disorder Promote Behavioral Symptoms in Mice

Case study này sử dụng bài báo:

> Sharon G., Cruz N. J., Kang D.-W., Gandal M. J., Wang B., Kim Y.-M. *và cs.* (2019). Human Gut Microbiota from Autism Spectrum Disorder Promote Behavioral Symptoms in Mice. *Cell* 177(6): 1600–1618.e17. PMID 31150625. https://doi.org/10.1016/j.cell.2019.05.004
>
> Toàn văn: https://pmc.ncbi.nlm.nih.gov/articles/PMC6993574/
>
> Dữ liệu: [GSE109827](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE109827)

### Câu hỏi nghiên cứu của bài báo

**Hệ vi sinh vật đường ruột của người mắc rối loạn phổ tự kỷ (ASD) có thực sự góp phần gây ra các biểu hiện hành vi của tự kỷ hay không, và qua cơ chế nào?**

Đây là câu hỏi về **quan hệ nhân quả**, không chỉ là quan hệ tương quan. Trước đó đã có nhiều nghiên cứu cho thấy người mắc ASD có hệ vi sinh vật ruột khác người bình thường, nhưng không rõ đó là **nguyên nhân** hay chỉ là **hệ quả** của bệnh.

Thiết kế của bài báo rất đặc biệt — đây là một thí nghiệm **cấy ghép hệ vi sinh vật xuyên loài**:

| Bước | Nội dung                                                                                          |
| ------ | -------------------------------------------------------------------------------------------------- |
| 1      | Lấy mẫu phân từ trẻ phát triển bình thường (TD) và trẻ mắc ASD                        |
| 2      | Cấy vào **chuột vô trùng** (germ-free), tức chuột hoàn toàn không có vi sinh vật |
| 3      | Cho chuột sinh sản; thế hệ con được gọi là **oTD** và **oASD**               |
| 4      | Đánh giá hành vi của chuột con, rồi giải phẫu lấy mô não ở ngày tuổi P45            |

Các kết luận chính của bài báo:

1. Chuột nhận hệ vi sinh vật từ trẻ ASD (**oASD**) có hành vi lặp lại nhiều hơn, giảm tương tác xã hội và giảm phát âm siêu âm.
2. **Ở não: rất ít gene biểu hiện khác biệt, nhưng 560 gene thay đổi kiểu cắt nối**, trong đó 52 gene thuộc nhóm liên quan tự kỷ. Con đường spliceosome được điều hòa tăng.
3. Hai chất chuyển hóa **taurine** và **5-aminovaleric acid (5AV)** giảm trong ruột chuột oASD.
4. Bổ sung taurine hoặc 5AV cho chuột mô hình tự kỷ BTBR **cải thiện được hành vi** — đây là bằng chứng nhân quả mạnh nhất của bài báo.

Phần RNA-seq mà nhóm 3 phân tích chỉ là **một mảnh** trong chuỗi bằng chứng đó.

### Dữ liệu

| Thông tin         | Nội dung                                                                                                  |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| Mã GEO            | [GSE109827](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE109827)                                   |
| Loài, mô         | Chuột C57BL/6J; hai vùng não: **vỏ não trước trán (PFC)** và **thể vân (STRIATUM)** |
| Quy mô            | **69 mẫu**, 48.709 gene                                                                             |
| Dạng dữ liệu    | **Raw count** từ featureCounts: `GSE109827_RNAseq_featureCounts.csv.gz`                           |
| Nhóm so sánh     | oASD (nhận hệ vi sinh từ trẻ ASD) so với oTD (nhận từ trẻ phát triển bình thường)             |
| Tuổi, giới tính | Tất cả P45, **tất cả đều là chuột đực**                                                    |

Phân bố mẫu:

| Vùng não | oTD | oASD | Tổng |
| ---------- | --- | ---- | ----- |
| PFC        | 15  | 20   | 35    |
| STRIATUM   | 14  | 20   | 34    |

Ngoài ma trận count, series này còn có thêm một số file kết quả khác do nhóm tác giả nộp lên. Hãy tự xem danh sách file bổ sung trên trang GEO của series.

# 4. Case study 4: Metabolic, Epigenetic, and Transgenerational Effects of Gut Bacterial Choline Consumption

Case study này sử dụng bài báo:

> Romano K. A., Martinez-del Campo A., Kasahara K., Chittim C. L., Vivas E. I., Amador-Noguez D., Balskus E. P., Rey F. E. (2017). Metabolic, Epigenetic, and Transgenerational Effects of Gut Bacterial Choline Consumption. *Cell Host & Microbe* 22(3): 279–290.e7. PMID 28844887. https://doi.org/10.1016/j.chom.2017.07.021
>
> Toàn văn: https://pmc.ncbi.nlm.nih.gov/articles/PMC5599363/
>
> Dữ liệu: [GSE100983](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE100983) · recount3 `SRP111408`

### Câu hỏi nghiên cứu của bài báo

**Khi vi khuẩn đường ruột tiêu thụ choline trong thức ăn, chúng có lấy mất của vật chủ một chất dinh dưỡng thiết yếu không — và nếu có thì hậu quả là gì?**

Choline là chất vật chủ cần cho hai việc: tổng hợp màng tế bào (phosphatidylcholine) và cung cấp nhóm methyl cho các phản ứng methyl hóa, trong đó có methyl hóa DNA. Một số vi khuẩn ruột mang gene `cutC` có thể cắt choline thành trimethylamine (TMA), chất sau đó được gan chuyển thành TMAO. Trước bài báo này, người ta đã biết TMAO liên quan tới bệnh tim mạch, nhưng câu hỏi ngược lại chưa ai trả lời: **việc vi khuẩn "ăn" choline có làm vật chủ thiếu choline không?**

Khó khăn của câu hỏi này là không thể trả lời bằng cách so sánh chuột có vi sinh vật với chuột vô trùng — hai nhóm đó khác nhau quá nhiều thứ. Nhóm tác giả giải bằng một thiết kế tối giản:

| Bước | Nội dung                                                                                                                                                                                                                                                               |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Nuôi **chuột vô trùng** (germ-free) C57BL/6, hoàn toàn không có vi sinh vật                                                                                                                                                                              |
| 2      | Cấy vào mỗi chuột một **cộng đồng vi khuẩn nhân tạo gồm 5 loài** không tiêu thụ choline                                                                                                                                                           |
| 3      | Thêm vào cộng đồng đó **một chủng *E. coli* MS 200-1 duy nhất**, ở hai dạng: bản hoang dã (có `cutC`, tiêu thụ choline — ký hiệu **CC+**) hoặc bản đột biến Δ`cutC` (không tiêu thụ choline — ký hiệu **CC−**) |
| 4      | Theo dõi chất chuyển hóa, methyl hóa DNA, bệnh chuyển hóa; rồi cho sinh sản để xem thế hệ con                                                                                                                                                             |

Điểm mạnh của thiết kế: hai nhóm chuột **chỉ khác nhau một gene vi khuẩn duy nhất**. Mọi khác biệt quan sát được đều quy về chính chức năng tiêu thụ choline.

Các kết luận chính của bài báo:

1. Chuột **CC+** có choline huyết thanh thấp hơn khoảng **ba lần** và TMAO cao hơn so với chuột CC−. Vi khuẩn thật sự cạnh tranh choline với vật chủ.
2. Các chất chuyển hóa của **chu trình một carbon** (betaine, methionine, SAM) giảm ở chuột CC+ — tức là nguồn cung nhóm methyl bị thu hẹp.
3. Chuột CC+ nuôi bằng **chế độ ăn giàu chất béo** bị gan nhiễm mỡ nặng hơn và có **mức methyl hóa DNA toàn hệ gene giảm**.
4. **Hiệu ứng truyền sang thế hệ sau:** chuột con của mẹ CC+ có mức methyl hóa DNA ở não thấp hơn và biểu hiện hành vi lo âu nhiều hơn (thử nghiệm marble-burying), dù bản thân chúng được nuôi trong điều kiện giống nhau.

Phần RNA-seq mà nhóm 4 phân tích là **transcriptome gan** của chuột CC+ so với CC−. Cần chú ý vị trí của mảnh dữ liệu này trong bài báo: bằng chứng chính của tác giả nằm ở **chất chuyển hóa và methyl hóa DNA**, còn transcriptome là một lớp bằng chứng bổ trợ.

### Dữ liệu

Bộ dữ liệu này có **hai nguồn**, nhóm có thể dùng một nguồn hoặc dùng cả hai để đối chiếu.

| Thông tin         | Nội dung                                                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Mã GEO            | [GSE100983](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE100983)                                                                        |
| Mã recount3       | `SRP111408` (project `sra`, loài `mouse`)                                                                                                |
| Loài, mô         | Chuột C57BL/6, **gan**                                                                                                                   |
| Quy mô            | **8 mẫu**, 4 mẫu mỗi nhóm                                                                                                             |
| Nhóm so sánh     | **CC+** (cộng đồng chứa *E. coli* hoang dã, tiêu thụ choline) so với **CC−** (cộng đồng chứa *E. coli* Δ`cutC`) |
| Tuổi, giới tính | 9 tuần tuổi, **tất cả đều là chuột cái**                                                                                         |
| Điều kiện       | Cấy vi khuẩn 2 tuần, chế độ ăn chứa 1% choline, nhịn ăn 4 giờ trước khi lấy mẫu                                                  |

Về dạng dữ liệu, hai nguồn khác nhau rõ rệt:

| Nguồn   | File                                                                                                                | Dạng dữ liệu                                                                                                                                                  |
| -------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GEO      | `GSE100983_RAW.tar` — bên trong là **8 file riêng lẻ**, mỗi mẫu một file `*.genes.results.txt.gz` | Đầu ra của **RSEM**, gồm các cột `expected_count`, `TPM`, `FPKM`; 20.325 gene, định danh bằng **ký hiệu gene** (ví dụ `Slc4a4`) |
| GEO      | `GSE100983_EBseq_Outputs_Sorted_By_PPDE.csv.gz`                                                                   | **Kết quả phân tích sẵn** của nhóm tác giả (EBSeq), không phải dữ liệu đầu vào                                                             |
| recount3 | `sra.gene_sums.SRP111408.M023.gz`                                                                                 | Dạng **tổng độ phủ base** theo annotation Gencode M23, định danh bằng **Ensembl ID**                                                         |

Hai điểm cần tự xử lý trước khi phân tích:

- Phía GEO, ma trận biểu hiện **chưa tồn tại** — phải tự ghép 8 file từng mẫu lại. Cũng cần xác định xem cột nào trong file RSEM là cột phù hợp để đưa vào công cụ phân tích biểu hiện khác biệt.
- NCBI **không sinh sẵn** ma trận count cho series này (nút tải count matrix của GEO trả về lỗi), nên không có đường tắt.

Quy mô 4 mẫu mỗi nhóm là nhỏ nhất trong năm case study. Hãy để điều đó ảnh hưởng tới cách nhóm đặt câu hỏi và cách nhóm phát biểu kết luận.

# 5. Case study 5: Gene and metabolite time-course response to cigarette smoking in mouse lung and plasma

Case study này sử dụng bài báo:

> Miller M. A., Danhorn T., Cruickshank-Quinn C. I., Leach S. M., Jacobson S., Strand M. J., Reisdorph N. A., Bowler R. P., Petrache I., Kechris K. (2017). Gene and metabolite time-course response to cigarette smoking in mouse lung and plasma. *PLoS ONE* 12(6): e0178281. PMID 28575117. https://doi.org/10.1371/journal.pone.0178281
>
> Toàn văn: https://pmc.ncbi.nlm.nih.gov/articles/PMC5456044/
>
> Dữ liệu: [GSE76205](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE76205) · recount3 `SRP067636`

### Câu hỏi nghiên cứu của bài báo

**Phổi thay đổi theo thời gian như thế nào khi bị phơi nhiễm khói thuốc lá kéo dài, và những thay đổi đó có hồi phục được sau khi cai thuốc hay không?**

Bệnh phổi tắc nghẽn mạn tính (COPD) do hút thuốc lá lâu dài gây ra, nhưng có một quan sát lâm sàng khó giải thích: bệnh **vẫn tiếp tục tiến triển ở nhiều bệnh nhân sau khi họ đã cai thuốc**. Nếu khói thuốc chỉ gây hại trong lúc còn hút, cai thuốc phải chặn được bệnh. Thực tế không như vậy.

Câu hỏi này đòi hỏi một điều mà hầu hết nghiên cứu không có: **trục thời gian**. Nhóm tác giả thiết kế thí nghiệm gồm sáu mốc thời gian phơi nhiễm, cộng thêm một nhóm riêng dành cho câu hỏi về cai thuốc:

| Nhóm             | Nội dung                                                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **CS**      | Phơi nhiễm khói thuốc liên tục, lấy mẫu phổi ở 6 mốc: 1 ngày, 7 ngày, 1 tháng, 3 tháng, 6 tháng, 9 tháng |
| **AC**      | Chuột cùng lứa, hít khí phòng, lấy mẫu ở cùng các mốc thời gian — nhóm đối chứng                        |
| **6CS+3AC** | Phơi nhiễm khói thuốc 6 tháng, rồi **chuyển sang khí phòng 3 tháng**, lấy mẫu ở mốc 9 tháng          |

Nhóm **6CS+3AC** là chìa khóa của bài báo. Nó cùng tuổi với nhóm CS 9 tháng và nhóm AC 9 tháng, nên so sánh ba nhóm này ở cùng một thời điểm sẽ trả lời được câu hỏi hồi phục mà không lẫn với yếu tố tuổi.

Ngoài RNA-seq phổi, nhóm tác giả còn đo **chuyển hóa (metabolomics) trên huyết tương của cùng những con chuột đó**, rồi đối chiếu hai lớp dữ liệu.

Các kết luận chính của bài báo:

1. Các con đường chuyển hóa **glutathione** và **gene nhịp sinh học (circadian)** bị thay đổi — xác nhận lại những phát hiện đã biết trước đó.
2. Phát hiện mới: **chuyển hóa pyrimidine** và **hệ tín hiệu phosphatidylinositol** cũng bị rối loạn.
3. **Gần như tất cả các con đường đều hồi phục sau khi cai thuốc — trừ con đường lysosome.** Đây là ứng viên giải thích vì sao bệnh vẫn tiến triển sau cai thuốc.
4. Thay đổi chuyển hóa quan sát trong phổi **phản ánh được trên huyết tương**, tức là có thể tìm chỉ dấu trong máu thay vì phải sinh thiết phổi.

### Dữ liệu

| Thông tin            | Nội dung                                                                               |
| --------------------- | --------------------------------------------------------------------------------------- |
| Mã GEO               | [GSE76205](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE76205)                  |
| Mã recount3          | `SRP067636` (project `sra`, loài `mouse`)                                        |
| Loài, mô            | Chuột C57BL/6 cái, **phổi toàn phần**                                        |
| Quy mô               | **62 mẫu**, khoảng 4–5 mẫu mỗi tổ hợp nhóm × thời điểm                |
| Dạng dữ liệu (GEO) | **Raw count**, file `GSE76205_mouse126_all_reads.csv.gz`, 24.272 dòng, 62 cột |

Phân bố mẫu:

| Thời điểm | AC | CS | 6CS+3AC |
| ------------ | -- | -- | ------- |
| 1 ngày      | 5  | 4  | —      |
| 7 ngày      | 5  | 5  | —      |
| 1 tháng     | 5  | 5  | —      |
| 3 tháng     | 5  | 5  | —      |
| 6 tháng     | 4  | 5  | —      |
| 9 tháng     | 4  | 5  | 5       |

Trên GEO, series này có **ba file ma trận khác nhau** (`all_reads`, `filtered_reads`, `filtered_9month_reads`). Hãy tự xác định file nào phù hợp với câu hỏi nhóm đặt ra, và ghi rõ lựa chọn đó trong bản thảo.

Một điểm cần lưu ý về tên cột: tên cột trong file ma trận **không chứa thông tin nhóm hay thời điểm**. Thông tin đó nằm trong phần mô tả mẫu trên trang GEO của series. Việc ghép hai nguồn này lại là bước đầu tiên nhóm phải làm, và làm sai bước này thì mọi kết quả sau đó đều sai mà không có cảnh báo nào.

---

# 6. Case study 6: Transcriptomic RNAseq drug screen in cerebrocortical cultures

Case study này sử dụng bài báo:

> Hadwen J., Schock S., Mears A., Yang R., Charron P., Zhang L., Xi H. S., MacKenzie A. (2018). Transcriptomic RNAseq drug screen in cerebrocortical cultures: toward novel neurogenetic disease therapies. *Human Molecular Genetics* 27(18): 3206–3217. PMID 29901742. https://doi.org/10.1093/hmg/ddy221
>
> Dữ liệu: [GSE110256](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE110256) · recount3 `SRP132346`

### Câu hỏi nghiên cứu của bài báo

**Trong số các thuốc đã được phê duyệt lâm sàng, thuốc nào làm thay đổi mức biểu hiện của những gene gây bệnh di truyền thần kinh — và do đó có thể dùng lại cho những bệnh hiếm hiện chưa có thuốc?**

Bài toán nền là một bài toán kinh tế hơn là sinh học. Đã biết hơn 4.500 kiểu gene gây bệnh hiếm, nhưng **chỉ khoảng 5% có thuốc điều trị**. Mỗi bệnh quá ít bệnh nhân để một chương trình phát triển thuốc truyền thống có thể hoàn vốn. Lối ra khả thi là **tái định hướng thuốc** (drug repurposing): dùng thuốc đã được phê duyệt cho bệnh khác.

Logic sinh học để làm việc đó: rất nhiều bệnh di truyền phát sinh do **lượng protein quá nhiều hoặc quá ít**, chứ không phải do protein mất hoàn toàn chức năng. Nếu tìm được thuốc kéo mức biểu hiện về phía bình thường, thuốc đó có tiềm năng điều trị. Ví dụ điển hình là bệnh thần kinh ngoại biên Charcot-Marie-Tooth type 1A, do **nhân đôi gene `PMP22`** — ở đây thuốc cần làm *giảm* biểu hiện.

Thiết kế của bài báo được quyết định bởi quy mô, không phải bởi mong muốn:

| Đặc điểm     | Nội dung                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------- |
| Hệ thống       | Nuôi cấy sơ cấp **tế bào vỏ não chuột**, 21 ngày in vitro                             |
| Số điều kiện | **218 thuốc** đã thử nghiệm lâm sàng và **đi qua được hàng rào máu–não** |
| Số lần lặp    | **Một lần lặp cho mỗi thuốc**                                                              |
| Đối chứng     | **9 mẫu vehicle** (dung môi, không thuốc)                                                   |

Hãy đọc kỹ hai dòng cuối của bảng trên trước khi lên kế hoạch phân tích. Thiết kế này **không giống** bất kỳ case study nào khác trong tập đề: không có nhóm so với nhóm, mà là 218 điều kiện đơn lẻ so với một nhóm đối chứng dùng chung. Bố trí như vậy là lựa chọn bắt buộc khi sàng lọc ở quy mô lớn, và nó quyết định những gì phân tích có thể và không thể kết luận.

Các kết luận chính của bài báo:

1. Tạo được một **cơ sở dữ liệu tra cứu** mức biểu hiện toàn hệ gene dưới tác động của 218 thuốc — bản thân bộ dữ liệu là sản phẩm chính.
2. Khai thác cơ sở dữ liệu đó, tác giả tìm ra **liên hệ mới giữa hormone tuyến giáp và biểu hiện gene `Pmp22`**.
3. Liên hệ này được **kiểm chứng lại bằng ba phương pháp độc lập**: qRT-PCR, western blot và nhuộm miễn dịch huỳnh quang.

Điểm 3 là phần nhóm 6 cần chú ý nhất về mặt phương pháp luận. Tác giả **không coi kết quả RNA-seq là kết luận**; họ coi đó là **danh sách ứng viên** rồi mang đi kiểm chứng bằng thí nghiệm khác. Thiết kế một lần lặp cho phép quét rộng, nhưng không cho phép khẳng định.

### Dữ liệu

| Thông tin            | Nội dung                                                                                            |
| --------------------- | ---------------------------------------------------------------------------------------------------- |
| Mã GEO               | [GSE110256](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE110256)                             |
| Mã recount3          | `SRP132346` (project `sra`, loài `mouse`)                                                     |
| Loài, mô            | Chuột (phôi F1 FVBN × C3B6F1), **nuôi cấy tế bào vỏ não sơ cấp**, 21 ngày in vitro |
| Quy mô               | **227 mẫu** = 218 thuốc + 9 vehicle                                                          |
| Dạng dữ liệu (GEO) | Hai file: `GSE110256_combined.count.txt.gz` và `GSE110256_combined.rpkm.txt.gz`, 31.689 dòng   |

File count trên GEO **không chỉ có cột mẫu**: vài cột đầu là thông tin chú giải gene và một số cột thống kê. Hãy đọc dòng tiêu đề trước khi cắt ma trận.

Tên cột trong file ma trận là **mã thư viện giải trình tự**, không phải tên thuốc. Tên thuốc nằm trong phần mô tả mẫu trên GEO. Nhóm phải tự ghép hai nguồn.

Với thiết kế này, câu hỏi nghiên cứu nhóm đặt ra có thể sẽ phải khác về bản chất so với câu hỏi "nhóm A khác nhóm B ở những gene nào". Hãy chọn một câu hỏi mà thiết kế dữ liệu thật sự trả lời được, và nói rõ trong bản thảo vì sao câu hỏi đó phù hợp với thiết kế.

---

# 7. Case study 7: Multicellular Transcriptional Analysis of Mammalian Heart Regeneration

Case study này sử dụng bài báo:

> Quaife-Ryan G. A., Sim C. B., Ziemann M., Kaspi A., Rafehi H., Ramialison M., El-Osta A., Hudson J. E., Porrello E. R. (2017). Multicellular Transcriptional Analysis of Mammalian Heart Regeneration. *Circulation* 136(12): 1123–1139. PMID 28733351. https://doi.org/10.1161/CIRCULATIONAHA.117.028252
>
> Toàn văn: https://pmc.ncbi.nlm.nih.gov/articles/PMC5598916/
>
> Dữ liệu: [GSE95755](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE95755) · recount3 `SRP101460`

### Câu hỏi nghiên cứu của bài báo

**Vì sao tim chuột sơ sinh tái tạo được sau tổn thương, còn tim trưởng thành thì không — và cái gì đã mất đi trong quá trình trưởng thành?**

Đây là một câu hỏi lâu năm của y học tim mạch. Tim chuột **ngày đầu sau sinh (P1)** có khả năng tái tạo gần như hoàn toàn sau nhồi máu cơ tim; khả năng đó **mất đi chỉ trong vòng một tuần**. Tim người trưởng thành cũng không tái tạo được, nên mỗi lần nhồi máu là một lần mất cơ tim không hồi phục.

Khó khăn của câu hỏi: tim không phải một loại tế bào. Một tín hiệu quan sát được trên mô tim toàn phần có thể đến từ tế bào cơ tim, nguyên bào sợi, tế bào nội mô hay bạch cầu — và bốn loại này phản ứng với tổn thương theo những cách hoàn toàn khác nhau. Nhóm tác giả giải bằng cách **tách riêng từng loại tế bào bằng FACS trước khi giải trình tự**:

| Chiều         | Các mức                                                                                                                              |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Tổn thương  | **MI** (nhồi máu cơ tim) so với **Sham** (phẫu thuật giả)                                                           |
| Độ tuổi     | **P1** (sơ sinh, tái tạo được) so với **P56** (trưởng thành, không tái tạo được)                           |
| Loại tế bào | **Myo** (tế bào cơ tim), **Fibro** (nguyên bào sợi), **CD31** (tế bào nội mô), **CD45** (bạch cầu) |

Toàn bộ các tổ hợp đều có mẫu, mỗi tổ hợp 4 lần lặp. Mẫu được lấy **ngày thứ 3 sau mổ**. Ngoài RNA-seq, nhóm tác giả còn làm **ATAC-seq** trên nhân tế bào cơ tim ở ba mốc tuổi (P1, P14, P56) để đo mức mở của chromatin.

Các kết luận chính của bài báo — và đây là phần cần đọc cẩn thận:

1. Có một số gene đáp ứng với tổn thương ở cả trạng thái tái tạo được và không tái tạo được.
2. **Nhưng phần lớn thay đổi biểu hiện ở mọi loại tế bào là do trưởng thành phát triển từ sơ sinh sang trưởng thành, chứ không phải do một chương trình gene đặc hiệu cho tái tạo.** Đây là kết luận phản trực giác nhất của bài báo.
3. Bạch cầu và nguyên bào sợi **trưởng thành** vẫn bật được mạng gene tăng sinh sau nhồi máu, giống như ở sơ sinh.
4. Riêng **tế bào cơ tim trưởng thành thì không** bật lại được mạng gene tăng sinh đó — và dữ liệu ATAC-seq cho thấy vùng chromatin quanh các gene chu kỳ tế bào đã **đóng lại** trong quá trình trưởng thành. Rào cản là biểu sinh, không phải thiếu tín hiệu.

Kết luận 2 có một hệ quả trực tiếp với cách nhóm 7 thiết kế phân tích: trong bộ dữ liệu này, **tuổi là yếu tố biến thiên mạnh nhất**. Một phân tích không tính đến điều đó sẽ gán cho tổn thương những khác biệt thực chất do tuổi.

### Dữ liệu

| Thông tin             | Nội dung                                                                                                    |
| ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| Mã GEO                | [GSE95755](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE95755)                                       |
| Mã recount3           | `SRP101460` (project `sra`, loài `mouse`)                                                             |
| Loài, mô             | Chuột, **bốn loại tế bào tim tách bằng FACS**                                                   |
| Quy mô                | **64 mẫu** = 2 (MI/Sham) × 2 (P1/P56) × 4 (loại tế bào) × 4 lần lặp, đầy đủ mọi tổ hợp |
| Thời điểm lấy mẫu | Ngày thứ 3 sau phẫu thuật                                                                                |

Về dạng dữ liệu, **đây là điểm khác biệt quan trọng nhất của case study này**:

| Nguồn   | File                                                               | Dạng dữ liệu                                                            |
| -------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| GEO      | `GSE95755_MultiCellularRNAseq_EdgeR_CPM.txt.gz`                  | **CPM đã chuẩn hóa bằng edgeR**                                 |
| GEO      | `GSE95755_MultiCellularRNAseq_AllSignificantRegulatedGenes.xlsx` | Danh sách gene có ý nghĩa — kết quả phân tích sẵn của tác giả |
| recount3 | `sra.gene_sums.SRP101460.M023.gz`                                | Dạng **tổng độ phủ base** theo annotation Gencode M23           |

Trên GEO **không có ma trận count thô**, và nút tải count matrix do NCBI sinh cũng không có cho series này. Hai file GEO ở trên là dữ liệu đã qua xử lý.

Trước khi chọn nguồn dữ liệu và công cụ phân tích, hãy xác định rõ dạng dữ liệu của từng file và đối chiếu với giả định đầu vào của công cụ mà nhóm dự định dùng. Chọn sai ở bước này, công cụ **vẫn chạy và vẫn cho ra bảng kết quả**, nên sẽ không có thông báo lỗi nào để nhóm nhận ra.

Thiết kế ba chiều đầy đủ của bộ dữ liệu này cho phép đặt những câu hỏi mà các case study khác không đặt được. Hãy tận dụng, nhưng cũng hãy chọn một phạm vi mà nhóm làm xong được trong thời gian có.
