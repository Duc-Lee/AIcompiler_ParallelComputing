# LLM Serving & GPU Optimization

Kho lưu trữ kiến thức, mã nguồn và tài liệu nghiên cứu chuyên sâu về **Hạ tầng phục vụ mô hình ngôn ngữ lớn (LLM Serving Infrastructure)**, **Tối ưu hóa GPU (GPU Optimization)** và **AI Compiler**.

---

## Bản đồ kiến trúc & Cấu trúc thư mục

### 1. Nền tảng Hệ thống & Phần cứng (Foundations)
* [`OperatingSystem/`](./OperatingSystem): Quản lý bộ nhớ tiến trình, Virtual Memory, IPC, eBPF, Linux Kernel.
* [`ParallelPrograming/`](./ParallelPrograming): Lập trình song song CPU đa luồng, OpenMP, MPI.
* [`GPU&Cuda/`](./GPU&Cuda):
  * [`GPU_PrallelPrograming/`](./GPU&Cuda/GPU_PrallelPrograming): Kiến trúc SM, Warp, Thread, Memory Hierarchy của GPU NVIDIA.
  * [`NVIDIA_CUDA/`](./GPU&Cuda/NVIDIA_CUDA): Lập trình CUDA C/C++ native.
  * [`OpenAI_Triton/`](./GPU&Cuda/OpenAI_Triton): Lập trình kernel GPU hiệu năng cao với Python DSL.
  * [`Attention_Kernels/`](./GPU&Cuda/Attention_Kernels): FlashAttention-v1/v2/v3, FlashDecoding, PagedAttention kernels.
  * [`CUDA_Graphs_Optimization/`](./GPU&Cuda/CUDA_Graphs_Optimization): Triệt tiêu CPU Launch Overhead trong Decode phase.
  * [`RAPIDS_GPU/`](./GPU&Cuda/RAPIDS_GPU) & [`eBPF_GPUkernel/`](./GPU&Cuda/eBPF_GPUkernel).

### 2. Trình biên dịch AI & Tối ưu Đồ thị (AI Compilers & Codegen)
* [`AIcompiler/`](./AIcompiler):
  * `CompilerTheory`: Lý thuyết biên dịch, Lexing, Parsing, AST.
  * `ComputerArchitechture`: Kiến trúc tập lệnh và vi kiến trúc.
  * `GraphLevelIR_GraphOptimizations`: Đồ thị tính toán, Operator Fusion, Dead Code Elimination.
  * `Codegen_TargetLowering`: Hạ cấp mã nguồn sang LLVM IR, PTX, Machine Code.
  * `MemoryOptimization`: Quản lý bộ nhớ và cấp phát buffer.
* [`LoopTransformations_PolyhedralModel/`](./LoopTransformations_PolyhedralModel): Biến đổi vòng lặp, Tiling, Skewing, Polyhedral compilation.
* [`AutoTuning_CostModeling/`](./AutoTuning_CostModeling): Tự động tìm kiếm không gian siêu tham số cấu hình phần cứng.

### 3. LLM Serving Chuyên sâu (LLM Serving & Inference Engine)
* [`LLM/`](./LLM):
  * [`LLM_Inference_Mechanics/`](./LLM/LLM_Inference_Mechanics): Prefill (Compute-bound) vs Decode (Memory-bound), Roofline Model, TTFT, TPOT.
  * [`KV_Cache_Optimization/`](./LLM/KV_Cache_Optimization): PagedAttention, Prefix Caching (RadixTree), MQA, GQA, MLA, KV Cache Quantization.
  * [`Serving_Engine_Architecture/`](./LLM/Serving_Engine_Architecture): Continuous Batching, Chunked Prefill, PD-Disaggregation, Guided Decoding.
  * [`Speculative_Decoding/`](./LLM/Speculative_Decoding): Draft-Target verification, Medusa, EAGLE.
  * [`LLM_Parallelism/`](./LLM/LLM_Parallelism): Tensor Parallelism (TP), Pipeline Parallelism (PP), Expert Parallelism (EP cho MoE), DeepSpeed/NCCL.
  * [`Quantization_GenAIModel/`](./LLM/Quantization_GenAIModel): AWQ, GPTQ, SmoothQuant, FP8, Marlin kernels.

### 4. Động cơ Thực tế & Đo kiểm (Engines Internals & Profiling)
* [`Production_Engines_Internals/`](./Production_Engines_Internals): Mổ xẻ mã nguồn vLLM, TensorRT-LLM, SGLang, llama.cpp.
* [`Profiling_Benchmarking/`](./Profiling_Benchmarking): Phân tích hiệu năng với NVIDIA Nsight Systems (`nsys`), Nsight Compute (`ncu`), vLLM benchmark runner.

---

### 5. Nền tảng Học máy & Xử lý Ngôn ngữ (ML & NLP Foundations)
* [`Machine_learning/`](./Machine_learning)
* [`Neural_Network/`](./Neural_Network)
* [`Deep_learning/`](./Deep_learning)
* [`NLP/`](./NLP)