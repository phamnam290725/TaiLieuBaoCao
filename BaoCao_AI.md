# Báo cáo tổng hợp về AI Agent và các Model hiện nay
----------------------------------------------------

# 1. Bản chất AI Agent khác gì LLM thường?
- Về cơ bản, Agent = LLM + Công cụ (Tools) + Vòng lặp + Mục tiêu
- Thay vì chỉ hỏi-đáp 1 lượt như LLM, Agent có khả năng tự chạy theo vòng lặp (quan sát → suy nghĩ → hành động) cho đến khi hoàn thành mục tiêu
- Điểm "ăn tiền" nhất là nó biết tự nhận phản hồi từ công cụ (ví dụ chạy lỗi) để tự sửa sai ngay trong lúc làm, điều mà LLM một lượt không làm được

# 2. Các nhóm AI Agent nổi bật trên thị trường
+ Thị trường có rất nhiều, nhưng thực tiễn nhất hiện nay chia thành các nhóm:
- Agent lập trình (Cursor, Devin, Claude Code): Đây là nhóm trưởng thành nhất, có khả năng tự đọc toàn bộ kho code (repo), tự sửa nhiều file, chạy test và tự fix lỗi
==> Rất hợp để em dev áp dụng vào project
- Agent tự động hoá (AI Agent, Zapier): Kết nối các dịch vụ API, cho phép AI tự quyết định luồng xử lý linh hoạt thay vì code luồng "nếu... thì..." cứng nhắc
- Agent nghiên cứu: Tự lên kế hoạch tìm kiếm, tổng hợp từ hàng chục nguồn ra một báo cáo hoàn chỉnh có trích dẫn

# 3. Các Model "bộ não" mạnh nhất cho Agent
+ Agent, người ta thường phân tầng: dùng model mạnh để suy luận chính, model nhẹ để đọc file vặt cho rẻ
+ ĐÁNH GIÁ CHI TIẾT CÁC MODEL MẠNH NHẤT HIỆN NAY
(Tiêu chí: Cửa sổ ngữ cảnh hiện tại đều ở mức ~1 Triệu token nên không còn là yếu tố quyết định, quan trọng là Lập luận và Chi phí)
* Claude Fable 5.1 (Anthropic)  Chi phí: Rất đắt ($10 input / $50 output trên 1M token)|
- Điểm mạnh: Là model mạnh nhất của Anthropic, luôn bật suy nghĩ sâu, dành cho các tác vụ suy luận nặng nhất
- Điểm yếu: Chi phí cao và tốc độ trả lời chậm do luôn phải nghĩ kỹ. Không phù hợp cho các luồng xử lý nhanh

* Claude Opus 5 (Anthropic)
- Chi phí: $5 input / $25 output trên 1M token 
- Điểm mạnh: Cực mạnh về lập trình và chạy Agent nhiều bước. Có 5 nấc điều chỉnh độ sâu suy nghĩ linh hoạt (việc dễ nghĩ nhanh, việc khó nghĩ kỹ)
- Điểm yếu: Vẫn tốn kém nếu để chạy toàn bộ các tác vụ phụ trong vòng lặp Agent

* GPT-5.5 (OpenAI)
- Chi phí: Cạnh tranh trực tiếp với nhóm Opus/Fable
- Điểm mạnh: Độ phổ biến cao nhất, hệ sinh thái công cụ/API hỗ trợ cực kỳ rộng mở và dễ tích hợp nhất
- Điểm yếu: Tính năng tự điều chỉnh các nấc suy nghĩ chuyên sâu đôi khi chưa linh hoạt bằng cơ chế 5 nấc của Claude

* Gemini 3.1 Pro (Google)
- Chi phí: Thường tối ưu nhất khi chạy trong hệ sinh thái Google
- Điểm mạnh: Khả năng đa phương thức (Multimodal) vô đối. Xử lý cực tốt khi input là Ảnh, Video, Âm thanh
- Điểm yếu: Khả năng lập luận code logic thuần túy chưa bứt phá mạnh bằng nhóm Claude chuyên biệt

# 4. THẾ LỰC MÃ NGUỒN MỞ
+ Với các model mở có sức mạnh tương đương nhưng chi phí rẻ hơn hàng chục lần. Đây là cứu cánh thực sự cho AI Agent khi phải chạy nhiều vòng lặp tốn ngữ cảnh:

