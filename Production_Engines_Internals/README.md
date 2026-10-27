# Production Serving Engines Internals

Nghiên cứu kiến trúc mã nguồn và nguyên lý thiết kế của các LLM Serving Engine thực tế.

## 1. Nội dung trọng tâm
- **vLLM Internals:**
  - `LLMEngine` vs `AsyncLLMEngine`.
  - `Scheduler`: Quy trình lập lịch các `SequenceGroup`, phân bổ block memory.
  - `BlockSpaceManager` & `CacheEngine`: Quản lý cấp phát PagedAttention blocks.
  - `ModelRunner` & `Worker`: Cơ chế truyền tensor, thực thi kernel, tích hợp CUDA Graphs.
- **SGLang Internals:**
  - RadixAttention runtime cho high cache hit rate.
  - Structured Decoding và phân tách Frontend / Backend.
- **TensorRT-LLM (NVIDIA):**
  - C++ Runtime, In-Flight Batching (IFB).
  - TensorRT Plugins, FP8/FP4 optimization, tối ưu hóa sâu cho phần cứng NVIDIA.
- **llama.cpp Internals:**
  - Kiến trúc suy luận đơn giản bằng C/C++, không phụ thuộc runtime cồng kềnh.
  - Xử lý định dạng GGUF, mmap tải model nhanh, tối ưu hóa CPU SIMD (AVX-512) và GPU offloading.
