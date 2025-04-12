
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

### Body
- **Type:** multipart/form-data
- **Content:**
  - `purpose`: user_data
  - `file`: File to upload

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

> ⚠️ Replace `YOUR_API_KEY` with your actual OpenAI API key.


### Body
- **Type:** application/json
- **Content:**
  - `purpose`: user_data
  - `file`: File to upload

### Sample Request (using curl)
```
curl https://api.openai.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o",
    "functions": [
      {
        "name": "danh_gia_ung_vien",
        "description": "Lấy về điểm đánh giá ứng viên",
        "parameters": {
          "type": "object",
          "properties": {
            "diem_so": {
              "type": "integer",
              "description": "Điểm số đánh giá của ứng viên, ví dụ 8"
            },
            "thong_tin_ung_vien": {
              "type": "string",
              "description": "Thông tin ứng viên cơ bản của ứng viên, ví dụ tên, tuổi, địa chỉ"
            },
            "danh_gia": {
              "type": "string",
              "description": "Đánh giá về thông tin kinh nghiệm của ứng viên"
            },
            "ngay_sinh": {
              "type": "string",
              "description": "Ngày sinh của ứng viên trong CV, giá trị tham số có định dạng '\''yyyy-MM-dd'\''"
            },
            "gioi_tinh": {
              "type": "string",
              "description": "Giới tính của ứng viên, Nam thì nhập giá trị là '\''Nam'\'', Nữ thì nhập giá trị là '\''Nữ'\''"
            },
            "truong_dao_tao": {
              "type": "string",
              "description": "Trường đại học, cao đẳng ứng viên tốt nghiệp"
            }
          },
          "required": [
            "diem_so",
            "thong_tin_ung_vien",
            "danh_gia"
          ]
        }
      }
    ],
    "messages": [
      {
        "role": "user",
        "content": [
          {
            "type": "file",
            "file": {
              "file_id": "$action.Gui_file_CV_len_ChatGPT.output.body.id"
            }
          },
          {
            "type": "text",
            "text": "Tôi đang tuyển dụng ứng viên Kế toán trưởng cho công ty về SAAS. Hãy đánh giá CV của ứng viên như file, chấm điểm và đưa ra điểm của ứng viên từ 1 đến 10. Cao nhất là 10 điểm. Đưa điểm số vào 1 tham số trong kết quả trả về. Kết quả trả về cần dạng json: 1: Thông tin ứng viên. 2 : đánh giá. 3. Điểm số: . Trong đó phần 3. Điểm số chỉ đưa lại là con số từ 1 đến 10. Hãy trả về tham số message.content là định dạng json."
          }
        ]
      }
    ]
  }'
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