* DeepSeek (DeepSeek AI): "Kẻ phá bĩnh thị trường"
- Đặc điểm: Các dòng model của họ (đặc biệt là nhóm Coder và Reasoner) có khả năng lập luận và viết code tiệm cận 
- Giá trị cho Agent: Giá API của DeepSeek rẻ đến mức "phá giá" (chỉ bằng 1/10 đến 1/20 so với các ông lớn)
- Vì Agent chạy rất tốn ngữ cảnh khi gọi tool liên tục, dùng DeepSeek làm não bộ điều phối sẽ giúp tiết kiệm ngân sách khổng lồ mà vẫn đảm bảo độ thông minh logic

* Qwen (Alibaba Cloud)
- Đặc điểm: Hệ sinh thái model mở mạnh nhất Châu Á hiện tại, có đủ các phiên bản từ siêu nhẹ (0.5B) đến siêu nặng (72B+). Hỗ trợ đa ngôn ngữ 
- Giá trị cho Agent: Qwen thậm chí phát triển sẵn một framework riêng mang tên Qwen-Agent. Rất phù hợp nếu công ty muốn tự host (cài đặt cục bộ trên server công ty) để làm Agent xử lý dữ liệu nội bộ bảo mật mà không cần đẩy data lên server của OpenAI hay Google

* Llama (Meta)
- Đặc điểm: Tiêu chuẩn vàng của giới mã nguồn mở
- Giá trị cho Agent: Có thể tải về chạy offline. Cộng đồng developer hỗ trợ Llama làm Agent cực kỳ đông đảo, dễ dàng tìm thấy các tool và framework tích hợp sẵn
 
# 5. CHIẾN LƯỢC TỐI ƯU CHI PHÍ KHI DỰNG AGENT
Đặc thù của Agent là chạy lặp lại nhiều vòng, mỗi vòng lại nhồi thêm kết quả log của Tools vào ngữ cảnh (Context). Nếu cứ dùng model xịn chạy từ đầu đến cuối, chi phí sẽ tăng cấp số nhân và cạn kiệt bộ nhớ rất nhanh
- Ta sẽ sử dụng phân tầng theo 1 kế hoạch nhất định 

* Khi nào ĐƯỢC PHÉP dùng model xịn (Opus 5 / GPT-5.5): Chỉ gọi khi cần bộ não "Chỉ huy" — lúc Agent cần lập kế hoạch, đưa ra quyết định rẽ nhánh, hoặc khi gặp lỗi cần phân tích sâu để tự sửa sai  
* Khi nào BẮT BUỘC dùng model rẻ (Claude, Sonnet 5, hoặc Gemini Flash): Dùng cho các bộ phận "Chạy vặt" — lúc Agent gọi Tool để đọc file log dài, tóm tắt text, crawl web, hoặc bóc tách dữ liệu. Những việc này dùng model xịn là lãng phí
* Quản lý Context: Hệ thống bắt buộc phải có bước dùng model rẻ để tóm tắt, nén ngữ cảnh hoặc xóa bớt log cũ trước khi đưa lại cho não chính xử lý bước tiếp theo

-------------------------------------------------------
# Những điểm rút ra được 
- Tư duy làm chủ AI, dùng AI thông minh và bóc tách vấn đề, sau đó tự mình kiểm chứng và tổng hợp lại
- Tư duy nghiên cứu mở (Không tự trói chân), Khi tiếp cận một kiến thức mới, đừng giới hạn AI bằng những con số cứng nhắc ("hãy kể 3 ví dụ"). Hãy yêu cầu AI "phân loại", "vẽ ra bức tranh tổng quát" trước để nắm được khung sườn, rồi mới đi sâu vào từng nhánh
- Sử dụng đúng "tầng" công cụ của AI
====> Agent không phải là LLM thông minh hơn: Điểm cốt lõi là Agent = LLM + Công cụ (Tools) + Vòng lặp + Mục tiêu
- LLM chỉ biết trả lời câu hỏi bằng văn bản, còn Agent có "tay chân" (Tools) để tạo ra thay đổi thật và quan trọng nhất là có vòng lặp tự thực thi (Agentic loop) để tự sửa sai ngay trong lúc làm
- Nhìn ra "điểm nghẽn" của hệ thống: Một người làm kỹ thuật sâu sắc không chỉ nhìn vào những lời quảng cáo hào nhoáng (như model có 2 triệu token)
- Mà ta Phải nhìn ra rào cản thực tế: khi Agent chạy liên tục qua nhiều vòng lặp, nó sẽ liên tục nhồi kết quả từ Tools vào, khiến Cửa sổ ngữ cảnh (Context Window) bị ngốn và cạn kiệt rất nhanh
- Không phải cứ dùng Agent là phải mua API của OpenAI hay Anthropic. Đối với các dự án cần chạy Agent tự động hóa số lượng lớn, DeepSeek hoặc việc tự host Qwen/Llama mới là giải pháp tối ưu chi phí đường dài nhất