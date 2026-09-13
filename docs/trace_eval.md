# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Trần Đức Lộc 
> **Mã Sinh Viên / Mã Học viên:** 2A202602431  
> **Chủ đề Lựa chọn:** Tra cứu thông tin và đặt lịch tự vấn của sinh viên - Lĩnh vực Giáo dục & Đào tạo (Education & Academics)

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | **4 / 5** | Với yêu cầu đặt lịch tư vấn, Agent cần xác định mã sinh viên, tra cứu thông tin học vụ và cố vấn, sau đó dùng kết quả để tạo lịch hẹn. Các câu hỏi tra cứu đơn giản chỉ cần một bước, nhưng luồng tra cứu rồi đặt lịch có nhiều bước nối tiếp. |
| **2. Tool Interaction** | **5 / 5** | Hệ thống cần gọi các tool qua MCP Server để tra cứu hồ sơ, GPA, lịch thi và thực hiện đặt lịch tư vấn. LLM không tự có dữ liệu nghiệp vụ nên phải tương tác với lớp dữ liệu và dịch vụ bên ngoài. |
| **3. Dynamic Decision** | **5 / 5** | Quyết định của Agent phụ thuộc vào kết quả tool: nếu tìm thấy sinh viên thì có thể tiếp tục đặt lịch với đúng cố vấn; nếu mã sinh viên không tồn tại thì phải dừng và thông báo, không được bịa dữ liệu. |
| **4. Long Horizon Goal** | **4 / 5** | Agent phải duy trì mục tiêu của người dùng qua nhiều bước từ tra cứu đến hoàn tất lịch hẹn, đồng thời giữ đúng mã sinh viên, thời gian và cố vấn. Phạm vi bài toán chưa quá dài nên chấm 4/5 thay vì 5/5. |
| **TỔNG ĐIỂM AGENTIC FIT** | **18 / 20** | *Bài toán đạt trên 12/20 nên phù hợp triển khai Agentic System với ReAct Loop và MCP.* |


---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Hãy đặt lịch tư vấn học vụ cho sinh viên SV2026001 với cố vấn PGS.TS Nguyễn Văn A lúc 14:00 ngày 15/09/2026.",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "schedule_appointment",
    "arguments": {
      "advisor_name": "PGS.TS Nguyễn Văn A",
      "datetime_str": "14:00 15/09/2026",
      "student_id": "SV2026001"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "student_id": "SV2026001",
      "datetime": "14:00 15/09/2026",
      "advisor": "PGS.TS Nguyễn Văn A",
      "message": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 14:00 15/09/2026."
    },
    "latency_ms": 1754.7
  },
  {
    "step": 2,
    "query": "Hãy đặt lịch tư vấn học vụ cho sinh viên SV2026001 với cố vấn PGS.TS Nguyễn Văn A lúc 14:00 ngày 15/09/2026.",
    "action_type": "FINAL_ANSWER",
    "thought": "OpenAI phản hồi trực tiếp bằng văn bản (không cần gọi công cụ).",
    "output": "Dựa trên kết quả từ hệ thống, lịch hẹn tư vấn học vụ của bạn đã được đặt thành công. Dưới đây là thông tin chi tiết về lịch hẹn:\n\n* **Mã sinh viên:** SV2026001\n* **Cố vấn học tập:** PGS.TS Nguyễn Văn A\n* **Thời gian:** 14:00 ngày 15/09/2026\n* **Mã đặt lịch (Booking ID):** BK-SV2026001-99\n* **Trạng thái:** Thành công\n\nBạn vui lòng có mặt đúng giờ tại buổi tư vấn nhé! Nếu cần thay đổi hoặc hỗ trợ thêm thông tin nào khác, bạn cứ cho mình biết nha.",
    "latency_ms": 1557.71
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [x] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** _5_ / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** _5_ lượt.
- **Kết quả đẩy Repo nộp bài:** [X] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
