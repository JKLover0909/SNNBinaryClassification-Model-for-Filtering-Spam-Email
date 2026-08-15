# AGENTS.md — SNNBinaryClassification-Model-for-Filtering-Spam-Email

## Vai trò Agent

Coding agent hỗ trợ phát triển và bảo trì hệ thống phân loại email spam/ham song ngữ (EN/VI) dựa trên SNN với TensorFlow/Keras và Flask.

## Quy tắc

1. Đọc `CLAUDE.md` trước khi thực hiện bất kỳ thay đổi nào.
2. Không sửa đổi dataset gốc (`data_en.csv`, `data_vi.csv`, stopwords files).
3. Không commit model weights, checkpoints hoặc file nhị phân lớn.
4. Không commit `.env`, credentials hoặc PII.
5. Giữ nguyên cấu trúc Flask app hiện tại (`main.py` là entrypoint).

## Kiểm tra

```bash
# Syntax check toàn bộ Python files
python -m py_compile main.py
python -m py_compile model_tensorflow.py
python -m py_compile standard_data.py
python -m py_compile prepare_stopwords.py
python -m py_compile test.py

# Test chuẩn hóa văn bản (không cần GPU/model)
python test.py
```

## Luồng dữ liệu

1. `prepare_stopwords.py` đọc stopwords từ file text.
2. `standard_data.py` chuẩn hóa văn bản đầu vào (lowercase, xóa dấu câu, loại stopwords).
3. `model_tensorflow.py` downsampling, tokenize, train SNN model.
4. `main.py` khởi động Flask server, train model in-memory, phục vụ API `/process_mail`.

## Phạm vi mở rộng

- Thêm `requirements.txt` để chuẩn hóa dependencies.
- Tách model training ra khỏi startup flow (serialize/deserialize model).
- Thêm unit tests cho `standard_data` và `prepare_stopwords`.
- Cải thiện xử lý lỗi trong Flask endpoints.
