# LLM Inference Mechanics

Tài liệu và ghi chú về cơ chế suy luận của Large Language Models (LLM) và các điểm nghẽn hiệu năng phần cứng.

## 1. Nội dung trọng tâm
- **Prefill Phase (Prompt Evaluation):**
  - Compute-bound đặc trưng.
  - Ma trận tính toán GEMM (General Matrix Multiply).
  - Tận dụng tối đa Tensor Cores.
- **Decode Phase (Token Generation):**
  - Memory-bound / Memory bandwidth-bound đặc trưng.
  - GEMV (Matrix-Vector Multiply) với batch size nhỏ.
  - Bottleneck tại băng thông bộ nhớ HBM / VRAM.
- **Roofline Model cho LLM:**
  - Định nghĩa và tính toán Arithmetic Intensity (FLOPs / Byte).
  - Phân tích ranh giới giữa Compute-bound và Memory-bound.
- **Metrics đo lường hiệu năng:**
  - TTFT (Time To First Token) - độ trễ phản hồi ban đầu.
  - TPOT (Time Per Output Token) / ITL (Inter-Token Latency) - tốc độ sinh từng token tiếp theo.
  - Throughput (Tokens/s, Requests/s).
