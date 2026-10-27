# OpenAI Triton for High-Performance GPU Kernels

Lập trình GPU hiệu năng cao với ngôn ngữ Triton (Python-like DSL).

## 1. Nội dung trọng tâm
- **Tại sao cần Triton:**
  - So sánh Triton vs Native CUDA C++ (năng suất lập trình vs độ kiểm soát phần cứng).
  - Khái niệm Block-level programming thay vì Thread-level programming của CUDA.
- **Kiến trúc cơ bản của Triton:**
  - `tl.program_id`, `tl.arange`, `tl.load`, `tl.store`.
  - Con trỏ khối (Block Pointers) và cơ chế Masking (xử lý biên out-of-bounds).
  - Tự động quản lý Shared Memory (SRAM) và Warp scheduling.
- **Tự động tối ưu (Auto-tuning):**
  - Trình trang trí `@triton.autotune`.
  - Cấu hình `BLOCK_SIZE`, `num_warps`, `num_stages`.
- **Thực hành viết các Fused Kernels:**
  - Fused Softmax.
  - Fused LayerNorm / RMSNorm.
  - Fused SwiGLU / GeLU.
  - Tiled Matrix Multiplication (GEMM).
