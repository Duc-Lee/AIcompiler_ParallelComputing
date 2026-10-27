# Profiling & Benchmarking

Công cụ và phương pháp đo lường, giám sát, tìm điểm nghẽn (bottleneck) trên GPU và Serving Engine.

## 1. Nội dung trọng tâm
- **NVIDIA Nsight Systems (`nsys`):**
  - Profiling toàn bộ timeline hệ thống: CPU threads, CUDA Streams, Memcpy, Kernel executions.
  - Nhận diện CPU-GPU bubbles, bất đồng bộ và tắc nghẽn liên lạc IPC / NCCL.
- **NVIDIA Nsight Compute (`ncu`):**
  - Đi sâu vào từng kernel riêng lẻ:
    - Speed of Light (SOL): Tỉ lệ phần trăm đạt được so với trần lý thuyết của GPU (Compute vs Memory).
    - Memory Workload Analysis: Băng thông L1, L2, HBM/DRAM.
    - Warp Scheduler & Stall Reasons: Tìm hiểu vì sao Warp bị dừng (chờ nạp dữ liệu, tranh chấp thanh ghi, branch divergence).
- **PyTorch Profiler & Kineto:**
  - `torch.profiler` tích hợp trực tiếp trong code Python.
- **Serving Benchmarking Frameworks:**
  - `vllm benchmark` (`benchmark_throughput.py`, `benchmark_serving.py`).
  - `llmperf` đo lường TTFT, ITL, Throughput dưới các kịch bản tải thực tế.
