# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature thấp như 0.0, câu trả lời thường ổn định, trực tiếp và ít thay đổi giữa các lần gọi. Khi tăng lên 0.5 và 1.0, phản hồi bắt đầu đa dạng hơn về cách diễn đạt và lựa chọn sự thật thú vị. Ở mức 1.5, nội dung sáng tạo hơn nhưng cũng dễ lan man hoặc kém nhất quán hơn, nên cần cẩn thận nếu yêu cầu độ chính xác cao.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature khoảng 0.2–0.4 cho chatbot hỗ trợ khách hàng. Mức này vẫn đủ tự nhiên trong giao tiếp, nhưng ưu tiên câu trả lời nhất quán, rõ ràng và ít rủi ro bịa thông tin hơn so với temperature cao.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Workload có khoảng 10.000 × 3 × 350 = 10.500.000 token mỗi ngày. Theo bảng giá trong `template.py`, GPT-4o đắt hơn GPT-4o-mini khoảng 33,3 lần cho cả input token (5.00 / 0.150) lẫn output token (20.00 / 0.600), nên workload này cũng đắt hơn khoảng 33,3 lần nếu dùng GPT-4o.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi tác vụ cần lập luận phức tạp, độ chính xác cao hoặc xử lý tình huống nhạy cảm, ví dụ trợ lý phân tích hợp đồng, tư vấn kỹ thuật chuyên sâu, hoặc tổng hợp tài liệu quan trọng. GPT-4o-mini phù hợp hơn cho các tác vụ khối lượng lớn, rủi ro thấp như phân loại tin nhắn, trả lời FAQ đơn giản, tóm tắt ngắn, hoặc chatbot tuyến đầu trước khi chuyển các ca khó cho model mạnh hơn.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi phản hồi dài hoặc người dùng cần cảm giác hệ thống đang xử lý ngay lập tức, chẳng hạn chatbot hội thoại, trợ lý viết nội dung, giải thích bài học, hoặc các tác vụ có thể mất vài giây để sinh câu trả lời đầy đủ. Việc hiển thị từng phần giúp giảm cảm giác chờ đợi và cho phép người dùng đọc sớm trong khi model vẫn đang tạo tiếp. Non-streaming phù hợp hơn khi cần nhận toàn bộ kết quả trước khi xử lý, ví dụ gọi API backend, phân loại dữ liệu, trả JSON có cấu trúc, chấm điểm, hoặc các tác vụ mà giao diện chỉ nên hiển thị kết quả sau khi đã hoàn chỉnh và kiểm tra xong.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
