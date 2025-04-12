
# 📄 ChatGPT API Documentation

This document describes how to interact with OpenAI's ChatGPT API for uploading files and sending chat prompts.

---

## 📁 1. Upload a File to ChatGPT

### Endpoint
```
POST https://api.openai.com/v1/files
```

### Headers
```
Authorization: Bearer YOUR_API_KEY
```

> ⚠️ Replace `YOUR_API_KEY` with your actual OpenAI API key.

### Sample Request (using curl)
```bash
curl https://api.openai.com/v1/files \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "purpose=user_data" \
  -F "file=@mydata.jsonl"
```

### Sample Response
```json
{
  "id": "file-abc123",
  "object": "file",
  "bytes": 120000,
  "created_at": 1677610602,
  "filename": "mydata.jsonl",
  "purpose": "user_data"
}
```

---

## 💬 2. Send a Question to ChatGPT

### Endpoint
```
POST https://api.openai.com/v1/chat/completions
```

### Headers
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

### Sample Request (JSON body)
```json
{
  "model": "gpt-4o-2024-08-06",
  "messages": [
    {
      "role": "user",
      "content": "Giới thiệu về bản thân bạn."
    }
  ]
}
```

### Sample Response
```json
{
  "id": "chatcmpl-BEXXmchzHa1zLDtn1dOEinFGXIYjg",
  "object": "chat.completion",
  "created": 1742805234,
  "model": "gpt-4o-2024-08-06",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": null,
        "function_call": {
          "name": "danh_gia_ung_vien",
          "arguments": "{\"thong_tin_ung_vien\":\"Thuy Linh Tran, Consultant, sinh ngày 30/09/1996, địa chỉ CT7D apartment, Duong Noi ward, Ha Dong district, Hanoi.\",\"danh_gia\":\"Ứng viên có kiến thức và kinh nghiệm vững chắc trong lĩnh vực kế toán và kiểm toán, đã từng đảm nhiệm các vị trí cao cấp như Advisory Manager và Senior Consultant tại các công ty lớn như UHY Auditing & Consulting Co., Ltd và NEXIA STT Co., Ltd. Ứng viên có bằng Thạc sĩ Kế toán và chứng chỉ CPA Việt Nam, ICAEW, và TOEIC 890/990. Có kỹ năng lãnh đạo đội nhóm, quản lý thời gian, và làm việc dưới áp lực cao, phù hợp cho vị trí Kế toán trưởng.\",\"diem_so\":9,\"ngay_sinh\":\"1996-09-30\",\"gioi_tinh\":\"nu\",\"truong_dao_tao\":\"National Economics University, Academy of Finance\"}"
        }
      },
      "finish_reason": "function_call"
    }
  ],
  "usage": {
    "prompt_tokens": 2427,
    "completion_tokens": 230,
    "total_tokens": 2657
  },
  "service_tier": "default",
  "system_fingerprint": "fp_83df987f64"
}
```




