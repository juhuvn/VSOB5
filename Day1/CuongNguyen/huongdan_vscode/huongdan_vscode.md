# VSOB5

## Hướng dẫn thực hành cho học viên

**VS Code · Remote SSH · Codex · DeepSeek**

**Áp dụng cho tài khoản hv01 đến hv50**

Máy chủ: `vsob5.lobi.vn`

Tài khoản minh họa xuyên suốt: `hv01`

Phiên bản tài liệu: 2.0 | Ngày cập nhật: 26/10/2026

Tài liệu hướng dẫn từ bước cài VS Code trên Windows đến kết nối VSOB5, mở thư mục cá nhân và sử dụng Codex với DeepSeek trên máy chủ Linux.

**Trước khi làm:** nhận tên tài khoản và mật khẩu từ giảng viên hoặc quản trị viên. Mỗi học viên chỉ đăng nhập tài khoản được cấp. Khi tài liệu dùng `hv01`, thay bằng tài khoản của bạn trong dải `hv01` đến `hv50`.

> Ví dụ: học viên được cấp hv12 sử dụng lệnh ssh hv12@vsob5.lobi.vn và thư mục /home/hv12/. Không dùng hv01 chỉ vì tài khoản này xuất hiện trong ảnh.

Bản hướng dẫn sử dụng 36 ảnh chụp được sắp theo trình tự thao tác. Ảnh kiểm tra phiên bản và một số ảnh kết nối được dùng lại tại bước tương ứng để thuận tiện tra cứu.



<!-- pagebreak -->

## Mục lục

- 1. Chuẩn bị và phân biệt môi trường
- 2. Tải Visual Studio Code
- 3. Cài và khởi động VS Code
- 4. Cài Remote - SSH và mở kết nối
- 5. Thêm kết nối bằng tài khoản học viên
- 6. Mở kết nối sau khi lưu host
- 7. Chọn đúng tài khoản trước khi đăng nhập
- 8. Nhập mật khẩu SSH
- 9. Xác nhận kết nối và mở Explorer
- 10. Mở thư mục cá nhân của học viên
- 11. Hoàn tất mở thư mục từ xa
- 12. Mở terminal và kiểm tra tài khoản
- 13. Cài và kiểm tra Codex CLI
- 14. Khởi động Codex lần đầu
- 15. Cấu hình DeepSeek cho tài khoản hiện tại
- 16. Kiểm tra Codex sau cấu hình
- 17. Cài extension Codex trong phiên SSH
- 18. Chọn đúng tab Codex
- 19. Kết nối lại trong những lần sau
- 20. Xử lý lỗi SSH và tài khoản
- 21. Xử lý lỗi Codex và DeepSeek

<!-- pagebreak -->

## 1. Chuẩn bị và phân biệt môi trường

Chuẩn bị máy Windows có Internet, tài khoản VSOB5 được cấp và API key DeepSeek theo hướng dẫn của lớp. Nếu đơn vị yêu cầu VPN hoặc cổng SSH riêng, sử dụng đúng thông tin được cung cấp.

| Thành phần | Nơi sử dụng | Vai trò |
| --- | --- | --- |
| VS Code | Máy Windows | Giao diện soạn thảo và kết nối |
| Remote - SSH | VS Code trên Windows | Mở môi trường làm việc trên VSOB5 |
| Tài khoản hv01-hv50 | Máy chủ VSOB5 | Xác định người dùng và thư mục cá nhân |
| Codex CLI | Terminal Linux trên VSOB5 | Trợ lý chạy bằng dòng lệnh |
| Extension Codex | Phiên VS Code kết nối SSH | Giao diện Codex trong trình soạn thảo |
| API key DeepSeek | Cấu hình Codex của tài khoản Linux | Xác thực với nhà cung cấp mô hình |

**Quy ước trong hướng dẫn**

