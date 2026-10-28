# Không gian làm việc
Đây là thư mục home của học viên trong khóa thực hành, gồm:
- agents/: định nghĩa các AI agent, mỗi agent một file (ví dụ agents/BioinformaticianAgent.md).
- tinh_huong_1/, tinh_huong_2/, ...: mỗi thư mục là một dự án. Mỗi dự án có file PROJECT.md mô tả mục tiêu, dữ liệu, thành viên, quy trình và thư mục kết quả.

# Nguyên tắc tách bạch
- File trong agents/ mô tả **năng lực nghề nghiệp** của agent: là ai, giỏi gì, làm việc theo cách nào. Những file này dùng chung cho mọi dự án.
- File PROJECT.md mô tả **đặc thù của dự án**: đề tài, bối cảnh chuyên môn, thiết kế thí nghiệm, tên file dữ liệu, phương pháp dự kiến.
- Nếu một thông tin chỉ đúng với một dự án, nó thuộc về PROJECT.md, **không được viết vào file định nghĩa agent**.

# Cách nhận việc
- Khi tôi yêu cầu "đóng vai <TênAgent>, làm việc cho dự án <thư mục dự án>": đọc agents/<TênAgent>.md và <thư mục dự án>/PROJECT.md trước khi làm bất cứ việc gì, rồi chỉ làm đúng vai trò đó.
- Mọi đường dẫn trong file định nghĩa agent và trong PROJECT.md (ví dụ 00_RawData/, scripts/) đều tính từ thư mục dự án.
- Chỉ đọc và ghi trong thư mục dự án được giao. Không sửa file trong agents/ và trong các dự án khác, trừ khi tôi yêu cầu.

# Quy tắc chung cho mọi agent, mọi dự án
- Trước khi làm, trình bày ngắn gọn kế hoạch và chờ tôi đồng ý.
- Không xóa, sửa, đổi tên hay ghi đè file trong các thư mục 00_* của dự án (dữ liệu đầu vào).
- Không tự cài thêm phần mềm. Nếu thiếu công cụ, dừng lại và báo tôi.
- Server dùng chung cho cả lớp: mỗi lệnh dùng tối đa 2 luồng (threads), không chạy song song nhiều lệnh nặng.
- Kiểm tra tham số bằng lệnh --help của công cụ đã cài, không dùng tham số theo trí nhớ.
- Viết lệnh vào script trong thư mục scripts/ của dự án rồi mới chạy. Ghi lỗi gặp phải và cách sửa vào logs/agent_log.md của dự án.
- Không bịa thông tin, số liệu hay trích dẫn. Nếu không chắc, ghi "chưa xác minh".
- Báo cáo viết bằng tiếng Việt; phân biệt rõ kết quả và giả thuyết.
