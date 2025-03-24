# Phân Tích Cảm Xúc Tiếng Việt Sử Dụng PhoBERT và Mô Hình RNN
- Dự án này thực hiện phân tích cảm xúc trong câu tiếng Việt trên các câu văn tiếng Việt sử dụng mô hình PhoBERT kết hợp với mạng nơ-ron hồi tiếp (RNN).

- Mô hình sử dụng mô hình PhoBERT (một biến thể của BERT cho tiếng Việt) để trích xuất đặc trưng từ văn bản, sau đó đưa vào một mô hình RNN để phân loại cảm xúc. Các cảm xúc được phân loại thành 3 nhóm: **Tích Cực (Positive)**, **Tiêu Cực (Negative)**, và **Trung Lập (Neutral)**. Ngoài ra mô hình được huấn luyện và tối ưu hóa với bộ dữ liệu cảm xúc đã được chuyển đổi, kết hợp với từ điển cảm xúc để cải thiện dự đoán.

1. **Tiền Xử Lý Dữ Liệu**: 
   - Chuyển đổi các nhãn cảm xúc trong bộ dữ liệu thành các nhãn có dạng nhị phân: **Tiêu Cực**, **Tích Cực**, và **Trung Lập**.
   - Áp dụng tokenization sử dụng PhoBERT tokenizer.

2. **Mô Hình PhoBERT kết hợp với RNN**:
   - Sử dụng PhoBERT làm lớp encoder để trích xuất đặc trưng ngữ nghĩa.
   - Kết hợp với một mạng RNN để học các đặc trưng tuần tự.
   - Phần phân loại được thực hiện bởi một lớp fully connected (FC).

3. **Tối Ưu và Đánh Giá**:
   - Đánh giá hiệu suất mô hình bằng cách sử dụng chỉ số độ chính xác trên bộ kiểm tra.
   - Tối ưu mô hình bằng cách kết hợp các điểm số từ từ điển cảm xúc vào kết quả dự đoán của mô hình.

## Mức phân bố dữ liệu 

1. **Trước khi encoding**:

![dataDistribute](https://github.com/RedBallooon/PhoBERT-RNN-for-VietNamese-Sentimental-Analysis/blob/51fb66332603246d820488b5b9e2652dc2bbb223/img/Data%20Distribute.png)

2. **Sau khi encoding**:

![AfterEncod](https://github.com/RedBallooon/PhoBERT-RNN-for-VietNamese-Sentimental-Analysis/blob/51fb66332603246d820488b5b9e2652dc2bbb223/img/after%20encoding.png)

## Từ điển từ khóa VietSentiWordnet.txt

![Dict](https://github.com/RedBallooon/PhoBERT-RNN-for-VietNamese-Sentimental-Analysis/blob/934b15d3b3295c14df19aa50d905e2fd73f05aed/img/image_2025-03-24_224848796.png)


## Cấu Trúc Dự Án
| Thư mục      | Tệp tin                              |
|--------------|--------------------------------------|
| `data/`      | `train_data.xlsx`                    |
|              | `test_data.xlsx`                     |
|              | `valid_data.xlsx`                    |
|              | `VietSentiWordnet.txt`               |
| `model/`     | `phobert_sentiment_vsmec.pth`        |
| `notebooks/` | `sentiment_analysis.ipynb`           |
| `README.md`  |                                      |



## Các Thư Viện Yêu Cầu

- `torch`
- `transformers`
- `pandas`
- `matplotlib`
- `seaborn`
- `re`

Cài đặt các thư viện này thông qua `pip`: 
```bash
pip install torch transformers pandas matplotlib seaborn
```

## Cách Sử Dụng

### 1. Chuẩn Bị Dữ Liệu

Đảm bảo rằng bạn đã chuẩn bị các file dữ liệu sau:
- `train_data.xlsx`: Dữ liệu huấn luyện.
- `test_data.xlsx`: Dữ liệu kiểm tra.
- `valid_data.xlsx`: Dữ liệu kiểm tra vali.
- `VietSentiWordnet.txt`: Từ điển cảm xúc tiếng Việt (VietSentiWordnet).

### 2. Huấn Luyện Mô Hình

Chạy đoạn mã dưới đây để huấn luyện mô hình:

```python
train_loss_history, train_acc_history = train_model(model, dataloaders, epochs=7)
```

### 3.Thực hiển kiểm tra với text ngẫu nhiên sau khi huấn luyện mô hình

1. **Model đầu được huấn luyện với PhoBERT - RNN**:

![Before](https://github.com/RedBallooon/PhoBERT-RNN-for-VietNamese-Sentimental-Analysis/blob/51fb66332603246d820488b5b9e2652dc2bbb223/img/before%20optimized.png)


2. **Model được huấn luyện với PhoBERT - RNN kết hợp với dict từ khóa**: 
```python
text_input = "Tên đó hắn ta đã lấy tiền của tôi"
result = predict_sentiment(text_input, model, tokenizer, sentiment_lexicon)
```
![After](https://github.com/RedBallooon/PhoBERT-RNN-for-VietNamese-Sentimental-Analysis/blob/51fb66332603246d820488b5b9e2652dc2bbb223/img/after.png)

