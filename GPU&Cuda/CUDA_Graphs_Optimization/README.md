# CUDA Graphs for LLM Serving

Tối ưu hóa độ trễ thực thi bằng cách loại bỏ CPU Launch Overhead với CUDA Graphs.

## 1. Nội dung trọng tâm
- **Vấn đề CPU Launch Overhead trong Decode Phase:**
  - Ở mỗi bước Decode sinh 1 token, thời gian chạy kernel trên GPU chỉ mất vài chục micro-giây.
  - Chi phí gọi hàm từ CPU (Kernel launch latency) qua CUDA driver có thể lớn hơn thời gian thực thi của GPU.
- **Cơ chế hoạt động của CUDA Graphs:**
  - Định nghĩa đồ thị thực thi một lần (Capture phase).
  - Khởi tạo và tối ưu hóa topology đồ thị trên GPU (Instantiate phase).
  - Thực thi toàn bộ đồ thị chỉ với 1 lời gọi API duy nhất từ CPU (Launch phase).
- **Ứng dụng trong LLM Serving Engines:**
  - Xử lý bài toán kích thước batch / seq_len động (Dynamic Shapes) khi dùng CUDA Graphs.
  - Bucketting / Padded Batching: Tạo sẵn các CUDA Graph cho từng ngưỡng batch size (ví dụ: batch 1, 2, 4, 8, 16...).
