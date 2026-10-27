# Serving Engine Architecture & Scheduling

Kiến trúc các engine phục vụ LLM, cơ chế lập lịch (scheduling) và quản lý batching.

## 1. Nội dung trọng tâm
- **Continuous Batching / Dynamic Batching (Orca Paper):**
  - Giới hạn của Static Batching trong sinh chuỗi có độ dài biến thiên.
  - Iteration-level scheduling: Thêm request mới và trả kết quả request cũ ở từng token step.
- **Chunked Prefill & Piggybacking (Sarathi / vLLM):**
  - Vấn đề Prefill Starvation: Khi 1 prompt dài làm nghẽn quá trình decode của hàng chục user khác.
  - Kỹ thuật chia nhỏ prompt (chunking) và ghép chung với decode token.
- **PD Disaggregation (Prefill-Decode Disaggregation):**
  - Tách riêng GPU Cluster cho Prefill (compute-bound) và GPU Cluster cho Decode (memory-bound).
  - Nghiên cứu: Splitwise, DistServe, Mooncake.
  - Truyền KV Cache qua RDMA / mạng tốc độ cao.
- **Guided Decoding / Structured Outputs:**
  - Fast JSON schema / Regex sampling (Outlines, XGrammar).
  - Tối ưu mask logits trên GPU không làm suy giảm throughput.
