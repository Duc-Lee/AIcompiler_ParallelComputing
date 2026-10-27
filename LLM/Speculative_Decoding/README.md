# Speculative Decoding

Kỹ thuật tăng tốc suy luận bằng cách dự đoán trước nhiều token đồng thời.

## 1. Nội dung trọng tâm
- **Nguyên lý cốt lõi:**
  - Biến bài toán memory-bound (sinh 1 token mỗi lần) thành compute-bound (kiểm chứng song song $K$ token).
  - Draft Model (nhỏ, nhanh) sinh candidate tokens + Target Model (lớn) verify trong 1 forward pass duy nhất.
- **Các phương pháp phổ biến:**
  - **Standard Speculative Sampling:** Thuật toán chấp nhận/từ chối bảo toàn phân phối xác suất.
  - **Self-Speculative Decoding / Early Exiting:** Dùng chính các layer sớm của mô hình để sinh draft.
  - **Medusa / EAGLE / Lookahead Decoding:** Thêm các multi-token prediction heads mà không cần draft model riêng biệt.
- **Tối ưu Tree Attention:**
  - Xây dựng attention mask dạng cây để verify nhiều nhánh token ứng viên cùng một lúc.
