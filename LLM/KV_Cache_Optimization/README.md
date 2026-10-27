# KV Cache Optimization

Tối ưu hóa bộ nhớ và truy xuất Key-Value Cache trong LLM Serving.

## 1. Nội dung trọng tâm
- **Bản chất và Kích thước KV Cache:**
  - Tại sao cần KV Cache trong Autoregressive Generation.
  - Công thức tính dung lượng VRAM:
    $$\text{Memory} = 2 \times 2 \times n_{\text{layers}} \times n_{\text{heads}} \times d_{\text{head}} \times \text{context\_len} \times \text{batch\_size} \times \text{dtype\_bytes}$$
  - Phân tích hiện tượng phân mảnh bộ nhớ (Internal & External Fragmentation).
- **PagedAttention (vLLM Core):**
  - Khái niệm Virtual Memory Paging cho KV Cache.
  - Logical Blocks vs Physical Blocks.
  - Block Table và ánh xạ địa chỉ trên GPU.
- **Prefix Caching & Prompt Sharing (SGLang / RadixAttention):**
  - Cây Radix Trie lưu trữ KV Cache dùng chung.
  - Tối ưu cho System prompt, multi-turn chat, multi-agent frameworks.
- **Kiến trúc Attention tiết kiệm KV Cache:**
  - Multi-Query Attention (MQA) và Grouped-Query Attention (GQA).
  - Multi-head Latent Attention (MLA trong DeepSeek V2/V3).
- **KV Cache Quantization:**
  - FP8 (E4M3, E5M2) KV Cache.
  - INT8 / INT4 KV Cache compression.
