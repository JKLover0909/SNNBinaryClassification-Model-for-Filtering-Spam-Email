# CLAUDE.md — SNNBinaryClassification-Model-for-Filtering-Spam-Email

## Tổng quan

Dự án phân loại nhị phân email spam/ham sử dụng mạng nơ-ron tuần tự (Sequential Neural Network) với TensorFlow/Keras. Hỗ trợ song ngữ Tiếng Anh và Tiếng Việt.

## Cấu trúc

- `main.py` — Flask web server, endpoint `/process_mail` nhận text + language, trả kết quả spam/ham.
- `model_tensorflow.py` — Xây dựng và huấn luyện SNN model: downsampling, tiền xử lý, tokenize, train với EarlyStopping/ReduceLROnPlateau.
- `standard_data.py` — Chuẩn hóa văn bản: lowercase, xóa dấu câu, loại stopwords.
- `prepare_stopwords.py` — Đọc danh sách stopwords từ file text cho EN và VI.
- `test.py` — Script test nhanh chuẩn hóa văn bản tiếng Việt.
- `data_en.csv`, `data_vi.csv` — Dataset email spam/ham.
- `e-stopwords.txt`, `vietnamese-stopwords.txt` — Danh sách stopwords.
- `baocaomodel_en.ipynb`, `baocaomodel_vi.ipynb` — Notebook báo cáo phân tích model.

## Công nghệ

- Python, Flask, TensorFlow, Keras, scikit-learn, pandas, matplotlib, seaborn
- Không có `requirements.txt` — cần tự cài: `pip install flask tensorflow pandas scikit-learn matplotlib seaborn`

## Lệnh chạy

```bash
# Chạy web server (train model khi khởi động)
python main.py

# Test chuẩn hóa văn bản
python test.py
```

## Giới hạn

- Không sửa `data_en.csv`, `data_vi.csv` — dataset gốc.
- Không commit model weights (.h5, .keras, SavedModel).
- Không commit `.env` hoặc credentials.
- Không chạy training nặng trong CI/CD.
- Model được train lại mỗi lần khởi động `main.py` (in-memory, không lưu file).
