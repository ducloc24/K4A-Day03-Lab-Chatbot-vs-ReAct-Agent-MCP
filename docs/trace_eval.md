# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Trần Đức Lộc 
> **Mã Sinh Viên / Mã Học viên:** 2A202602431  
> **Chủ đề Lựa chọn:** Lĩnh vực Giáo dục & Đào tạo (Education & Academics)

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
    "step": 2,
    "query": "Hãy tra cứu cố vấn học tập của sinh viên SV2026001 rồi đặt lịch tư vấn với cố vấn đó lúc 14:00 ngày 15/09/2026.",
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
    "latency_ms": 1579.71
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI
[
  {
    "step": 1,
    "query": "Mã sinh viên SV2026002",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "academic_query",
    "arguments": {
      "student_id": "SV2026002"
    },
    "observation": {
      "status": "SUCCESS",
      "student_id": "SV2026002",
      "data": {
        "full_name": "Trần Thị Bình",
        "class": "AI-K4",
        "gpa": 3.6,
        "email": "binh.tt@vinuni.edu.vn",
        "status": "Đang học",
        "advisor": "TS. Lê Thị B"
      }
    },
    "latency_ms": 1282.26
  },
  {
    "step": 2,
    "query": "Mã sinh viên SV2026002",
    "action_type": "FINAL_ANSWER",
    "thought": "OpenAI phản hồi trực tiếp bằng văn bản (không cần gọi công cụ).",
    "output": "Dựa trên dữ liệu hồ sơ học vụ thu được từ hệ thống của Đại học VinUni, đây là thông tin chi tiết của sinh viên mang mã **SV2026002**:\n\n- **Họ và tên:** Trần Thị Bình\n- **Lớp:** AI-K4\n- **GPA:** 3.6\n- **Email:** binh.tt@vinuni.edu.vn\n- **Trạng thái học tập:** Đang học\n- **Cố vấn học tập:** TS. Lê Thị B\n\nBạn có cần hỗ trợ thêm thông tin gì khác hoặc muốn đặt lịch hẹn tư vấn học vụ với cố vấn học tập không?",
    "latency_ms": 1722.96
  }
]
- [ ] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** _5_ / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** _2_ lượt.
- **Kết quả đẩy Repo nộp bài:** [X] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
