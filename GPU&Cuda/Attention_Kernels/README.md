# Attention Kernels Optimization

Nghiên cứu và triển khai các thuật toán Attention tăng tốc trên GPU.

## 1. Nội dung trọng tâm
- **Thuật toán FlashAttention (v1, v2, v3):**
  - **Online Softmax:** Kỹ thuật tính Softmax tăng dần không cần lưu toàn bộ ma trận $N \times N$.
  - **Tiling:** Chia nhỏ $Q, K, V$ thành các khối vừa vặn trong SRAM (L1 Cache / Shared Memory).
  - Giảm thiểu lưu lượng I/O ra HBM từ $O(N^2)$ xuống $O(N)$.
  - Tối ưu hóa tính toán ma trận với Tensor Cores (MMA/WGMMA).
- **FlashDecoding & FlashDecoding++:**
  - Tại sao FlashAttention chưa tối ưu cho Decode phase (do $Q$ chỉ có 1 token).
  - Kỹ thuật chia nhỏ sequence length của $K, V$ và song song hóa qua nhiều SMs (Split-KV Attention), sau đó reduce kết quả.
- **Triển khai PagedAttention Kernel:**
  - Viết kernel đọc dữ liệu $K, V$ từ các khối nhớ không liên tục thông qua Block Table.