- Lệnh `powershell` chạy trên máy Windows cá nhân.
- Lệnh `bash` chạy trong terminal của VSOB5 sau khi kết nối SSH.
- Lệnh như `/status` hoặc `/model` nhập trong Codex CLI đang mở.
- Không chép phần dấu nhắc `hv01@lobi-server:~$` vào lệnh.

Trước khi bắt đầu, có thể mở PowerShell và kiểm tra SSH:

```powershell
ssh -V
```

Nếu lệnh không tồn tại, bật hoặc nhờ hỗ trợ cài OpenSSH Client trên Windows. Các lệnh cài Codex ở phía sau sẽ chạy trên máy chủ, vì vậy cần kết nối SSH thành công trước.



<!-- pagebreak -->

## 2. Tải Visual Studio Code

Trên máy Windows, mở [trang Visual Studio Code](https://code.visualstudio.com/), bấm **Download for Windows** và đợi tải xong. Bộ ảnh dùng bộ cài `VSCodeUserSetup-x64-1.143.1.exe`; số phiên bản có thể thay đổi.

![Hình 01. Trang tải VS Code trên Windows.](<img/Screenshot 2026-10-26 152908.png>)

![Hình 02. Trình duyệt đang tải bộ cài.](<img/Screenshot 2026-10-26 153000.png>)



<!-- pagebreak -->

## 3. Cài và khởi động VS Code

Trong Downloads của trình duyệt, bấm **Open file**. Thực hiện các bước của trình cài đặt, hoàn tất rồi mở Visual Studio Code.

![Hình 03. Mở bộ cài đã tải xong.](<img/Screenshot 2026-10-26 153031.png>)

![Hình 04. Màn hình Welcome sau khi mở VS Code.](<img/Screenshot 2026-10-26 153106.png>)

**Kiểm tra:** cửa sổ có thanh menu, Explorer và mục Welcome. Máy mới có thể không có danh sách Recent. Các mục trong Recent ở ảnh thuộc lịch sử máy chụp, không phải tài khoản học viên cần sử dụng.

<!-- pagebreak -->

## 4. Cài Remote - SSH và mở kết nối

1. Nhấn **Ctrl + Shift + X** để mở Extensions.
2. Tìm **Remote - SSH** của **Microsoft**, bấm **Install** nếu chưa có.
3. Nhấn biểu tượng kết nối từ xa ở góc dưới bên trái, chọn **Connect to Host...**. Hoặc dùng **Ctrl + Shift + P**, tìm **Remote-SSH: Connect to Host...**.

![Hình 05. Remote - SSH của Microsoft đã được cài; hiện Disable và Uninstall.](<img/Screenshot 2026-10-26 153150.png>)

![Hình 06. Menu kết nối từ xa; chọn Connect to Host...](<img/Screenshot 2026-10-26 153220.png>)



<!-- pagebreak -->

## 5. Thêm kết nối bằng tài khoản học viên

Chọn **Add New SSH Host...**, nhập lệnh dưới rồi nhấn **Enter**. Thay `hv01` bằng tài khoản của bạn:

```powershell
ssh hv01@vsob5.lobi.vn
```

Chọn file cấu hình SSH của người dùng Windows hiện tại, thường là `C:\Users\<ten-Windows>\.ssh\config`. Không thay `<ten-Windows>` bằng mã học viên trừ khi đó cũng là tên tài khoản Windows thực tế.

![Hình 07. Danh sách host và mục Add New SSH Host...](<img/Screenshot 2026-10-26 153247.png>)

![Hình 08. Nhập lệnh SSH với hv01 làm ví dụ.](<img/Screenshot 2026-10-26 153329.png>)

![Hình 09. Chọn file cấu hình SSH cá nhân trên Windows.](<img/Screenshot 2026-10-26 153353.png>)

Nếu lớp cấp cổng riêng, dùng `ssh -p PORT hv01@vsob5.lobi.vn`, thay `PORT` và tài khoản theo thông tin được cấp. Bộ ảnh sử dụng lệnh không khai báo cổng riêng.

<!-- pagebreak -->

## 6. Mở kết nối sau khi lưu host

Sau khi chọn file cấu hình, thông báo **Host added!** cho biết kết nối đã được lưu.

**Nếu vẫn thấy thông báo:** bấm **Connect** ở góc dưới bên phải. Nếu VS Code đã hỏi mật khẩu, chuyển đến **mục 8**.

**Nếu đã bỏ lỡ hoặc đóng thông báo:** không cần thêm host lại. Làm như sau:

1. Nhìn xuống **góc dưới bên trái** cửa sổ VS Code, bấm biểu tượng kết nối từ xa hình hai dấu góc đối nhau.
2. Menu **Select an option to open a Remote Window** hiện ở phía trên. Bấm dòng **Connect to Host...**; không chọn dòng **Connect to WSL** đang được tô sáng trong ảnh.
3. Danh sách host sẽ hiện ra. Tiếp tục **mục 7** để chọn tài khoản và máy chủ.

**Cách mở bằng bàn phím:** nhấn **Ctrl + Shift + P**, gõ `Remote-SSH: Connect to Host...`, chọn đúng lệnh rồi nhấn **Enter**. Cách này cũng đưa đến danh sách host ở mục 7.

![Hình 10. Có thể bấm Connect khi thông báo Host added! còn hiển thị.](<img/Screenshot 2026-10-26 153418.png>)

![Hình 11. Nếu bỏ lỡ thông báo, bấm biểu tượng góc dưới bên trái rồi chọn Connect to Host...](<img/Screenshot 2026-10-26 153635.png>)



<!-- pagebreak -->

## 7. Chọn đúng tài khoản trước khi đăng nhập

Sau khi chọn **Connect to Host...** ở mục 6, VS Code hiển thị ô **Select configured SSH host or enter user@host** và danh sách bên dưới.

1. Nếu host đã lưu ở mục 5 dùng đúng tài khoản của bạn, bấm **vsob5.lobi.vn** trong danh sách.
2. Nếu chưa chắc tài khoản được lưu, bấm ô nhập phía trên và gõ rõ `hv01@vsob5.lobi.vn`, thay `hv01` bằng tài khoản được cấp. Chọn dòng trùng với nội dung vừa nhập rồi nhấn **Enter**. Tại ô này chỉ nhập `user@host`, không thêm chữ `ssh`.
3. Chờ cửa sổ SSH mở ra. Khi xuất hiện yêu cầu mật khẩu, tiếp tục **mục 8**.

Đây là bước chọn kết nối để đăng nhập; không cần bấm **Add New SSH Host...** lần nữa nếu đã lưu host ở mục 5.

![Hình 12. Danh sách có tên host vsob5.lobi.vn.](<img/Screenshot 2026-10-26 153654.png>)

![Hình 13. Nhập rõ tài khoản và host để tránh đăng nhập nhầm.](<img/Screenshot 2026-10-26 154125.png>)

Nếu VS Code hỏi loại hệ điều hành máy chủ, chọn **Linux**. Nếu có bước xác nhận khóa máy chủ lần đầu, đối chiếu dấu vân tay với thông tin quản trị viên cung cấp trước khi chấp nhận.

Tên host hiển thị ở thanh trạng thái chỉ xác nhận máy chủ. Sau khi mở terminal, dùng `whoami` để xác nhận tài khoản.

<!-- pagebreak -->

## 8. Nhập mật khẩu SSH

VS Code mở cửa sổ từ xa và yêu cầu mật khẩu. Kiểm tra lời nhắc đang hỏi cho đúng tài khoản, ví dụ **hv01@vsob5.lobi.vn**, rồi nhập mật khẩu được cấp và nhấn **Enter**.

![Hình 14. Yêu cầu mật khẩu SSH cho hv01.](<img/Screenshot 2026-10-26 153441.png>)

![Hình 15. Mật khẩu được che khi nhập.](<img/Screenshot 2026-10-26 153941.png>)

Chờ thiết lập VS Code Server hoàn tất. Không gõ mật khẩu vào cửa sổ Chat hoặc terminal khi đang có hộp nhập mật khẩu riêng ở phía trên.

<!-- pagebreak -->

## 9. Xác nhận kết nối và mở Explorer

Quan sát góc dưới bên trái: **SSH: vsob5.lobi.vn** cho biết cửa sổ đã kết nối máy chủ. Bấm Explorer, rồi **Open Folder** để chọn thư mục làm việc.

![Hình 16. Thanh trạng thái hiển thị kết nối SSH tới VSOB5.](<img/Screenshot 2026-10-26 154251.png>)

![Hình 17. Explorer báo Connected to remote và có nút Open Folder.](<img/Screenshot 2026-10-26 154312.png>)



<!-- pagebreak -->

## 10. Mở thư mục cá nhân của học viên

Nhập đường dẫn thư mục của tài khoản được cấp. Ví dụ `hv01` mở `/home/hv01/`, còn `hv50` mở `/home/hv50/`. Nhấn **OK**.

Nếu xuất hiện câu hỏi tin cậy thư mục, chọn **Trust Folder & Continue** khi đó là thư mục của bạn hoặc nội dung bạn tin cậy.

![Hình 18. Chọn /home/hv01/ trong hộp Open Folder.](<img/Screenshot 2026-10-26 154334.png>)

![Hình 19. Xác nhận tin cậy thư mục vừa mở.](<img/Screenshot 2026-10-26 154355.png>)

Danh sách thư mục cấu hình trong ảnh có thể khác trên tài khoản mới. Chưa có `.codex` hoặc `.local` trước khi cài đặt không nhất thiết là lỗi.

<!-- pagebreak -->

## 11. Hoàn tất mở thư mục từ xa

VS Code có thể hỏi lại mật khẩu khi nạp thư mục hoặc mở terminal. Nhập lại mật khẩu của cùng tài khoản, rồi chờ Explorer tải xong.

![Hình 20. Mở thư mục hv01 và được hỏi lại mật khẩu.](<img/Screenshot 2026-10-26 154516.png>)

![Hình 21. Nhập mật khẩu lần nữa khi được yêu cầu.](<img/Screenshot 2026-10-26 154539.png>)

**Kiểm tra:** tên thư mục ở Explorer là tài khoản của bạn, kèm `[SSH: vsob5.lobi.vn]`. Nếu thấy tài khoản khác, hãy ngắt kết nối và đăng nhập lại đúng người dùng.

<!-- pagebreak -->

## 12. Mở terminal và kiểm tra tài khoản

Chọn **Terminal > New Terminal**. Terminal cần chạy trên VSOB5; ảnh minh họa có dấu nhắc `hv01@lobi-server:~$`.

![Hình 22. Vị trí menu Terminal trên thanh công cụ.](<img/Screenshot 2026-10-26 155016.png>)

![Hình 23. Explorer và terminal của tài khoản hv01 trên VSOB5.](<img/Screenshot 2026-10-26 154656.png>)

![Hình 24. Dấu nhắc Linux trong terminal từ xa.](<img/Screenshot 2026-10-26 155045.png>)

```bash
whoami
echo "$HOME"
pwd
```

Kết quả mong đợi với tài khoản minh họa: `whoami` là `hv01`, thư mục cá nhân là `/home/hv01`. Tên `lobi-server` trong dấu nhắc có thể khác tên miền SSH và không phải lỗi.

<!-- pagebreak -->

## 13. Cài và kiểm tra Codex CLI

Chạy trong terminal Linux của tài khoản học viên:

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Đợi bộ cài kết thúc, mở terminal mới nếu được yêu cầu rồi chạy `codex --version`. Ảnh minh họa trả về `codex-cli 0.164.0`.

![Hình 25. Chạy script cài Codex từ terminal của hv01.](<img/Screenshot 2026-10-26 155127.png>)

![Hình 26. Kiểm tra phiên bản: codex --version trả về codex-cli 0.164.0.](<img/Screenshot 2026-10-26 163934.png>)

**Kiểm tra:** lệnh trả về phiên bản Codex và quay lại dấu nhắc terminal. Số phiên bản có thể khác ảnh nếu bộ cài đã được cập nhật.

Lệnh cài tham khảo [tài liệu Codex CLI của OpenAI](https://learn.chatgpt.com/docs/codex/cli).

<!-- pagebreak -->

## 14. Khởi động Codex lần đầu

Gõ lệnh sau trong terminal:

```bash
codex
```

![Hình 27. Mở Codex lần đầu.](<img/Screenshot 2026-10-26 155235.png>)

![Hình 28. Màn hình lựa chọn cách đăng nhập ban đầu.](<img/Screenshot 2026-10-26 160118.png>)

Để tiếp tục theo quy trình DeepSeek, khởi động Codex ít nhất một lần rồi thoát về Bash, chẳng hạn bằng **Ctrl + C**, và làm mục tiếp theo. Không nhập API key DeepSeek vào lựa chọn **Use an OpenAI API key**.

Nếu lớp hướng dẫn dùng ChatGPT hoặc OpenAI thay cho DeepSeek, thực hiện theo phương thức đăng nhập tương ứng. Các mục cấu hình tiếp theo áp dụng cho DeepSeek.

<!-- pagebreak -->

## 15. Cấu hình DeepSeek cho tài khoản hiện tại

Trong Bash trên VSOB5, chạy:

```bash
bash <(curl -fsSL https://cdn.deepseek.com/api-docs/codex-deepseek-setup-en.sh)
```

Theo menu trong ảnh, chọn **2** để dùng `deepseek-v4-pro`. Mục **1** là `deepseek-flash`; mục **9** khôi phục cấu hình mặc định. Kiểm tra tên mô hình nếu số thứ tự menu thay đổi.

![Hình 29. Chạy trình cấu hình DeepSeek dưới tài khoản hv01.](<img/Screenshot 2026-10-26 160310.png>)

![Hình 30. Cài lần đầu: chọn 2 rồi nhập API key DeepSeek khi được yêu cầu.](<img/Screenshot 2026-10-26 163751.png>)

![Hình 31. Chạy codex --version để kiểm tra phiên bản Codex CLI.](<img/Screenshot 2026-10-26 163934.png>)

**Cài lần đầu:** màn hình có dòng `First-time install` và yêu cầu API key. Nhập key được cấp hoặc tạo tại [DeepSeek API keys](https://platform.deepseek.com/api_keys), rồi nhấn **Enter**. Không dùng key của học viên khác.

**Kiểm tra phiên bản:** sau khi hoàn tất và quay về terminal, chạy `codex --version` như hình 31. Lệnh này kiểm tra phiên bản CLI; để kiểm tra mô hình DeepSeek, mở Codex theo mục tiếp theo.

Kiểm tra đường dẫn Codex thuộc tài khoản của bạn, ví dụ `/home/hv01/.codex`. Cấu hình trên hv01 không có nghĩa hv02-hv50 cũng đã được cấu hình. [Nguồn đối chiếu: hướng dẫn DeepSeek](https://api-docs.deepseek.com/quick_start/agent_integrations/codex/).

<!-- pagebreak -->

## 16. Kiểm tra Codex sau cấu hình

Sau khi script hoàn tất, mở lại `codex`. Kiểm tra mô hình hiển thị là **DeepSeek-V4-Pro** theo lựa chọn của lớp.

![Hình 32. Khởi động lại Codex sau cấu hình.](<img/Screenshot 2026-10-26 160417.png>)

![Hình 33. CLI hiển thị DeepSeek-V4-Pro high.](<img/Screenshot 2026-10-26 160434.png>)

Nhập các lệnh sau **trong Codex CLI**:

- `/status`: xem cấu hình phiên hiện tại.
- `/model`: xem hoặc thay đổi mô hình và mức suy luận.
- `/permissions`: kiểm tra quyền thực hiện của Codex.
- `/review`: xem xét các thay đổi trong dự án khi cần.

Ảnh có **1 warning · f2 to view**. Nhấn **F2** nếu thấy cảnh báo để đọc nội dung cụ thể. Không suy ra nguyên nhân chỉ từ số lượng cảnh báo. Tên mô hình xuất hiện chưa thay thế bước thử một yêu cầu thực tế.

<!-- pagebreak -->

## 17. Cài extension Codex trong phiên SSH

1. Trong cửa sổ kết nối VSOB5, mở Extensions bằng **Ctrl + Shift + X**.
2. Tìm **Codex - OpenAI’s coding agent**, nhà phát hành **OpenAI**, identifier `openai.chatgpt`.
3. Bấm **Install** hoặc **Install in SSH: vsob5.lobi.vn** nếu có.
4. Kiểm tra trạng thái **Extension is enabled on 'SSH: vsob5.lobi.vn'**.

![Hình 34. Trang extension Codex chính thức trước khi cài.](<img/Screenshot 2026-10-26 160638.png>)

![Hình 35. Codex đã được bật trên host SSH.](<img/Screenshot 2026-10-26 160657.png>)

Nếu VS Code yêu cầu Reload, thực hiện để nạp extension. Nhiều extension có tên gần giống Codex; kiểm tra nhà phát hành trước khi cài.

<!-- pagebreak -->

## 18. Chọn đúng tab Codex

Bảng bên phải có tab **Chat** và **Codex**. Trong bộ ảnh, tab Chat đang là Copilot; chọn **Codex** để mở giao diện Codex riêng và kiểm tra mô hình ở cuối ô nhập.

![Hình 36. Tab Chat đang dùng Copilot và hiển thị Quota reached.](<img/Screenshot 2026-10-26 160851.png>)

![Hình 37. Tab Codex riêng hiển thị DeepSeek-V4-Pro High.](<img/Screenshot 2026-10-26 161103.png>)

Thông báo quota trong tab Copilot không chứng minh DeepSeek đã hết hạn mức. Ảnh tab Codex có tiêu đề một cuộc trò chuyện cũ chứa đoạn lỗi bị cắt ngắn; đó chưa đủ để xác định lỗi hiện tại. Hãy tạo cuộc trò chuyện mới để kiểm tra phản hồi thực tế.

<!-- pagebreak -->

## 19. Kết nối lại trong những lần sau

Bấm biểu tượng kết nối từ xa ở góc dưới bên trái, chọn **Connect to Host...** như hình dưới. Chọn kết nối đã lưu hoặc nhập rõ tài khoản và host. Sau khi đăng nhập, mở thư mục cá nhân hoặc dự án đã dùng.

![Hình 38. Mở menu kết nối từ xa và chọn Connect to Host...](<img/Screenshot 2026-10-26 153635.png>)

![Hình 39. Chọn tài khoản và host khi kết nối lần sau.](<img/Screenshot 2026-10-26 154125.png>)

![Hình 40. Mở thư mục làm việc, thay hv01 bằng tài khoản của bạn.](<img/Screenshot 2026-10-26 154334.png>)

**Mỗi buổi làm việc:** kiểm tra host SSH, chạy `whoami`, mở đúng dự án, mở Codex và kiểm tra mô hình. Không cần cài lại toàn bộ nếu các bước kiểm tra đều đạt.

**Khi kết thúc:** lưu file, kết thúc tác vụ đang chạy phù hợp rồi chọn **File > Close Remote Connection**. Tác vụ cần chạy lâu sau khi ngắt kết nối phải dùng phương án giảng viên hoặc quản trị viên hỗ trợ.

<!-- pagebreak -->

## 20. Xử lý lỗi SSH và tài khoản

**Không có Connect to Host...**

Kiểm tra Remote - SSH của Microsoft đã cài và bật. Tìm đầy đủ **Remote-SSH: Connect to Host...** trong Command Palette.

**Sai tài khoản hoặc đường dẫn**

Giữ đúng định dạng hai chữ số: `hv01`, không phải `hv1`. Nếu được cấp hv12, phải đăng nhập hv12 và mở `/home/hv12/`. Dùng `whoami` và `echo "$HOME"` để kiểm tra thực tế. Không tự mở thư mục của học viên khác để thay thế.

**Không đăng nhập được**

Thử kết nối trong PowerShell, thay tên tài khoản cho đúng:

```powershell
ssh hv01@vsob5.lobi.vn
```

Nếu không tìm được host hoặc hết thời gian kết nối, kiểm tra mạng/VPN theo yêu cầu lớp. Nếu bị từ chối xác thực, kiểm tra tài khoản và mật khẩu hoặc SSH key được cấp. Không đoán mật khẩu của tài khoản khác.

**Dừng ở Setting up SSH Host**

Mở **View > Output**, chọn **Remote - SSH** để đọc log. Gửi thông báo lỗi cùng thời điểm cho người hỗ trợ. Cần kiểm tra mạng, dung lượng hoặc quyền ghi dựa trên lỗi thực tế.

**Lệnh Bash báo lỗi trong PowerShell**

Chuyển sang cửa sổ có thanh trạng thái **SSH: vsob5.lobi.vn** và mở terminal ở đó. Lệnh `bash <(...)` trong hướng dẫn phải chạy từ Bash trên VSOB5; nếu terminal từ xa dùng shell khác, chạy `bash` trước.



<!-- pagebreak -->

## 21. Xử lý lỗi Codex và DeepSeek

**codex: command not found hoặc chạy nhầm bản cài**

Mở terminal mới rồi chạy các lệnh kiểm tra trên máy chủ:

```bash
command -v codex
type -a codex
codex --version
```

Nếu Codex được cài theo người dùng ở `~/.local/bin` và file này thực sự tồn tại nhưng chưa vào PATH, có thể thử cho terminal hiện tại:

```bash
export PATH="$HOME/.local/bin:$PATH"
codex --version
```

Nếu có nhiều bản, báo quản trị viên kèm kết quả đường dẫn. Không tự gỡ bản ở `/usr/local/bin` hoặc dùng sudo để thay đổi cài đặt chung.

**DeepSeek chưa xuất hiện hoặc API báo lỗi**

Kiểm tra script đã chạy dưới đúng tài khoản hv của bạn. Đóng phiên Codex cũ, mở lại và xem `/status`, `/model`. Nếu tài khoản mới được hỏi API key, dùng key được cấp cho mình. Kiểm tra hiệu lực key, quyền mô hình và hạn mức theo mã lỗi thực tế.

**CLI hoạt động nhưng extension không chạy**

Kiểm tra extension chính thức đang bật trên host SSH. Thử **Developer: Reload Window** rồi mở lại tab Codex. Xác nhận CLI và extension đang dùng cùng tài khoản trên VSOB5. Nếu gặp lỗi daemon, ghi lại đầy đủ thông báo và đường dẫn bản cài để nhờ hỗ trợ; tiêu đề chat bị cắt trong ảnh không đủ chẩn đoán.

**Muốn khôi phục cấu hình DeepSeek**

Chạy lại script chính thức, đọc lựa chọn **9** và hướng dẫn khôi phục của DeepSeek trước khi xác nhận. Không xóa cấu hình của học viên khác hoặc chia sẻ nguyên file cấu hình nếu chứa key.


