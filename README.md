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

